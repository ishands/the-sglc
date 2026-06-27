# SGLC — Backlog

**Last updated:** 2026-06-27
**Status key:** `[ ]` todo · `[~]` in progress · `[x]` done · `[-]` descoped

---

## Vision

The Software Development Life Cycle was designed for an era when software was
_developed_ — slowly, by humans. That era is ending. Software is now
_generated_ at AI speed, and the lifecycle that governs it has to be
reinvented from first principles.

The **SGLC** (Software Generation Life Cycle) is that reinvention: a
principles-first process framework for governing AI-driven software
work. It has three components, shipped in stages:

1. A **manifesto** — values and principles, quotable, ~1 page.
2. An **invariants spec** — the laws that hold across any organisation, any
   stack, any AI tool.
3. A **conformance suite** — a durable frame for describing the mechanisms
   that control ambiguity, a dated snapshot of current tooling, and
   invariant evaluators an organisation runs against its own toolchain to
   check it honours the invariants.

The manifesto and the invariants spec ship in v0.1.0. The conformance
suite ships in v0.2.0.

The SGLC does not prescribe a process, and it does not hand you an
implementation to adopt. It states the invariants every generation
pipeline must respect, gives you the instrument to verify your own
pipeline against them, and gets out of the way.

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

## v0.2.0 — Conformance Suite

**Goal:** make the SGLC self-testing. Rather than shipping a process for
organisations to adopt, v0.2.0 ships the _instrument_ they check their own
toolchain against — so the principles can be verified, not just read.

All scoped items complete; pending the `v0.2.0` release tag.

- [x] `docs/mechanisms.md` — the durable frame: the role × strength ×
      residence axes any ambiguity-control mechanism sits on, independent
      of any specific tool
- [x] `schema/evaluation-report.md` — the shared evaluation report and
      remediation format
- [x] `schema/skill.md` — the SKILL.md frontmatter spec
- [x] `guide/` — a dated, supersedable snapshot of how today's tools
      (AGENTS.md, skills, rules, hooks) map onto the frame
- [x] Invariant evaluators — one `review-*` skill per invariant
      (all eight shipped, on the validated I-4 mould)
- [x] `review-sglc-compliance` — the orchestrator producing a graded,
      reasoned compliance assessment with prioritised remediation
- [x] `AGENTS.md` — repo agent instructions documenting the durable/contingent
      split and the dated-snapshot superseding discipline
- [x] `guide/howto-create-an-sglc-instance.md` — why an organisation should
      define its own SGLC rather than adopt an off-the-shelf "AI SDLC", and
      how to do it in an SGLC-compliant way
- [x] `guide/howto-run-a-compliance-review.md` — using the evaluators and
      orchestrator to assess an organisation's SGLC (or an in-flight AI SDLC)
- [x] README and docs wiring — front door leads with v0.2.0; read-order and
      repository table extended to the mechanism frame, schema, guide, skills

---

## v0.3.0 — TBD

The previous "Extension and Verification" scope was largely absorbed by the
v0.2.0 pivot: verification is now central to the conformance suite, and the
default library became disposable exemplars. What remains for a v0.3.0, if
anything, is proving the suite against real shapes — a worked example or
case study. Scope to be decided after v0.2.0 ships.

---

## Future / Unscheduled

- WYAIWYG companion piece (Invariant I-3 expanded)
- IGE exploration
- Cross-provider adapter notes
