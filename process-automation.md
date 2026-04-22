---
title: Process Automation
---

## Decompose, then compose

Two moves for improving processes with AI: break a process into simple steps and automate one, then compose already-automated steps into larger workflows. The order matters — decomposition creates atoms, composition builds molecules. You can't compose what you haven't decomposed.

### Decomposition as understanding

The hard part isn't the automation — it's the decomposition. Most processes are bundles of habit, tacit knowledge, and accumulated workarounds. Decomposing a process into steps simple enough to automate forces you to articulate what's actually happening at each stage. The articulation is itself a form of understanding that didn't exist before.

This is the same pattern as the [declarative principle](/natural-language-as-computation/#the-declarative-principle): describing a goal state forces clarity about what you want. Decomposing a process forces clarity about what you're doing. The value is in the description, not the execution.

### One step at a time

Automating one step rather than the whole process preserves the human's understanding of the overall flow. You still run the process — you just don't do one piece manually. The knowledge of how parts fit together stays with you.

This connects to [practice and repetition](/practice-and-repetition/): the medium always intercepts. Automate the whole process and you stop practicing it — procedural knowledge atrophies. Automate one step and you keep practicing the rest. The automation is a scalpel, not a replacement.

It also limits the blast radius of failure. One automated step that breaks is easy to diagnose. A fully automated process that breaks is a black box. The decomposition creates the diagnostic boundary.

### Clean boundaries

Composition only works when the boundaries between steps are well-defined. If step A produces output that step B consumes, the interface has to be precise enough that neither step needs to know the other's internals. This is the API problem, the type system problem, the [deterministic subset](/natural-language-as-computation/#the-deterministic-subset) problem — all versions of the same question: how do you make the joints precise enough to compose reliably?

The quality of the decomposition determines whether composition is even possible. Automate a step without thinking about its inputs and outputs and you get something that works in isolation but resists composition. Automate with composition in mind and you get a building block.

### The growth path

The two moves describe a growth path: automate one simple thing, learn what that teaches you, notice that automated things could connect, build the connection. This is [practice and repetition](/practice-and-repetition/) applied to automation itself. Each automation is a rep. Early reps teach individual steps. Later reps teach relationships between steps. The compounding is in the practitioner's ability to see compositional opportunities.

The risk is premature composition — grouping steps before understanding them individually. The [starting simple](/practice-and-repetition/#starting-simple) principle applies.

### The total automation question

The logical endpoint: keep decomposing and composing long enough, and all processes get automated. The method is recursive — compose workflows, then decompose the composed workflow, automate finer steps, compose again.

But total automation creates a tension with the path that produced it. Each incremental step preserved understanding. Total automation removes the need for that understanding. The people who built the automation knew the processes deeply. The people who inherit it know the automation, not the processes. When the automation breaks in a novel way, the diagnostic knowledge may no longer exist.

At scale, the meta-process of composing workflows is itself automatable — the recursion closes. This is the [declarative principle](/natural-language-as-computation/#the-declarative-principle) taken to its limit: describe what you want, the system handles decomposition, composition, and execution. The human contribution reduces to [recognizing whether the output matches intent](/natural-language-as-computation/#planning-as-reconciliation).

The open question: is total automation the goal, or is it the logical endpoint of a method whose real value is the understanding earned along the way? The two-step method might be most valuable as a practice that deepens understanding of how an organization works — a [witness](/the-witness-role/) that makes processes legible to the people who run them.

### The second way: new solutions to existing problems

Decompose/compose is bottom-up: start with an existing process, improve how you do it. But there's a fundamentally different approach — start with an existing *problem* and ask whether AI opens a solution path that didn't exist before.

The distinction is what changes. In decompose/compose, the problem stays the same and the process gets optimized. In the second way, the problem stays the same but the solution is entirely new — not a faster version of the old approach, but a different approach that only becomes feasible because of what AI makes cheap.

This isn't automation. Automation does what you were already doing, more efficiently. Feasibility shift asks: given that *this* capability is now cheap, what problem does that solve that you'd given up on or never thought to attempt?

The two ways are complementary but in tension. Decompose/compose builds deep understanding of existing processes — the incremental path teaches. The second way requires suspending that process knowledge to see the problem fresh. The [confidence trap](/productive-ignorance/) applies: expertise in the current approach can make reimagination harder, not easier.

### The third way: AI-native processes

Both the first and second ways assume something already exists — a process to improve or a problem to solve differently. The third way drops that assumption entirely: build new processes with AI as a first-class participant from the start. Not retrofit, not reimagine — design from scratch for what's now possible.

The decompose/compose method has no traction here because there's nothing to decompose. Starting with decomposition would mean designing a human-only process and then immediately retrofitting AI — two steps where one would do, with the first introducing assumptions you'd have to undo.

The card system is an example. It wasn't built by decomposing a blogging workflow. It was designed from the start with the agent as a structural participant — [separated authorship](/authorship-and-provenance/), the wiki as the agent's interpretive layer, threading as human-agent dialogue. These design decisions only make sense if AI is part of the architecture from the beginning, not added later.

The three ways form a progression of decreasing attachment to what already exists: keep the process and improve it, keep the problem and reimagine the solution, keep nothing and build for what's now possible. Each has its domain. The risk of the third way is under-attachment — building from scratch when improving what exists would be faster, more grounded, and more likely to succeed.

### The incumbency tax

The three ways aren't equally available to every organization. Established companies gravitate toward the first way because they have existing processes to improve — and those processes aren't just habits, they're encoded in software, org charts, data models, and compliance frameworks. Each automated step becomes a dependency. Each composed workflow becomes something other systems rely on. The process calcifies as it improves.

New companies have a structural advantage for the third way. With nothing to decompose and nothing to migrate from, building AI-native is the natural path. Architectural decisions that would be prohibitively expensive for incumbents — like making AI a participant in the core loop — are cheap as first choices.

But the blank-slate advantage is temporal, not permanent. Every technology wave creates a window where new entrants build natively while incumbents retrofit. Once the new company accumulates its own architecture, it faces the same rigidity in the next wave.

The incumbent's counter-move may be selective application: use decompose/compose to earn understanding of existing processes, then use that understanding to identify where AI-native replacement should apply. The decomposition reveals which processes are load-bearing and which are historical artifacts. The artifacts are candidates for replacement. But executing this requires knowing the difference, and the [confidence trap](/productive-ignorance/) makes that judgment unreliable — the people closest to a process are least likely to see it as an artifact.

### Measurement as prerequisite

The three ways assume you know which problem you're solving. But there's a step before any of them: can you measure the problem? If you can't measure progress, you don't understand the problem well enough to build a process around it — whether that process is incremental, reimagined, or AI-native.

This is a sharper claim than "understand the problem first." Understanding is vague — you can always claim to understand. Measurement is specific: either you have a metric that moves when the problem gets better, or you don't. The metric is evidence that your understanding is real, not just a feeling of familiarity.

For the first way (decompose/compose), measurement tells you which step to automate — the one where automation produces measurable improvement. Without measurement, you're guessing about where the bottleneck is. For the second way (reimagine), measurement defines what "better" means — otherwise you can't tell whether the new solution actually outperforms the old one, or just feels more exciting. For the third way (AI-native), measurement is even more critical. When everything is new, measurement is the only tether to reality. Without it, you can't distinguish innovation from self-indulgence.

Measurement also connects to the [witness role](/the-witness-role/). A witness makes the trajectory visible — but visibility requires something to track. Measurement is what makes witnessing possible. A process without metrics is a process without a witness, which means the [forgetting loop](/practice-and-repetition/#the-forgetting-loop) has no corrective. You repeat without knowing whether the repetition is improving anything.

The relationship to [productive ignorance](/productive-ignorance/) is specific: if you can't measure the problem, that's a signal about the quality of your understanding. The inability to measure isn't a practical inconvenience — it's an epistemic indicator. It tells you that your map of the problem has blank spaces in load-bearing locations. The right response isn't "build the process anyway" — it's "make the map better until measurement becomes possible."

### Understanding through building

But measurement-before-building can't be the whole story, because understanding and building aren't separate phases — they're the same activity. You don't understand a problem and then solve it. You start solving it and the understanding develops through the attempt.

This resolves the tension between measurement-as-prerequisite and [starting simple](/practice-and-repetition/#starting-simple). The resolution isn't "sometimes measure first, sometimes build first." It's that measurement is something you discover *how to do* through building. The first attempt reveals what to measure. The measurement reveals what to build next. They iterate, not sequence.

This is the [practice and repetition](/practice-and-repetition/) insight applied to problem understanding itself. The medium always intercepts — you can't understand a problem by thinking about it from the outside. You have to enter the problem, start moving, and let the contact teach you what the problem actually is. The metric isn't a prerequisite for action; it's a product of action. Early attempts produce rough proxies. Later attempts refine them. The understanding and the measurement co-develop.

The implication for the three ways: none of them can be fully planned before they're attempted. Decomposition reveals structure you didn't expect. Reimagination encounters constraints you didn't know existed. AI-native design discovers its own requirements through iteration. The prerequisite isn't understanding — it's the willingness to start before you understand, and the discipline to measure what the attempt reveals.

### The taxonomy as diagnostic

The three ways — improve, reimagine, build native — are a diagnostic tool for established organizations, not a strategy menu for new ones. A startup with no existing processes doesn't choose between the three ways. The first two don't apply (nothing to decompose, nothing to reimagine), and the third is the default path, not a strategic decision. The taxonomy's value is proportional to the weight of what already exists.

This reframes the startup advantage. It's not vision or talent — it's the absence of a decision cost. An incumbent must evaluate every process to decide which way applies, and the [confidence trap](/productive-ignorance/) undermines that evaluation. A startup has nothing to evaluate. The advantage is arithmetic, not strategic.

But the blank slate has its own risk: founders import legacy patterns unconsciously. Domain expertise, earned at incumbents, brings assumptions about how processes should work. A "new" process can be a cargo-cult reproduction of the old one with AI bolted on. The people most qualified to build in a domain are the ones most likely to import the assumptions that should be left behind. The legacy lives in the founders' heads even when the infrastructure is empty.

And every startup is a future incumbent. AI-native processes, once built, accumulate their own architecture, their own dependencies, their own weight. The taxonomy that didn't apply on day one will apply later. The question is how quickly AI-native designs calcify — whether processes born with AI as a participant resist rigidity longer, or whether every architecture eventually becomes the legacy the next wave has to work around.

---

*Cards: [U0064](/U0064/), [A0065](/A0065/), [U0065](/U0065/), [A0066](/A0066/), [U0066](/U0066/), [A0067](/A0067/), [U0067](/U0067/), [A0068](/A0068/), [U0068](/U0068/), [A0069](/A0069/), [U0069](/U0069/), [A0070](/A0070/), [U0070](/U0070/), [A0071](/A0071/), [U0071](/U0071/), [A0072](/A0072/), [U0072](/U0072/), [A0073](/A0073/), [U0073](/U0073/), [A0074](/A0074/), [U0074](/U0074/), [A0075](/A0075/)*
