---
name: review-ask-precision
description: Assess whether an SGLC instance forces well-formed input before
  generation. Use when checking whether an instance honours I-3 — that asks
  are made precise (structured stories, specs, acceptance criteria) before
  generation runs, since output can be no sharper than the question.
---

# Evaluate I-3 — A vague ask produces vague output

This skill assesses one invariant against an organisation's own SGLC
instance. It is a **reviewer, not a linter**: it returns a graded, reasoned
judgement with cited evidence and a remediation shaped against the
[mechanism frame](../../docs/mechanisms.md) — never a code fix. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
report format this skill fills; read
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## The invariant

> **I-3 — A vague ask produces vague output.**
>
> Generation can't be sharper than the question that drives it. Garbage-in /
> garbage-out is the same law it always was; AI just executes faster on
> whatever clarity you give it. The discipline of asking precisely — knowing
> _what_ and _how_ to ask — is now a critical engineering skill, not a soft
> one.

Quoted from
[docs/invariants.md](../../docs/invariants.md#i-3--a-vague-ask-produces-vague-output).
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

With the inventory in hand, assess I-3. Gather evidence from the instance's
_own_ mechanisms — not an abstract ideal. The question is whether the inputs
to generation are made precise before generation runs, or whether output
quality is left hostage to however a prompt happened to be phrased.

- **The shape of the input.** What feeds generation — structured stories and
  specifications with acceptance criteria, or freeform prompts? Look for
  templates, intent checklists, and definition-of-ready artefacts that force
  well-formed input.
- **Whether precision is required or merely available.** A story template
  that exists in the repo but that generation does not actually depend on is
  optional precision — and optional precision is skipped under pressure. Note
  the [**strength**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling):
  is there a
  [**Recognition**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
  trigger that catches an under-formed ask, or an
  [**Enforcement**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
  gate (a definition-of-ready) that blocks generation on a vague one?
- **Acceptance criteria — does the ask say what "correct" means?** An ask
  that names a feature but not the criteria it must satisfy is vague in the
  way that matters most: there is nothing precise to generate toward, and
  nothing for [output verification (I-4)](../review-output-verification/) to
  check against later.
- **Whether precision is treated as engineering work.** Is the discipline of
  asking well owned and reviewed — templates maintained, criteria critiqued —
  or treated as a soft, optional nicety?

## Compliant patterns

Signals the invariant is honoured:

- Structured input formats — templated stories, specifications carrying
  acceptance criteria — are the norm before generation, not the exception.
- A definition-of-ready or intent checklist gates generation: an
  under-specified ask does not proceed.
- The precision discipline is owned and reviewed like other engineering work,
  and the templates that carry it are repo-resident.

## Anti-patterns

Signals of violation; what this evaluator flags:

- **Freeform asks.** Generation runs off unstructured prompts with no
  required structure; output quality rides on whoever phrased the request.
- **Templates that are not required.** A story or spec template exists in the
  repo, but nothing makes generation depend on it — precision is optional, so
  under deadline it is the first thing dropped. This is the **At risk**
  signature: the asks look governed until you notice nothing enforces it.
- **Acceptance criteria absent or vague.** The ask states a feature but not
  what "done" or "correct" means, so generation has no sharp target — and the
  downstream check has nothing to verify against.
- **Precision as afterthought.** Specs are written to look tidy rather than to
  constrain generation; the document exists but does not actually sharpen the
  question.

## Coupling notes

This result depends on and affects sibling invariants — surface these so the
orchestrator can reason across strands:

- **Ask precision (I-3) ceilings [Output verification (I-4)](../review-output-verification/).**
  This is the headline coupling, and it runs both ways. You cannot verify
  output against intent that was never made precise — weak ask precision caps
  the achievable output verification, because an intent-vs-output check has
  nothing sound to test against. Conversely, _strong_ ask precision un-caps
  output verification: where acceptance criteria are already precise, an intent
  check becomes cheap to add. State which direction the instance is in.
- **Intent origin (I-1) and the Judgement boundary (I-2)** feed this one. A
  precise ask presupposes that a decision exists
  ([intent origin](../review-intent-origin/)) and is human-owned
  ([judgement boundary](../review-judgement-boundary/)); ask precision
  grades the quality of that decision as stated. Where those are weak,
  precision has nothing to sharpen.
- **Rule residence (I-5)** governs whether the templates and checklists are
  durable: a story format that lives only in someone's personal prompt file is
  a residence gap showing up as inconsistent ask precision.

## Verdict rubric

Grade on the four-point scale (see
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-grade-scale)).
For this invariant:

- **Honoured** — structured asks carrying acceptance criteria are required
  before generation; precision is enforced or strongly recognised, and the
  formats are owned and repo-resident.
- **Partial** — structure exists and is usually used, but not required; some
  asks are precise and others freeform.
- **At risk** — templates exist but nothing requires them; precision rests on
  individual diligence and degrades under pressure.
- **Absent** — generation runs off freeform prompts; no mechanism forces
  well-formed input.

## Output contract

Emit one per-invariant report in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-per-invariant-report):
an `# Evaluation — I-3 …` header block (instance, date, grade, summary), a
**Working** section crediting what is upheld, zero or more **Findings** in
the six-part finding format, and a **Coupling** section naming the siblings
above — in particular state how ask precision here ceilings or un-caps output
verification. Every
finding cites real evidence from the instance, and its remediation is stated
**durable first** (which [axis](../../docs/mechanisms.md) to act on —
typically add a
[**Recognition**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
trigger or
[**Enforcement**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
gate that requires a well-formed ask) and only **then** concrete (today's
binding — point into the current [tooling snapshot](../../guide/)). The
report is itself committed to the repository alongside the instance it
assesses.
