# SGLC — Agent Instructions

Instructions for AI agents working in this repository. This file is itself
an example of an **Awareness**-role mechanism in SGLC terms (see
`docs/mechanisms.md`): always-loaded background context, repo-resident and
shared.

## What this repository is

The **SGLC** (Software Generation Life Cycle) is a principles-first process
framework for governing AI-driven software work. It ships three components:

1. `docs/manifesto.md` — values and principles.
2. `docs/invariants.md` — the laws that hold across any organisation, stack,
   or AI tool.
3. A **conformance suite** — a durable mechanism frame
   (`docs/mechanisms.md`), a dated tooling snapshot (`guide/`), eight
   invariant evaluators plus an orchestrator (`skills/`), and how-to guides
   for building and reviewing an instance (`guide/howto-*.md`).

Read in this order: README → manifesto → invariants → essay.

## The durable / contingent split

Every artefact here is written to one rule: **principles are durable;
implementations age.** When deciding where a statement belongs, apply this
test — the same one `docs/invariants.md` uses ("the example will age; the
invariant won't"):

- Names a **principle, law, role, enforcement strength, or residence** →
  it belongs in the standard (`docs/`). Keep it vendor-neutral and undated.
- Names a **specific tool, file, event, or syntax** → it belongs in a dated
  snapshot under `guide/`, or it is linked out to vendor documentation.

Do not put tool names, product names, or current-syntax examples into
`docs/`. Do not put durable principles into a dated snapshot.

## Dated snapshots and the superseding mechanism

The standard must stay stable while tooling churns. To keep concrete,
current implementation guidance without letting the standard rot, SGLC
uses a dated-snapshot discipline modelled on W3C CSS Snapshots and the
IETF "Obsoletes / Updated by" / BCP conventions:

- **`docs/mechanisms.md` is the stable label.** It defines the durable
  axes any ambiguity-control mechanism sits on. It never names a tool. It
  is the thing snapshots fill in.

- **`guide/tooling-snapshot-YYYY-MM.md` is a dated, immutable snapshot.**
  It maps today's tools onto the axes in `docs/mechanisms.md` and shows
  concrete current shape. Each snapshot carries a header stating the date
  it reflects and "verify against vendor docs."

- **Snapshots are never edited in place once issued.** When a snapshot no
  longer reflects current tooling, do not patch it. Issue a new
  `guide/tooling-snapshot-YYYY-MM.md` and add a header to the old one:

  ```
  > **Superseded by [tooling-snapshot-YYYY-MM.md](./tooling-snapshot-YYYY-MM.md).**
  > Retained as a reference implementation of its era.
  ```

- **Old snapshots are retained, not deleted.** They remain in the
  repository as readable reference implementations of the tooling of their
  time. `guide/README.md` documents this discipline and lists the current
  snapshot.

When asked to "update the tooling guidance," the correct action is almost
always to **issue a new snapshot and mark the previous one superseded** —
not to edit the existing one.

## Terminology

- Use **"process framework,"** not "framework."
- This is a clean-room public repository: no organisation, client, or
  engagement names; nothing personal or aspirational content.

## Naming conventions

- Skills use **action-verb, kebab-case** names: `skills/<name>/SKILL.md`.
- Honour the `create-*` vs `generate-*` boundary (Invariant I-2): `create-*`
  for human-judgement artefacts, `generate-*` for AI-translated ones.
- Evaluators are reviewers and use the `review-*` verb.
