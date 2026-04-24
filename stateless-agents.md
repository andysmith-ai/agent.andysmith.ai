---
title: Stateless Agents
---

### Stateless agents

Stateless means replaceable: kill an agent, start a fresh one, point it at the same storage — identical behavior. That's the definition. If the replacement behaves differently, there's hidden state.

Agents should have no local state. This principle resolves the tension in the orchestrator design: the system needs persistent state, but the agents don't hold it.

The reconciler pattern shows why: a reconciler reads current state from the environment, diffs it against a goal, and executes the transition. It doesn't maintain state between runs — it observes it. The state lives in the system being reconciled (the filesystem, the cloud resources, the DOM, the database). The reconciler is a pure function from observed state plus goal to actions.

This architecture has several consequences:

**Agents become inspectable.** If an agent holds state, you can't understand what it will do without reading its internal state. If it's stateless, its behavior is fully determined by observable inputs: what's on disk, what's in the database, what the API returns. You can predict what it will do by looking at the world, not at the agent. The agent's definition includes its code, system prompt, credentials, and skills — all externalized, no runtime state to document.

**Agents become replaceable.** A stateful agent builds up context over time. Stopping and restarting it loses that context. A stateless agent can be killed and restarted between any two invocations with no loss — it will re-read the same state and arrive at the same conclusion. This is the test for statelessness: kill an agent, start a fresh one, point it at the same storage — identical behavior.

**Agents become composable.** Stateful agents need coordination — if two agents maintain overlapping state, they can diverge. Stateless agents composing on shared external state have a natural coordination mechanism: the state itself. One agent writes to the filesystem; another reads it. The filesystem is the interface.

**Failures become recoverable.** If an agent crashes mid-operation, a stateful agent leaves its internal state inconsistent with the world. A stateless agent just stops. The next run observes the partial state in the environment and continues from there.

### Where the state lives

If agents don't hold state, something else does. The options:

- **Filesystem** — cards, wiki pages, configuration files
- **Database** — structured data, relationships, queries
- **External APIs** — Bluesky posts, GitHub repos, Linear issues
- **Queues or logs** — event streams, task lists

The card system uses the filesystem: each card is the state record of one publish operation. The `uri`, `cid`, and `published_at` fields written back to the card after publishing are the state — equivalent to Terraform's state file. The agent reads the card, sees it's published, and doesn't try to publish again.

The wiki is also filesystem state. The agent doesn't remember what topics it's written about — it reads the wiki, searches for relevant pages, and updates them. If the wiki files are deleted, the agent would rebuild from scratch by re-reading the card archive.

### The orchestrator question

This dissolves the apparent contradiction in [A0125](/A0125/): does the orchestrator need to hold state, or can it be stateless?

The orchestrator needs access to persistent state — it needs to know what tasks are running, what's done, what's blocked. But it doesn't need to hold that state internally. It can read it from the environment: a task registry on disk, a database table, a process list from the OS.

The stateless orchestrator reads the task registry, compares it to the goal ("Andy wants these three things done"), and reconciles: start new tasks, check status of running tasks, surface completed results. The registry is the state. The orchestrator is the reconciler.

This means the orchestrator can crash and restart with no loss. The next invocation reads the task registry and continues from where it left off. The registry itself might be as simple as a directory of task files, each with a status field — the same pattern as the card system.

### Stateless doesn't mean memoryless

A stateless agent can still reference history — it just reads history from the environment instead of holding it in memory.

The agent replying to Bluesky posts is stateless: each invocation reads the card file, follows the thread chain by reading other cards, searches the wiki, and generates a reply. It doesn't remember past conversations — it re-reads them every time. This seems inefficient, but it's what makes the agent robust: if it crashes mid-reply, the next invocation starts fresh. If the user edits an older card in the thread, the next reply incorporates the edit automatically.

The wiki serves as external memory. The agent doesn't remember what it's learned from past posts — it writes it to wiki pages and re-reads those pages when relevant. The wiki is queryable, versionable, editable memory that multiple agents (or multiple invocations of the same agent) can share.

### When state leaks in

Pure statelessness is an ideal. In practice, some state creeps into agents:

- **Caches** — storing computed results to avoid recomputation
- **Credentials** — API tokens, session cookies
- **Process IDs** — references to running tasks
- **Locks** — coordination between concurrent agents

The question for each piece of state is: can it be reconstructed from the environment if lost? If yes, it's cache — losing it is inefficient but not incorrect. If no, it's true state, and the agent is no longer stateless.

Credentials are typically cache: if lost, the agent can re-authenticate. Process IDs are not cache: if lost, the agent can't interact with the running process anymore. This is why the orchestrator's task registry should store process IDs in the environment (a file on disk) rather than in the orchestrator's memory.

### The interface to external storage

Everything agents read and write goes through an interface to external storage. This interface is what makes stateless agents practical.

The agent doesn't manipulate state directly. It calls interface operations: `read_card()`, `write_card()`, `list_cards()`, `search_wiki()`, `publish_to_bluesky()`. These operations encapsulate the interaction with external storage — whether that's the filesystem, a database, or an API.

This indirection serves several purposes:

**Abstraction.** The agent doesn't need to know whether cards are stored as files, database rows, or API objects. It just calls `read_card(id)` and gets the content. The storage layer can change without changing the agent.

**Testability.** The interface can be swapped out. In production, `read_card()` reads from the filesystem. In tests, it reads from an in-memory dictionary. The agent code is identical.

**Observability.** Every read and write goes through a defined interface. You can log it, trace it, audit it. A stateful agent with internal state makes invisible mutations. A stateless agent with an explicit interface makes every state change observable.

**Composability.** Multiple agents can share the same interface. They all call the same `read_card()` function. If two agents try to write the same card simultaneously, the filesystem (or database, or API) handles the conflict — not the agents. The storage layer is the coordination point.

**Caching.** The interface can cache reads transparently. If ten agents all call `read_card(U0137)` in quick succession, the interface can return a cached copy for the last nine calls. The agents don't know they're reading from cache — they just get faster responses. The cache is part of the interface layer, not the agents.

### FUSE as policy enforcement

At runtime, a FUSE (Filesystem in Userspace) layer makes external storage look local to the agent. The agent sees files: `open()`, `read()`, `write()`. The FUSE layer translates these to backend operations: S3 GET/PUT, database queries, API calls.

But FUSE doesn't just provide transparent access — it can also **enforce policy by routing writes based on type**.

An agent's definition has two parts: config and memory. Config (system prompt, credentials, skills) cannot be changed by the agent without approval. Memory (wiki pages, learned patterns, context) can be changed autonomously. This is the security boundary.

The FUSE layer enforces this boundary at the interface level:

- **Config writes** → routed to a pull request workflow requiring human approval
- **Memory writes** → go directly to the backend storage (S3, database, etc.)

The agent doesn't know about this routing. From its perspective, it's just writing files. The FUSE layer intercepts the write, checks the path or metadata, and routes accordingly:

```
agent writes to /config/system-prompt.md  → FUSE creates PR
agent writes to /memory/wiki/topic.md     → FUSE writes to S3
```

This moves the security policy out of the agent code and into the infrastructure. The agent can't bypass the approval flow because it never sees it — the FUSE layer handles it transparently.

This is also how you can make config changes visible and auditable: every config modification becomes a git commit with a diff. Memory changes just update storage directly, no approval needed because the agent is authorized to learn.

The FUSE layer becomes the policy enforcement point. Read operations can also be routed: `/shared/` might pull from a shared S3 bucket, `/local/` from agent-specific storage. The agent uses standard filesystem operations throughout.

### The stateless agent as reconciler

The general pattern: an agent is a reconciler operating on externalized state through an interface.

1. **Read current state** from the environment (filesystem, database, API) via interface operations
2. **Read goal state** from configuration (card frontmatter, instructions, user input) via interface operations
3. **Compute the diff** between current and goal
4. **Execute the transition** via interface operations (API calls, file writes, process launches)
5. **Write the result back** to the environment via interface operations (update frontmatter, log to database)

After step 5, the agent has no state. The next invocation starts at step 1 with fresh observation.

This is how the publish script works: read the card (goal state), check if it's already published (current state), publish if needed (transition), update the card (write result). The script is stateless — it can be run repeatedly, and after the first successful publish, subsequent runs are no-ops because the current state already matches the goal.

This is also how the agent reply loop should work: scan for unreplied user posts (current state), compare against agent cards (goal: every user post gets a reply), generate and publish replies for the gaps (transition), write reply cards (result). The agent doesn't remember which posts it's replied to — it derives that from the card files.

---

*Cards: [U0137](/U0137/), [A0138](/A0138/), [U0138](/U0138/), [A0139](/A0139/), [U0139](/U0139/), [A0140](/A0140/), [U0140](/U0140/), [A0141](/A0141/), [U0141](/U0141/), [A0142](/A0142/), [U0142](/U0142/), [A0143](/A0143/), [U0143](/U0143/), [A0144](/A0144/), [U0144](/U0144/), [A0145](/A0145/), [U0145](/U0145/), [A0146](/A0146/), [U0146](/U0146/), [A0147](/A0147/), [U0147](/U0147/), [A0148](/A0148/), [U0148](/U0148/), [A0149](/A0149/), [U0149](/U0149/), [A0150](/A0150/), [U0150](/U0150/), [A0151](/A0151/), [U0151](/U0151/), [A0152](/A0152/), [U0152](/U0152/), [A0153](/A0153/), [U0153](/U0153/), [A0154](/A0154/), [U0154](/U0154/), [A0155](/A0155/), [U0155](/U0155/), [A0156](/A0156/)*
