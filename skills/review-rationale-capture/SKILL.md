---
name: review-rationale-capture
description: Assess whether an SGLC instance captures the reason behind a
  choice at the moment it is made. Use when checking whether an instance
  honours I-6 — that the why behind generated work is recorded at the time,
  in the repo, not left to be reconstructed later from the code.
---

# Evaluate I-6 — The reason behind a choice fades fastest — capture it at the moment, or lose it

This skill assesses one invariant against an organisation's own SGLC
instance. It is a **reviewer, not a linter**: it returns a graded, reasoned
judgement with cited evidence and a remediation shaped against the
[mechanism frame](../../docs/mechanisms.md) — never a code fix. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
report format this skill fills; read
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## The invariant

> **I-6 — The reason behind a choice fades fastest — capture it at the moment, or lose it.**
>
> _Why_ a thing was generated a given way is the first piece of context to
> decay and the hardest to recover from the code alone. It has to be captured
> at the time of generation, not reconstructed later from a clean repository
> six months on. AI accelerates this decay by making the _what_ trivially
> fast while leaving the _why_ implicit.

Quoted from
[docs/invariants.md](../../docs/invariants.md#i-6--the-reason-behind-a-choice-fades-fastest--capture-it-at-the-moment-or-lose-it).
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

With the inventory in hand, assess I-6. Gather evidence from the instance's
_own_ mechanisms — not an abstract ideal. The question is whether the _why_
behind generated work is captured at the moment of the choice and committed,
or left implicit to be reconstructed later (which the invariant says fails).

- **Whether decisions carry their rationale.** Look for decision records,
  ADRs, principle documents, or rationale fields that record _why_, not just
  _what_. A repo full of precise specs and clean code but silent on reasoning
  is the gap this invariant names.
- **Whether capture happens at the moment.** Is there a step in the workflow —
  a [**Procedure**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
  such as a create-decision-record step — that records the why _as_ the choice
  is made, or is documentation a later-cleanup intention? At generation speed,
  "later" rarely catches up.
- **Where the why lives.** Rationale that exists only in a chat session or a
  PR discussion thread is durable only as long as the thread and the people
  persist. Note the
  [**residence**](../../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds)
  of the captured reasoning. (A why captured but not repo-resident couples to
  [rule residence (I-5)](../review-rule-residence/).)
- **The acceleration gap.** High generation throughput with no capture step
  means the why is being lost at AI speed. Is there a counter-mechanism, or is
  the volume outrunning the record?

## Compliant patterns

Signals the invariant is honoured:

- Decision records, ADRs, or principle docs capture _why_ at the moment of
  the choice and are committed to the repo.
- The workflow includes a rationale-capture step tied to generation, not a
  retrospective documentation pass.
- The principles that shaped how things are generated are written down and
  owned, so a later reader recovers intent without archaeology.

## Anti-patterns

Signals of violation; what this evaluator flags:

- **Why lives only in chat or PR threads.** Rationale was articulated at
  decision time but in a non-durable place; it is recoverable only while the
  thread and the people who wrote it remain.
- **No capture step.** Decisions are made and generated, but the why is never
  recorded; reconstruction-from-code-later is the implicit plan — which the
  invariant says does not work.
- **What captured, why omitted.** Rich specs and code with the reasoning
  behind key choices left implicit. It looks documented; it is not. The most
  seductive version of this failure.
- **Capture deferred.** "We will write up the decisions later." At AI
  generation speed, later never catches up, and the backlog of un-captured why
  grows faster than anyone clears it. This is the **At risk** signature.

## Coupling notes

This result depends on and affects sibling invariants — surface these so the
orchestrator can reason across strands:

- **Rule residence (I-5)** is the sibling durability invariant, and the two
  underwrite durability everywhere together: rule residence is _where the
  rules live_, rationale capture is _whether the why was captured_. A rationale
  that was captured but not committed is both a rationale-capture and a
  rule-residence finding — name where the root sits.
- **Intent origin (I-1) and the Judgement boundary (I-2)** produce the
  decision whose reasoning rationale capture preserves. A decision recorded
  ([intent origin](../review-intent-origin/)) without its why is an origin
  missing its rationale — adjacent findings that often travel together.
- **Ask precision (I-3)** overlaps at the edge: precise acceptance criteria
  carry some intent, but ask precision grades the precision of the _what_ while
  rationale capture grades the capture of the _why_ behind choices. Keep them
  distinct.

## Verdict rubric

Grade on the four-point scale (see
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-grade-scale)).
For this invariant:

- **Honoured** — rationale is captured at the moment of choice, committed, and
  owned; the workflow has a capture step that keeps pace with generation.
- **Partial** — significant decisions carry rationale (big choices get
  records) but routine generation choices lose their why.
- **At risk** — rationale exists only in transient places (chat, PR threads),
  or capture is perpetually deferred; the why survives only as long as the
  people and threads do.
- **Absent** — no why is captured anywhere; reconstruction from the code is
  the only recourse, which the invariant says fails.

## Output contract

Emit one per-invariant report in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-per-invariant-report):
an `# Evaluation — I-6 …` header block (instance, date, grade, summary), a
**Working** section crediting what is upheld, zero or more **Findings** in
the six-part finding format, and a **Coupling** section naming the siblings
above. Every finding cites real evidence from the instance, and its
remediation is stated **durable first** (which
[axis](../../docs/mechanisms.md) to act on — typically add a rationale-capture
[**Procedure**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
tied to generation, or correct the
[**residence**](../../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds)
of captured reasoning into the repo) and only **then** concrete (today's
binding — point into the current [tooling snapshot](../../guide/)). The
report is itself committed to the repository alongside the instance it
assesses.
