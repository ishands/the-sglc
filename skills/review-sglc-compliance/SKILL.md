---
name: review-sglc-compliance
description: Assess whether a repository is an SGLC instance and how fully it
  honours the invariants. Use when checking the overall SGLC compliance of an
  organisation's toolchain — or of an in-flight AI SDLC not yet formally
  adopted as SGLC. Runs the eight per-invariant evaluators and aggregates
  them into a graded, coupling-aware remediation roadmap.
---

# Assess SGLC compliance — the orchestrator

This skill answers one question — _is this an SGLC instance, and how fully
does it honour the invariants?_ — by running the eight per-invariant
[evaluators](../) against an organisation's own repository and aggregating
their reports into one assessment.

It is a **reviewer, not a linter**, and it does **not** collapse the eight
strands into a single number or an overall pass/fail — that would discard
exactly the information a team needs. It produces a graded scorecard, the
weakest strands surfaced first, and a sequenced remediation roadmap. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
composite format this skill fills, and
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## What it does

Three steps, in order.

### 1. Build the mechanism inventory once

Walk the instance and map what plays each role — Awareness, Recognition,
Procedure, Enforcement — and where each lives. Start at the front door
(`README.md` and `AGENTS.md`, or the equivalent), which a well-formed
instance wires its mechanisms from, then inventory by role. Follow
[Locating mechanisms in an instance](../../guide/tooling-snapshot-2026-06.md#locating-mechanisms-in-an-instance)
for where today's bindings sit. This is the **single discovery walk** for
the whole assessment — do it here, once.

### 2. Run the eight evaluators, passing the inventory

Apply each per-invariant evaluator, **supplying the inventory built in
step 1 as its input** so it does not re-walk the repo. Each evaluator that
runs writes its own per-invariant report to
`docs/reviews/sglc-eval-<i-n>-<YYYY-MM-DD>.md` (the schema's filename
convention) and returns it for aggregation — so the graded strands leave
durable, individually citable artefacts behind, not just rows in the
composite.

| Invariant | Evaluator |
| --------- | --------- |
| I-1 — every artifact starts with someone deciding what it should be | [`review-intent-origin`](../review-intent-origin/) |
| I-2 — deciding what to build is human work; producing it isn't | [`review-create-generate-boundary`](../review-create-generate-boundary/) |
| I-3 — a vague ask produces vague output | [`review-ask-precision`](../review-ask-precision/) |
| I-4 — when AI writes the code, checking it becomes the work | [`review-verification-pace`](../review-verification-pace/) |
| I-5 — the rules you give AI belong in the repo | [`review-rule-residence`](../review-rule-residence/) |
| I-6 — the reason behind a choice fades fastest | [`review-rationale-capture`](../review-rationale-capture/) |
| I-7 — universal principles and team-specific rules both apply, layered | [`review-layering`](../review-layering/) |
| I-8 — no process framework survives contact with a real team | [`review-local-fit`](../review-local-fit/) |

If an evaluator is not present in this suite, record its invariant as **not
assessed** rather than skipping it silently — an unassessed strand is itself
information. A not-assessed invariant produces no per-invariant report but
still gets its row in the scorecard, and the composite must lead with the
[**Coverage** caveat](../../schema/evaluation-report.md#the-composite-assessment)
so a partial run is never mistaken for a clean pass.

### 3. Aggregate — do not average

Combine the eight reports into one composite assessment. Carry each
evaluator's grade into the scorecard verbatim; do not blend them. The
deliverable is the roadmap, not the scorecard: a scorecard tells a team
where it stands; a coupling-aware sequence tells it what to do first.

## The inventory hand-off

Step 1 is the orchestrator's half of the contract each evaluator's "What to
look at" describes: invoked here, an evaluator receives the inventory and
skips its own discovery; run standalone, it builds the inventory itself from
the same snapshot section. One source, one walk per assessment — eight walks
only if the evaluators are run individually.

## Coupling-aware sequencing

The reason not to average is that the invariants constrain one another, and a
fix applied in the wrong order is wasted. Sequence the roadmap so an
upstream invariant is fixed before the one it caps. The standing couplings:

- **I-3 ceilings I-4.** You cannot verify output against intent that was
  never made precise. Fix a vague-ask gap before investing in stronger
  checks — otherwise the checks have nothing sound to test against.
- **I-1 / I-2 feed I-3 and I-4.** Where intent origin or the judgement
  boundary is weak, the precision and verification downstream inherit the
  weakness.
- **I-5 and I-6 underwrite durability everywhere.** A mechanism that is not
  repo-resident (I-5) or whose rationale was never captured (I-6) will
  decay whatever invariant it serves. A weak I-5 frequently surfaces _as_
  another invariant's risk — for example a verification gate (I-4) that
  lives only in habit or platform config is an I-5 residence gap wearing an
  I-4 mask. Name the root, not the symptom.
- **I-7 and I-8 govern shape.** Layering (I-7) and local fit (I-8) determine
  whether the other mechanisms compose and survive contact with the team;
  treat them as structural constraints on the roadmap, not standalone
  line-items.

When findings interact, attribute each to its root invariant and order the
roadmap from root to symptom. State the couplings you relied on so the team
can see why the order is what it is.

## Verdict philosophy

There is no single overall grade. The honest composite is eight grades, the
weakest surfaced first because they cap the rest, and a sequence that
respects the couplings above. An instance with seven Honoured strands and one
Absent is not "87% compliant" — it has a specific hole, and the assessment's
job is to name it and say what to do about it.

## Output contract

Emit one composite assessment, written to
`docs/reviews/sglc-compliance-<YYYY-MM-DD>.md`, in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-composite-assessment):
the `# SGLC Compliance Assessment` header block, the standard
probabilistic-self caveat, the **Coverage** caveat whenever any strand is
not assessed, a **Scorecard** (one row per invariant), a
**Findings summary** triage table (one row per finding), **Weakest strands**
(lowest grades first, with why they matter), **Couplings in play** (where one
weak invariant caps another), and the **Remediation roadmap** — the
sequenced, durable-before-concrete plan that is the real deliverable. Like
the per-invariant reports it aggregates, this assessment is itself committed
to the repository alongside the instance it assesses
([I-5](../../docs/invariants.md#i-5--the-rules-you-give-ai-belong-in-the-repo-not-in-someones-chat),
[I-6](../../docs/invariants.md#i-6--the-reason-behind-a-choice-fades-fastest--capture-it-at-the-moment-or-lose-it)).
