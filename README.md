# the-sglc

**The Software Generation Life Cycle.**

_Version `v0.2.0` — work in progress._

Software is no longer _developed_ the slow human way; it is _generated_
at AI speed. The SDLC was designed for development. The SGLC is designed
for generation.

This repository is the home of the SGLC: a principles-first process
framework for governing AI-driven software work. It does not prescribe a
process or hand you an implementation to adopt. It states the invariants
every generation pipeline must respect, gives you the instrument to verify
your own pipeline against them, and gets out of the way.

## Read in this order

Start with the thesis:

1. **[The Manifesto](docs/manifesto.md)** — values, principles, ~1 page.
2. **[The Invariants](docs/invariants.md)** — the laws of software generation, formal.
3. **[The Essay](docs/essay.md)** — the argued read, long form.

Then, to put it to work:

4. **[The Mechanism Frame](docs/mechanisms.md)** — the durable role × strength × residence axes any ambiguity-control mechanism sits on.
5. **[How to Create an SGLC Instance](guide/howto-create-an-sglc-instance.md)** — why define your own rather than adopt an off-the-shelf "AI SDLC," and how to do it.
6. **[How to Run a Compliance Review](guide/howto-run-a-compliance-review.md)** — check an instance against the invariants with the evaluators and the orchestrator.

## What's in this repository

| Path                       | What                                                                          |
| -------------------------- | ----------------------------------------------------------------------------- |
| [`docs/`](docs/)           | Manifesto, invariants, essay, and the mechanism frame                         |
| [`schema/`](schema/)       | The shared evaluation-report and SKILL.md formats the suite fills             |
| [`guide/`](guide/)         | Dated tooling snapshots and the how-to guides — the contingent layer          |
| [`skills/`](skills/)       | The eight invariant evaluators and the orchestrator                           |
| [`archive/`](archive/)     | Frozen historical record — original concept draft and prior design documents  |
| [`BACKLOG.md`](BACKLOG.md) | Public roadmap                                                                 |
| [`LICENSE`](LICENSE)       | CC-BY 4.0 (content)                                                            |

## Provenance

The SGLC has been forming over years of practice across software
engineering, technical leadership, toolchain work, and AI-assisted
delivery. Earlier written artefacts behind the thesis are preserved in
[`archive/`](archive/). The `v0.1.0` git tag anchors this first
published shape.

## Founding Author

Ishan De Silva — [@ishands](https://github.com/ishands).

## License

CC-BY 4.0 for content. See [`LICENSE`](LICENSE). A code licence will
be added when a later release introduces code.

## Contributions

This is pre-1.0 and under active development. A full contribution
guide will ship in a later release. Until then: open an issue to
discuss before opening a PR.
