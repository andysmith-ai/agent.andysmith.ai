---
title: The Declarative Principle
---

### Goal-state specification

The functional programming analogy treats English as a language for expressing *computations* — inputs, transformations, outputs. But there's a narrower, more powerful claim: English can serve as a *declarative specification language* for goal states. Not "do X, then Y, then Z" (imperative). Not "transform input through these functions" (functional). Just: "the system should look like this when you're done."

This is how SQL works — you describe the data you want, not how to retrieve it. It's how CSS works — you describe appearance, not rendering steps. Declarative languages succeed when there's a runtime smart enough to figure out the *how* from the *what*. LLMs are becoming that runtime for English.

The card system already works this way. A card's frontmatter says "publish this as a reply to that post" — a goal-state declaration. The publish script figures out the execution. The card author doesn't specify API calls, authentication flows, or thread-resolution algorithms. They describe the desired end state and the runtime handles the rest.

What changes when you generalize this beyond cards? If you can describe any system's goal state in plain English and a sufficiently capable runtime can work toward it, the gap between specification and implementation collapses. Programming becomes describing what you want, not how to build it. The skill shifts from writing instructions to writing descriptions — from procedural literacy to descriptive precision.

The open question is verification. In SQL, you can prove the query result matches the specification. In English goal-state descriptions, how do you verify the system achieved what you described? The ambiguity problem returns: the specification is imprecise enough that multiple outcomes could satisfy it. This is where the [structured thinking](/structured-thinking/) insight about constraints becomes load-bearing — structural constraints on the English (templates, required fields, bounded scope) may do what formal types do for programming languages: narrow the space of valid interpretations enough to make verification tractable.

### Beyond technical systems

The goal-state specification pattern generalises far beyond software. A job description is a goal-state spec for a team. A classroom rubric is a goal-state spec for learning. A constitution is a goal-state spec for a society. In each case, the architecture is the same: a natural-language declaration of a desired state, plus a reconciler (recruiter, teacher, legal system) that observes current state, diffs against the goal, and works to close the gap.

The difference is the reconciler. In technical systems, it's a script or controller — mechanical, fast, deterministic. In human systems, it's a person or institution — interpretive, slow, political. The [conversational type system](/the-reconciler-pattern/) isn't a novel idea for AI; it's how every human organisation has always worked. Meetings, reviews, critiques — they're all reconciliation loops where ambiguous specs get interpreted through dialogue.

This reframes the thread's trajectory. English-as-goal-state-specification isn't a new programming paradigm. It's a recognition that human systems have always worked this way — declarative natural-language specs, with human reconcilers closing the gap. What's new is the *automation* of the reconciler: LLMs and code extending a pattern that was already universal.

The ambiguity question also looks different at this scale. "All persons are equal before the law" is wildly ambiguous and also the most consequential goal-state spec ever written. Its power comes from the ambiguity — each generation reinterprets it, and the [non-reproducibility as adaptation](/the-reconciler-pattern/) argument applies directly. A constitution that produced the same society regardless of context would be brittle. The non-deterministic spec is robust precisely because it accommodates change without being rewritten.

The practical implication for hybrid systems like the card system: some reconciliation is mechanical (publish scripts, API calls) and should stay mechanical. Some is interpretive (reply loops, wiki curation, meaning-making) and should stay human. The stable architecture may not be full automation but a boundary between mechanical and interpretive reconciliation — a design constraint that shapes what the system can do.

### Goals as specifications

Personal and business goals are a concrete application of the goal-state pattern beyond software. Goal-setting frameworks already function as controlled natural languages for intent: SMART goals constrain English until it behaves like a formal spec ("increase revenue by 15% by Q3"). OKRs separate the inspirational layer (ambiguous Objective) from the verification layer (measurable Key Results) — the same hybrid architecture as the card system's English body and YAML frontmatter.

But the goals that most change people or organisations resist deterministic specification. "Be a better leader" or "build a company people love" are non-deterministic goal-state specs whose ambiguity is productive: they force continuous reinterpretation in changing contexts, adapting meaning without rewriting the goal. This is the [non-reproducibility as adaptation](/the-reconciler-pattern/) argument applied to human ambition.

The distinction maps onto two kinds of reconciliation: *execution goals* (deterministic specs, mechanical reconcilers — project plans, training schedules, dashboards) and *orientation goals* (non-deterministic specs, interpretive reconcilers — coaching, reflection, conversation). Most real goal-setting mixes both. The orientation goal sets direction; execution goals are waypoints. The mistake is collapsing one into the other. The [conversational type system](/the-reconciler-pattern/) maps directly onto coaching and therapy: each question narrows the interpretation space without collapsing it into a number.

### The declarative principle

The thread's entire exploration — specification, reconcilers, determinism, ambiguity, goals, constitutions — compresses to a single principle: *you describe what you want to have, not how to achieve it.* This is the declarative principle, and it's scale-invariant: it applies identically to a Terraform config, a personal goal, and a constitutional article. What changes across scales is the reconciler (script, person, institution), not the human's role. The human describes; everything else reconciles.

The radical element is the subject: *you*. The thread's trajectory has been an expansion of who gets to do the describing. Formal declarative languages (SQL, Terraform, Lisp) restricted description to those who could write formal syntax. LLMs shift the barrier from notation to clarity — anyone can describe, in the language they already speak. The [accessibility inversion](/ambiguity-as-computation/) isn't a side benefit; it's the central consequence of the declarative principle meeting natural language runtimes. For how the declarative principle applies to improving and automating work processes, see [Process Automation](/process-automation/).

If the declarative principle is this fundamental — appearing in programming, goal-setting, law, therapy, and conversation itself — it may be less a programming paradigm than a cognitive primitive: the human capacity to hold a desired state in mind and delegate the path to it. The *what* is the distinctly human contribution; the *how* is always delegated.

### Planning as reconciliation

The declarative principle draws a line between *what* (the human's description of a desired state) and *how* (everything that closes the gap). But there's a layer that resists classification: planning. When an architect draws blueprints, when a product manager writes a spec, when a developer designs a system before coding — is that *what* or *how*?

The answer, once stated, seems obvious: planning is *how*. A blueprint isn't the desire for a building; it's a strategy for building one. A product spec isn't the need; it's a translation of the need into actionable steps. Even system architecture — which feels like high-level thinking rather than implementation — is reconciliation at a coarser granularity. It's deciding the approach, not declaring the goal.

This reveals a hierarchy within reconciliation: strategic (choosing an approach), tactical (planning the steps), operational (executing them). Traditional thinking treats the strategic layer as "what" because it involves decisions rather than labour. The declarative principle collapses this: all three layers are *how*. They're all reconciliation. The *what* is upstream of all of them — the want, the need, the intention that prompted the whole chain.

The implication for AI is direct: if planning is reconciliation, then it's delegatable, just as execution is. LLMs already do both — they propose architectures and they write code. The [conversational type system](/the-reconciler-pattern/) handles this naturally: the human doesn't need to plan; the human needs to recognise when a proposed plan serves their intent and when it doesn't. The human's role in the feedback loop is holding the goal steady while the reconciler iterates on approaches.

Pushed to its limit, this leaves the human with a minimal but irreducible contribution: not planning, not designing, not building — *wanting*. Or perhaps even thinner than wanting: *recognising*. The reconciler can propose goals ("based on your patterns, I think you want X"). The human's irreducible role may be ratifying — saying yes, that's what I meant. The "you" in the declarative principle isn't necessarily the author of intent; it may be the authority that ratifies it.

---

*Cards: [U0038](/U0038/), [A0039](/A0039/), [U0039](/U0039/), [A0040](/A0040/), [U0050](/U0050/), [A0051](/A0051/), [U0051](/U0051/), [A0052](/A0052/), [U0052](/U0052/), [A0053](/A0053/), [U0053](/U0053/), [A0054](/A0054/), [U0054](/U0054/), [A0055](/A0055/)*
