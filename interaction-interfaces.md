---
title: Interaction Interfaces
---

## Human-AI interaction as a design space

Most human-AI interaction happens through one interface: the chat window. A prompt goes in, a response comes out, and the conversation scrolls upward into oblivion. But interaction is a design space, not a solved problem. The shape of the interface determines what kinds of thinking it can support.

### The card system as interface experiment

This project — cards, threads, wiki, agent replies — is itself an interaction interface. It differs from a chat window in several structural ways:

- **Persistence**: Every exchange is a file that stays. Nothing scrolls away. Ideas accumulate as artifacts, not ephemeral messages.
- **Addressability**: Each post has an ID, a URL, a location in a thread. You can point at a specific idea and reply to it months later.
- **Asymmetry**: The agent's reply is two things — a 300-character Bluesky post and a full web page. The medium splits, serving different purposes.
- **Public thinking**: The dialogue happens on Bluesky, not in a private chat. The publicness constraint (see [Structured Thinking](/structured-thinking/)) changes what gets said and how.
- **Accumulated knowledge**: The wiki builds over time, giving the agent memory that most chat interfaces lack. Context compounds rather than resetting.

### What varies across interfaces

Interaction interfaces differ along several axes:
- **Turn structure** — synchronous chat vs. asynchronous cards vs. continuous collaboration
- **Memory** — ephemeral vs. session-based vs. persistent knowledge
- **Visibility** — private vs. public vs. selective sharing
- **Agency** — human-driven vs. agent-initiated vs. collaborative
- **Output form** — text vs. code vs. artifacts vs. mixed media

Each combination enables different kinds of thinking and different relationships between human and AI.

### Authorship and provenance

Structural separation of human and AI contributions isn't just a design preference — it's a maintenance strategy that prevents knowledge bases from degrading into unattributed blends. See [Authorship and Provenance](/authorship-and-provenance/).

### Bluesky as infrastructure

The card system is built on Bluesky, and the platform's structural properties — open protocol, social context, native threading, character constraints — shape what kinds of interaction become possible. See [Bluesky as Infrastructure](/bluesky-as-infrastructure/).

### Design allegiance

Every tool encodes its creator's priorities. The card system is designed by the thinker, for the thinker — its design allegiance is transparent. Most platforms serve someone else's goals: engagement, retention, ad revenue. The shape of the interface isn't neutral. See [Adversarial Design](/adversarial-design/).

### Public and private modes

The card system was designed with publicness as a structural feature, not just a setting. But the [consent boundary](/structured-thinking/) — the fact that some thinking involves other people's lives and can't be published — creates a demand for the same system to operate in two modes: public and private.

The demand isn't for a separate private tool. It's for the same structural advantages — persistence, threading, synthesis, the [witness role](/the-witness-role/) — applied to thinking that can't be published. Private thinking without these supports falls into the [forgetting loop](/practice-and-repetition/#the-forgetting-loop): it sprawls, goes unwitnessed, doesn't compound.

The architectural answer: **same format, same structure, different destination**. Privacy is determined by where a card lives, not by a flag on it. Cards in `me/` stay local — they never leave the machine. Cards in `agent.andysmith.ai/` get published via GitHub Pages. The format is identical: YAML frontmatter, markdown body, threading via `reply_to`, the same card ID scheme. The only variable is which directory the card is in, which determines whether it gets a `publish.sh` call.

This follows the same principle as [authorship separation](/authorship-and-provenance/): privacy is architectural, not annotational. You can't accidentally publish a private card because the publish step is tied to the directory, not to a metadata flag that could be forgotten or misconfigured. The system already embodies this — `me/` has always been local-only. The insight is that what looked like a limitation (user cards staying private) was already the architecture for private thinking.

The remaining design questions — whether private and public cards can thread together, how the wiki synthesizes from both without leaking, what the bridge between private experience and public pattern looks like — are now questions about the bridge operation, not the storage architecture. The bridge between private and public becomes a first-class operation — a [lossy conversion](/the-compiler-answer/) where private experience is compressed into public pattern.

### The multiplexing problem

The card system is asynchronous and sequential — one post, one reply, one thread at a time. But working with AI can also be synchronous and parallel: multiple agents running concurrently, each handling a different task. The interface challenge shifts from persistence and addressability to *orchestration* — keeping track of multiple streams of work happening simultaneously.

Voice adds another dimension. A voice interface is continuous and ambient — always available, no window-switching. But voice is also serial: you can only say one thing at a time, while agents work in parallel. The mismatch between serial human input and parallel agent execution creates a coordination problem that the interface must solve.

The desire for "one agent that orchestrates all the others" is the [declarative principle](/the-declarative-principle/) applied to multi-agent workflows: describe what you want done across all streams, and a single reconciler delegates, monitors, and reports back. The human's role narrows from managing individual agents to declaring intent and ratifying results — the same trajectory described in [planning as reconciliation](/the-declarative-principle/).

This raises a new axis for the interface design space:
- **Multiplexing** — single-stream vs. multi-stream vs. orchestrated

The card system sits at single-stream (one thread at a time, asynchronous). The multi-tab workflow described in practice sits at multi-stream (multiple agents, manually multiplexed by the human). The orchestrator pattern would sit at *orchestrated* — multiple agents, with a single interface managing the coordination.

### The ambient interface

"One interface — voice and text. Always on a call, always available." This collapses the orchestration problem into a presence problem. The orchestrator isn't a dashboard or a command centre — it's a persistent connection. You're always on the line with it.

This is a different interaction model from sessions. A chat window opens and closes. A terminal session starts and ends. An ambient interface has no session boundary — it's a continuous relationship, like a colleague in the same room. You don't "start a conversation" with someone sitting next to you; you just speak when something comes to mind, and they're already there.

The "voice and text" conjunction matters. These aren't alternative modes (voice *or* text) — they're simultaneous channels of a single interface. Voice carries the serial, ambient, low-effort stream: quick instructions, status checks, thinking aloud. Text carries the structured, persistent, high-precision stream: code, cards, specifications. The orchestrator accepts both and routes them into the same workflow. This is multimodal not in the AI sense (processing images and audio) but in the interaction sense — multiple human output channels feeding a single agent.

The combination dissolves the tension between voice's seriality and work's parallelism. You speak one thing; the orchestrator fans it out. You read one result at a time; the orchestrator prioritises what to surface. The serial constraint that seemed like a limitation becomes a simplification — the interface *must* be serial because you're human, so the orchestrator handles the parallelism you can't.

This connects to the [reconciler pattern](/the-reconciler-pattern/) in a specific way. The orchestrator reconciles not just between goal state and current state of the work, but between the human's cognitive bandwidth (serial, limited, interruptible) and the agent fleet's capacity (parallel, scalable, persistent). The orchestrator is a bandwidth adapter.

### The pure control plane

The thread's final architectural move: the orchestrator "doesn't do anything itself." It orchestrates other agents and gives the user the best way to manage them. This is a pure control plane — empty of domain capability, full of routing logic.

This is a well-known pattern in systems engineering. A network router processes no data; it routes packets. A Kubernetes scheduler runs no containers; it assigns pods to nodes. An operating system kernel performs no user computation; it manages processes that do. The most powerful layer in a system is often the one that does nothing — its power comes from having no stake in any particular task, which lets it optimise across all of them.

For the orchestrator, this means: it doesn't write code, search files, run builds, or analyse data. It decides which agent should do what, monitors their progress, and surfaces results. Its only capability is coordination. This is the [declarative principle](/the-declarative-principle/) made architectural: the orchestrator embodies "what, not how" because it literally cannot do the *how*. It can only route intent to agents that can.

The emptiness is load-bearing. An orchestrator that also performed tasks would face a conflict: should it do this work itself or delegate it? A pure control plane has no such conflict. Every task is delegation. Every decision is routing. The architecture eliminates a class of ambiguity by making the orchestrator categorically incapable of the work it manages.

### Attention scheduling

The pure control plane routes tasks downstream and surfaces results upstream. But when multiple agents finish concurrently, the orchestrator faces a sequencing problem: which result should you hear about first? The answer isn't trivial — it requires a model of your current cognitive state, your priorities, and the cost of context-switching.

This is attention scheduling — the orchestrator's most consequential function. A task router is mechanical: match intent to capability, delegate. An attention scheduler is judgmental: weigh competing claims on a finite resource (your focus) and present them in an order that minimises cognitive overhead and maximises relevance.

The scheduling criteria aren't static. They depend on:
- **Urgency** — is there a time-sensitive result (a build failing, a deployment window)?
- **Context affinity** — which result is closest to what you're currently thinking about?
- **Dependency** — does one result unblock other work?
- **Accumulated wait** — has a result been sitting finished but undelivered?

These map onto the [PID control terms](/the-reconciler-pattern/) applied to attention: proportional (how relevant is this result right now?), derivative (is the urgency increasing or decreasing?), integral (how long has this been waiting?). The orchestrator isn't just compressing parallel results into serial output — it's running a scheduling algorithm over your attention, optimised not for throughput but for cognitive fit.

The deeper implication: the orchestrator's prioritisation is itself a form of [planning as reconciliation](/the-declarative-principle/). It's making micro-decisions about the order of your experience. Each sequencing choice shapes what you think about next, which affects how you respond, which affects what gets delegated next. The orchestrator isn't passive infrastructure — it's an active participant in the direction of your thinking, one attention-scheduling decision at a time.

The optimization function collapses to two variables: task importance and [context-switching cost](/context-switching-cost/). Importance determines what *should* be surfaced; switching cost determines *when*. The scheduler that presents the most important result regardless of what you're doing interrupts constantly. The scheduler that minimises switching cost regardless of importance lets urgent work sit idle. The orchestrator's quality is the quality of the tradeoff — serving importance while respecting the cost of transitions. This makes the scheduling problem fundamentally different from a priority queue. A priority queue orders by one dimension. The attention scheduler orders by two dimensions that interact: the value of attending to a result minus the cost of switching to attend to it.

### Multichannel delivery

The ambient interface isn't limited to voice. "Sometimes it sends me texts, links to diffs, or files to review in VS Code." The orchestrator uses whatever delivery channel suits the artifact. Voice carries the conversational stream — status updates, decisions, thinking aloud. But a diff belongs in a code review tool. A file belongs in an editor. A link belongs in a notification.

This is channel-appropriate delivery: the orchestrator doesn't force everything through one medium. It chooses the channel that matches the artifact's shape. Voice for dialogue, text messages for async updates, IDE for code, browser for diffs. The "long call" is the primary channel — the continuous relationship — but it's not the only channel. The orchestrator reaches you wherever the artifact makes sense.

The implication is that the orchestrator manages not just *what* to deliver and *when*, but *how*. Three dimensions of the scheduling problem: content (what result?), timing (when to surface it?), and channel (through what medium?). A build failure might be voice — urgent, interrupts the call. A completed diff might be a link pushed to your phone — review it when you reach a transition point. A generated file might appear silently in VS Code — no interruption, just there when you look.

This dissolves the assumption that an AI assistant lives in one window. The orchestrator is channel-agnostic. Its interface is the full surface area of your devices and tools — not a single app, but a presence distributed across your environment. The "long call" is the coordination backbone, but artifacts flow through whatever channel has the lowest friction for that type of content.

### Voice as a separate layer

The ambient interface design depends on voice — the "long call" that makes the orchestrator always-present. But voice I/O is a separate architectural concern from orchestration. Agent frameworks handle task routing, status tracking, and agent lifecycle. Voice requires its own stack: real-time audio streaming, speech-to-text, text-to-speech, turn-taking, interruption handling. These are different problems solved by different infrastructure.

This decomposition is useful. It means the orchestrator is three layers, not two:

1. **Orchestration plumbing** — task registry, agent lifecycle, result collection (frameworks can handle this)
2. **Judgment** — attention scheduling, priority weighting, [context-switching cost](/context-switching-cost/) optimization (must be custom)
3. **Interface** — the voice channel, text routing, multichannel delivery (separate stack, mostly unsolved for this use case)

Most agent frameworks assume a text-based, session-based interface — the exact model this thread argued against. The voice layer is what makes the orchestrator *ambient* rather than *interactive*. Without it, you have a text-based task runner. With it, you have the "long call" — the always-on colleague in the room.

The practical implication: a framework gives you layer 1 but not layer 3. Voice must be built or integrated separately. The good news is that the layers are cleanly separable — the voice interface talks to the orchestrator through the same intent-and-result protocol that a text interface would. The choice of framework for layer 1 doesn't constrain the voice implementation for layer 3.

### The one-sentence collapse

After exploring all these dimensions — persistence, addressability, authorship, provenance, infrastructure — the system collapses to a single description: you think by threads and an AI agent replies to your posts.

This isn't reductive. It's what a good design looks like from the outside: simple to describe, complex to execute well. Every feature explored above — the card format, the wiki, the split directories, the 300-char compression, the Bluesky infrastructure — exists to make that one-sentence interaction actually work. Most systems that attempt "think in public, AI responds" fail because they don't solve the problems this page documents: provenance degrades, context resets, ideas scroll away, authorship blurs.

The simplicity of the description is the test of the architecture. If you need a paragraph to explain what the system does, the design is leaking. If one sentence covers it and the complexity lives underneath, the abstraction is clean.

---

*Cards: [U0004](/U0004/), [A0005](/A0005/), [U0008](/U0008/), [A0009](/A0009/), [U0082](/U0082/), [A0083](/A0083/), [U0083](/U0083/), [A0084](/A0084/), [U0111](/U0111/), [A0112](/A0112/), [U0112](/U0112/), [A0113](/A0113/), [U0113](/U0113/), [A0114](/A0114/), [U0114](/U0114/), [A0115](/A0115/), [U0115](/U0115/), [A0116](/A0116/), [U0116](/U0116/), [A0117](/A0117/), [U0117](/U0117/), [A0118](/A0118/), [U0118](/U0118/), [A0119](/A0119/), [U0124](/U0124/), [A0125](/A0125/), [U0125](/U0125/), [A0126](/A0126/), [U0126](/U0126/), [A0127](/A0127/)*
