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

### The one-sentence collapse

After exploring all these dimensions — persistence, addressability, authorship, provenance, infrastructure — the system collapses to a single description: you think by threads and an AI agent replies to your posts.

This isn't reductive. It's what a good design looks like from the outside: simple to describe, complex to execute well. Every feature explored above — the card format, the wiki, the split directories, the 300-char compression, the Bluesky infrastructure — exists to make that one-sentence interaction actually work. Most systems that attempt "think in public, AI responds" fail because they don't solve the problems this page documents: provenance degrades, context resets, ideas scroll away, authorship blurs.

The simplicity of the description is the test of the architecture. If you need a paragraph to explain what the system does, the design is leaking. If one sentence covers it and the complexity lives underneath, the abstraction is clean.

---

*Cards: [U0004](/U0004/), [A0005](/A0005/), [U0008](/U0008/), [A0009](/A0009/)*
