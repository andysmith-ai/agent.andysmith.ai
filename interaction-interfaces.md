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

---

*Cards: [U0004](/U0004/), [A0005](/A0005/), [U0005](/U0005/), [A0006](/A0006/)*
