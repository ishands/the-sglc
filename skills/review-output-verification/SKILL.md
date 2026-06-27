---
name: review-output-verification
description: Assess whether an SGLC instance keeps verification in step with
  generation. Use when checking whether an instance honours I-4 — that
  checking AI-written output is treated as the real work, gated and paced,
  not assumed.
---

# Evaluate I-4 — When AI writes the code, checking it becomes the work

This skill assesses one invariant against an organisation's own SGLC
instance. It is a **reviewer, not a linter**: it returns a graded, reasoned
judgement with cited evidence and a remediation shaped against the
[mechanism frame](../../docs/mechanisms.md) — never a code fix. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
report format this skill fills; read
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## The invariant

> **I-4 — When AI writes the code, checking it becomes the work.**
>
> The bottleneck moves from production to verification. When generating is
> cheap and fast, the scarce act is confirming the output actually matches
> the intent. Controlling the speed of generation _is_ keeping verification
> in step with it. Engineering value migrates upstream (toward better
> intent) and downstream (toward stronger checks).

Quoted from
[docs/invariants.md](../../docs/invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work).
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

With the inventory in hand, assess I-4. Gather evidence from the instance's
_own_ mechanisms — not an abstract ideal. The question is whether the
verification effort scales with the generation it has to keep up with.

- **The gates between generation and acceptance.** What must pass before
  generated output is merged or shipped? Look for
  [**Enforcement**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
  mechanisms — test gates, review checkpoints, intent-vs-output checks — and
  note their [**strength**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling):
  are they deterministic, or do they rest on someone remembering?
- **Intent-vs-output checking — and against _which_ intent.** Is there a
  step that compares the output against _what the work was asked to do_, or
  only against a lower bar? Three layers are easily confused, and only the
  last is what I-4 means:
  - _well-formed_ — it compiles, lints, passes its own tests;
  - _internally consistent_ — the code matches its design doc, types, and
    signatures (doc-to-code consistency);
  - _correct against intent_ — the output satisfies the acceptance criteria
    or specification it was generated to meet.

  A check that confirms the code matches its design doc still does not
  confirm that the code does what the _story_ asked — doc-to-code
  consistency verifies the documentation matches the code, the reverse of
  verifying the code matches the intent. Credit only the third layer as a
  genuine intent-vs-output check; the first two are necessary but not
  sufficient.
- **Pace control.** Is there anything that throttles how much un-verified
  generation can accumulate — small reviewable changes, a ceiling on batch
  size — or does generated work pile up faster than anyone can check it?
- **Where the human effort sits.** I-4 predicts effort migrating to intent
  (upstream) and checks (downstream). If the instance still spends its
  scarce attention on _producing_ output rather than confirming it, the
  invariant is not being lived even if gates nominally exist.

## Compliant patterns

Signals the invariant is honoured:

- A deterministic gate — a test or check that _blocks_ acceptance — stands
  between generation and merge, not merely an advisory reminder to review.
- At least one check compares output against stated intent (the
  specification, the acceptance criteria, the issue), not only against
  itself.
- Verification strength rises with stakes: higher-risk paths carry harder
  gates, consistent with the escalation discipline on the
  [**Strength** axis](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling).
- Changes arrive in reviewable units; the volume of generation is paced to
  what verification can absorb.

## Anti-patterns

Signals of violation; what this evaluator flags:

- **Generation gated only by advice.** Acceptance depends on a person
  remembering to review — an
  [**advisory**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
  mechanism — where the stakes call for
  [**Enforcement**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling).
  This is the **At risk** signature: it looks fine until a missed review
  ships a defect.
- **Well-formed — or doc-consistent — mistaken for correct.** Checks confirm
  the output compiles, lints, passes its own tests, or matches its design
  doc, but nothing confirms it satisfies the acceptance criteria it was asked
  to meet. Doc-to-code consistency is the most seductive version of this: it
  looks like intent-checking but verifies the documentation against the code,
  not the code against the intent. Fast green builds on the wrong thing.
- **Verification outrun.** Generation produces output faster than it can be
  checked, so review degrades to rubber-stamping under volume — the gate
  exists but is no longer real.
- **Effort still on production.** The instance optimises for generating more
  rather than confirming what was generated; the bottleneck I-4 names has
  not been acknowledged.

## Coupling notes

This result depends on and affects sibling invariants — surface these so the
orchestrator can reason across strands:

- **Ask precision (I-3)** ceilings this one. You cannot verify output against
  intent if the intent was never made precise — an intent-vs-output check has
  nothing to check against. Weak ask precision caps the achievable output
  verification; flag the coupling rather than grading this strand in isolation.
- **Intent origin (I-1) and the Judgement boundary (I-2)** feed the upstream
  half of output verification's "migrate toward better intent." Where those
  are weak, the upstream investment this strand expects is missing.
- **Rule residence (I-5)** governs whether the gates themselves are durable: a
  verification step that lives in one engineer's habit, not in a committed
  mechanism, is a residence gap showing up as an output-verification risk.

## Verdict rubric

Grade on the four-point scale (see
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-grade-scale)).
For this invariant:

- **Honoured** — deterministic gates stand between generation and
  acceptance, at least one check tests output against intent, and gate
  strength tracks stakes.
- **Partial** — checks exist but verify form more than intent, or cover only
  some of the paths that need them.
- **At risk** — acceptance rests on advisory review or human memory where
  enforcement is needed; it holds today and will fail on the first missed
  check.
- **Absent** — no mechanism stands between generated output and acceptance.

## Output contract

Emit one per-invariant report in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-per-invariant-report):
an `# Evaluation — I-4 …` header block (instance, date, grade, summary), a
**Working** section crediting what is upheld, zero or more **Findings** in
the six-part finding format, and a **Coupling** section naming the siblings
above. Every finding cites real evidence from the instance, and its
remediation is stated **durable first** (which
[axis](../../docs/mechanisms.md) to act on — typically raise a
[**strength**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
from advisory to deterministic, or add an
[**Enforcement**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
**role**) and only **then** concrete (today's binding — point into the
current [tooling snapshot](../../guide/)). The report is itself committed
to the repository alongside the instance it assesses.
