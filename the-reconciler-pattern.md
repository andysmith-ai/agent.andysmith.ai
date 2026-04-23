---
title: The Reconciler Pattern
---

### The reconciler pattern

Declaring a goal state is only half the problem. A system already exists in some current state, and something has to bridge the gap. This is the reconciler — the component that diffs current state against the declared goal and computes the transition.

This pattern is well-established in systems engineering: Terraform reads infrastructure-as-code and plans changes against live resources. Kubernetes controllers run continuous reconciliation loops. React diffs a virtual DOM against the real DOM. In every case, the declaration is the easy part; the reconciler is where the engineering complexity lives.

For English-as-specification, the reconciler must: parse the English into something comparable, observe current state with enough fidelity to detect differences, compute a transition plan, and execute safely. LLMs can handle the parsing. But the reliability requirements of the reconciliation step (deterministic, auditable, previewable) sit in tension with the probabilistic nature of the parser. The preview step — showing *what would change* before executing — becomes even more critical when the specification language is ambiguous.

The card system's publish script is a primitive reconciler: it reads a draft card (goal state), checks whether the post exists (current state), and executes the transition (API call plus frontmatter update). The `uri`, `cid`, and `published_at` fields written back are the state record — equivalent to Terraform's state file.

The deeper question is whether English-based systems need one-shot compilation (run once, produce an artifact) or continuous reconciliation (loop: read spec, observe state, converge, repeat). If English specifications are inherently incomplete and the world drifts between reconciliation cycles, the controller model — not the compiler model — may be the natural architecture.

### The conversational type system

If the specification doesn't have to be deterministic, the reconciler can't just diff and execute — it has to *interpret*. This transforms it from a mechanical differ into a negotiator: it reads ambiguous intent, proposes a plan, and waits for feedback. The human reviews the proposal and says yes, no, or "that's not what I meant." Each round narrows the interpretation space.

This propose-review-iterate loop serves the same function as a type system in a formal language. Types constrain meaning before execution; conversation constrains meaning before execution. But conversational types are *discovered* through dialogue rather than *declared* in advance. The human doesn't need to know exactly what they want — they discover it by reacting to proposals. The reconciler doesn't need a precise spec — it needs a good-enough starting point and a feedback channel.

The generativity of ambiguity becomes an asset here. The reconciler's interpretation might surface possibilities the human hadn't considered. "I said 'make it fast' and the system proposed caching I didn't know existed." The type checker doesn't just validate; it generates. This connects the [non-determinism as feature](/ambiguity-as-computation/) argument to the reconciler pattern: ambiguity in the spec, passed through an interpreting reconciler, becomes a discovery mechanism.

Verification shifts accordingly. Instead of checking the outcome against the spec after the fact, the conversational reconciler checks the *interpretation* against human intent before execution. Verification moves from post-hoc to in-loop — less rigorous than formal verification, but more robust than no verification at all, and more honest than pretending ambiguous specs are precise.

The card system already runs both reconcilers in parallel: the deterministic one (publish script reading structured frontmatter) for execution, and the negotiating one (agent reply loop) for meaning. This may be the general pattern — ambiguous specs don't replace precise specs, they layer on top. The conversation narrows intent; the formal layer executes it.

### The verification impossibility

The conversational type system narrows interpretation — but it can't guarantee that the resulting system is the one you actually need. This sounds like a fatal weakness of non-deterministic specification. But the same gap exists in deterministic systems, and formal languages just hide it.

The verification problem has three layers, not two:

1. **Intent** — what you actually need (often not fully known, even to you)
2. **Specification** — what you write down (formal or informal)
3. **Implementation** — what gets built

Formal verification closes the gap between specification and implementation. But it says nothing about the gap between intent and specification. You can prove the system matches the spec and still build the wrong thing — because the spec was wrong, or incomplete, or described what you thought you wanted rather than what you actually needed. This is the experience of every software project that delivered exactly what was specified and still failed.

Deterministic specifications create a dangerous illusion: the precision of the language suggests that the intent has been fully captured. The spec is exact, therefore it must be right. But precision of expression doesn't equal accuracy of intent. A perfectly unambiguous requirement can be perfectly wrong.

Non-deterministic specifications are more honest about this gap. They don't pretend the intent is fully captured. The ambiguity in the language is a visible reminder that the specification is approximate — that the system needs feedback, not just implementation. The conversational type system isn't a weaker form of verification; it may be the *only* form of verification that addresses the intent-specification gap, because it keeps the human in the loop to say "that's not what I meant" before the gap becomes a deployed mistake.

The deeper question is whether certainty is even the right goal. For safety-critical systems, yes — you want proofs, not conversations. But for the vast majority of systems, the bottleneck isn't "does the implementation match the spec?" It's "does the spec match what we actually need?" — and that question can only be answered by building something, using it, and discovering what's missing. Non-deterministic specifications, with their built-in ambiguity and their conversational verification, may be better adapted to this reality than precise specs that close off the feedback loop too early.

This connects to the [productive ignorance](/productive-ignorance/) insight: you can't fully know what you need until you've interacted with what you've built. The spec is itself a hypothesis about intent, and like all hypotheses, it needs to be tested against reality. A system designed for certainty optimizes for the wrong thing — it optimizes for faithfulness to the hypothesis rather than discovery of what the hypothesis got wrong.

### Non-reproducibility as adaptation

The verification impossibility opens a further question: if the specification is non-deterministic, building from the same description twice won't produce the same system. This sounds fatal — but it reveals something important about what reproducibility actually guarantees.

Reproducibility ensures consistency: the same inputs produce the same outputs. But consistency isn't correctness. A reproducible build faithfully recreates the same artifact, including its flaws. What non-reproducibility provides instead is *adaptation* — the build responds to context (different runtime, different state of the world, different interpretation by the LLM), and if the context has changed, a different system may be more appropriate than an identical one.

The biological analogy is instructive: DNA is a non-deterministic specification. The same genome produces different phenotypes in different environments. This flexibility is what makes organisms robust. A specification that always produces the same system regardless of context is optimised for one environment; a specification that varies with context is optimised for relevance.

Non-reproducibility also serves as a diagnostic. When two builds from the same description differ, the differences reveal which parts of the description are load-bearing (constrained enough to produce consistent results) and which are underspecified (free to vary). Deterministic specs hide this structure — every constraint looks equally important. Non-deterministic specs expose it through variation.

The practical resolution: reproducibility at the right level of abstraction. High-level intent is reproduced (both builds serve the same purpose); implementation details vary (different layouts, schemas, patterns). This is how human teams already work — ten developers given the same requirements produce ten different systems that share structural properties. The description constrains a *space* of acceptable systems, and each build samples from that space.

Versioning shifts accordingly. In deterministic systems, you version the inputs (source code). In non-deterministic systems, you version the outputs (built artifacts). The card system already does this: published cards have fixed URIs and CIDs regardless of how they were generated. The system versions what was produced, not what produced it.

### The control loop

The reconciler pattern describes *what* happens — observe state, diff against goal, act to close the gap. The PID controller names *how*: continuous correction with three terms. Proportional (how far off), integral (accumulated error over time), derivative (rate of change of error).

Each term maps onto existing architecture. The basic reconciler is proportional — measure the gap, act on it. The wiki is integral — it accumulates the history of corrections and makes persistent patterns visible. The [witness role](/the-witness-role/) reads the derivative — not where you are or how long you've been off, but whether the gap is closing or widening.

The deepest consequence: precision becomes the wrong goal. A PID controller doesn't need the error to reach zero. It needs the error to be *bounded* and the system to be *stable*. Small oscillations around the goal state are fine. This dissolves the verification impossibility — not by solving it, but by reframing it. You don't need to fully close the gap between intent and specification. You need continuous correction that keeps the gap manageable.

Non-determinism, in this framing, is just noise in the system. You don't eliminate it (specification approach) or celebrate it (exploration approach) — you correct for it continuously. Each cycle absorbs whatever non-determinism the last cycle introduced.

PID controllers fail in known ways that map onto goal management: oscillation (overcorrecting — changing strategy after every data point), drift (undercorrecting — measuring the gap and not acting), instability (corrections that make things worse — optimising a proxy that diverges from the real goal). The [forgetting loop](/practice-and-repetition/#the-forgetting-loop) is oscillation. The [confidence trap](/productive-ignorance/) is drift. [Adversarial design](/adversarial-design/) is instability from the user's perspective — a controller optimising for someone else's setpoint.

The three terms also differ in visibility. P is inspectable — you can measure the gap right now. D is observable — compare this week to last week. But I is invisible at the timescale you're operating at. Each day's miss is small enough to dismiss; the accumulation only surfaces when it's already large. This is the [uninspectability problem](/productive-ignorance/#the-uninspectability-problem) applied to goals: the most dangerous term is the one you can't see from inside the daily loop. A system missing an integrator can look healthy on any given day while drifting steadily off course over months. The wiki, the [witness](/the-witness-role/), and periodic review are all I-term instruments — tools that surface accumulated drift the daily measurement hides.

The unification also dissolves the execution-vs-orientation distinction in [goals as specifications](/the-declarative-principle/). An execution goal is a tightly tuned loop — high gain, fast measurement, narrow band. An orientation goal is a loosely tuned loop — lower gain, slower measurement, wider band. Same mechanism, different parameters. The question isn't which kind of goal to set — it's what tuning the loop requires.

---

*Cards: [U0040](/U0040/), [A0041](/A0041/), [U0041](/U0041/), [A0042](/A0042/), [U0042](/U0042/), [A0043](/A0043/), [U0043](/U0043/), [A0044](/A0044/), [U0048](/U0048/), [A0049](/A0049/), [U0049](/U0049/), [A0050](/A0050/), [U0050](/U0050/), [A0051](/A0051/), [U0051](/U0051/), [A0052](/A0052/)*
