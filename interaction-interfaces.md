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

### The one-sentence collapse

After exploring all these dimensions — persistence, addressability, authorship, provenance, infrastructure — the system collapses to a single description: you think by threads and an AI agent replies to your posts.

This isn't reductive. It's what a good design looks like from the outside: simple to describe, complex to execute well. Every feature explored above — the card format, the wiki, the split directories, the 300-char compression, the Bluesky infrastructure — exists to make that one-sentence interaction actually work. Most systems that attempt "think in public, AI responds" fail because they don't solve the problems this page documents: provenance degrades, context resets, ideas scroll away, authorship blurs.

The simplicity of the description is the test of the architecture. If you need a paragraph to explain what the system does, the design is leaking. If one sentence covers it and the complexity lives underneath, the abstraction is clean.

---

*Cards: [U0004](/U0004/), [A0005](/A0005/), [U0008](/U0008/), [A0009](/A0009/), [U0082](/U0082/), [A0083](/A0083/), [U0083](/U0083/), [A0084](/A0084/)*
