---
name: review-local-fit
description: Assess whether an SGLC instance is fitted to the real team
  rather than adopted off-the-shelf. Use when checking whether an instance
  honours I-8 — that the process framework took the shape of its container
  (this team's stack, history, constraints) and survives contact with
  practice, rather than being an imported catalogue or dead ceremony.
---

# Evaluate I-8 — No process framework survives contact with a real team

This skill assesses one invariant against an organisation's own SGLC
instance. It is a **reviewer, not a linter**: it returns a graded, reasoned
judgement with cited evidence and a remediation shaped against the
[mechanism frame](../../docs/mechanisms.md) — never a code fix. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
report format this skill fills; read
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## The invariant

> **I-8 — No process framework survives contact with a real team.**
>
> Every team and every codebase differs in people, history, tools, and
> constraints. A fixed lifecycle is dead on arrival; only principles plus a
> mechanism for local fitting endure. The process framework must be like
> water — taking the shape of its container.

Quoted from
[docs/invariants.md](../../docs/invariants.md#i-8--no-process-framework-survives-contact-with-a-real-team).
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

With the inventory in hand, assess I-8. This is partly a _reality check_ on
the rest: the question is whether the instance is a framework fitted to this
team, or an imported catalogue that has not survived contact with how the team
actually works.

- **Fitted, or adopted as-is.** Does the instance show evidence of local
  adaptation — mechanisms chosen for _this_ team's stack, domain, history, and
  constraints — or does it read like a generic "AI SDLC" bolted on, naming a
  stack or flow that is not this team's?
- **Explicit fit points.** Are there places designed to be customized —
  extension points, replaceable defaults — and evidence they were actually
  used? Principles plus a fitting mechanism is what the invariant says endures.
- **Did it survive contact?** Compare the documented process against actual
  practice — the commit history, the artefacts that really exist, the workflow
  as run. Mechanisms that are present on paper but bypassed, ignored, or
  worked around are the literal failure this invariant names: the team routed
  around the framework.
- **Fit to the team's real shape.** Process ceremony heavier than the team
  sustains is non-fit just as much as a rigid lifecycle is — water takes the
  shape of its container, it does not impose one.

## Compliant patterns

Signals the invariant is honoured:

- The instance is visibly fitted: mechanisms match this team's stack, domain,
  and constraints; extension points exist and have been used.
- Evidence of adopt-what-fits, replace-what-doesn't — deliberate selection,
  not wholesale import of a prescribed catalogue.
- The documented process matches actual practice: the artefacts the process
  calls for are the artefacts the repo actually contains.

## Anti-patterns

Signals of violation; what this evaluator flags:

- **Imported catalogue.** A generic framework adopted as-is, unfitted to the
  team; mechanisms reference a stack, role set, or flow that is not this
  team's. Dead on arrival.
- **Dead ceremony.** Mechanisms exist on paper but are bypassed in practice;
  the documented process and the commit history disagree. The framework did
  not survive contact and the team is routing around it. This is the **At
  risk** signature when partial, and the failure outright when pervasive.
- **Rigid lifecycle.** A fixed phase model with no extension points; teams
  cannot fit it, so they either suffer it or ignore it.
- **Process–practice gap.** The instance describes a team that does not exist —
  the written SGLC says one thing, the way work actually happens says another.

## Coupling notes

This result depends on and affects sibling invariants — surface these so the
orchestrator can reason across strands:

- **Local fit (I-8) and [Layering (I-7)](../review-layering/) govern shape
  together.** Local fit is most often _delivered_ through layering: the local
  layer is how a team fits a shared baseline to its container. A baseline with
  no specialization layer fails both — nothing composes and nothing fits.
  Assess the pair and state how they relate here.
- **Local fit is a reality check on the whole assessment.** If the mechanisms
  other evaluators credit are in fact dead ceremony — present but bypassed —
  their nominal presence is illusory, and local fit is where that surfaces. A
  high grade elsewhere on a mechanism that did not survive contact should be
  reconciled against this strand; flag the tension for the orchestrator rather
  than silently overriding the other evaluator.
- **Rule residence (I-5)** underwrites durable fitting: local adaptations that
  live only in habit, not in committed mechanisms, will not endure — a
  residence gap showing up as fragile local fit.

## Verdict rubric

Grade on the four-point scale (see
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-grade-scale)).
For this invariant:

- **Honoured** — the instance is fitted to this team; extension points are
  used; the documented process matches practice.
- **Partial** — some fitting is evident, but parts are unadapted import or are
  partly bypassed in practice.
- **At risk** — the process looks complete on paper but practice is diverging
  (mechanisms bypassed); it has not survived contact and is being routed
  around.
- **Absent** — an imported or rigid framework unfitted to the team, or so out
  of step with practice that it is effectively ignored.

## Output contract

Emit one per-invariant report in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-per-invariant-report):
an `# Evaluation — I-8 …` header block (instance, date, grade, summary), a
**Working** section crediting what is upheld, zero or more **Findings** in
the six-part finding format, and a **Coupling** section naming the siblings
above — in particular state how I-7 and I-8 relate here, and reconcile any
mechanism another evaluator credited that did not survive contact. Every
finding cites real evidence from the instance, and its remediation is stated
**durable first** (which [axis](../../docs/mechanisms.md) to act on —
typically add explicit fit points and a local-specialization seam, and keep
the fitted choices repo-resident) and only **then** concrete (today's
binding — point into the current [tooling snapshot](../../guide/)). The
report is itself committed to the repository alongside the instance it
assesses.
