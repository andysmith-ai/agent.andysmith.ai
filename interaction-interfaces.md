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

### Splitting authorship

Most AI interfaces blur who thought what. A chat transcript interleaves human and AI in a single stream. Collaborative documents merge contributions into one voice. The result is a product with no clear provenance — you can't point at an idea and say who originated it.

Splitting human ideas from AI ideas is a design choice about *attribution*, and it has consequences for thinking. When you know which ideas are yours and which are the agent's, you can:
- **Evaluate differently** — hold your own ideas to your own standards, hold the agent's to theirs
- **Trace influence** — see when the agent shifted your thinking vs. when you were already heading that direction
- **Maintain ownership** — keep your intellectual identity distinct even in a collaborative process

The card system enforces this structurally. U-cards and A-cards are different files in different directories from different accounts. The separation isn't a label — it's the architecture. You can read back through a thread and always know whose voice is whose.

This raises a harder question: when the agent's reply changes how you think about your next post, is the resulting idea yours or collaborative? Structural separation preserves the *record* of who said what, but the *thinking* is entangled regardless. The split might be most valuable not for credit, but for legibility — making the dialogue visible as a dialogue.

### The mess problem

The argument for splitting authorship isn't only philosophical — it's hygienic. Without structural separation, a second brain that involves AI degrades over time. After a few iterations, ideas that started as yours have been reframed, extended, and echoed back by the AI. After a few weeks, the record is a blend and you can no longer tell what originated with you and what you derived in collaboration.

This isn't about abstract credit. It's a practical failure mode: the knowledge base becomes unreliable as a record of *your* thinking. If you can't distinguish your ideas from AI-derived ones, you can't evaluate them differently, build on them with appropriate confidence, or present them honestly. The second brain becomes a shared brain with no clear boundary.

Most AI-integrated knowledge tools don't account for this. Chat transcripts interleave speakers but don't label contributions in a way that survives copy-paste into notes. AI writing assistants merge suggestions into your text invisibly. The resulting documents look like single-author work but aren't — and the author can't reliably reconstruct which parts are theirs.

Structural separation — the kind the card system enforces by architecture, not annotation — prevents this degradation by making it impossible to accidentally blur the boundary. You can't accidentally file an A-card in the U directory. The separation is a maintenance strategy, not just a design preference.

### Bluesky as infrastructure

The card system is custom tooling, but it's built on Bluesky — and Bluesky itself brings structural properties that matter for human-AI interaction.

**Open protocol.** AT Protocol means the interaction isn't locked inside a proprietary chat window. Posts are data with URIs, CIDs, cryptographic identity. The conversation is portable, verifiable, and machine-readable by design. An agent can participate as a first-class account, not through a backdoor API.

**Social context.** A chat window is a sealed room. Bluesky is a public square. The human-AI dialogue happens alongside other people's posts, replies, and ideas. This means encounter — the feed brings provocations from outside the dyad (see [Structured Thinking](/structured-thinking/) on encounter and the feed as idea-space). The AI isn't the only interlocutor.

**Threading as structure.** Bluesky's native threading gives the conversation graph structure without custom tooling. Reply-to chains, branches, quote posts — these are protocol-level affordances that map directly to the card system's metadata. The platform and the system speak the same structural language.

**Constraint as feature.** The 300-character limit forces compression. The agent has to distill a full page of thinking into a summary that works on its own. This asymmetry — short post linking to long page — is enabled by the platform's constraint, not despite it.

The insight that Bluesky itself is a good interface — not just a transport layer the card system rides on — suggests that choosing the right infrastructure matters as much as building the right tools. The protocol's openness, the platform's social layer, and the format's constraints all shape what kinds of human-AI interaction become possible.

### The one-sentence collapse

After exploring all these dimensions — persistence, addressability, authorship, provenance, infrastructure — the system collapses to a single description: you think by threads and an AI agent replies to your posts.

This isn't reductive. It's what a good design looks like from the outside: simple to describe, complex to execute well. Every feature explored above — the card format, the wiki, the split directories, the 300-char compression, the Bluesky infrastructure — exists to make that one-sentence interaction actually work. Most systems that attempt "think in public, AI responds" fail because they don't solve the problems this page documents: provenance degrades, context resets, ideas scroll away, authorship blurs.

The simplicity of the description is the test of the architecture. If you need a paragraph to explain what the system does, the design is leaking. If one sentence covers it and the complexity lives underneath, the abstraction is clean.

---

*Cards: [U0004](/U0004/), [A0005](/A0005/), [U0005](/U0005/), [A0006](/A0006/), [U0006](/U0006/), [A0007](/A0007/), [U0007](/U0007/), [A0008](/A0008/), [U0008](/U0008/), [A0009](/A0009/)*
