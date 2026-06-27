# How to Create an SGLC Instance

An **SGLC instance** is your organisation's own concrete pipeline for
governing AI-driven software work — the actual files, skills, rules, and
gates that carry the [invariants](../docs/invariants.md) into your
repositories. The SGLC does not hand you that pipeline. It gives you the
laws every pipeline must respect and a [frame](../docs/mechanisms.md) for
describing the mechanisms that uphold them, and leaves the building to you.

This guide is about why that division is the right one, and how to build your
instance so that it honours the very invariants it will later be
[reviewed against](./howto-run-a-compliance-review.md).

> It stays at the **durable** level — which moves to make, not which product
> to buy. For which tool plays which role _today_, it points to the current
> [tooling snapshot](./tooling-snapshot-2026-06.md) (the contingent layer,
> superseded as tooling moves — see [guide/README.md](./README.md)).

## Why define your own, rather than adopt an "AI SDLC"

You can buy a finished "AI SDLC" — a fixed lifecycle, a prescribed catalogue
of stages and tools. Don't mistake it for what you need. Four reasons to
author your own instance instead.

**A fixed lifecycle is dead on arrival — [Local fit (I-8)](../docs/invariants.md#i-8--no-process-framework-survives-contact-with-a-real-team).**
Every team differs in people, history, tools, and constraints. An
off-the-shelf "AI SDLC" is someone else's coordinates, pre-chosen for someone
else's container. The process framework must be like water, taking the shape
of _your_ container — and a catalogue you adopt as-is cannot be water.

**The universal part is the invariants, not the implementation.** What
actually holds across every organisation is the eight laws. Everything
beneath them — which tool, which file, which gate — is contingent and changes;
the [dated snapshot](./README.md) exists precisely because tooling churns.
Adopt the part that is stable and build the part that is local. Adopting
someone's implementation is adopting their contingent layer, expiry date and
all.

**Building it is how the team understands it.** Siting each mechanism forces
the decisions the invariants demand — where intent originates, where the
judgement boundary sits, what must be enforced rather than merely advised. A
copied pipeline skips those decisions, so the team never internalises them,
and it rots the first time reality diverges from the template.

**You still don't start from a blank page — [Layering (I-7)](../docs/invariants.md#i-7--universal-principles-and-team-specific-rules-both-apply-layered).**
Authoring your own instance is not reinventing everything. You inherit the
universal baseline — the invariants and this mechanism frame — and add your
local specialisation on top. That is exactly the layering the SGLC asks for:
baseline plus specialisation, both active. And the shape is fractal: it
recurs _inside_ your instance too, an org-wide baseline carrying team- and
product-level specialisations layered on it — not only your instance layered
over the universal.

So: **adopt the invariants; author the instance.**

## What an instance is made of

An instance is a set of **mechanisms**, and every mechanism is a coordinate
in the frame defined by [docs/mechanisms.md](../docs/mechanisms.md):
**(role × strength × residence)**.

- [**Role**](../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
  — Awareness, Recognition, Procedure, or Enforcement: how the guidance
  reaches the point of generation.
- [**Strength**](../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
  — advisory (rests on model attention) through deterministic (a gate that
  fires regardless): the compliance ceiling.
- [**Residence**](../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds)
  — repo-shared and durable, or machine-local and personal: who it binds and
  how long it survives.

Building an instance is **choosing your coordinates** — which mechanism plays
each role, at what strength, in what residence. The frame names the axes; it
does not choose your points. That choice is yours to fit, and refit.

## Build it by walking the invariants

Here is the load-bearing idea: **build the instance in the order the
invariants impose, and it honours them by construction.** The eight laws a
[compliance review](./howto-run-a-compliance-review.md) checks are also the
best blueprint for building. Each step is a build move plus the invariant it
satisfies.

1. **Start from intent, not tooling — [Intent origin (I-1)](../docs/invariants.md#i-1--every-artifact-still-starts-with-someone-deciding-what-it-should-be).**
   Decide what your generation pipeline is _for_ before wiring a single tool.
   Name the artefacts that must exist before generation runs — discovery,
   framing, specification, under whatever names you give them.

2. **Mark the judgement boundary — [Judgement boundary (I-2)](../docs/invariants.md#i-2--deciding-what-to-build-is-human-work-producing-it-isnt).**
   Decide which artefacts are human-judged (the _what_ and _why_) and which
   are AI-translated (the _how_). This split is structural: it says where
   humans must stay in the loop, and it drives your naming — `create-*` for
   judgement artefacts, `generate-*` for translation ones.

3. **Make the ask precise — [Ask precision (I-3)](../docs/invariants.md#i-3--a-vague-ask-produces-vague-output).**
   Give generation a well-formed input contract: templated specs, structured
   stories, intent checklists — whatever forces clarity before generation
   begins. This is the highest-leverage mechanism you will build, because it
   caps everything downstream.

4. **Site verification to match the stakes — [Output verification (I-4)](../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work).**
   For each kind of output, decide how it is checked and how hard. Match the
   [strength](../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
   of the check to what is at stake: advisory review where a miss is cheap, a
   deterministic gate where it must hold every time. Escalate advisory →
   enforced as stakes rise; never downgrade unless the risk genuinely falls.

5. **Put every rule in the repo — [Rule residence (I-5)](../docs/invariants.md#i-5--the-rules-you-give-ai-belong-in-the-repo-not-in-someones-chat).**
   Skills, templates, principles, gates — all of it committed, versioned,
   owned by name. A standard the team must honour that lives in someone's
   chat history or personal config is not part of the instance; it is a
   liability. (Personal _preference_ belongs in machine-local residence; team
   _standards_ belong in the repo.)

6. **Capture the why as you choose — [Rationale capture (I-6)](../docs/invariants.md#i-6--the-reason-behind-a-choice-fades-fastest--capture-it-at-the-moment-or-lose-it).**
   Build a step that records the reason behind a choice at the moment it is
   made — a decision record, an ADR, a rationale field — committed alongside
   the work. At generation speed, "document it later" never catches up.

7. **Layer, don't fork — [Layering (I-7)](../docs/invariants.md#i-7--universal-principles-and-team-specific-rules-both-apply-layered).**
   Compose a shared baseline with local specialisations that activate _on top
   of_ it, rather than each team editing its own copy. Inherit and extend; do
   not duplicate and diverge. This is how an instance scales across teams
   without fragmenting.

8. **Fit it to your team, and expect to refit — [Local fit (I-8)](../docs/invariants.md#i-8--no-process-framework-survives-contact-with-a-real-team).**
   Adopt what fits, replace what doesn't, and treat every mechanism as
   reshapeable. An instance is never finished; it bends as the team and the
   tooling change. The dated-snapshot discipline ([guide/README.md](./README.md))
   is this invariant applied to the tooling layer — supersede, don't ossify.

The order is not arbitrary. It follows the
[couplings the orchestrator relies on](../skills/review-sglc-compliance/):
intent and the judgement boundary feed precision and verification; residence
and rationale capture underwrite all of it; layering and local fit govern the
shape. **Build upstream before downstream and each mechanism has something
sound to rest on.**

## Wire the front door

A mechanism that exists but is not discoverable is only half-resident. Wire
your instance from its front door — `README.md` and `AGENTS.md`, or your
tool's equivalent — so every rule, skill, and gate is reachable from the
entry point a new contributor or agent reads first. The discovery walk a
reviewer performs
([Locating mechanisms in an instance](./tooling-snapshot-2026-06.md#locating-mechanisms-in-an-instance))
starts at that front door; mechanisms not wired from it will not be found — by
the reviewer, the next engineer, or the agent. **The wiring is part of what
makes residence real.**

## Adopting what you already do

You may already run an AI-assisted workflow that was never called "SGLC" —
instruction files, a few skills, a pre-commit gate. You do not have to tear
it down to start. An in-flight AI SDLC _is_ a candidate SGLC instance.
Adopting the SGLC can mean naming what you already have in frame terms, then
[running a compliance review](./howto-run-a-compliance-review.md) to see which
invariants it already honours and where the gaps are — and retrofitting
against those gaps in the order the review sequences them.

## The instance is never done

An instance evolves on two clocks: the tooling clock, where new snapshots
supersede old bindings, and the team clock, where
[Local fit (I-8)](../docs/invariants.md#i-8--no-process-framework-survives-contact-with-a-real-team)
keeps reshaping it. Neither stops. The invariants are what stay still while
everything beneath them moves — which is exactly why you build to them and not
to a tool. When you want to know how well your instance holds, [run the suite
against it](./howto-run-a-compliance-review.md).
