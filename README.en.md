# Reasoning Skills

Thirteen composable reasoning skills that load a person's proven thinking methods into an AI agent — so it thinks before it acts; they cover how to think, not what to think ([boundaries](#boundaries-non-goals)).

[English](README.en.md) · [简体中文](README.md)

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Harness](https://img.shields.io/badge/Claude%20Code%20%C2%B7%20Codex%20%C2%B7%20Cursor-supported-1f6feb)

## What problem does it solve?

Good thinkers keep a personal toolkit of methods — clarify the question before acting, check the evidence before concluding, build the strongest case for the opposing side before a big decision. This library turns such a personal thinking-method toolkit into skills an AI can execute: twelve classic reasoning methods (adapted from a shared article — see [Source](#source--acknowledgment)) become small, single-job skills, plus a [`reason`](skills/reason/SKILL.md) router that diagnoses and dispatches. A useful analogy: `reason` works like a hospital triage desk — it first works out which kind of gap your "illness" falls under, then sends you to the right department; and if nothing is wrong, you don't register at all: simple tasks get done directly, with no reasoning workflow forced on top.

The whole library is plain Markdown — no scripts, no dependencies.

```text
reason: diagnose the blocking gap first, then take the shortest sufficient path

├─ no gap blocking  -> complete the task directly, no reasoning workflow
├─ one gap blocking -> pick one skill from the matching family (table below)
└─ gaps interlocked -> shortest chain; reassess each step, stop when actionable
```

Six cognitive gaps, each served by one to three methods:

| Gap | Skill | Source method | What it does |
|---|---|---|---|
| Clarity — question unclear | [`socratic-clarify`](skills/socratic-clarify/SKILL.md) | Socratic questioning | One question at a time, turning a mixed-up request like "I feel stuck" into a problem definition you can act on |
| Knowledge — concept not understood | [`explain-two-levels`](skills/explain-two-levels/SKILL.md) | Two-level explanation | Explains a concept in two levels — intuition and one example first, then the real mechanism — avoiding the illusion of understanding that "explain like I'm five" creates |
| Knowledge — concept not understood | [`reverse-engineer`](skills/reverse-engineer/SKILL.md) | Reverse teardown | Takes a concrete successful artifact and works backward to why it works and which lessons transfer |
| Evidence — missing | [`deep-research`](skills/deep-research/SKILL.md) | Horizontal-vertical analysis | Builds a source-backed panorama of a whole topic: history, landscape, where it is heading |
| Evidence — missing | [`fact-audit`](skills/fact-audit/SKILL.md) | Fact-check | Decomposes one specific claim into verifiable claims, inferences, and value judgments; rules on each, then checks the reasoning itself for holes |
| Solution — trapped in inherited assumptions | [`first-principles`](skills/first-principles/SKILL.md) | First principles | Strips inherited assumptions down to facts and goals and re-derives the design — "only a rewrite can fix this" is often just an unverified assumption |
| Solution — trapped in inherited assumptions | [`cross-domain`](skills/cross-domain/SKILL.md) | Cross-domain borrowing | Abstracts the problem into structure and retrieves mature solutions from distant domains, stating where each analogy breaks |
| Solution — trapped in inherited assumptions | [`expert-panel`](skills/expert-panel/SKILL.md) | Expert consultation | Has genuinely complementary professional perspectives analyze, challenge one another, and surface the real disagreements before synthesizing — not a staged debate |
| Decision — weak grounds | [`steelman-decision`](skills/steelman-decision/SKILL.md) | Two-way steelman | Builds the strongest case for every option (not just the favored one), then names the few variables that could flip the ranking |
| Decision — weak grounds | [`minimum-experiment`](skills/minimum-experiment/SKILL.md) | Minimum experiment over speculation | Turns speculation like "should we invest three months" into a minimal experiment you can start tomorrow and stop anytime |
| Direction — undefined | [`talent-discovery`](skills/talent-discovery/SKILL.md) | Hidden talent discovery | Infers your transferable strengths — and the conditions that amplify or suppress them — from concrete episodes, not adjective lists |
| Direction — undefined | [`life-design`](skills/life-design/SKILL.md) | Life design | From confirmed strengths and values, generates several genuinely different, individually testable future paths — including staying the course |

## Three design choices worth knowing

1. **The router looks only for the highest blocking gap**: with no gap it just does the work. Only when gaps depend on one another does it form a chain, reassessing after every step and stopping as soon as the user can act — never reasoning for reasoning's sake.
2. **Behavior is governed by five shared protocols**: how evidence is graded (fact / inference / hypothesis / judgment / unknown), when a skill may pause to ask the user, which skills may combine — so all thirteen skills behave predictably instead of drifting with the model and context.
3. **They govern how to think, not what to think**: no replacing domain expertise, no code generation or engineering actions, no promise of live web access — search capability depends on the host agent (see [boundaries](#boundaries-non-goals)).

## Examples

**Engineering decision** — a full routing pass:

```text
Input: Should we rewrite our legacy service in Rust?

reason diagnosis (visible in plan-only mode):
  problem: whether to rewrite the core service; the current argument cannot decide it
  solution_gap: high  <- the option set rests on the inherited "rewrite vs patch" assumption
  decision_gap: high
  other gaps: low
  outcome: chain
  selected: first-principles -> steelman-decision -> minimum-experiment

Step 1 first-principles (output excerpt):
  Basic facts: the performance pain sits in 2 of 11 modules; 3 maintainers; 40+ callers
  Inherited assumption: "only a full rewrite fixes performance" — unverified
  Re-derived path: rewrite the 2 hot modules locally, keep the public API and existing callers
  First verification: one week of profiling on the hot modules to bound the achievable gain
```

If the re-derivation makes the choice obvious, the chain stops at `first-principles` and the remaining steps are skipped.

**Personal development**: starting from concrete experience, `talent-discovery` infers transferable strengths, `life-design` generates testable future paths, optionally closing with `minimum-experiment`.

Each of the twelve skills gets three short entries: when to use it (with what the request sounds like), when not to (when it is the wrong tool), and what it does in practice. Routing and composition rules live in `protocols/`.

**socratic-clarify**

When to use it:

```text
"I feel stuck and want a different life."
"Our metrics are bad, we need a dashboard."
```

The pattern: the message mixes several concerns, states no success condition, and treats feelings, facts, and guesses as one thing.

When not to: the problem is already precise and only information, a solution, or a choice is missing — clarification would be performative.

What it does: one question at a time, each chosen for its effect on the problem definition; the output separates the original concern, the actionable problem, confirmed facts, and unverified assumptions, ending with a question only if one still blocks progress.

**explain-two-levels**

When to use it:

```text
"What is differential privacy?"
"How does CRDT replication actually work?"
```

The pattern: a concept stands between the user and their task, and "explain like I'm five" would only create the illusion of understanding.

When not to: the real task is verification, design, or selection — explaining the concept would dodge the job.

What it does: level one builds an accurate intuition with one concrete example and states where the analogy breaks; level two introduces the real mechanism and boundaries, closing with checks that reveal whether the mechanism — not the analogy — was understood.

**reverse-engineer**

When to use it:

```text
"This onboarding flow is excellent — why does it work?"
```

The pattern: a concrete artifact exists and the goal is to learn from it, not to review it.

When not to: no specific artifact is available. Reverse-engineering from reputation alone is fabrication.

What it does: work backward from observable results to the key choices, each inference with its evidence and a plausible alternative explanation; the output separates transferable principles from artifact-specific details.

**deep-research**

When to use it:

```text
"Give me a real picture of solid-state batteries — history, landscape, where this is going."
```

The pattern: the task is orientation across a whole topic.

When not to: one or a few specific claims need verification — that is a bounded audit, not a landscape.

What it does: the request becomes a bounded question; a vertical sourced timeline, a horizontal comparison of alternatives on dimensions that follow from the user's goal, and a few forward scenarios with prerequisites and warning signals — conflicts and unsupported points stay marked.

**fact-audit**

When to use it:

```text
"This post says the framework makes every API 10x faster. Reliable?"
```

The pattern: a specific claim, analysis, or argument needs testing.

When not to: the goal is broad orientation to a field — an audit of everything becomes a survey of nothing.

What it does: every material claim gets a ledger verdict (verified, supported but needs narrowing, disputed, insufficient evidence, contradicted), then the reasoning itself is audited; the output is a narrowed claim with an explicit confidence level.

**first-principles**

When to use it:

```text
"Our Java service is increasingly hard to maintain. Rewrite in Rust?"
```

The pattern: the option set itself grew out of inherited assumptions, and patches have been accumulating on patches.

When not to: the options are already sound and the facts are agreed — choosing is the job, not reframing.

What it does: irreducible facts, unverified assumptions, the actual goal, and real constraints are separated, each alleged constraint must defend itself, and a minimal design is re-derived from the survivors — with migration cost and existing users respected; the output names which parts of the old approach were surface patches.

**cross-domain**

When to use it:

```text
"We've tried everything our industry knows — how do other fields handle this?"
```

The pattern: the local solution space feels exhausted.

When not to: a same-domain solution or a direct fact answers the question — cheaper and safer than analogy.

What it does: the problem is stripped of domain nouns into structure, and distant domains with mature responses are retrieved (agent memory: CPU caches, library weeding); each analogue gets its structural mapping and breaking points, and the output is adapted options with transfer limits.

**expert-panel**

When to use it:

```text
"Engineering says it's ready, legal is worried, sales needs it this quarter."
```

The pattern: genuinely different professional models are deadlocking the problem.

When not to: one domain has a determinate answer, or the request is really for entertaining dialogue.

What it does: the smallest set of complementary models challenges one another to separate shared facts from true disagreements; the output is an integrated recommendation or a bounded option set, with panel positions labeled as judgment, never laundered into consensus.

**steelman-decision**

When to use it:

```text
"Both vendors and an internal build are feasible. Which?"
```

The pattern: two or more plausible options with real trade-offs, and the facts are clear enough to compare.

When not to: the option set still needs reframing (`first-principles`) or the factual basis is missing (`fact-audit`).

What it does: every option gets its strongest case under comparable standards, and the few decision-flip variables are named; if one unanswered question could reverse the ranking, only that question is asked. The recommendation separates evidence from value weights and states its confidence.

**minimum-experiment**

When to use it:

```text
"Should we spend three months building the enterprise integration?"
```

The pattern: further analysis cannot resolve the uncertainty; only behavior can.

When not to: existing evidence can answer the question directly — researching first is then cheaper than testing.

What it does: the highest-value uncertainty becomes the cheapest reversible test, with the metric and continue/revise/stop thresholds precommitted before execution; the output names what each result would mean and the first action to take tomorrow — designing a test authorizes nothing by itself.

**talent-discovery**

When to use it:

```text
"I don't know what I'm genuinely good at."
```

The pattern: the evidence about strengths has never been assembled, one episode at a time.

When not to: the user wants future paths before strength evidence exists (`life-design` first needs material), or wants a personality label — this skill does not assign identities.

What it does: one concrete episode at a time — situation, behavior, result, difficulty, energy; patterns become capability hypotheses with supporting and contrary evidence and the conditions that amplify or suppress them.

**life-design**

When to use it:

```text
"What should my next chapter look like?"
```

The pattern: the user knows enough about their strengths and values to construct futures, and wants more than cosmetic variants of one answer.

When not to: strength evidence is still missing — generating paths before `talent-discovery` produces fiction.

What it does: a design brief built from actual choices, not aspirations; several genuinely different paths — including continuity paths — each with required assumptions, trade-offs, and a reversible probe. The output is a portfolio of testable futures, not a destiny.

Full workflows live in [`examples/`](examples/) (software engineering, product decisions, research, personal development); routing fixtures live in [`evals/`](evals/).

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

## How it works

Routing and behavior are governed by shared protocols in [`protocols/`](protocols/):

- [`reasoning-contract.md`](protocols/reasoning-contract.md) defines the common contract.
- [`evidence-policy.md`](protocols/evidence-policy.md) separates facts, inferences, hypotheses, judgments, and unknowns.
- [`questioning-policy.md`](protocols/questioning-policy.md) controls when a skill may pause for questions.
- [`composition-policy.md`](protocols/composition-policy.md) defines canonical paths and forbidden combinations.
- [`skill-boundaries.md`](protocols/skill-boundaries.md) is the routing and boundary source of truth.

`reason` reads the boundary and composition rules, diagnoses the highest blocking gap, selects one skill or a chain, executes, and reassesses after every step. How you invoke a skill depends on your agent: Claude Code triggers skills automatically from their descriptions, or you can just say "use fact-audit on this claim"; Codex-style agents use `$reason`-style commands; plan-only mode returns the routing without executing it.

## Boundaries (non-goals)

- Does not replace domain expertise — skills structure the reasoning; domain content still comes from you or the agent's tools.
- Does not generate code or perform engineering actions — this is a reasoning-method library.
- Does not aim for a single "perfect answer" — every step stops once the user can take the next meaningful action.
- Does not promise live web access — `deep-research` and `fact-audit` work within the host agent's tool capabilities.

## Source & acknowledgment

The original article is a **personal** toolkit of thinking methods — twelve prompts the author validated through long personal use; this library turns it into a version any agent can load: your methods, its execution.

### Why not just use the original 12 prompts?

You absolutely can — they still work standalone. What this library adds is the layer above them:

- **Choosing**: which of the 12 methods to apply, in what order, and when to stop is left to the reader in the article; `reason` turns that judgment into an executable gap diagnosis for the agent
- **Chaining**: a single prompt is one isolated conversation; only skills with composition fields and stop conditions can form dependency-ordered chains
- **Consistency**: prompt output drifts with model and context; five protocols standardize evidence grading, questioning timing, and behavioral boundaries, so all thirteen skills behave predictably

### The article and thanks

The core reasoning methods behind the twelve skills come from this article (in Chinese) by 数字生命卡兹克:

> [《都 Agent 时代了，我还是想分享给你这 12 个我最常用的 Prompt》](https://mp.weixin.qq.com/s/NAdhdFrUq9-BKelqzqpwBQ) — "Even in the Agent era, I still want to share the 12 prompts I use most" (original, on WeChat)

The article organizes its twelve prompts into five scenarios: clarifying the question, learning, solving problems, deciding, and knowing yourself. On top of that, this library:

- rewrites each method into an independent, composable skill;
- splits the article's "learning" scenario into the Learn and Research families, remapping everything onto six cognitive gaps;
- adds the `reason` router and the shared `protocols/` layer, which are not part of the article.

The twelve methods are not a ceiling — follow the repo conventions (`AGENTS.md`) to add your own thinking methods as skills, and they join the same routing system.

The "Source method" column in the [skill table](#what-problem-does-it-solve) at the top maps each skill back to its original prompt. Thanks to the author for sharing.

If these skills help you, a star is appreciated.

## License

[MIT](LICENSE) · Copyright (c) 2026 pbwheel
