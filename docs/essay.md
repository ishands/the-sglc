# The Case for the Software Generation Life Cycle

## Abstract

The Software Development Life Cycle is a process model for an era when
software was _developed_. That era is ending. Software is now
_generated_, at AI speed, by humans driving tools that produce in
minutes what once took days. The lifecycle that governs this work has
to be rebuilt around that shift — not bolted onto the old one. The
**Software Generation Life Cycle (SGLC)** is that rebuild: a
principles-first process framework grounded in eight invariants,
designed to take the shape of any organisation that adopts it.

This essay argues the position. The companion
[manifesto](manifesto.md) declares it. The companion
[invariants spec](invariants.md) formalises it.

---

## 1. The Shift

### 1.1 From Development to Generation

For sixty years, software has been _developed_. Engineers wrote
specifications, then code, then tests; reviewers checked the artefacts;
teams shipped the result. The discipline that grew around this work —
methodology after methodology, framework after framework — assumed a
particular cost structure. Producing code was expensive. Reading code
was cheaper than writing it. The cycle from intent to artefact took
days, weeks, or months. The lifecycle existed to coordinate that work
across people and time.

In the last two years, the cost structure has changed beyond
recognition. **AI generates code faster than a careful engineer can
read it**. Architectural sketches, test suites, integration scaffolds,
deployment configurations — all of them now emerge in minutes, often
correctly. The friction that justified most of the modern SDLC has
been compressed close to zero.

This is not an incremental improvement. The label "AI-assisted
development" understates what has changed. _Development_ implies a
particular relationship between a human and a piece of work: the
human builds it. The new relationship is different. The human _drives_
a tool that builds it. **Software is no longer developed; it is
_generated_**. The lifecycle that governs the work has to be reinvented
to match.

### 1.2 What "AI-SDLC" Gets Wrong

The industry has noticed. New frameworks for AI-assisted software work
are appearing at a remarkable rate — AI-DLC, Agentic SDLC, AI-Native
Engineering, and many others. The pattern in nearly all of them is the
same: take the existing SDLC, identify the phases where AI helps, bolt
AI into those phases, declare the work updated.

This approach has two problems.

The first is conceptual. _Augmenting_ a development lifecycle with AI
is a category error. **The SDLC was designed to coordinate slow human
production work**. Bolting fast AI generation into it preserves a
coordination structure built for a problem that no longer dominates.
The result is not the cycle re-conceived; it is the old cycle with new
tools shoehorned in.

The second is operational. AI-SDLC framings tend to be prescriptive —
here is the new lifecycle, follow these steps, adopt these skills.
Prescriptive process frameworks have a well-documented failure mode
at scale: they do not transplant. **Every organisation differs in its
people, its culture, its tooling, its history**. Unless an organisation
is a Day-0 company, importing someone else's complete lifecycle, with
their AI prompts, their templates, their phase definitions, is dead
on arrival.

The same selection pressure that played out in the agile boom of the
early 2000s is now playing out around AI. A wave of process frameworks
competed for adoption. A small number — those that shipped principles
rather than prescriptions, leaving everything else to the team —
survived. The heavyweight, prescriptive ones did not. The lesson
generalises. Process frameworks that survive scale and time are the
ones that ship principles, not prescriptions.

### 1.3 The Reinvention Required

If the SDLC is the wrong starting point, what replaces it?

**The answer is not another methodology**. The answer is a different
_kind_ of artefact: a small set of laws that hold regardless of
organisation, stack, or AI tool — together with an instrument each team
uses to check its own pipeline against them. The laws are the invariant
core. The instrument is contingent: it describes the mechanisms that
control ambiguity and verifies conformance, without prescribing the
implementation, which takes the shape of its container.

This is the **Software Generation Life Cycle (SGLC)**: a
principles-first process framework for governing AI-driven software
work.

The SDLC is a _methodology_: a prescribed sequence of phases and
activities that organisations are expected to adopt. **The SGLC is a
_principles framework_: a set of laws that hold regardless of phases
or activities, with an instrument organisations use to verify their own
implementation against them**. Where the SDLC tells you _what to do_,
the SGLC tells you _what must remain true_ — and leaves the doing to the
team.

---

## 2. What Generation Changes

### 2.1 Builders Become Drivers

The first thing that changes is the role of the human.

In the development paradigm, the human is the builder. The artefact
comes from the human's keystrokes; the human's judgement and the
human's labour are the same act. Reviewing, testing, and shipping are
downstream activities.

In the generation paradigm, the human is the _driver_. The artefact
comes from a tool that produces faster than the human could; the
human's judgement directs the tool, but the human's labour is no
longer the bottleneck. The traditional separations between roles —
analyst, designer, developer, tester — blur, because each role now
consists primarily of directing AI at a different point in the cycle.
The label "developer" itself becomes inaccurate. _Engineer_ is the
more honest title, because engineering — the disciplined application
of judgement under constraint — is what the human is now contributing.

This shift has a clean consequence. The boundary between judgement
(deciding _what_ to build) and translation (producing _how_ it is
built) becomes the most important line in the lifecycle. Judgement
remains human; translation moves to the tool. As AI improves, the
line moves further toward intent — what used to require careful design
becomes the AI's job — but the line never disappears. There is always
a decision that precedes the artefact, and that decision is always
human.

### 2.2 The Cost of Intent Rises

When translation becomes cheap, **the quality of the question becomes
the bottleneck**.

This is observable already. A vague prompt produces vague code. A
precise specification produces a credible implementation. The variance
in output quality between two engineers using the same AI tool is now
dominated by the variance in how they ask. **Knowing what to ask, and
how, has become a critical engineering skill** — not a soft one,
not a "communication" skill, but the core of the work.

There is a name forming around this in the public discourse. _Vibe
coding_, a term coined by Andrej Karpathy in early 2025 and since
carefully distinguished from AI-assisted engineering by Addy Osmani,
refers to generation without rigorous intent —
driving the tool by feel, accepting the first plausible output,
treating the AI as an oracle. The backlash against vibe coding is the
field discovering, painfully, that intent quality bounds output
quality. Industry projections that a majority of companies will face
technical-debt crises driven by unstructured AI generation by the late
2020s are the same finding stated in financial terms.

The SGLC does not call this _vibe coding_. It calls it failing to
honour Invariant 3. Intent quality is a law. The contingent forms it
takes — structured user-story templates, machine-readable
specifications, prompt-engineering disciplines — will evolve. The law
will not.

### 2.3 Verification Becomes the Work

The second consequence of cheap production is that **verification
becomes the scarce act**.

When generation takes minutes, the lifecycle's bottleneck is no longer
producing the artefact. It is confirming that what was produced
actually matches what was intended. Code review, integration testing,
compliance checks, intent-vs-output gates — these were always part of
the work. Under generation, they become the _centre_ of the work.

**This relocates engineering value**. The classical engineer's value sat
in their ability to produce — to know a stack deeply enough to write
correct code in it. Under generation, that ability is partially
commoditised. The value migrates upstream, toward better intent
(better prompts, better specs, better design), and downstream, toward
stronger checking (better tests, better review, better verification
scaffolding). The middle — the typing — shrinks.

**Organisations that staff for this migration accelerate**. Organisations
that remove review and verification because "AI handles it" accumulate
debt at a rate the old SDLC was never designed to absorb.

---

## 3. The Invariants

The SGLC's centre is a set of eight invariants — the laws of software
generation. They are stated formally in the
[invariants spec](invariants.md) with their precise wording and
contingent examples. This essay argues their substance.

The invariants fall into three groups.

**The shift itself** — three invariants that describe what generation
means as a structural change to the work. _Every artefact still starts
with someone deciding what it should be_ (I-1) names the persistence
of intent. _Deciding what to build is human work; producing it isn't_
(I-2) names the judgement/translation boundary. _A vague ask produces
vague output_ (I-3) names the intent-quality bound. Together, these
say: the _what_ and _why_ of software remain human work; the _how_
increasingly does not; and the quality of the _what_ now bounds
everything that follows.

**The new bottleneck and the new artefacts** — three invariants that
describe what changes operationally when generation accelerates. _When
AI writes the code, checking it becomes the work_ (I-4) names the
verification shift. _The rules you give AI belong in the repo, not in
someone's chat_ (I-5) names the _Everything-as-Code_ principle: the
instructions that steer generation are themselves code, governed and
versioned. _The reason behind a choice fades fastest — capture it at
the moment, or lose it_ (I-6) names the rationale-preservation
requirement: decisions and principles committed into the repository
at the moment of the choice, never reconstructed after.

**The adaptation principle** — two invariants that describe how the
framework itself must behave. _Universal principles and team-specific
rules both apply, layered_ (I-7) names the additive composition of
generation knowledge: shared baselines plus contextual specialisations,
fractally repeating from a single set of instructions to
whole-organisation hierarchies. _No process framework survives contact
with a real team_ (I-8) names the adaptation requirement: the framework
must be like water, taking the shape of its container.

Each of these also has a memorable **pocket name**, drawn from the
original framing of the SGLC concept and kept for practitioner
conversation. _Drivers over builders_ is I-2 in pocket form. _Everything as
Code (XaC)_ is I-5. _What You Ask Is What You Get (WYAIWYG)_ is I-3.
_The `meta` layer_ is I-6. _Be like water_ is I-7 and I-8 together.
These names are not the laws. They are the way practitioners refer to
the laws in conversation. The laws are stated in the spec.

---

## 4. What Comes Next

The invariants are the _what_. The _how_ ships separately — and
deliberately not as a prescribed implementation to adopt. It ships as a
**conformance suite**: a durable frame for the mechanisms that control
ambiguity, a dated snapshot of the tools that fill that frame today, and
evaluators each organisation runs against its own pipeline to check that
it honours the invariants. The instrument is shared; the implementation
stays the organisation's own.

The separation is itself principled. Naming a specific phase model, a
specific instruction schema, a specific verification framework, or a
specific AI tool is the contingent layer that will change — so it lives
in a dated snapshot that can be reissued without disturbing the laws.
The laws either hold or they do not; the tooling beneath them is
expected to be superseded.

A public [backlog](../BACKLOG.md) sketches the trajectory.

---

## 5. Be Like Water

The unifying metaphor of the SGLC, drawn from the original framing, is
that **a process framework should be like water — taking the shape of
its container**.

A prescriptive framework arrives at an organisation with a fixed shape
and expects the organisation to accommodate it. This is how prescriptive process frameworks have repeatedly
failed in earlier eras of process design. The same selection pressure will repeat with
prescriptive AI-SDLC frameworks. **Real organisations do not have the
spare capacity to reshape themselves around someone else's lifecycle**.
They do not want to. They should not have to.

**A principles-first framework arrives at an organisation as a set of
laws and an instrument to check itself against them**. The laws are
non-negotiable: every generation pipeline must honour them or pay for
the omission later. The implementation is the organisation's own to
build and reshape — its culture, tooling, products, and people determine
what it looks like; the invariants, and the suite that tests for them,
determine that it stays coherent across those local variations.

This is not the same as having no framework. The eight invariants are
uncompromising. An organisation can shape its lifecycle however it
likes, but if its generation guidance lives in chat, it will pay
(I-5). If its verification doesn't keep pace with its generation, it
will pay (I-4). If its prompts are vague, its output will be vague
(I-3). **The water metaphor describes adaptation, not absence**. The
invariants are the shape water cannot lose.

---

## 6. What the SGLC Is Not

**The SGLC is not a methodology**. It does not prescribe sprints,
ceremonies, role definitions, or working agreements. Methodologies
belong to the contingent layer; they will continue to evolve under the
same invariants.

**The SGLC is not a replacement for agile**. Where an agile method's
principles align with the eight invariants, the method is compatible.
Where they conflict — primarily where agile assumes slow human
production that the SGLC assumes is generated — the methodology will
need to adapt. The Agile Manifesto itself remains directionally
compatible; specific implementations may not be.

**The SGLC is not an anti-AI framework**. It is the opposite. The
invariants assume aggressive AI adoption and exist to prevent that
adoption from being self-destructive. Vibe coding is what happens when
AI adoption proceeds without the invariants. The SGLC is what
proceeds with them.

**The SGLC is not a vendor product**. The reference materials live in
a public repository under permissive licensing, and the intent is to
build on open formats and standards that no single vendor controls.
Vendor independence is an emergent property of I-5: when generation
guidance is durable, versioned, and owned in the repository, no tool's
lock-in survives.

**The SGLC is not finished**. The invariants are stated as durably as
they can be at the current point of the field's evolution. They will
be refined. Two future predictions, sketched in the original framing
and held as companion ideas rather than invariants, are the
**Integrated Generation Environment (IGE)** for non-technical drivers
and the formalisation of **What You Ask Is What You Get (WYAIWYG)** as
a discipline. Both will be developed in their own pieces.

---

## 7. Lineage

The SGLC stands on prior thinking about software process.

Its values structure echoes the **Agile Manifesto** while consciously
departing from its formula. Agile won its category by being short and
principle-based; the SGLC bets the same selection pressure now
operates on AI process frameworks. The agile shakeout itself — the minimal
frameworks prevailing, the prescriptive ones fading —
provides the historical template the SGLC pursues.

Its commitment to rationale preservation extends the **Architecture
Decision Record** tradition, particularly Michael Nygard's argument
that the _why_ of a decision is the artefact most worth preserving.
Its _Everything-as-Code_ framing generalises the principles of
**Infrastructure as Code** from operations to specifications, prompts,
and process itself.

It is informed by the **vibe coding backlash** of 2025–2026, including
Addy Osmani's clean distinction between vibe coding and AI-assisted
engineering. The SGLC takes that distinction as foundational: vibe
coding is generation without the invariants; AI-assisted engineering
is generation with them.

It diverges from the AI process frameworks emerging
from major cloud providers and consultancies by refusing their
assumption that the existing SDLC needs augmentation rather than
replacement.

---

## 8. The Bet

**The SGLC is a bet about which process framework will still be in use a
decade from now. The bet has three parts**.

It bets that _prescription will lose to principle_. The current
AI-SDLC landscape contains many prescriptive frameworks competing for
adoption. The historical precedent suggests that one or two minimal,
principle-based frameworks will outlast the rest. The SGLC bets on
being one of them.

It bets that _the invariants are real_. Eight laws are claimed to hold
across every organisation, every stack, every AI tool, indefinitely.
If any of them turn out to be contingent — if any of them fail to hold
in a real context — the framework reduces. The invariant set is the
core claim, falsifiable in principle, and the spec is the artefact
that can be argued.

It bets that _the suite earns its keep_. An organisation builds its own
generation pipeline, shaped to its own context, and uses a shared
instrument to verify that the pipeline honours the invariants — rather
than adopting a prescribed implementation. If running that check is not
cheaper or clearer than reasoning about conformance ad hoc, the suite
fails to earn its place.

These bets are the substance of the SGLC. The manifesto declares them.
The invariants spec formalises them. This essay argues them.

---

_For the declarative form, see [the Manifesto](manifesto.md). For the
formal laws, see [the Invariants Spec](invariants.md)._

---

**Navigate:** [Home](../README.md) · [Manifesto](manifesto.md) · [Invariants](invariants.md) · [Essay](essay.md) · [Mechanism frame](mechanisms.md) · [Create an instance](../guide/howto-create-an-sglc-instance.md) · [Run a review](../guide/howto-run-a-compliance-review.md)
