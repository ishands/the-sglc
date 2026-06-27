---
name: review-layering
description: Assess whether an SGLC instance composes universal and
  team-specific guidance additively. Use when checking whether an instance
  honours I-7 — that a shared baseline and local specializations both apply,
  layered, rather than one replacing the other or each team forking its own.
---

# Evaluate I-7 — Universal principles and team-specific rules both apply, layered

This skill assesses one invariant against an organisation's own SGLC
instance. It is a **reviewer, not a linter**: it returns a graded, reasoned
judgement with cited evidence and a remediation shaped against the
[mechanism frame](../../docs/mechanisms.md) — never a code fix. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
report format this skill fills; read
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## The invariant

> **I-7 — Universal principles and team-specific rules both apply, layered.**
>
> Generation knowledge composes additively: a shared baseline plus a
> contextual specialization, not one replacing the other. A general
> code-review skill and a team's stack-specific code-review skill both
> activate together. The same shape recurs at every scale — within a single
> set of instructions, across team boundaries, across phases. It is fractal.

Quoted from
[docs/invariants.md](../../docs/invariants.md#i-7--universal-principles-and-team-specific-rules-both-apply-layered).
Do not paraphrase it; assess against it.

## What to look at

**Start from the mechanism inventory** — the map of what plays each role
(Awareness, Recognition, Procedure, Enforcement) in the instance, and where
each lives. How you obtain it depends on how you were invoked:

- **Invoked by the orchestrator** ([`review-sglc-compliance`](../review-sglc-compliance/)):
  the inventory is **supplied to you as input**. Use it as given — do _not_
  re-read the navigation map or re-walk the repo. The orchestrator walks once
  for all eight evaluators.
- **Running standalone** (no inventory supplied): build it yourself. Start at
  the instance's `README.md` and `AGENTS.md` (or equivalent), which a
  well-formed instance wires its mechanisms from, then follow
  [Locating mechanisms in an instance](../../guide/tooling-snapshot-2026-06.md#locating-mechanisms-in-an-instance)
  to find what plays each role and where today's bindings sit.

With the inventory in hand, assess I-7. Gather evidence from the instance's
_own_ mechanisms — not an abstract ideal. The question is whether generation
guidance _composes_ — a shared baseline plus local specializations, both
active — or whether it is monolithic, duplicated, or override-only.

- **Whether a shared baseline exists.** Is there universal guidance — general
  skills, principles, conventions — that every team or phase inherits, or does
  each context start from scratch with nothing in common?
- **Whether local specialization layers on rather than replaces.** When a team
  needs a stack- or domain-specific rule, does it add a layer that activates
  _on top of_ the baseline (both apply), or does it fork and edit a copy, or
  override the baseline wholesale (one replaces the other)?
- **Whether both actually activate together.** Composition on paper is not
  composition in practice: check that a general and a specific mechanism for
  the same job both fire, rather than the specific one shadowing the general.
- **Whether the shape recurs.** The invariant is fractal — look for the same
  baseline-plus-specialization pattern at more than one scale (org → team →
  product, or across phases), not a one-off.
- **Residence of each layer.** Layers compose durably only when each is
  itself repo-resident; a baseline layered with personal-residence additions
  does not compose for the team (couples to
  [rule residence (I-5)](../review-rule-residence/)).

## Compliant patterns

Signals the invariant is honoured:

- A shared baseline exists and is inherited; local specializations add to it
  rather than replacing it, and both activate together.
- The baseline-plus-specialization shape recurs across scales consistently —
  the composition is a deliberate structure, not an accident in one corner.
- Updating the baseline propagates to everyone who layers on it, because they
  extend it rather than holding edited copies.

## Anti-patterns

Signals of violation; what this evaluator flags:

- **Copy-and-diverge.** Teams duplicate the baseline and edit their copies;
  the shared layer rots because improvements never propagate. It looks like
  reuse; it is fragmentation. This is the **At risk** signature: it composes
  today and quietly diverges over time.
- **Override-not-extend.** Local rules replace the baseline wholesale, so the
  universal principles are lost wherever a team specializes.
- **No baseline.** Only per-team or per-phase rules, nothing shared; every
  context reinvents the common core.
- **Flattening.** Everything is jammed into one undifferentiated file with no
  layer separation, so nothing can be cleanly inherited or specialized — there
  is no seam to layer along.

## Coupling notes

This result depends on and affects sibling invariants — surface these so the
orchestrator can reason across strands:

- **Layering (I-7) and [Local fit (I-8)](../review-local-fit/) govern shape
  together.** Layering is _how_ guidance composes (additive layers); local fit
  is _whether_ the framework bends to the real team. They are usually two views
  of the same structure: a baseline with no specialization layer fails both —
  there is nothing to compose and nowhere to fit. Assess them as a pair and say
  how they relate in this instance.
- **Rule residence (I-5)** underwrites layering: composition is durable only if
  every layer is repo-resident. Layering on top of personal-residence guidance
  is a residence gap showing up as brittle layering.
- Layering applies to _all_ generation knowledge — the judgement guidance
  ([intent origin](../review-intent-origin/) /
  [judgement boundary](../review-create-generate-boundary/)), the
  [ask precision](../review-ask-precision/) templates, the
  [output verification](../review-verification-pace/) checks — so a layering
  weakness can blunt several strands at once.

## Verdict rubric

Grade on the four-point scale (see
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-grade-scale)).
For this invariant:

- **Honoured** — a shared baseline plus additive local specializations, both
  active; the layering shape recurs across scales.
- **Partial** — layering works in places (some guidance composes) but other
  guidance is duplicated or monolithic.
- **At risk** — layering is nominal: a baseline exists but teams are quietly
  diverging via edited copies; it composes today but is fragmenting.
- **Absent** — no composition: either one monolith for everyone, or per-team
  silos with no shared core.

## Output contract

Emit one per-invariant report in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-per-invariant-report):
an `# Evaluation — I-7 …` header block (instance, date, grade, summary), a
**Working** section crediting what is upheld, zero or more **Findings** in
the six-part finding format, and a **Coupling** section naming the siblings
above — in particular state how I-7 and I-8 relate here. Every finding cites
real evidence from the instance, and its remediation is stated **durable
first** (which [axis](../../docs/mechanisms.md) to act on — typically
introduce a baseline layer and an additive specialization seam so mechanisms
compose, and keep each layer repo-resident) and only **then** concrete
(today's binding — point into the current [tooling snapshot](../../guide/)).
The report is itself committed to the repository alongside the instance it
assesses.
