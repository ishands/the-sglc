# SGLC — Backlog

**Last updated:** 2026-05-30
**Status key:** `[ ]` todo · `[~]` in progress · `[x]` done · `[-]` descoped

---

## Vision

The Software Development Life Cycle was designed for an era when software was
*developed* — slowly, by humans. That era is ending. Software is now
*generated* at AI speed, and the lifecycle that governs it has to be
reinvented from first principles.

The **SGLC** (Software Generation Life Cycle) is that reinvention: a
principles-first process framework for governing AI-driven software
work. It has three components, shipped in stages:

1. A **manifesto** — values and principles, quotable, ~1 page.
2. An **invariants spec** — the laws that hold across any organisation, any
   stack, any AI tool.
3. A **default starter implementation** — the configurable, extendable
   layer that any organisation can fork and shape to its own
   container.

The manifesto and the invariants spec ship in v0.1.0. The starter
implementation is deferred.

The SGLC does not prescribe a process. It states the invariants every
generation pipeline must respect, intends a default to start from, and
gets out of the way.

---

## v0.1.0 — Foundations

**Goal:** publish the principles.

The first release establishes the thesis. The default skeleton is
intentionally deferred so the principles can stand on their own and be
evaluated on their own terms.

Shipped:

- [x] `docs/manifesto.md` — declarative manifesto: value pairs + named principles
- [x] `docs/invariants.md` — the SGLC invariants, formalised
- [x] `docs/essay.md` — long-form argued read
- [x] `README.md` — front door (vision, read-in-this-order, what's in the repo, provenance, license)
- [x] `BACKLOG.md` — public roadmap
- [x] `LICENSE` — CC-BY 4.0 for content (code licence to follow with a later release)
- [x] `archive/` — frozen historical artefacts behind the thesis

---

## v0.2.0 — Default Skills Library

**Goal:** turn the skeleton into a usable starter library that an
organisation can fork and run with.

In planning. Scope and shape to be defined.

---

## v0.3.0 — Extension and Verification

**Goal:** prove the skeleton fits real shapes; make verification a
first-class concern, not an afterthought.

Backlog. Scope to be defined.

---

## Future / Unscheduled

- **WYAIWYG companion piece** — standalone treatment of *knowing what and how to ask* (Invariant I-3 expanded)
- **IGE exploration** — design notes for an Integrated Generation Environment for non-technical drivers
- Cross-provider adapter notes (Cursor, Gemini CLI, etc.)
