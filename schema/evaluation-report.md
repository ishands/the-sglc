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

Four commitments shape the format.

**A reviewer, not a linter.** An evaluator returns a graded, reasoned
judgement — never a bare pass/fail, and never a code fix. Some invariants
are near-mechanically checkable; others —
[Ask precision (I-3)](../docs/invariants.md#i-3--a-vague-ask-produces-vague-output),
[Output verification (I-4)](../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work),
[Local fit (I-8)](../docs/invariants.md#i-8--no-process-framework-survives-contact-with-a-real-team)
— are irreducibly matters of degree. The report grades and explains; it does
not stamp. This is
[Output verification (I-4)](../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work)
applied to the suite itself: verification is judgement work.

**Evidence-bound.** Every finding cites something real in the instance — a
file, a mechanism, a location. A judgement with nothing to point at is an
opinion, not an evaluation. This forces the evaluator to read the
organisation's own material rather than an abstract ideal.

**The report is itself an artefact.** Its proper home is the repository,
committed alongside the instance it assesses. A conformance judgement that
lives only in a chat session violates the very laws it checks —
[Rule residence (I-5)](../docs/invariants.md#i-5--the-rules-you-give-ai-belong-in-the-repo-not-in-someones-chat)
and [Rationale capture (I-6)](../docs/invariants.md#i-6--the-reason-behind-a-choice-fades-fastest--capture-it-at-the-moment-or-lose-it).
By convention an evaluator writes its report to
`docs/reviews/sglc-eval-<i-n>-<YYYY-MM-DD>.md` (the orchestrator's composite
to `docs/reviews/sglc-compliance-<YYYY-MM-DD>.md`), so reports are
discoverable and the orchestrator can find them. The evaluator _writes_ the
report; **committing it is the instance owner's step**, not the evaluator's —
consistent with the reviewer stance and the human-as-final-gate caveat
below.

**The evaluation is itself generated output.** An evaluator is an AI
reviewer, so its own findings are a probabilistic outcome — the very thing
[Output verification (I-4)](../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work)
warns about, now turned on the suite. A report is a reasoned recommendation
to be weighed, not a verdict to be applied unread; the human stays the final
gate. Every report carries this caveat in its header so no reader mistakes a
grade for a guarantee. This is output verification once more, recursive: even
the verification needs verifying.

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

## Citing invariants in prose

Refer to an invariant by its **handle and number** — _Ask precision (I-3)_ —
not by the bare number. The handle carries the meaning, so a reader never has
to recall what _I-3_ stands for; the number stays for cross-referencing the
scorecard. The handles are fixed in
[docs/invariants.md](../docs/invariants.md): I-1 Intent origin · I-2 Judgement
boundary · I-3 Ask precision · I-4 Output verification · I-5 Rule residence ·
I-6 Rationale capture · I-7 Layering · I-8 Local fit. Reserve the full headline
for the scorecard, where it is the anchor; everywhere else the handle reads
better than the law restated and clearer than the number alone.

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
  Cite the snapshot by name, date, and section (e.g. _SGLC
  tooling-snapshot-2026-06, Enforcement binding_) rather than a local file
  path — the instance under review is usually a different repository, so a
  relative link will not resolve. This is the only part that names a tool,
  and it is deliberately the most disposable part of the report.
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

> _This evaluation is itself AI-generated and probabilistic. Treat it as a
> reasoned recommendation, not a verdict — apply your own judgement and
> verify the findings before acting on them._

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

> _This assessment is itself AI-generated and probabilistic. Treat it as a
> reasoned recommendation, not a verdict — apply your own judgement and
> verify the findings before acting on them._

> **Coverage** _(include this block only if any invariant was not assessed)_ —
> this is a **partial** assessment: N of 8 invariants were graded; the rest
> are marked _not assessed_ in the scorecard below. Silence on an invariant
> is not a pass — it means no evaluator ran for it.

## Scorecard
| Invariant | Handle | Grade |
|-----------|--------|-------|
| I-1 — <headline> | Intent origin | … |
| …         | …      | …     |

## Findings summary
| # | Invariant | Finding | Priority |
|---|-----------|---------|----------|
| 1 | I-4 …     | <short label> | High |
| … | …         | …       | …    |

## Weakest strands
<the lowest-graded invariants, surfaced first, with why they matter most>

## Couplings in play
<where one weak invariant caps another — e.g. Ask precision (I-3)
ceilings Output verification (I-4)>

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

An invariant with no evaluator to run — because the suite is incomplete, an
evaluator errored, or only a subset was requested — is **not assessed**, not
omitted. It keeps its scorecard row (marked _not assessed_) and the composite
leads with the **Coverage** caveat above. A partial assessment must never read
as a clean bill of health on the strands it never examined; the caveat and the
explicit rows are what keep silence from being mistaken for a pass.
