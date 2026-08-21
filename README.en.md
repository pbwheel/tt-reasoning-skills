# Reasoning Skills

Thirteen composable reasoning skills that help an AI agent think before it acts.

[English](README.en.md) · [简体中文](README.md)

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Harness](https://img.shields.io/badge/Claude%20Code%20%C2%B7%20Codex%20%C2%B7%20Cursor-supported-1f6feb)

> Scope: this is a library of **reasoning-method skills** — it helps an agent diagnose what is blocking progress and pick the right thinking path. It is not a code-generation toolkit, it does not replace domain expertise, and it does not promise one "perfect answer".

## What problem does it solve?

When an agent jumps straight to an answer, the failure is usually not missing knowledge but one of six cognitive gaps: the problem is unclear, the mechanism is not understood, the evidence is missing, the solution is trapped in inherited assumptions, the decision rests on weak grounds, or the direction itself is undefined. This library turns twelve classic reasoning methods into single-purpose atomic skills, plus a `reason` router that diagnoses and dispatches:

```text
                         reason
                            |
              +-------------+-------------+
              v             v             v
          Understand      Research        Solve
              |             |             |
              +-------------+-------------+
                            v
                          Decide
                            |
                            v
                         Validate
```

| Gap | Skills |
|---|---|
| Clarity | `socratic-clarify` |
| Knowledge | `explain-two-levels`, `reverse-engineer` |
| Evidence | `deep-research`, `fact-audit` |
| Solution | `first-principles`, `cross-domain`, `expert-panel` |
| Decision | `steelman-decision`, `minimum-experiment` |
| Direction | `talent-discovery`, `life-design` |

When no cognitive gap blocks a requested deliverable, `reason` returns a direct outcome and uses no atomic skill.

## Core features

- **`reason` router** — diagnoses the highest blocking gap, then selects the shortest sufficient path; with no gap it just does the work instead of forcing a reasoning workflow
- **Composable chains** — skills combine by dependency (for example `first-principles -> steelman-decision -> minimum-experiment`); the chain is reassessed after every step and stops as soon as the user can act
- **Shared protocols** — evidence, questioning, composition, and boundary behavior are governed by five protocol documents shared across all thirteen skills
- **Platform-neutral** — plain Markdown skills, no scripts, no dependencies

## Install

### Option 1: npx skills (recommended)

```bash
# install into the current project (auto-detects your agent)
npx skills add pbwheel/tt-reasoning-skills

# or install user-level, for all projects
npx skills add pbwheel/tt-reasoning-skills -g

# see what's inside first
npx skills add pbwheel/tt-reasoning-skills --list
```

Claude Code installs into `.claude/skills/`; Cursor / Codex-style agents into `.agents/skills/` (add `-g` for user-level `~/` install).

Note: the `skills` CLI copies skill directories only, while the `reason` router depends on the repo's root-level `protocols/` (referenced via `../..` relative paths). After installing with npx, also copy `protocols/` next to your `skills/` directory (e.g. `.claude/protocols/`).

### Option 2: manual copy

Copy both `skills/` and `protocols/` under the same parent directory, e.g. `.claude/skills/` and `.claude/protocols/`. The `reason` router references protocols via `../..` relative paths, so the two directories must stay side by side.

### Option 3: hand the repo URL to your agent

Send your agent a message like this and let it read and route by itself:

> Read https://github.com/pbwheel/tt-reasoning-skills and follow its `skills/reason/SKILL.md` to route this question through the right reasoning skills: "…"

## Skill catalog

| Family | Skill | Job |
|---|---|---|
| Router | [`reason`](skills/reason/SKILL.md) | Diagnose the blocking gap, then select and execute the minimum sufficient reasoning path |
| Clarify | [`socratic-clarify`](skills/socratic-clarify/SKILL.md) | Turn a vague or mixed problem into an actionable problem definition |
| Learn | [`explain-two-levels`](skills/explain-two-levels/SKILL.md) | Build intuitive and technical understanding of a concept |
| Learn | [`reverse-engineer`](skills/reverse-engineer/SKILL.md) | Recover the problem, principles, and transferable lessons behind an artifact |
| Research | [`deep-research`](skills/deep-research/SKILL.md) | Build a source-backed model of a topic: history, alternatives, future paths |
| Research | [`fact-audit`](skills/fact-audit/SKILL.md) | Test claims, and whether the verified facts support the conclusion |
| Solve | [`expert-panel`](skills/expert-panel/SKILL.md) | Reconcile genuinely different professional models |
| Solve | [`first-principles`](skills/first-principles/SKILL.md) | Re-derive a solution from facts, goals, and constraints |
| Solve | [`cross-domain`](skills/cross-domain/SKILL.md) | Transfer mechanisms from structurally similar domains |
| Decide | [`steelman-decision`](skills/steelman-decision/SKILL.md) | Choose among plausible options without caricaturing them |
| Decide | [`minimum-experiment`](skills/minimum-experiment/SKILL.md) | Replace unresolved uncertainty with a cheap reversible test |
| Self | [`talent-discovery`](skills/talent-discovery/SKILL.md) | Infer transferable strengths from experience evidence |
| Self | [`life-design`](skills/life-design/SKILL.md) | Create multiple testable future paths |

## How it works

Routing and behavior are governed by shared protocols in [`protocols/`](protocols/):

- [`reasoning-contract.md`](protocols/reasoning-contract.md) defines the common contract.
- [`evidence-policy.md`](protocols/evidence-policy.md) separates facts, inferences, hypotheses, judgments, and unknowns.
- [`questioning-policy.md`](protocols/questioning-policy.md) controls when a skill may pause for questions.
- [`composition-policy.md`](protocols/composition-policy.md) defines canonical paths and forbidden combinations.
- [`skill-boundaries.md`](protocols/skill-boundaries.md) is the routing and boundary source of truth.

`reason` reads the boundary and composition rules, diagnoses the highest blocking gap, selects one skill or a chain, executes, and reassesses after every step. How you invoke a skill depends on your agent: Claude Code triggers skills automatically from their descriptions, or you can just say "use fact-audit on this claim"; Codex-style agents use `$reason`-style commands; plan-only mode returns the routing without executing it.

## Examples

- **Engineering decision**: "Should we rewrite our legacy service in Rust?" routes to `first-principles -> steelman-decision -> minimum-experiment`, stopping early as soon as any step enables the next meaningful action.
- **Personal development**: starting from concrete experience, `talent-discovery` infers transferable strengths, `life-design` generates testable future paths, optionally closing with `minimum-experiment`.

Full workflows live in [`examples/`](examples/) (software engineering, product decisions, research, personal development); routing fixtures live in [`evals/`](evals/).

## Boundaries (non-goals)

- Does not replace domain expertise — skills structure the reasoning; domain content still comes from you or the agent's tools.
- Does not generate code or perform engineering actions — this is a reasoning-method library.
- Does not aim for a single "perfect answer" — every step stops once the user can take the next meaningful action.
- Does not promise live web access — `deep-research` and `fact-audit` work within the host agent's tool capabilities.

## License

[MIT](LICENSE) · Copyright (c) 2026 pbwheel
