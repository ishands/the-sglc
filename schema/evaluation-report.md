# The SGLC Evaluation Report Schema

**v0.2.0 — draft**

The conformance suite answers one question — _is this an SGLC instance, and
does it honour the invariants?_ — by running [evaluators](../skills/)
against an organisation's own toolchain. This document defines the single
format those evaluators report in, so that the eight per-invariant
evaluators and the orchestrator that aggregates them speak with one voice
and cannot drift apart.

It is defined once here and referenced everywhere. An evaluator does not
invent its own output shape; it fills this one.

---

## Principles

Three commitments shape the format.

**A reviewer, not a linter.** An evaluator returns a graded, reasoned
judgement — never a bare pass/fail, and never a code fix. Some invariants
are near-mechanically checkable; others
([I-3](../docs/invariants.md#i-3--a-vague-ask-produces-vague-output),
[I-4](../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work),
[I-8](../docs/invariants.md#i-8--no-process-framework-survives-contact-with-a-real-team))
are irreducibly matters of degree. The report grades and explains; it does
not stamp. This is [I-4](../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work)
applied to the suite itself: verification is judgement work.

**Evidence-bound.** Every finding cites something real in the instance — a
file, a mechanism, a location. A judgement with nothing to point at is an
opinion, not an evaluation. This forces the evaluator to read the
organisation's own material rather than an abstract ideal.

**The report is itself an artefact.** Its proper home is the repository,
committed alongside the instance it assesses. A conformance judgement that
lives only in a chat session violates the very laws it checks
([I-5](../docs/invariants.md#i-5--the-rules-you-give-ai-belong-in-the-repo-not-in-someones-chat),
[I-6](../docs/invariants.md#i-6--the-reason-behind-a-choice-fades-fastest--capture-it-at-the-moment-or-lose-it)).

---

## The grade scale

Every evaluation resolves to one of four grades. The scale is deliberately
coarse — it expresses degree of honour, not a score.

- **Honoured** — the invariant is upheld. Mechanisms address it, at
  appropriate strength and residence.
- **Partial** — upheld in part. Gaps weaken it but do not negate it.
- **At risk** — it appears upheld but rests on something that will not hold:
  model attention where enforcement is needed, or personal residence for a
  team standard.
- **Absent** — no mechanism addresses the invariant.

---

## The finding

A finding is the unit of an evaluation: one observed gap or risk. An
evaluator emits zero or more. Each finding has six parts.

- **Finding** — what was observed: the anti-pattern matched, or the gap
  identified.
- **Evidence** — the citation: the file, mechanism, or location in the
  instance that grounds the finding.
- **Impact** — the cost the invariant warns of, made concrete for this case.
- **Remediation — durable** — the fix stated in
  [mechanism-frame](../docs/mechanisms.md) terms: which axis to act on. Add
  or change a **role**, raise a **strength**, or correct a **residence**.
- **Remediation — concrete** — a pointer into the current
  [tooling snapshot](../guide/) for today's binding of that durable move.
  This is the only part that names a tool, and it is deliberately the
  most disposable part of the report.
- **Priority** — severity of the gap weighted by the stakes of what it
  governs. High / Medium / Low.

The durable-before-concrete ordering is the point: the report diagnoses
against the invariants, prescribes against the axes, and only then reaches
for a tool — so the advice survives the tool it currently names.

### Finding template

```markdown
- **Finding:** <observed gap or anti-pattern>
  - **Evidence:** <file / mechanism / location in the instance>
  - **Impact:** <the cost this invokes>
  - **Remediation (durable):** <axis to act on — role / strength / residence>
  - **Remediation (concrete):** <today's binding — see guide/ snapshot>
  - **Priority:** <High | Medium | Low>
```

---

## The per-invariant report

One evaluator run produces one report for one invariant.

```markdown
# Evaluation — <I-N: invariant headline>

- **Instance:** <what was assessed>
- **Date:** <YYYY-MM-DD>
- **Grade:** <Honoured | Partial | At risk | Absent>
- **Summary:** <one or two sentences on why this grade>

## Working
<what the evaluator found upheld — credit where due>

## Findings
<zero or more findings, in the finding format above>

## Coupling
<sibling invariants this result depends on or affects>
```

The **Coupling** section is what lets the orchestrator reason across
strands rather than scoring each in isolation.

---

## The composite assessment

The orchestrator
([`review-sglc-compliance`](../skills/)) runs all eight evaluators and
aggregates them. It does **not** collapse them into a single number or an
overall pass/fail — that would discard exactly the information a team needs.

```markdown
# SGLC Compliance Assessment

- **Instance:** <what was assessed>
- **Date:** <YYYY-MM-DD>

## Scorecard
| Invariant | Grade |
|-----------|-------|
| I-1 …     | …     |
| …         | …     |

## Findings summary
| # | Invariant | Finding | Priority |
|---|-----------|---------|----------|
| 1 | I-4 …     | <short label> | High |
| … | …         | …       | …    |

## Weakest strands
<the lowest-graded invariants, surfaced first, with why they matter most>

## Couplings in play
<where one weak invariant caps another — e.g. a vague-ask gap (I-3)
ceilings achievable verification (I-4)>

## Remediation roadmap
<a sequenced plan, not a flat list. Order by coupling: fix the upstream
invariant before the one it constrains. Each step carries its durable and
concrete remediation from the underlying findings.>
```

The **findings summary** is a triage tier: one row per finding, only the
short cells, so a team can scan the whole picture at a glance. The full
findings — in the six-part finding format — live in the remediation
roadmap, where they are sequenced. The summary scans; the roadmap acts.

The roadmap is the deliverable. A scorecard tells a team where it stands; a
coupling-aware sequence tells it what to do first — and the durable
remediation on each step keeps that advice good after today's tools have
been superseded.
