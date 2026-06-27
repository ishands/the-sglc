# How to Run a Compliance Review

A **compliance review** runs the SGLC [conformance suite](../skills/) against
an instance to answer one question — _is this an SGLC instance, and how fully
does it honour the [invariants](../docs/invariants.md)?_ It produces a graded,
evidence-bound, coupling-aware assessment with a sequenced remediation
roadmap. It is **not** a score and **not** a pass/fail stamp.

This guide covers what you can review, the two ways to run it, how to read
what comes back, and the one disclaimer you must not skip.

## What you can review

- A formal SGLC instance, built per
  [howto-create-an-sglc-instance.md](./howto-create-an-sglc-instance.md).
- An in-flight AI SDLC not yet formally adopted as SGLC — the suite assesses
  what is actually there against the invariants, regardless of what it is
  called.

In both cases the review reads the instance's _own_ mechanisms — its files,
skills, rules, and gates — and grades them against the laws, citing real
evidence. It does not measure against an abstract ideal or a reference
implementation.

## Two ways to run it

**The whole suite — orchestrated.** Run the orchestrator,
[`review-sglc-compliance`](../skills/review-sglc-compliance/). It walks the
instance once to build a mechanism inventory, runs all eight evaluators
against that shared inventory, and aggregates them into one **composite
assessment**. The composite is the deliverable — it embeds every finding in
full. Use this for a complete picture.

**One strand — standalone.** Run a single evaluator on its own to check one
invariant. Each builds its own inventory from the same
[discovery walk](./tooling-snapshot-2026-06.md#locating-mechanisms-in-an-instance)
and emits a per-invariant report. Use this for a focused check, or to re-test
one strand after remediation.

| Invariant | Handle | Evaluator |
| --------- | ------ | --------- |
| I-1 | Intent origin | [`review-intent-origin`](../skills/review-intent-origin/) |
| I-2 | Judgement boundary | [`review-judgement-boundary`](../skills/review-judgement-boundary/) |
| I-3 | Ask precision | [`review-ask-precision`](../skills/review-ask-precision/) |
| I-4 | Output verification | [`review-output-verification`](../skills/review-output-verification/) |
| I-5 | Rule residence | [`review-rule-residence`](../skills/review-rule-residence/) |
| I-6 | Rationale capture | [`review-rationale-capture`](../skills/review-rationale-capture/) |
| I-7 | Layering | [`review-layering`](../skills/review-layering/) |
| I-8 | Local fit | [`review-local-fit`](../skills/review-local-fit/) |
| — | _all eight, aggregated_ | [`review-sglc-compliance`](../skills/review-sglc-compliance/) |

## Running it

Point the suite at the instance repository and invoke the orchestrator. In an
agent session that is a single instruction — for example:

> Invoke the `review-sglc-compliance` skill at
> `…/the-sglc/skills/review-sglc-compliance/SKILL.md` against the SGLC instance
> rooted at `/path/to/your/org/repo`, and write the compliance report to its
> `docs/reviews/` directory.

A standalone evaluator is invoked the same way — name the single `review-*`
skill instead of the orchestrator. The orchestrator then does three things, in
order:

1. **Builds the inventory once** — the single discovery walk, starting at the
   front door (`README.md` and `AGENTS.md`) and inventorying by role.
   [Locating mechanisms in an instance](./tooling-snapshot-2026-06.md#locating-mechanisms-in-an-instance)
   is the procedure it follows.
2. **Runs the eight evaluators**, handing each the shared inventory so none
   re-walks the repo.
3. **Aggregates — does not average** — into the composite, written to
   `docs/reviews/sglc-compliance-<YYYY-MM-DD>.md`.

The suite _writes_ the report; **committing it is your step**, not the
suite's — consistent with the reviewer stance and with keeping the human as
the final gate. A report committed to the repo is the instance honouring
[Rule residence (I-5)](../docs/invariants.md#i-5--the-rules-you-give-ai-belong-in-the-repo-not-in-someones-chat)
and [Rationale capture (I-6)](../docs/invariants.md#i-6--the-reason-behind-a-choice-fades-fastest--capture-it-at-the-moment-or-lose-it):
a conformance judgement that lived only in a chat session would violate the
laws it checks.

If only part of the suite runs — an evaluator errors, or you ran a subset —
the unassessed invariants are marked **not assessed**, not omitted, and the
composite leads with a **Coverage** caveat. **Silence on an invariant is not
a pass.**

## Reading the report

The composite format is defined by
[schema/evaluation-report.md](../schema/evaluation-report.md). Read it in this
order; each part does a different job.

- **Scorecard** — eight grades on a deliberately coarse four-point scale:
  [Honoured / Partial / At risk / Absent](../schema/evaluation-report.md#the-grade-scale).
  There is no ninth, aggregate grade. An instance with seven Honoured and one
  Absent is not "87% compliant" — it has a specific hole, and the assessment's
  job is to name it.
- **Findings summary** — a triage table, one row per finding, scannable at a
  glance.
- **Weakest strands** — the lowest grades, surfaced first, because they cap
  the rest.
- **Couplings in play** — where one weak invariant ceilings another. The
  classic:
  [Ask precision (I-3)](../docs/invariants.md#i-3--a-vague-ask-produces-vague-output)
  caps
  [Output verification (I-4)](../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work)
  — you cannot verify output against an intent that was never made precise.
- **Remediation roadmap** — the deliverable. A _sequenced_ plan, not a flat
  list, ordered by coupling so you fix the upstream invariant before the one
  it constrains. Each step carries its remediation **durable first, concrete
  second**.

The **durable-before-concrete** ordering is the thing to internalise. Every
fix names the [axis](../docs/mechanisms.md) to move — add or change a _role_,
raise a _strength_, correct a _residence_ — _before_ it names today's tool to
move it with. Act on the durable move; the tool pointer is the most
disposable line in the report, and deliberately so. **Diagnose against the
invariants, prescribe against the axes, reach for a tool last.**

Read **At risk** carefully. It does not mean broken now — it means something
_looks_ upheld but rests on what will not hold: model attention where
enforcement is needed, or personal residence for a team standard. At risk is
the grade that catches the failure before it happens.

## The disclaimer you don't skip

**The review is itself generated output.** An evaluator is an AI reviewer, so
its findings are a probabilistic outcome — the very thing
[Output verification (I-4)](../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work)
warns about, now turned on the suite itself. Every report carries this caveat
in its header, and it is not boilerplate:

> Treat the assessment as a reasoned recommendation, not a verdict — apply
> your own judgement and verify the findings before acting on them.

The human stays the final gate. A grade is an argument to be weighed, not a
guarantee to be banked. This is verification, recursive: even the verification
needs verifying — the SGLC holding itself to its own law.

## After the review

Work the roadmap in the order it gives you — root before symptom, upstream
invariant before the one it caps. The durable remediation on each step names
which [mechanism axis](../docs/mechanisms.md) to move;
[howto-create-an-sglc-instance.md](./howto-create-an-sglc-instance.md) covers
making those moves. Then re-run — the whole suite, or just the strands you
touched — and confirm the grades moved.

An instance is never finished
([Local fit (I-8)](../docs/invariants.md#i-8--no-process-framework-survives-contact-with-a-real-team)),
so neither is its review. It is a recurring check, not a one-time
certification.

---

**Navigate:** [Home](../README.md) · [Manifesto](../docs/manifesto.md) · [Invariants](../docs/invariants.md) · [Essay](../docs/essay.md) · [Mechanism frame](../docs/mechanisms.md) · [Create an instance](howto-create-an-sglc-instance.md) · [Run a review](howto-run-a-compliance-review.md)
