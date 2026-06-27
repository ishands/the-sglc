# The SGLC Invariants

The invariants are the laws of software generation. They are intended to
hold across any organisation, any technology stack, any AI tool, and
any product. They are the things you cannot ignore without paying for it
later — the _what_ of the SGLC, separate from the _how_ of any specific
implementation.

Each invariant carries a short **handle** — a two- or three-word tag for
citing it in prose and reports without restating the headline — and then
three parts:

- **The headline** — the form a practitioner recognises from their own
  work.
- **The law** — the precise statement, and why it holds.
- **A contingent example** — one concrete way the invariant shows up in
  today's tooling. The example will age; the invariant won't.

The handles, for reference: I-1 Intent origin · I-2 Judgement boundary ·
I-3 Ask precision · I-4 Output verification · I-5 Rule residence ·
I-6 Rationale capture · I-7 Layering · I-8 Local fit.

---

## I-1 — Every artifact still starts with someone deciding what it should be.

**Handle:** Intent origin.

Software is always the translation of a human decision into a working
result. AI compresses how long that translation takes — sometimes from
days to minutes — but it doesn't remove the need for the decision
itself. The phases between intent and artifact shorten; they don't
vanish.

_Contingent example:_ the discovery, framing, and specification work
that exists before any generation runs — under whatever name a team
gives it.

---

## I-2 — Deciding what to build is human work; producing it isn't.

**Handle:** Judgement boundary.

There is always a boundary between deciding _what_ and _why_ (judgment,
human-owned) and producing _how_ (translation, increasingly AI-owned).
As AI improves, that boundary moves further toward intent — it never
disappears. The role of the human shifts up the stack, never out of it.

_Contingent example:_ the distinction between artefacts where the
human exercises judgement (stories, decisions, specifications) and
artefacts where the AI translates that judgement into form (code,
tests, configuration).

---

## I-3 — A vague ask produces vague output.

**Handle:** Ask precision.

Generation can't be sharper than the question that drives it.
Garbage-in / garbage-out is the same law it always was; AI just
executes faster on whatever clarity you give it. The discipline of
asking precisely — knowing _what_ and _how_ to ask — is now a
critical engineering skill, not a soft one.

_Contingent example:_ templated specifications, structured user
stories, and intent checklists that force well-formed input before
generation begins.

---

## I-4 — When AI writes the code, checking it becomes the work.

**Handle:** Output verification.

The bottleneck moves from production to verification. When generating
is cheap and fast, the scarce act is confirming the output actually
matches the intent. Controlling the speed of generation _is_ keeping
verification in step with it. Engineering value migrates upstream
(toward better intent) and downstream (toward stronger checks).

_Contingent example:_ gated review steps and intent-vs-output checks
that compare what was produced against what was asked, before the
change is accepted.

---

## I-5 — The rules you give AI belong in the repo, not in someone's chat.

**Handle:** Rule residence.

The instructions that steer generation — skills, principles,
templates — are themselves code. They must be durable, versioned, and
owned by name. Guidance that lives in collaboration tool threads, personal
prompt files, or one engineer's head dies with the conversation, the
employment, or the keystroke.

_Contingent example:_ generation instructions committed to the
repository as named, owned, versioned files — propagated to consuming
codebases through whatever mechanism the toolchain provides.

---

## I-6 — The reason behind a choice fades fastest — capture it at the moment, or lose it.

**Handle:** Rationale capture.

_Why_ a thing was generated a given way is the first piece of context
to decay and the hardest to recover from the code alone. It has to be
captured at the time of generation, not reconstructed later from a
clean repository six months on. AI accelerates this decay by making the
_what_ trivially fast while leaving the _why_ implicit.

_Contingent example:_ decisions and principles written into the
repository at the moment of the choice, not reconstructed later.

---

## I-7 — Universal principles and team-specific rules both apply, layered.

**Handle:** Layering.

Generation knowledge composes additively: a shared baseline plus a
contextual specialization, not one replacing the other. A general
code-review skill and a team's stack-specific code-review skill both
activate together. The same shape recurs at every scale — within a
single set of instructions, across team boundaries, across phases. It
is fractal.

_Contingent example:_ a generic code-review checklist that every
team inherits, with team-specific additions that activate on top
of it rather than replacing it; the same shape applied from a
community core, through an organisation layer, to product-specific
specialisations.

---

## I-8 — No process framework survives contact with a real team.

**Handle:** Local fit.

Every team and every codebase differs in people, history, tools, and
constraints. A fixed lifecycle is dead on arrival; only principles
plus a mechanism for local fitting endure. The process framework must be like
water — taking the shape of its container.

_Contingent example:_ a starter implementation with explicit
extension points, where teams adopt what fits and replace what
doesn't, rather than a prescribed catalogue every team must adopt
as-is.

---

## What the invariants do not say

The invariants are deliberately silent on the _implementation_ of any
of these laws. They do not specify a phase model, a skill schema, a
distribution mechanism, a verification framework, or a particular AI
tool. Those are the contingent layer — the _how_ — and they will
change. The SGLC intends to ship a default for each in a later
release, but every default is meant to be replaceable.

The invariants are also silent on roles, titles, and organisational
structure. They describe the work, not who does it. How an
organisation distributes the work across people is the organisation's
choice; the work itself doesn't change.
