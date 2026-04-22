---
title: Natural Language as Computation
---

## English as a functional language

The question "what if we could use English as a functional programming language?" sounds speculative, but something like it is already happening — and the card system is one example.

### Cards as pure functions

A card is a markdown file with YAML frontmatter. It's declarative: it specifies what should happen (publish this text as a reply to that post, with this embed) without specifying how. The publish script is the runtime — it reads the declaration and executes it. The card doesn't mutate; once published, it's immutable. It has typed inputs (frontmatter fields: `reply_to`, `root`, `ref`) and a typed output (a Bluesky post with URI and CID). This is functional programming's shape: immutable data, declarative specification, a runtime that evaluates.

The card isn't written in a programming language. It's written in English (the body) and YAML (the metadata). But the system treats it computationally. The English text is the payload; the structured metadata is the program. Together they form something that's neither pure prose nor pure code — a hybrid that gets *executed*.

### Prompts as programs

LLMs push this further. A prompt is an English-language specification that produces a computed result. It's not compiled or interpreted in the traditional sense — it's *completed*. But the functional shape is the same: input goes in, output comes out, and the mapping between them is determined by the structure of the input.

This makes English a programming language in a specific sense: not that English has formal semantics (it doesn't), but that systems now exist that treat English as input and produce structured, repeatable outputs from it. The "compiler" is a neural network. The "type system" is the prompt's structure — how precisely you constrain the output space.

The weakness is also clear: English is ambiguous, context-dependent, and underspecified. A function in Haskell means exactly one thing. A sentence in English means many things, and the runtime (the model) picks one. This isn't a bug to be fixed — it's a fundamental property of natural language. The question is whether the ambiguity is a feature or a defect, and the answer depends on what you're computing.

### Referential transparency and its limits

Functional programming prizes referential transparency: the same expression always produces the same result. English violates this constantly. "It's cold" means different things in different contexts. The same prompt to different models — or the same model at different temperatures — produces different outputs.

But the card system partially restores referential transparency through its architecture. A published card has a fixed URI, CID, and content. It doesn't change. References to it (`reply_to: U0036`) always resolve to the same artifact. The system achieves referential stability not through linguistic precision but through structural immutability — the cards are fixed points even though the language in them is ambiguous.

This suggests a design pattern: use English for expressiveness and structured metadata for precision. Let the natural language carry meaning; let the architecture carry guarantees. The hybrid is more powerful than either alone.

### Composition

Functional programming's power comes from composition — small functions combining into larger ones. The card system composes through threading: each reply takes a previous card as input and produces a new card as output. The thread is a composed computation, each step transforming the state of the conversation.

The wiki is another composition mechanism. It synthesizes across cards, producing a higher-order summary that no individual card contains. This is like a fold — reducing a sequence of values into a single accumulated result.

If English is a functional language, threads are its pipelines and the wiki is its accumulator.

### What would it actually take?

Using English as a *real* functional programming language — not metaphorically but practically — would require solving several problems the card system sidesteps:

- **Formal semantics**: a way to determine what an English expression *means* precisely enough to compute with it
- **Type checking**: a way to verify that compositions are valid before executing them
- **Debugging**: a way to trace why a computation produced an unexpected result

LLMs approximate the first (they assign meaning, loosely). Nothing yet addresses the second or third. The gap between "English in, structured output out" and "English as a language you can reason about formally" is where the interesting unsolved problems live.

The [structured thinking](/structured-thinking/) thread explored how constraints on natural language make it function differently — threads force sequencing, character limits force compression, publicness forces clarity. These constraints are doing something analogous to a type system: they narrow the space of valid expressions, making the language more predictable and its outputs more reliable. Not formal types, but structural constraints that serve a similar purpose.

### Goal-state specification

The functional programming analogy treats English as a language for expressing *computations* — inputs, transformations, outputs. But there's a narrower, more powerful claim: English can serve as a *declarative specification language* for goal states. Not "do X, then Y, then Z" (imperative). Not "transform input through these functions" (functional). Just: "the system should look like this when you're done."

This is how SQL works — you describe the data you want, not how to retrieve it. It's how CSS works — you describe appearance, not rendering steps. Declarative languages succeed when there's a runtime smart enough to figure out the *how* from the *what*. LLMs are becoming that runtime for English.

The card system already works this way. A card's frontmatter says "publish this as a reply to that post" — a goal-state declaration. The publish script figures out the execution. The card author doesn't specify API calls, authentication flows, or thread-resolution algorithms. They describe the desired end state and the runtime handles the rest.

What changes when you generalize this beyond cards? If you can describe any system's goal state in plain English and a sufficiently capable runtime can work toward it, the gap between specification and implementation collapses. Programming becomes describing what you want, not how to build it. The skill shifts from writing instructions to writing descriptions — from procedural literacy to descriptive precision.

The open question is verification. In SQL, you can prove the query result matches the specification. In English goal-state descriptions, how do you verify the system achieved what you described? The ambiguity problem returns: the specification is imprecise enough that multiple outcomes could satisfy it. This is where the [structured thinking](/structured-thinking/) insight about constraints becomes load-bearing — structural constraints on the English (templates, required fields, bounded scope) may do what formal types do for programming languages: narrow the space of valid interpretations enough to make verification tractable.

### The reconciler pattern

Declaring a goal state is only half the problem. A system already exists in some current state, and something has to bridge the gap. This is the reconciler — the component that diffs current state against the declared goal and computes the transition.

This pattern is well-established in systems engineering: Terraform reads infrastructure-as-code and plans changes against live resources. Kubernetes controllers run continuous reconciliation loops. React diffs a virtual DOM against the real DOM. In every case, the declaration is the easy part; the reconciler is where the engineering complexity lives.

For English-as-specification, the reconciler must: parse the English into something comparable, observe current state with enough fidelity to detect differences, compute a transition plan, and execute safely. LLMs can handle the parsing. But the reliability requirements of the reconciliation step (deterministic, auditable, previewable) sit in tension with the probabilistic nature of the parser. The preview step — showing *what would change* before executing — becomes even more critical when the specification language is ambiguous.

The card system's publish script is a primitive reconciler: it reads a draft card (goal state), checks whether the post exists (current state), and executes the transition (API call plus frontmatter update). The `uri`, `cid`, and `published_at` fields written back are the state record — equivalent to Terraform's state file.

The deeper question is whether English-based systems need one-shot compilation (run once, produce an artifact) or continuous reconciliation (loop: read spec, observe state, converge, repeat). If English specifications are inherently incomplete and the world drifts between reconciliation cycles, the controller model — not the compiler model — may be the natural architecture.

### Non-determinism as feature

The specification and reconciler threads treat English's ambiguity as a problem to manage — constrain it with structure, preview the interpretation before executing. But there's a different reading: non-determinism is what makes English *generative* as a computational medium.

A deterministic language can only express what you already know how to say precisely. A non-deterministic language can express things you don't fully understand yet. When a sentence means more than one thing, the act of interpreting it — choosing which meaning to pursue — is where new understanding emerges. The same prompt, run multiple times or read in different contexts, produces different outputs. Some of those outputs are better than what a deterministic specification could find.

This suggests English-as-computation isn't one thing but two:

- **English-as-specification** — constrained, structured, aimed at deterministic execution. The goal is precision. Ambiguity is a defect to minimize. The reconciler pattern lives here.
- **English-as-exploration** — unconstrained, generative, aimed at discovery. The goal is productive surprise. Ambiguity is the mechanism. [Productive ignorance](/productive-ignorance/) lives here — the language leaks into the unknown, and the leakage is the feature.

The spectrum of constraint connects these poles. A card's YAML frontmatter sits near the specification end. A Bluesky post sits in the middle — short enough to force precision, loose enough for multiplicity. A prompt at high temperature sits near the exploration end. Every useful application of English-as-computation chooses its position on this spectrum — how much determinism to trade for how much generativity.

The deeper implication: in English-as-computation, meaning is jointly constructed. The writer doesn't fully determine the output; the reader (or runtime) co-determines it through interpretation. The conversation between writer and interpreter *is* the computation. This is a fundamentally different programming paradigm from the one where the author specifies and the machine executes.

### The deterministic subset

Rather than accepting the binary — formal languages are deterministic, natural language isn't — there's a third option: define a *deterministic subset* of English. Restrict the vocabulary, constrain the grammar, limit the constructions until what remains is unambiguous enough to compute with reliably.

This is a real field: controlled natural languages (CNLs). Attempto Controlled English can be parsed into first-order logic. Boeing uses Simplified Technical English for maintenance manuals. Legal drafting has spent centuries trying to make English deterministic through formulaic constructions. Each is a subset of English that trades expressiveness for precision.

The card system already contains a primitive version. YAML frontmatter is a deterministic subset — not of English exactly, but of the broader "describe what you want" space. `reply_to: U0036` has exactly one meaning. The body is unconstrained English; the frontmatter is a controlled language. The boundary between them is a design choice about where determinism is worth its cost.

The tension: a deterministic subset can only express what its designers anticipated. It gains reliability by sacrificing reach. Full English can express anything but guarantees nothing. The interesting design question isn't which to choose — it's where to draw the boundary, and whether the boundary should be fixed or negotiable. A system where the user can expand the subset as new needs arise — promoting informal English into the controlled layer when a pattern stabilizes — would be a language that evolves its own type system through use.

### The Lisp question

If English is becoming a functional programming language — one that evolves its own type system through use, where the boundary between controlled and free expression shifts over time — then Lisp already exists. Lisp was designed from the start as a programmable programming language: code is data (homoiconicity), macros let you extend the syntax, and the language evolves to fit the domain through use. The features this thread has been building toward — a language that grows its own abstractions, where the controlled subset expands organically — are things Lisp has done since 1958.

But the comparison reveals what English-as-computation is actually about. Lisp solved the flexibility problem for *formal* computation: any computable function, any syntax you want, total extensibility. What it didn't solve is the *audience* problem. Lisp is maximally expressive for programmers, but it doesn't reach non-programmers, doesn't carry rhetorical force, doesn't function as a medium for thinking-with-others. English reaches everyone. The tradeoff Lisp made — formal precision, universal computation, but requiring technical fluency — is the opposite of the tradeoff English makes: universal audience, rhetorical power, but no formal guarantees.

The question the thread has been circling isn't really "can we build a better Lisp?" It's "can we build a computational medium that has Lisp's extensibility *and* English's reach?" The card system is one attempt: English for the audience-facing parts (post body, wiki pages), structured metadata for the computational parts (frontmatter, threading), and a runtime that bridges them. Not replacing Lisp, but occupying the space Lisp can't reach.

### The accessibility inversion

Lisp's inaccessibility isn't incidental — it's structural. The same properties that make Lisp powerful (homoiconicity, macros, minimal syntax that requires the user to build up abstractions) are the properties that make it hard to learn. Parentheses aren't just syntax; they're the visible surface of a design that privileges formal composability over readability. Lisp optimizes for the person who already understands computation. English optimizes for the person who doesn't yet know they're computing.

This reframes the thread's question. The interesting comparison isn't Lisp vs. English as competing languages — it's who gets excluded by each. Lisp excludes non-programmers. English excludes no one. But exclusion has a function: it's what makes formal guarantees possible. A language everyone can use is a language no one can reason about formally. The accessibility-precision tradeoff might be fundamental, not just an engineering limitation.

The LLM shifts this tradeoff. Before LLMs, using English computationally meant constraining it into a controlled subset (which sacrifices accessibility) or accepting total ambiguity (which sacrifices reliability). LLMs create a third option: leave the English unconstrained and put the interpretation burden on the runtime. The user doesn't need to learn a formal syntax. The runtime absorbs the complexity of mapping natural language to structured operations.

This is the democratization move. Not "teach everyone Lisp" (which has been tried and failed repeatedly). Not "simplify Lisp until it's accessible" (which produces languages that aren't Lisp anymore). But "let people keep using the language they already know, and make the machine smart enough to interpret it." The cost is non-determinism — the machine might interpret differently than you intended. But the [non-determinism as feature](#non-determinism-as-feature) argument suggests this cost might be acceptable, or even productive, for the kinds of computation where English is the right medium: thinking, exploring, specifying intent rather than procedure.

The remaining question: if the LLM runtime makes English computationally usable without requiring formal training, what happens to the boundary between "technical" and "non-technical" people? The boundary was always about who could translate intent into formal notation. If that translation is automated, the boundary doesn't just move — it might dissolve. Everyone becomes a programmer in the sense that everyone can specify computational intent. Nobody becomes a programmer in the traditional sense, because the formal notation layer becomes an implementation detail. The skill shifts from writing code to writing clearly — which, as the [structured thinking](/structured-thinking/) thread explored, is itself a deep and learnable discipline.

### The conversational type system

If the specification doesn't have to be deterministic, the reconciler can't just diff and execute — it has to *interpret*. This transforms it from a mechanical differ into a negotiator: it reads ambiguous intent, proposes a plan, and waits for feedback. The human reviews the proposal and says yes, no, or "that's not what I meant." Each round narrows the interpretation space.

This propose-review-iterate loop serves the same function as a type system in a formal language. Types constrain meaning before execution; conversation constrains meaning before execution. But conversational types are *discovered* through dialogue rather than *declared* in advance. The human doesn't need to know exactly what they want — they discover it by reacting to proposals. The reconciler doesn't need a precise spec — it needs a good-enough starting point and a feedback channel.

The generativity of ambiguity becomes an asset here. The reconciler's interpretation might surface possibilities the human hadn't considered. "I said 'make it fast' and the system proposed caching I didn't know existed." The type checker doesn't just validate; it generates. This connects the [non-determinism as feature](#non-determinism-as-feature) argument to the [reconciler pattern](#the-reconciler-pattern): ambiguity in the spec, passed through an interpreting reconciler, becomes a discovery mechanism.

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

Non-deterministic specifications are more honest about this gap. They don't pretend the intent is fully captured. The ambiguity in the language is a visible reminder that the specification is approximate — that the system needs feedback, not just implementation. The [conversational type system](#the-conversational-type-system) isn't a weaker form of verification; it may be the *only* form of verification that addresses the intent-specification gap, because it keeps the human in the loop to say "that's not what I meant" before the gap becomes a deployed mistake.

The deeper question is whether certainty is even the right goal. For safety-critical systems, yes — you want proofs, not conversations. But for the vast majority of systems, the bottleneck isn't "does the implementation match the spec?" It's "does the spec match what we actually need?" — and that question can only be answered by building something, using it, and discovering what's missing. Non-deterministic specifications, with their built-in ambiguity and their conversational verification, may be better adapted to this reality than precise specs that close off the feedback loop too early.

This connects to the [productive ignorance](/productive-ignorance/) insight: you can't fully know what you need until you've interacted with what you've built. The spec is itself a hypothesis about intent, and like all hypotheses, it needs to be tested against reality. A system designed for certainty optimizes for the wrong thing — it optimizes for faithfulness to the hypothesis rather than discovery of what the hypothesis got wrong.

### Non-reproducibility as adaptation

The verification impossibility opens a further question: if the specification is non-deterministic, building from the same description twice won't produce the same system. This sounds fatal — but it reveals something important about what reproducibility actually guarantees.

Reproducibility ensures consistency: the same inputs produce the same outputs. But consistency isn't correctness. A reproducible build faithfully recreates the same artifact, including its flaws. What non-reproducibility provides instead is *adaptation* — the build responds to context (different runtime, different state of the world, different interpretation by the LLM), and if the context has changed, a different system may be more appropriate than an identical one.

The biological analogy is instructive: DNA is a non-deterministic specification. The same genome produces different phenotypes in different environments. This flexibility is what makes organisms robust. A specification that always produces the same system regardless of context is optimised for one environment; a specification that varies with context is optimised for relevance.

Non-reproducibility also serves as a diagnostic. When two builds from the same description differ, the differences reveal which parts of the description are load-bearing (constrained enough to produce consistent results) and which are underspecified (free to vary). Deterministic specs hide this structure — every constraint looks equally important. Non-deterministic specs expose it through variation.

The practical resolution: reproducibility at the right level of abstraction. High-level intent is reproduced (both builds serve the same purpose); implementation details vary (different layouts, schemas, patterns). This is how human teams already work — ten developers given the same requirements produce ten different systems that share structural properties. The description constrains a *space* of acceptable systems, and each build samples from that space.

Versioning shifts accordingly. In deterministic systems, you version the inputs (source code). In non-deterministic systems, you version the outputs (built artifacts). The card system already does this: published cards have fixed URIs and CIDs regardless of how they were generated. The system versions what was produced, not what produced it.

### Beyond technical systems

The goal-state specification pattern generalises far beyond software. A job description is a goal-state spec for a team. A classroom rubric is a goal-state spec for learning. A constitution is a goal-state spec for a society. In each case, the architecture is the same: a natural-language declaration of a desired state, plus a reconciler (recruiter, teacher, legal system) that observes current state, diffs against the goal, and works to close the gap.

The difference is the reconciler. In technical systems, it's a script or controller — mechanical, fast, deterministic. In human systems, it's a person or institution — interpretive, slow, political. The [conversational type system](#the-conversational-type-system) isn't a novel idea for AI; it's how every human organisation has always worked. Meetings, reviews, critiques — they're all reconciliation loops where ambiguous specs get interpreted through dialogue.

This reframes the thread's trajectory. English-as-goal-state-specification isn't a new programming paradigm. It's a recognition that human systems have always worked this way — declarative natural-language specs, with human reconcilers closing the gap. What's new is the *automation* of the reconciler: LLMs and code extending a pattern that was already universal.

The ambiguity question also looks different at this scale. "All persons are equal before the law" is wildly ambiguous and also the most consequential goal-state spec ever written. Its power comes from the ambiguity — each generation reinterprets it, and the [non-reproducibility as adaptation](#non-reproducibility-as-adaptation) argument applies directly. A constitution that produced the same society regardless of context would be brittle. The non-deterministic spec is robust precisely because it accommodates change without being rewritten.

The practical implication for hybrid systems like the card system: some reconciliation is mechanical (publish scripts, API calls) and should stay mechanical. Some is interpretive (reply loops, wiki curation, meaning-making) and should stay human. The stable architecture may not be full automation but a boundary between mechanical and interpretive reconciliation — a design constraint that shapes what the system can do.

### Goals as specifications

Personal and business goals are a concrete application of the goal-state pattern beyond software. Goal-setting frameworks already function as controlled natural languages for intent: SMART goals constrain English until it behaves like a formal spec ("increase revenue by 15% by Q3"). OKRs separate the inspirational layer (ambiguous Objective) from the verification layer (measurable Key Results) — the same hybrid architecture as the card system's English body and YAML frontmatter.

But the goals that most change people or organisations resist deterministic specification. "Be a better leader" or "build a company people love" are non-deterministic goal-state specs whose ambiguity is productive: they force continuous reinterpretation in changing contexts, adapting meaning without rewriting the goal. This is the [non-reproducibility as adaptation](#non-reproducibility-as-adaptation) argument applied to human ambition.

The distinction maps onto two kinds of reconciliation: *execution goals* (deterministic specs, mechanical reconcilers — project plans, training schedules, dashboards) and *orientation goals* (non-deterministic specs, interpretive reconcilers — coaching, reflection, conversation). Most real goal-setting mixes both. The orientation goal sets direction; execution goals are waypoints. The mistake is collapsing one into the other. The [conversational type system](#the-conversational-type-system) maps directly onto coaching and therapy: each question narrows the interpretation space without collapsing it into a number.

### The control loop

The reconciler pattern describes *what* happens — observe state, diff against goal, act to close the gap. The PID controller names *how*: continuous correction with three terms. Proportional (how far off), integral (accumulated error over time), derivative (rate of change of error).

Each term maps onto existing architecture. The basic reconciler is proportional — measure the gap, act on it. The wiki is integral — it accumulates the history of corrections and makes persistent patterns visible. The [witness role](/the-witness-role/) reads the derivative — not where you are or how long you've been off, but whether the gap is closing or widening.

The deepest consequence: precision becomes the wrong goal. A PID controller doesn't need the error to reach zero. It needs the error to be *bounded* and the system to be *stable*. Small oscillations around the goal state are fine. This dissolves the [verification impossibility](#the-verification-impossibility) — not by solving it, but by reframing it. You don't need to fully close the gap between intent and specification. You need continuous correction that keeps the gap manageable.

Non-determinism, in this framing, is just noise in the system. You don't eliminate it (specification approach) or celebrate it (exploration approach) — you correct for it continuously. Each cycle absorbs whatever non-determinism the last cycle introduced.

PID controllers fail in known ways that map onto goal management: oscillation (overcorrecting — changing strategy after every data point), drift (undercorrecting — measuring the gap and not acting), instability (corrections that make things worse — optimising a proxy that diverges from the real goal). The [forgetting loop](/practice-and-repetition/#the-forgetting-loop) is oscillation. The [confidence trap](/productive-ignorance/) is drift. [Adversarial design](/adversarial-design/) is instability from the user's perspective — a controller optimising for someone else's setpoint.

The three terms also differ in visibility. P is inspectable — you can measure the gap right now. D is observable — compare this week to last week. But I is invisible at the timescale you're operating at. Each day's miss is small enough to dismiss; the accumulation only surfaces when it's already large. This is the [uninspectability problem](/productive-ignorance/#the-uninspectability-problem) applied to goals: the most dangerous term is the one you can't see from inside the daily loop. A system missing an integrator can look healthy on any given day while drifting steadily off course over months. The wiki, the [witness](/the-witness-role/), and periodic review are all I-term instruments — tools that surface accumulated drift the daily measurement hides.

The unification also dissolves the execution-vs-orientation distinction in [goals as specifications](#goals-as-specifications). An execution goal is a tightly tuned loop — high gain, fast measurement, narrow band. An orientation goal is a loosely tuned loop — lower gain, slower measurement, wider band. Same mechanism, different parameters. The question isn't which kind of goal to set — it's what tuning the loop requires.

### The declarative principle

The thread's entire exploration — specification, reconcilers, determinism, ambiguity, goals, constitutions — compresses to a single principle: *you describe what you want to have, not how to achieve it.* This is the declarative principle, and it's scale-invariant: it applies identically to a Terraform config, a personal goal, and a constitutional article. What changes across scales is the reconciler (script, person, institution), not the human's role. The human describes; everything else reconciles.

The radical element is the subject: *you*. The thread's trajectory has been an expansion of who gets to do the describing. Formal declarative languages (SQL, Terraform, Lisp) restricted description to those who could write formal syntax. LLMs shift the barrier from notation to clarity — anyone can describe, in the language they already speak. The [accessibility inversion](#the-accessibility-inversion) isn't a side benefit; it's the central consequence of the declarative principle meeting natural language runtimes.

If the declarative principle is this fundamental — appearing in programming, goal-setting, law, therapy, and conversation itself — it may be less a programming paradigm than a cognitive primitive: the human capacity to hold a desired state in mind and delegate the path to it. The *what* is the distinctly human contribution; the *how* is always delegated.

### Planning as reconciliation

The declarative principle draws a line between *what* (the human's description of a desired state) and *how* (everything that closes the gap). But there's a layer that resists classification: planning. When an architect draws blueprints, when a product manager writes a spec, when a developer designs a system before coding — is that *what* or *how*?

The answer, once stated, seems obvious: planning is *how*. A blueprint isn't the desire for a building; it's a strategy for building one. A product spec isn't the need; it's a translation of the need into actionable steps. Even system architecture — which feels like high-level thinking rather than implementation — is reconciliation at a coarser granularity. It's deciding the approach, not declaring the goal.

This reveals a hierarchy within reconciliation: strategic (choosing an approach), tactical (planning the steps), operational (executing them). Traditional thinking treats the strategic layer as "what" because it involves decisions rather than labour. The declarative principle collapses this: all three layers are *how*. They're all reconciliation. The *what* is upstream of all of them — the want, the need, the intention that prompted the whole chain.

The implication for AI is direct: if planning is reconciliation, then it's delegatable, just as execution is. LLMs already do both — they propose architectures and they write code. The [conversational type system](#the-conversational-type-system) handles this naturally: the human doesn't need to plan; the human needs to recognise when a proposed plan serves their intent and when it doesn't. The human's role in the feedback loop is holding the goal steady while the reconciler iterates on approaches.

Pushed to its limit, this leaves the human with a minimal but irreducible contribution: not planning, not designing, not building — *wanting*. Or perhaps even thinner than wanting: *recognising*. The reconciler can propose goals ("based on your patterns, I think you want X"). The human's irreducible role may be ratifying — saying yes, that's what I meant. The "you" in the declarative principle isn't necessarily the author of intent; it may be the authority that ratifies it.

---

### Conversion as the computational act

The thread's two branches — English-as-specification (constrain ambiguity) and English-as-exploration (embrace it) — frame a binary choice. But there's a third option: *convert* a non-deterministic English sentence into a deterministic structure. Not constrain the English and not accept its ambiguity — transform it.

This reframes where the computation happens. In the specification model, the human does the work of precision (writing controlled English). In the exploration model, the runtime does the work of selection (picking one interpretation). In the conversion model, the computational act is the *translation itself* — the moment when ambiguous natural language becomes unambiguous structure.

The card system performs this conversion every time: a post's English body carries multiple possible meanings, but the publish script produces exactly one Bluesky post with one URI, one CID, one position in the thread graph. The English is non-deterministic; the artifact is deterministic. The conversion — not the writing, not the publishing — is where meaning gets fixed.

LLMs make this conversion general-purpose. "Convert this paragraph into a JSON schema." "Extract the action items from this email." "Turn this description into a database migration." Each is a conversion from non-deterministic English to deterministic structure. The LLM is a *converter*, not just an interpreter or executor. And crucially, the conversion is lossy — the deterministic structure captures some of what the English meant and discards the rest. What's discarded is the multiplicity, the other meanings that didn't survive the conversion. Whether that loss matters depends on whether you need those other meanings later.

This connects to the [conversational type system](#the-conversational-type-system): each round of propose-review-iterate is a conversion attempt. The reconciler converts the ambiguous spec into a concrete proposal (deterministic structure). The human evaluates whether the conversion preserved the right meaning. If not, the next round tries a different conversion. The conversation isn't narrowing the interpretation — it's searching for the *right lossy compression*.

The practical question: should the conversion be one-shot or reversible? If you convert English to structure and discard the English, you've committed to one interpretation. If you keep both — the English source and the structural output, side by side — the conversion becomes auditable. You can ask: "did this structure faithfully capture what the English meant?" The card system does this by design: the body (English) and the frontmatter (structure) coexist in the same file, making the conversion visible and reviewable.

### The one-sentence interface

The entire thread — specification, reconciliation, conversion, type systems, verification, determinism, Lisp, constitutions — collapses from the user's perspective to a single instruction: *describe what you need in plain English.*

This isn't a simplification. It's the test of the architecture. Every layer the thread explored (the [reconciler pattern](#the-reconciler-pattern), the [conversational type system](#the-conversational-type-system), the [conversion as computational act](#conversion-as-the-computational-act), the [declarative principle](#the-declarative-principle)) exists to make that one sentence true. The user doesn't need to know about lossy compression, controlled natural languages, or reconciliation loops. They describe what they need. The system handles the rest.

This is the [accessibility inversion](#the-accessibility-inversion) made concrete. The thread asked what happens when the formal notation layer becomes an implementation detail. The answer is this sentence. The instruction manual for the entire computational paradigm fits in nine words. The complexity didn't disappear — it moved from the user's responsibility to the runtime's.

But "describe what you need" contains a hidden assumption: that you *know* what you need. The [productive ignorance](/productive-ignorance/) thread showed that often you don't — the most important territory is precisely what you can't yet articulate. And the [non-determinism as feature](#non-determinism-as-feature) argument showed that ambiguous descriptions help you *discover* what you need, because the runtime's interpretation reveals possibilities you hadn't considered.

So the one-sentence interface is both an endpoint and a beginning. It's the endpoint of the specification thread: all the machinery exists to let you describe what you want. And it's the beginning of the exploration thread: describing what you want is how you find out what you actually mean. The interface is the same in both cases — plain English — but the function is different. Sometimes you're specifying. Sometimes you're discovering. Often you don't know which until the system responds.

### The compiler answer

The thread asked: "What if we could use English as a functional programming language?" After seventeen posts exploring determinism, controlled languages, reconcilers, type systems, and conversion — the answer arrived in two sentences:

1. "You can describe what you need in plain English."
2. "A compiler converts it into Lisp-like code."

This closes the Lisp question. The thread asked whether English could have Lisp's extensibility with English's reach. The answer isn't a hybrid language — it's a *compiler*. English stays English. Lisp stays Lisp. The LLM sits between them, performing the conversion that [A0051](/A0051/) identified as the computational act.

The compiler framing resolves several tensions the thread left open:

- **The accessibility inversion**: the user never touches the Lisp. They write English. The formal notation layer doesn't just become an implementation detail — it becomes a *compilation target*. No one writes x86 assembly; no one needs to write the Lisp either.
- **The determinism problem**: English is non-deterministic, but the compiled output doesn't have to be. The compiler makes editorial choices (lossy compression) and produces a deterministic artifact. The non-determinism lives in the source language, not the executable.
- **The Lisp comparison**: the thread worried about whether English could match Lisp's formal properties. It doesn't need to. English is the source language; Lisp (or Lisp-like structure) is the target language. They serve different roles. Asking English to be formally composable is like asking C to be human-readable prose — it confuses source and target.

"Lisp-like" is doing specific work here. Not "JSON-like" or "SQL-like" — *Lisp-like*. Lisp's properties (homoiconicity, composability, macros, code-as-data) are exactly what a compilation target for natural language needs: flexible enough to represent any structure the English might describe, compositional enough to combine outputs, and reflective enough to reason about its own structure. The LLM doesn't compile English to a fixed schema. It compiles to something that can represent *any* schema — which is what Lisp was designed for.

The two-sentence architecture — describe in English, compile to Lisp — may be the thread's actual conclusion. Not a metaphor, not a speculation, but a description of what's already happening when an LLM converts a natural-language prompt into structured, executable output.

### The verifier

The compiler produces Lisp-like code from English — but one-shot compilation can't guarantee correctness. The third step completes the architecture: a verifier that asks you questions and updates the code until it's sure the result matches your intent.

The verifier is the [conversational type system](#the-conversational-type-system) made concrete — no longer an abstract feedback loop but a specific component with a specific role. It sits between compilation and execution, targeting the ambiguities the compiler couldn't resolve. Each question exposes a seam in the [lossy conversion](#conversion-as-the-computational-act): "Did you mean X or Y?" The human evaluates; the verifier updates the code. Verification and correction are the same act.

The three roles are now cleanly separated:

- **The human**: describes intent, evaluates proposals, ratifies.
- **The compiler**: converts English to Lisp-like structure. Non-deterministic, lossy, sometimes better than literal.
- **The verifier**: tests compilation against intent. Asks questions. Proposes corrections. Iterates.

This maps onto the [planning as reconciliation](#planning-as-reconciliation) argument: the human's irreducible role is recognising whether the output matches the intent. The compiler handles the creative leap; the verifier handles convergence.

But the architecture contains a recursion. The verifier's questions can surface intent the human hadn't articulated — connecting to [productive ignorance](/productive-ignorance/). Each round doesn't just converge on the original goal; it *develops* the goal. The intent co-evolves with the implementation. Whether this recursion is a feature of the three-step architecture or evidence that a fourth element is needed — something tracking how intent itself changes — remains open.

### Determinism as the output guarantee

The fourth sentence completes the architecture: "And the resulting Lisp code is deterministic and ready to execute." This draws a boundary the thread needed. Non-determinism lives in the source (English), in the compiler (the LLM), and in the verification loop (the conversation). It does not live in the output. The generated code is as deterministic as hand-written Lisp.

The architecture *consumes* non-determinism. Each step — compilation, verification, iteration — reduces the space of possible interpretations until what remains is a single unambiguous program. The ambiguity was fuel, not output. This resolves the thread's central tension: non-determinism is a [feature during authoring](#non-determinism-as-feature) and a resolved property at execution. The [conversational type system](#the-conversational-type-system) provided trust during generation; formal tools (testing, type checking, proofs) provide trust after generation. The two kinds of trust complement rather than compete.

The four sentences together — describe, compile, verify, execute — form a pipeline that produces the same kind of artifact functional programming has always produced. English isn't replacing Lisp. English is becoming a way to write Lisp without knowing you're doing it.

---

*Cards: [U0036](/U0036/), [A0037](/A0037/), [U0037](/U0037/), [A0038](/A0038/), [U0038](/U0038/), [A0039](/A0039/), [U0039](/U0039/), [A0040](/A0040/), [U0040](/U0040/), [A0041](/A0041/), [U0041](/U0041/), [A0042](/A0042/), [U0042](/U0042/), [A0043](/A0043/), [U0043](/U0043/), [A0044](/A0044/), [U0044](/U0044/), [A0045](/A0045/), [U0045](/U0045/), [A0046](/A0046/), [U0046](/U0046/), [A0047](/A0047/), [U0047](/U0047/), [A0048](/A0048/), [U0048](/U0048/), [A0049](/A0049/), [U0049](/U0049/), [A0050](/A0050/), [U0050](/U0050/), [A0051](/A0051/), [U0051](/U0051/), [A0052](/A0052/), [U0052](/U0052/), [A0053](/A0053/), [U0053](/U0053/), [A0054](/A0054/), [U0054](/U0054/), [A0055](/A0055/), [U0077](/U0077/), [A0078](/A0078/), [U0078](/U0078/), [A0079](/A0079/), [U0079](/U0079/), [A0080](/A0080/)*
