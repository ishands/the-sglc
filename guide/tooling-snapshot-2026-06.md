# Tooling Snapshot — 2026-06

> **Current as of 2026-06.** This is a dated, contingent snapshot, not part
> of the standard. The specifics below will age. Verify every tool detail
> against current vendor documentation, and read the durable frame in
> [docs/mechanisms.md](../docs/mechanisms.md) first. See
> [README.md](./README.md) for how snapshots are superseded.

This snapshot fills in the [mechanism frame](../docs/mechanisms.md) with the
tools available in mid-2026. Each tool is a coordinate in
([**role**](../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
× [**strength**](../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
× [**residence**](../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds))
space; the frame is what endures, this is what occupies it today.

## The bindings at a glance

| Role        | Today's binding          | Strength      | Residence                          |
| ----------- | ------------------------ | ------------- | ---------------------------------- |
| Awareness   | `AGENTS.md`, `CLAUDE.md` | Advisory      | Repo (shared) or `~/` (personal)   |
| Recognition | path-scoped rules        | Advisory      | Repo (shared)                      |
| Procedure   | `SKILL.md` skills        | Advisory      | Repo (shared)                      |
| Enforcement | hooks                    | Deterministic | Repo (shared), needs local tooling |

## By role

The examples below are minimal and illustrative — enough to show the shape.
Exact frontmatter keys, hook events, and config formats vary by tool; treat
the syntax as disposable and confirm it against vendor docs.

**Awareness — `AGENTS.md` and `CLAUDE.md`.** Always-loaded background:
architecture, conventions, standards true in every session. `AGENTS.md` is
the cross-tool form; `CLAUDE.md` the tool-specific one. Keep these lean —
everything here is paid for in every session, so overloading them dilutes
attention rather than adding it.

```markdown
# Courses Service — Agent Instructions

Stack: Go 1.23, PostgreSQL. Timestamps are stored in UTC, never local time.
Commands: `make test`, `make lint`.
Convention: handlers stay thin; business logic lives in the service layer.
```

**Recognition — path-scoped rules.** Files that activate only when the work
touches a matching path, answering "does this apply right now?" without
carrying the full **Procedure** themselves. They are triggers that point at
the **Procedure** to run.

```markdown
---
applies-to: 'src/enrollment/**' # key name varies by tool
---

Enrollment code affects learner records. For any change to completion or
grading logic, invoke the `generate-grading-change` procedure before editing.
```

**Procedure — `SKILL.md` skills.** On-demand know-how, loaded when a task is
underway and absent otherwise. Governed by the open Agent Skills standard
(agentskills.io); see [schema/skill.md](../schema/skill.md) for the shape
SGLC skills take on top of it.

```markdown
---
name: generate-grading-change
description: Apply a change to grading or completion logic. Use when
  modifying how learner progress or eligibility is computed.
---

1. Recompute completion against the updated rule.
2. Update the affected progress records.
3. Revalidate certificate eligibility.
```

**Enforcement — hooks.** Deterministic gates that fire on lifecycle events
regardless of model attention — the only mechanism here that can _stop_ an
action rather than advise it. Use them for what must hold every time:
secret scanning, test gates, protected paths, approval checkpoints.

```bash
# Fires before commit; blocks the commit if the suite fails.
make test || { echo "Tests failed — commit blocked."; exit 1; }
```

## Two patterns worth carrying

These illustrate the durable axes; the syntax is contingent, the shape is
not.

**The Split Pattern (Recognition vs Procedure).** Do not put a full
procedure inside an always-or-often-loaded rule. The anti-pattern crams the
steps into the trigger, so they load on every matching edit:

```markdown
---
applies-to: 'src/enrollment/**'
---

When changing grading:

1. Recompute completion against the updated rule.
2. Update the affected progress records.
3. Revalidate certificate eligibility.
   … (and every further step the procedure needs, loaded on every edit)
```

Those are the same steps the `generate-grading-change` skill holds above —
here they have been crammed into the trigger, so they load on every
enrollment edit, even one that never touches grading. Use the form in the
**Recognition** example instead: the thin rule that points to
`generate-grading-change`, plus the `generate-grading-change` skill that
holds the steps and loads only when invoked. Same behaviour, far less
standing context cost. This is the
[**Role** axis](../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
applied: **Recognition** and **Procedure** are different roles and belong in
different mechanisms.

_Diagnostic:_ if the agent misses the moment to act, that is a
**Recognition** gap — the trigger was not in context. If it acts but skips a
step, that is a **Procedure** gap — the steps were not available. The two
failures point at different roles, and so at different fixes.

**The escalation chain (rule → hook).** The same requirement can sit at two
points on the
[**Strength** axis](../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling).
As an _advisory_ **Recognition** rule it is honoured most of the time:

```markdown
<!-- Advisory only: this relies on model attention, so it will be missed
     sometimes. Use this softer form when occasional misses are acceptable —
     not when enforcement is the desired behaviour. For that, use the hook. -->

Run the test suite before committing.
```

As a _deterministic_ **Enforcement** hook (the pre-commit gate above) it is
honoured every time. Promote a requirement from _advisory_ to _deterministic_
when "usually" stops being good enough; never downgrade unless the risk
genuinely falls. This is the
[**Strength** axis](../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
applied.

## Placing a requirement

When a new requirement appears, the axes give an ordered way to site it.
Ask, in order:

1. Does every contributor need it, in every session? →
   [**Awareness**](../docs/mechanisms.md#axis-1--role-how-guidance-reaches-generation)
   (`AGENTS.md`, or `CLAUDE.md` for a single tool).
2. Is it a procedure — steps for a specific task? → **Procedure** (a
   `SKILL.md` skill).
3. Does it apply only to certain files or paths? → **Recognition** (a
   path-scoped rule that points to the procedure).
4. Must it hold every time, no exceptions? →
   [**Enforcement**](../docs/mechanisms.md#axis-2--strength-the-compliance-ceiling)
   (a hook).
5. Is it personal preference, not a team standard? → machine-local
   [**residence**](../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds)
   (`~/`), never the repo.

The first match is usually the right home. A requirement that seems to need
two of these is often two requirements — split it.

## Open standards vs vendor-specific tools

[**Residence**](../docs/mechanisms.md#axis-3--residence-where-it-lives-who-it-binds)
has a second dimension today: whether a mechanism is portable across tools
or tied to one vendor. As of 2026-06:

- **Cross-tool open standards.** `AGENTS.md` (an open, cross-tool
  agent-instruction format, stewarded under the Agentic AI Foundation) and
  `SKILL.md` (the Agent Skills standard at agentskills.io) are read by a
  range of tools. These are the safest home for **Awareness** and
  **Procedure** that should outlive any one vendor choice.
- **Vendor-specific families.** Most **Recognition** and **Enforcement**
  mechanisms are still tool-specific. Claude Code uses `CLAUDE.md`,
  path-scoped rules, and hooks; other agents — Cursor, GitHub Copilot,
  Windsurf, Gemini CLI, and others — carry their own equivalents under their
  own names and formats.

Prefer the open standards for anything you want to keep when you change
tools, and treat the vendor-specific layer as the part most likely to be
superseded — in your own setup and in this snapshot alike. Tool names,
formats, and which vendors honour which standard all move quickly; verify
against current vendor documentation rather than trusting this list to stay
complete.

## What this snapshot does not cover

Raw syntax and reference detail — exact rule frontmatter, the full list of
hook events and matchers, settings file schemas — change fastest and are
owned better by vendor documentation. This snapshot names the bindings and
their shape; consult the vendors for current syntax.
