---
name: review-intent-origin
description: Assess whether an SGLC instance starts every artifact from a
  human decision. Use when checking whether an instance honours I-1 — that
  generation originates from a recorded, human-owned decision about what the
  artifact should be, not from a cold prompt.
---

# Evaluate I-1 — Every artifact still starts with someone deciding what it should be

This skill assesses one invariant against an organisation's own SGLC
instance. It is a **reviewer, not a linter**: it returns a graded, reasoned
judgement with cited evidence and a remediation shaped against the
[mechanism frame](../../docs/mechanisms.md) — never a code fix. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
report format this skill fills; read
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## The invariant

> **I-1 — Every artifact still starts with someone deciding what it should be.**
>
> Software is always the translation of a human decision into a working
> result. AI compresses how long that translation takes — sometimes from
> days to minutes — but it doesn't remove the need for the decision itself.
> The phases between intent and artifact shorten; they don't vanish.

Quoted from
[docs/invariants.md](../../docs/invariants.md#i-1--every-artifact-still-starts-with-someone-deciding-what-it-should-be).
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

With the inventory in hand, assess I-1. Gather evidence from the instance's
_own_ mechanisms — not an abstract ideal. The question is whether generation
begins from a human decision about what the artifact should be, or starts
cold with the AI inferring its own brief.

- **The entry point to generation.** What kicks off a generation task? Look
  for an artefact that represents a decision — a story, brief, ticket,
  specification — that exists _before_ code is produced, and that generation
  references. Generation that begins from a bare prompt with no decision
  record behind it is the failure this invariant names.
- **A recognised origination step.** Is there a named place where "what
  should this be" is decided and recorded before "produce it" runs —
  discovery, framing, specification, under whatever name the team uses? A
  [**Procedure**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
  for forming the decision, and an
  [**Awareness**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
  convention that nothing is built without one, are the signals.
- **Human ownership of the decision.** The invariant says _someone_ decides.
  Is the "what" owned by a named human, or is the AI both deciding the brief
  and producing against it? (Where the AI decides the what, the
  [judgement boundary (I-2)](../review-create-generate-boundary/) has also gone
  — flag the coupling.)
- **Where the decision lives.** A decision recorded in the repo survives; one
  that exists only in a chat session evaporates. Note the
  [**residence**](../../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds)
  of the decision artefacts.

## Compliant patterns

Signals the invariant is honoured:

- Generation tasks originate from a recorded decision artefact — a story,
  brief, or specification — that precedes and is referenced by the work.
- A recognised framing/origination step stands before generation, owned and
  used rather than nominally present.
- The decision is human-owned: a named person decided what the artifact
  should be, and the record shows it.
- Decision artefacts are repo-resident, so the origin of each artifact is
  recoverable later.

## Anti-patterns

Signals of violation; what this evaluator flags:

- **Generation from a cold start.** Work begins from a bare prompt with no
  decision artefact behind it; the AI infers what to build. There is no
  recorded "someone deciding."
- **The AI originates the brief.** The model decides what should be built,
  not merely how — the decision step has been handed to generation. (This is
  also a [judgement-boundary (I-2)](../review-create-generate-boundary/)
  collapse; name the root.)
- **Decision exists only in chat.** A human did decide, but the decision
  lives in a conversation or someone's head and was never recorded — so the
  artifact has no traceable origin once the session closes. (Couples to
  [rule residence (I-5)](../review-rule-residence/) /
  [rationale capture (I-6)](../review-rationale-capture/).)
- **Origination by individual habit.** Some people frame before generating
  and some don't; there is no mechanism, so the discipline holds only as long
  as the diligent people are present. This is the **At risk** signature.

## Coupling notes

This result depends on and affects sibling invariants — surface these so the
orchestrator can reason across strands:

- **Judgement boundary (I-2)** is adjacent and upstream-paired. Intent origin
  asks whether a decision exists and is recorded; the judgement boundary asks
  whether the _human_, not the AI, makes it. A missing origination step often
  means the AI is deciding scope — a judgement-boundary failure wearing an
  intent-origin mask, or vice versa.
- **Ask precision (I-3)** depends on this one. A decision must exist before
  its precision can be assessed: intent origin establishes that there is an
  ask at all; ask precision grades how sharp it is. Intent origin feeds it.
- **Rationale capture (I-6)** is the _why_ behind the decision intent origin
  requires. A decision recorded without its reasoning is an origin missing its
  rationale.
- **Rule residence (I-5)** governs whether the decision artefacts are durable:
  an origination step whose output never lands in the repo is a residence gap
  showing up as a lost intent origin.

## Verdict rubric

Grade on the four-point scale (see
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-grade-scale)).
For this invariant:

- **Honoured** — every generation task originates from a recorded,
  human-owned decision, and a recognised origination step is in place and
  used.
- **Partial** — decisions precede generation for some work but not all, or
  the origination step exists only as informal convention.
- **At risk** — decisions are made but live only in chat or in people's
  heads, or origination rests on individual habit; it holds today and fails
  on turnover or under pressure.
- **Absent** — generation routinely starts cold, with no decision artefact;
  the AI infers what to build.

## Output contract

Emit one per-invariant report in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-per-invariant-report):
an `# Evaluation — I-1 …` header block (instance, date, grade, summary), a
**Working** section crediting what is upheld, zero or more **Findings** in
the six-part finding format, and a **Coupling** section naming the siblings
above. Every finding cites real evidence from the instance, and its
remediation is stated **durable first** (which
[axis](../../docs/mechanisms.md) to act on — typically add an origination
[**Procedure**](../../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
or correct the
[**residence**](../../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds)
of decision artefacts) and only **then** concrete (today's binding — point
into the current [tooling snapshot](../../guide/)). The report is itself
committed to the repository alongside the instance it assesses.
