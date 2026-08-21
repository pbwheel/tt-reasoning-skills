---
name: minimum-experiment
description: Convert a decision-critical uncertainty into the cheapest reversible test that can change the decision, with precommitted metrics and continue/stop thresholds. Use when further thought cannot reliably resolve whether something is worth doing; do not use when existing evidence can answer it directly.
---

# Minimum Experiment

## Metadata

- Category: Decide
- Primary gap: `decision_gap`
- Input requirements: a live decision, its critical assumptions, and enough constraints to bound a reversible test
- Questions: Q1—ask at most one question if stakes or feasibility determine the test; follow the [questioning policy](../../protocols/questioning-policy.md)
- Evidence policy: [shared evidence policy](../../protocols/evidence-policy.md), precommitting to discriminating metrics and outcome interpretation
- Recommended predecessors: `steelman-decision`, `reverse-engineer`, `first-principles`, `cross-domain`, or `life-design`
- Recommended successors: None by default; this skill normally ends a chain
- Compatible with: the predecessor skills above when they expose the uncertainty to test

## Start from the decision

State the decision the experiment will inform. List its critical assumptions, then rank them by:

- probability of being wrong;
- effect on the decision if wrong;
- current evidence gap;
- cost and time to test.

Select the highest-value uncertainty, not the easiest metric to collect.

## Design the test

Create the cheapest test that is:

- capable of producing discriminating evidence;
- reversible and bounded in downside;
- short enough to preserve decision value;
- realistic enough that success means something;
- instrumented before execution.

Define the intervention or prototype, target participants or environment, duration, metric, baseline, and confounders. Precommit to continue, revise, and stop thresholds. Avoid vanity metrics and tests whose result cannot change the decision.

## Safety and authorization

Designing an experiment does not authorize spending money, contacting people, publishing material, deploying changes, or collecting sensitive data. Flag required authorization and ethical or privacy constraints before execution.

## Output contract

Include:

- the decision and critical assumptions;
- the highest-value uncertainty and why it dominates;
- experiment design;
- cost, duration, reversibility, and risks;
- metric and baseline;
- continue, revise, and stop thresholds;
- how each outcome changes the decision;
- the first action that can be taken next.

## Termination

Stop when the test is executable, decision-linked, and bounded. Do not append more research unless it is cheaper than the experiment and can resolve the same uncertainty.
