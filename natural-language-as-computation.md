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

---

*Cards: [U0036](/U0036/), [A0037](/A0037/)*
