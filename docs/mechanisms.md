# The SGLC Mechanism Frame

The invariants are silent on implementation by design. They state the
laws of software generation and leave the _how_ — the tools that carry
those laws into a working pipeline — deliberately open, because the tools
change and the laws do not.

This document fills part of that gap without closing it. It does not name
a tool, prescribe a stack, or hand you a configuration to adopt. It gives
you a **frame** for describing any mechanism that controls ambiguity in
AI-driven software work — the mechanisms an organisation reaches for when
it steers generation: instruction files, skills, scoped rules, intercepting
gates, and whatever replaces them next.

The core move is this: **a specific tool is a coordinate; the frame is the
axes.** `AGENTS.md`, a skill, a path-scoped rule, a pre-commit hook — each
is a point located on three axes. Name the axes and they outlast every
tool that currently occupies them. The current coordinates — which tool
fills which role today — live in a dated, replaceable snapshot under
[`guide/`](../guide/), kept separate from this frame precisely so the frame
can stay still while the snapshot is reissued.

Every mechanism sits somewhere in **(role × strength × residence)** space.

---

## Axis 1 — Role: how guidance reaches generation

A mechanism plays one of four roles, distinguished by _when_ and _how_ its
guidance reaches the point of generation.

- **Awareness** — always-loaded background. What must be true in every
  session: the architecture, the conventions, the standards that apply
  regardless of the task. Cheap to state, expensive to overload.

- **Recognition** — a situational trigger. It answers one question: _does
  this apply right now?_ It carries no procedure of its own; it notices a
  condition and points to what should happen.

- **Procedure** — on-demand know-how. The detailed steps for a task, loaded
  only when that task is actually underway, and absent the rest of the time.

- **Enforcement** — a deterministic gate. It fires regardless of the
  model's attention or judgement. It is the only role that can _stop_ an
  action rather than merely advise it.

The Role axis is how the repo-resident guidance demanded by
[**I-5**](invariants.md#i-5--the-rules-you-give-ai-belong-in-the-repo-not-in-someones-chat)
is actually delivered into generation — the same body of rules reaches the
work differently depending on the role its carrier plays. Keeping the four
roles distinct is what stops one swollen file from trying to be all of them
at once: always-loaded awareness bloated with procedure, or a recognition
trigger carrying an enforcement burden it cannot uphold.

---

## Axis 2 — Strength: the compliance ceiling

The first three roles share a limit: they depend on the model attending to
them. Instruction-following is probabilistic, and it degrades as context
fills and sessions lengthen. This is the **compliance ceiling** — a
property of how these systems work, not a flaw in any one of them.

The consequence is sharp: **anything that must always happen cannot rest on
model attention.** Awareness, Recognition, and Procedure are advisory — right
most of the time, with occasional misses. Only Enforcement is guaranteed.

Strength is therefore a spectrum from soft to hard, and it has a direction:

- **Escalate** a requirement from advisory to enforced as its stakes rise.
- **Never downgrade** an enforced requirement back to advisory unless its
  risk profile genuinely changes.

This axis is
[**I-4**](invariants.md#i-4--when-ai-writes-the-code-checking-it-becomes-the-work)
made structural. Keeping verification in step with
generation means matching the strength of a check to what is at stake — and
refusing to trust attention for the things that must hold every time.

---

## Axis 3 — Residence: where it lives, who it binds

A mechanism lives somewhere, and where it lives determines who it binds and
how long it survives.

- **Repo-resident and shared** — committed, versioned, owned by name,
  reviewed like code. Every contributor inherits it; it outlives any one
  person.

- **Machine-local and personal** — living on one contributor's machine,
  bound to one person, lost on a reformat or a departure.

Residence is
[**I-5**](invariants.md#i-5--the-rules-you-give-ai-belong-in-the-repo-not-in-someones-chat)
applied to mechanisms. A standard the whole team is
meant to honour, placed in machine-local configuration, fails the same way
guidance trapped in a chat thread fails: it dies with the conversation, the
employment, or the keystroke. Personal preference belongs in personal
residence; anything that is a team standard belongs in the repo.

---

## Reading a mechanism through the frame

Locate any mechanism by asking three questions:

1. **Role** — does it make the agent _aware_, help it _recognise_, supply a
   _procedure_, or _enforce_ an outcome?
2. **Strength** — is it advisory or deterministic, and does that match the
   stakes?
3. **Residence** — is it shared and durable, or personal and disposable,
   and does that match its scope?

The answers locate the mechanism, expose its limits, and point at the fix
when it is misplaced — an always-must-happen requirement sitting at advisory
strength, or a team standard sitting in personal residence. This is the
language the [invariant evaluators](../skills/) use to diagnose an SGLC
instance and to prescribe remediation: name the axis to move before naming
the tool to move it.

Mechanisms also **compose**. A baseline and a local specialisation can
occupy the same role and apply together rather than one replacing the
other — the layering of
[**I-7**](invariants.md#i-7--universal-principles-and-team-specific-rules-both-apply-layered),
expressed in mechanism terms.

---

## What this frame does not say

The frame is deliberately silent on which tool to use. It names roles, not
products; strengths, not syntaxes; residences, not file paths. Those are
the contingent layer — they belong in the dated snapshot under
[`guide/`](../guide/), which is expected to be superseded as tooling
evolves.

It is also silent on _how many_ mechanisms an organisation should run, or
which coordinates to choose. A process framework that fixed those choices
would stop being like water. The frame describes the space; the
organisation chooses its own points within it, and fits them to its own
container —
[**I-8**](invariants.md#i-8--no-process-framework-survives-contact-with-a-real-team).
