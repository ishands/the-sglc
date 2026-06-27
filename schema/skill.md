# The SGLC Skill Schema

The conformance suite ships as skills — the eight invariant
[evaluators](../skills/) and their orchestrator. SGLC does not define a
skill format; it uses the Agent Skills open standard (agentskills.io): a
folder containing a `SKILL.md` with YAML frontmatter (`name`,
`description`) and a markdown body loaded on demand.

This document covers only what SGLC adds on top of that standard. Where the
standard already specifies something — the file format, the frontmatter
fields, the loading model — SGLC defers to it and does not restate it.

```
skills/<skill-name>/SKILL.md
```

---

## Naming

The one hard addition. A skill name is an action verb, kebab-case, matching
its directory — because a skill does something, and the verb should respect
the
[create / generate boundary](../docs/invariants.md#i-2--deciding-what-to-build-is-human-work-producing-it-isnt)
([I-2](../docs/invariants.md#i-2--deciding-what-to-build-is-human-work-producing-it-isnt)),
the line between judgement work and translation work. Three verb families
anchor that boundary:

- **`create-*`** — supports human judgement work (a decision, a
  specification, a story).
- **`generate-*`** — translates settled judgement into form (code,
  configuration, release notes).
- **`review-*`** — assesses something against a standard. The
  conformance-suite evaluators are `review-*` skills.

These are guides, not a closed list. Other action verbs are fine where they
genuinely fit — `analyse-`, `plan-`, `refine-`, and the like — provided the
verb sits clearly on one side of the judgement / translation boundary and
names a single action. The test is not membership in the list; it is that
the name describes one thing the skill does. A name that needs two verbs is
usually two skills.

The `description` carries the same weight under SGLC as under the standard:
it is the activation cue, and must say both _what_ the skill does and _when_
it applies.

---

## The body is dual-readable and single-source

A skill's markdown body must read as prose to a person and run as
instructions to an agent — one file, not a runnable file shadowed by a
separate human document. For an evaluator this is what keeps its patterns
and anti-patterns from drifting: they live as sections _inside_ the
evaluator, not in a parallel catalogue. The body is the single source for
both how the skill reads and how it runs. An evaluator's body additionally
conforms to the [evaluation report schema](evaluation-report.md).

---

## Layering

Skills compose rather than replace. A universal skill and a more specific
one can both apply to the same work, the specific layering on top of the
general — the shape of
[I-7](../docs/invariants.md#i-7--universal-principles-and-team-specific-rules-both-apply-layered).
This schema fixes no single layering mechanism; it only requires that skills
be written to add to, not overwrite, the skills beneath them.

---

**Navigate:** [Home](../README.md) · [Manifesto](../docs/manifesto.md) · [Invariants](../docs/invariants.md) · [Essay](../docs/essay.md) · [Mechanism frame](../docs/mechanisms.md) · [Create an instance](../guide/howto-create-an-sglc-instance.md) · [Run a review](../guide/howto-run-a-compliance-review.md)
