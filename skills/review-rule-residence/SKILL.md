---
name: review-rule-residence
description: Assess whether an SGLC instance keeps the rules that steer
  generation in the repo. Use when checking whether an instance honours I-5 —
  that skills, principles, and templates are committed, versioned, and owned
  by name rather than living in chat threads, personal config, or one head.
---

# Evaluate I-5 — The rules you give AI belong in the repo, not in someone's chat

This skill assesses one invariant against an organisation's own SGLC
instance. It is a **reviewer, not a linter**: it returns a graded, reasoned
judgement with cited evidence and a remediation shaped against the
[mechanism frame](../../docs/mechanisms.md) — never a code fix. Read
[schema/evaluation-report.md](../../schema/evaluation-report.md) for the
report format this skill fills; read
[docs/mechanisms.md](../../docs/mechanisms.md) for the role / strength /
residence axes the remediation prescribes against.

## The invariant

> **I-5 — The rules you give AI belong in the repo, not in someone's chat.**
>
> The instructions that steer generation — skills, principles, templates —
> are themselves code. They must be durable, versioned, and owned by name.
> Guidance that lives in collaboration tool threads, personal prompt files,
> or one engineer's head dies with the conversation, the employment, or the
> keystroke.

Quoted from
[docs/invariants.md](../../docs/invariants.md#i-5--the-rules-you-give-ai-belong-in-the-repo-not-in-someones-chat).
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

With the inventory in hand, assess I-5. This evaluator owns the
[**residence**](../../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds)
axis: for each mechanism that steers generation, the question is _where it
lives and who it binds_, not whether it exists or how strong it is.

- **Where the steering guidance lives.** Are the skills, principles,
  templates, and conventions that actually steer generation committed to the
  repo — versioned, owned by name, reviewed like code — or do they live in
  chat history, personal prompt libraries, individual machine config, or
  someone's memory? A useful test: would a clean clone of the repo carry the
  rules, or would a new engineer have to be told them?
- **Personal scope versus team scope.** Personal preference may legitimately
  live machine-local. The violation is a _team standard_ placed in personal
  or local residence — a convention everyone is meant to honour that survives
  only while one person does. Separate the two; grade the misplacement of the
  team-scoped ones.
- **Platform-config-only rules.** A rule enforced solely by a hosted
  platform's settings (branch protection in the host UI, org-level prompt
  settings) binds today but is not versioned, reviewed, or portable with the
  repo. Note it as a partial residence gap even when it currently holds.

**Mind the line between residence and strength.** This evaluator grades where
the guidance that _exists_ resides. A mechanism that is missing _everywhere_
is not a residence problem — it is the owning invariant's absence or a
[**strength**](../../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
gap, and it belongs to that invariant's evaluator, not here. Do not absorb a
missing-gate or weak-gate finding into I-5; I-5 is about guidance that should
be shared and durable sitting somewhere it will not survive.

## Compliant patterns

Signals the invariant is honoured:

- The skills, principles, templates, and conventions that steer generation
  are committed, versioned, and owned by name in the repo.
- Team standards are repo-resident; only genuine personal preference lives
  machine-local.
- Guidance reaches consuming codebases through a versioned mechanism, not by
  copy-paste out of a chat thread.

## Anti-patterns

Signals of violation; what this evaluator flags:

- **Guidance in chat or heads.** The real rules steering generation live in
  conversation history or one engineer's memory; a clean clone would carry
  none of them.
- **Team standard in personal residence.** A convention everyone is meant to
  follow lives in one person's machine-local config or personal prompt file —
  it dies on a reformat or a departure. This is the **At risk** signature:
  fine while that person is here, gone the day they leave.
- **Platform-config-only rules.** A team rule represented only in a hosted
  platform's settings, absent from the repo: not versioned, not reviewed, not
  portable.
- **Orphaned guidance.** Rules committed but owned by no one and reviewed by
  no one — present in the tree but rotting, because residence without
  ownership is only half the invariant.

## Coupling notes

This result depends on and affects sibling invariants — surface these so the
orchestrator can reason across strands:

- **Rule residence (I-5) underwrites durability everywhere — so a residence
  gap often surfaces first as another invariant's risk.** An
  [Output verification (I-4)](../review-output-verification/) gate that lives
  only in habit, an [Ask precision (I-3)](../review-ask-precision/) template
  that sits in a personal prompt file, a
  [Rationale capture (I-6)](../review-rationale-capture/) record kept only in a
  chat — each is a residence problem wearing another invariant's mask. When you
  find one, name the root here rather than letting it be mis-filed.
- **The residence/strength distinction is the most common mis-call.** If a
  mechanism is missing or merely advisory, that is the owning invariant's
  problem, not rule residence. This strand fires only when guidance that
  exists is in the wrong _place_ to survive.
- **Rationale capture (I-6)** is the sibling durability invariant: rule
  residence is where the rules live, rationale capture is whether the _why_
  was captured. They co-occur and reinforce each other.
- **Layering (I-7)** depends on residence: layers compose durably only if each
  layer is itself repo-resident.

## Verdict rubric

Grade on the four-point scale (see
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-grade-scale)).
For this invariant:

- **Honoured** — the guidance that steers generation is committed, versioned,
  and owned; team standards are repo-resident; only personal preference is
  local.
- **Partial** — most steering guidance is repo-resident, but some
  team-relevant rules live in personal or platform-only configuration.
- **At risk** — key steering guidance rests on chat or personal residence and
  looks fine only because the current people remember it; it dies on turnover.
- **Absent** — the rules steering generation are not in the repo at all; a
  clean clone carries none of them.

## Output contract

Emit one per-invariant report in the format defined by
[schema/evaluation-report.md](../../schema/evaluation-report.md#the-per-invariant-report):
an `# Evaluation — I-5 …` header block (instance, date, grade, summary), a
**Working** section crediting what is upheld, zero or more **Findings** in
the six-part finding format, and a **Coupling** section naming the siblings
above — flag explicitly where another invariant's apparent risk is really a
residence gap rooted here. Every finding cites real evidence from the
instance, and its remediation is stated **durable first** (which
[axis](../../docs/mechanisms.md) to act on — here, correct the
[**residence**](../../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds):
move a team standard from personal or platform-only config into the repo,
versioned and owned) and only **then** concrete (today's binding — point into
the current [tooling snapshot](../../guide/)). The report is itself committed
to the repository alongside the instance it assesses.
