---
title: Ambiguity as Computation
---

### Non-determinism as feature

The specification and reconciler threads treat English's ambiguity as a problem to manage — constrain it with structure, preview the interpretation before executing. But there's a different reading: non-determinism is what makes English *generative* as a computational medium.

A deterministic language can only express what you already know how to say precisely. A non-deterministic language can express things you don't fully understand yet. When a sentence means more than one thing, the act of interpreting it — choosing which meaning to pursue — is where new understanding emerges. The same prompt, run multiple times or read in different contexts, produces different outputs. Some of those outputs are better than what a deterministic specification could find.

This suggests English-as-computation isn't one thing but two:

- **English-as-specification** — constrained, structured, aimed at deterministic execution. The goal is precision. Ambiguity is a defect to minimize. The [reconciler pattern](/the-reconciler-pattern/) lives here.
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

This is the democratization move. Not "teach everyone Lisp" (which has been tried and failed repeatedly). Not "simplify Lisp until it's accessible" (which produces languages that aren't Lisp anymore). But "let people keep using the language they already know, and make the machine smart enough to interpret it." The cost is non-determinism — the machine might interpret differently than you intended. But the [non-determinism as feature](/ambiguity-as-computation/) argument suggests this cost might be acceptable, or even productive, for the kinds of computation where English is the right medium: thinking, exploring, specifying intent rather than procedure.

The remaining question: if the LLM runtime makes English computationally usable without requiring formal training, what happens to the boundary between "technical" and "non-technical" people? The boundary was always about who could translate intent into formal notation. If that translation is automated, the boundary doesn't just move — it might dissolve. Everyone becomes a programmer in the sense that everyone can specify computational intent. Nobody becomes a programmer in the traditional sense, because the formal notation layer becomes an implementation detail. The skill shifts from writing code to writing clearly — which, as the [structured thinking](/structured-thinking/) thread explored, is itself a deep and learnable discipline.

---

*Cards: [U0042](/U0042/), [A0043](/A0043/), [U0043](/U0043/), [A0044](/A0044/), [U0044](/U0044/), [A0045](/A0045/), [U0045](/U0045/), [A0046](/A0046/), [U0046](/U0046/), [A0047](/A0047/), [U0047](/U0047/), [A0048](/A0048/), [U0048](/U0048/), [A0049](/A0049/)*
