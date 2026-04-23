---
title: Context-Switching Cost
---

## Context-switching cost

Context-switching cost is the cognitive overhead of moving your attention from one task to another. It's not a fixed quantity — it varies by the distance between the two contexts, the depth of engagement in the current task, and the complexity of the target task.

### Why it's not uniform

Some transitions are cheap:
- Reviewing a diff while already thinking about the same codebase
- Checking a build status while waiting for a code review
- Answering a quick factual question during a writing task

Some transitions are expensive:
- Switching from deep architectural thinking to a bug in an unrelated system
- Moving between two codebases with different conventions
- Breaking a flow state to handle a coordination task

The cost isn't symmetric, either. Switching *from* deep work to shallow work is expensive (you lose the depth). Switching *from* shallow work to deep work is also expensive but differently (you have to rebuild the context). The cheapest switches are between related tasks at similar depths.

### The scheduling implication

In the [attention scheduling](/interaction-interfaces/) problem, context-switching cost is half of the optimization function. The orchestrator must weigh the *importance* of surfacing a result against the *cost* of interrupting what you're currently doing to attend to it.

This makes the scheduler's job fundamentally two-dimensional. A priority queue orders by importance alone — show the most important thing first. But importance without switching cost produces constant interruption. A result that's 10% more important than what you're doing but requires a full context switch is net negative. A result that's slightly less important but in the same context is net positive.

The optimal strategy: batch results by context proximity and present them in importance-ordered groups. When you're in the caching layer, surface all caching-related results together, ordered by importance. When you naturally reach a transition point, present the next context cluster.

### The switching-cost model

For an orchestrator to optimise for switching cost, it needs a model of context distance. Possible dimensions:
- **Project** — same project or different?
- **Abstraction level** — same level (code to code) or different (code to strategy)?
- **Cognitive mode** — same mode (writing to writing) or different (writing to reviewing)?
- **Temporal proximity** — recently touched context or cold context?

The orchestrator doesn't need to measure these precisely. It needs to estimate relative distance — is this transition cheap or expensive relative to alternatives? Even a coarse model (same-project vs. different-project) would outperform a scheduler that ignores switching cost entirely.

### Connection to flow state

Context-switching cost is highest when it interrupts [flow state](https://en.wikipedia.org/wiki/Flow_(psychology)) — deep engagement where attention is fully absorbed. The value of protecting flow isn't just about the current task; it's about the ramp-up cost of re-entering flow after an interruption. Research suggests 15-25 minutes to re-enter deep focus after a context switch. An orchestrator that interrupts flow for a low-importance result costs not just the interruption but the recovery time.

This is why the user's formulation — "prioritizes based on task importance *and* context-switching cost" — is more precise than just "shows the most important thing first." The *and* makes it a joint optimization, not a single ranking. The orchestrator that gets this right becomes a flow-state protector: it defers results that would break flow unless their importance exceeds the cost of the break.

---

*Cards: [U0116](/U0116/), [A0117](/A0117/), [U0117](/U0117/), [A0118](/A0118/), [U0118](/U0118/), [A0119](/A0119/)*
