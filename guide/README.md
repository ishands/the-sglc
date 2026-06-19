# Implementation Guide — Dated Tooling Snapshots

This directory holds the **contingent layer** of the SGLC: concrete, dated
snapshots of how today's tools bind to the durable
[mechanism frame](../docs/mechanisms.md). It is deliberately kept separate
from the standard so that the standard can stay still while the tools churn.

The frame in `docs/mechanisms.md` names the axes — role, strength,
residence — and never names a tool. A snapshot here fills those axes in with
the products of its moment: which tool plays which role, today. When the
tools change, the snapshot ages; the frame does not.

## The snapshot discipline

The standard must not rot when tooling moves. To keep concrete guidance
available without letting it decay the standard, snapshots follow a
dated-and-superseded discipline modelled on
[W3C CSS Snapshots](https://www.w3.org/TR/css/) and the IETF
"Obsoletes / Updated by" and BCP conventions:

- **`docs/mechanisms.md` is the stable label.** It is the durable thing a
  snapshot fills in. Snapshots point back to it; it never points forward to
  any one of them.

- **A snapshot is dated and immutable.** Its filename carries the date it
  reflects (`tooling-snapshot-YYYY-MM.md`), and once issued it is not
  edited in place.

- **Supersede; do not edit.** When a snapshot no longer reflects current
  tooling, do not patch it. Issue a new `tooling-snapshot-YYYY-MM.md` and
  add a header to the old one:

  ```markdown
  > **Superseded by [tooling-snapshot-YYYY-MM.md](./tooling-snapshot-YYYY-MM.md).**
  > Retained as a reference implementation of its era.
  ```

- **Old snapshots are retained, not deleted.** They stay here as readable
  reference implementations of the tooling of their time.

When asked to "update the tooling guidance," the correct action is almost
always to **issue a new snapshot and mark the previous one superseded** —
not to edit the existing one.

## Current snapshot

- [tooling-snapshot-2026-06.md](./tooling-snapshot-2026-06.md) — current.
