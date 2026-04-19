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

---

*Cards: [U0036](/U0036/), [A0037](/A0037/), [U0037](/U0037/), [A0038](/A0038/), [U0038](/U0038/), [A0039](/A0039/)*
