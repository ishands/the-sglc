---
name: review-judgement-boundary
description: Assess whether an SGLC instance keeps deciding-what-to-build as
  human work and producing-it as AI work. Use when checking whether an
  instance honours I-2 — that a clear, observed boundary separates
  human-owned judgement artefacts from AI-produced translation artefacts.
---

# Evaluate I-2 — Deciding what to build is human work; producing it isn't

This skill assesses one invariant against an organisation's own SGLC
instance. It is a **reviewer, not a linter**: it returns a graded, reasoned
judgement with cited evidence and a remediation shaped against the
[mechanism frame](../../docs/mechanisms.md) — never a code fix. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
report format this skill fills; read
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## The invariant

> **I-2 — Deciding what to build is human work; producing it isn't.**
>
> There is always a boundary between deciding _what_ and _why_ (judgment,
> human-owned) and producing _how_ (translation, increasingly AI-owned). As
> AI improves, that boundary moves further toward intent — it never
> disappears. The role of the human shifts up the stack, never out of it.

Quoted from
[docs/invariants.md](../../docs/invariants.md#i-2--deciding-what-to-build-is-human-work-producing-it-isnt).
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

With the inventory in hand, assess I-2. Gather evidence from the instance's
_own_ mechanisms — not an abstract ideal. The question is whether a boundary
is drawn and observed between the artefacts where a human exercises judgement
(the _what_ and _why_) and the artefacts the AI translates into form (the
_how_) — and whether the human still owns the judgement side.

- **Where the boundary sits.** Which artefacts does the instance treat as
  human judgement (stories, decisions, specifications, acceptance criteria)
  and which as AI translation (code, tests, configuration)? Look for a clear
  line, named or structural — for example a `create-*` (judgement) versus
  `generate-*` (translation) distinction in its skills, or any equivalent.
  The contingent form will vary; the durable question is whether the line
  exists and is honoured.
- **Who owns the judgement side.** Does a human author or approve the "what"
  before generation runs, or does the AI decide scope and the human only see
  the result? The role shifting _up_ the stack is compliant; the role leaving
  the stack entirely is not.
- **The strength of the separation.** Is the boundary held by an
  [**Enforcement**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
  gate (a human sign-off on the decision before generation), or only by an
  [**Awareness**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
  convention that asks nicely? Match the strength to the stakes of the work.
- **Judgement artefacts that are themselves generated.** A spec or story the
  AI produced with no human judgement is translation wearing judgement's
  clothes — it looks like a decision but no one decided it.

## Compliant patterns

Signals the invariant is honoured:

- A clear, observed line: judgement artefacts are human-authored or approved;
  translation artefacts are AI-produced. The instance's structure marks it.
- The human owns and signs off the "what" before generation produces the
  "how" — the judgement step is not skippable.
- As AI capability grows, the human's work moves toward intent (sharper
  decisions, better acceptance criteria) rather than disappearing.

## Anti-patterns

Signals of violation; what this evaluator flags:

- **Boundary collapse.** The AI decides what to build and builds it; no human
  judgement step stands over scope. The human is out of the loop on the
  _what_, not merely elevated above the _how_.
- **Human pushed out, not up.** The human neither decides the what nor
  reviews it — the role left the stack rather than moving up it. Generation
  runs end to end unattended on decisions no one made.
- **Judgement artefacts treated as generation.** Stories or specs are
  auto-produced with no human judgement applied, so the "what" is itself an
  AI guess dressed as a decision. Seductive: there appears to be a spec, but
  no one owns it.
- **Boundary by habit only.** The separation rests on individuals choosing to
  apply judgement; nothing stops the AI taking scope decisions, and under
  time pressure it will. This is the **At risk** signature.

## Coupling notes

This result depends on and affects sibling invariants — surface these so the
orchestrator can reason across strands:

- **Intent origin (I-1)** is the paired upstream invariant. Intent origin
  asks whether a decision exists and is recorded; the judgement boundary asks
  whether the human, not the AI, makes it. Together they feed
  [Ask precision (I-3)](../review-ask-precision/) and
  [Output verification (I-4)](../review-output-verification/) — the precision and
  verification downstream inherit any weakness here.
- **Output verification (I-4)** is the other human-judgement bookend. The
  judgement boundary keeps the human owning the _what_ at the front; output
  verification keeps the human checking the output at the back. The same
  role-shift-up-the-stack logic governs both ends of AI translation.
- **Ask precision (I-3)** sits just downstream: a human-owned "what" that is
  vague is an ask-precision problem, not a judgement-boundary one — the
  judgement boundary only asks _who_ owns the decision, ask precision grades
  _how sharp_ it is.
- **Rule residence (I-5)** governs whether the boundary convention itself is
  durable: a separation that lives only in one lead's practice is a residence
  gap showing up as a judgement-boundary risk.

## Verdict rubric

Grade on the four-point scale (see
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-grade-scale)).
For this invariant:

- **Honoured** — a clear boundary is drawn and observed: the human authors or
  approves the what; the AI produces the how; the distinction is structurally
  marked and reinforced.
- **Partial** — the boundary exists but is inconsistently observed, or marked
  by convention without anything reinforcing it.
- **At risk** — the boundary rests on habit; nothing prevents the AI deciding
  scope, and it holds only while the careful people are watching.
- **Absent** — no boundary; the AI decides and produces; the human is out of
  the loop on the what.

## Output contract

Emit one per-invariant report in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-per-invariant-report):
an `# Evaluation — I-2 …` header block (instance, date, grade, summary), a
**Working** section crediting what is upheld, zero or more **Findings** in
the six-part finding format, and a **Coupling** section naming the siblings
above. Every finding cites real evidence from the instance, and its
remediation is stated **durable first** (which
[axis](../../docs/mechanisms.md) to act on — typically raise the
[**strength**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
of the human sign-off on the "what" from advisory to enforced, or make the
judgement/translation boundary explicit in structure) and only **then**
concrete (today's binding — point into the current
[tooling snapshot](../../guide/)). The report is itself committed to the
repository alongside the instance it assesses.
