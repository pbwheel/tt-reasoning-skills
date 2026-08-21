---
name: first-principles
description: Re-derive a solution from irreducible facts, the actual goal, and real constraints after stripping away inherited assumptions and conventions. Use for legacy complexity, cargo cults, and overengineered systems; do not use for a straightforward factual query or an already-sound option comparison.
---

# First Principles

## Metadata

- Category: Solve
- Primary gap: `solution_gap`
- Input requirements: the actual outcome, known facts, alleged constraints, and the current approach when one exists
- Questions: Conditional—ask only when the goal or a hard constraint is materially ambiguous; follow the [questioning policy](../../protocols/questioning-policy.md)
- Evidence policy: [shared evidence policy](../../protocols/evidence-policy.md), treating unverified constraints as hypotheses
- Recommended predecessors: `socratic-clarify` for a vague problem or `reverse-engineer` when adapting a benchmark
- Recommended successors: `cross-domain`, `steelman-decision`, or `minimum-experiment` when the derived design reveals their blocking gap
- Compatible with: `cross-domain` and `expert-panel`

## Frame the problem

Separate four inputs:

- irreducible or directly established facts;
- unverified assumptions and inherited conventions;
- the actual outcome and success measure;
- resource, safety, legal, time, and compatibility constraints.

Challenge each alleged constraint: what establishes it, what fails if it is removed, and whether it is a current constraint or merely a historical design choice.

## Re-derive

Temporarily set aside the current solution and industry defaults. From facts, goal, and validated constraints:

1. redefine the problem in implementation-neutral language;
2. derive the minimum capabilities the solution must provide;
3. generate the simplest coherent design that provides them;
4. add complexity only when a named constraint requires it;
5. compare the derived design with the current approach and explain each difference.

Do not treat “start from scratch” as permission to ignore migration cost, existing users, or irreversible risk.

## Evidence

Apply the [evidence policy](../../protocols/evidence-policy.md). Label uncertain constraints as hypotheses. When technical or external facts determine feasibility, inspect authoritative material rather than assuming.

## Output contract

Include:

- irreducible facts;
- hidden or weak assumptions;
- goal and validated constraints;
- neutral problem redefinition;
- derived minimum capabilities and design;
- complexity deliberately omitted and why;
- migration or transition implications;
- assumptions that need evidence or experiment.

## Termination

Stop when every major design element traces to a fact, goal, or validated constraint and the user has a viable next design action.
