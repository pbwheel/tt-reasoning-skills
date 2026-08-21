# Questioning Policy

Ask questions to remove a blocking uncertainty, not to make the workflow feel interactive.

## Levels

| Level | Rule | Skills |
|---|---|---|
| `Q0` | Do not pause by default; proceed with available context and state bounded assumptions | `explain-two-levels`, `deep-research`, `fact-audit` |
| `Q1` | Ask at most one highest-information-value question when it can flip the result | `steelman-decision`, `minimum-experiment` |
| `QN` | Multi-turn inquiry is intrinsic; ask one focused question at a time | `socratic-clarify`, `talent-discovery`, `life-design` |
| `Conditional` | Ask only when missing information would materially change the analysis | `reverse-engineer`, `expert-panel`, `first-principles`, `cross-domain` |

`reason` inherits the strictest question limit of the first selected skill. In plan-only mode it should state missing inputs rather than begin the child skill's interview.

For a QN skill, the child skill owns the interview. After each user answer, check that skill's termination condition before asking again. Return to router-level selection only when the answer materially changes the requested outcome or primary cognitive state; multi-turn interaction alone is not a reason to reroute.

## High-information-value test

A question is justified when its answer is likely to change at least one of:

- the primary cognitive gap;
- the selected skill or skill order;
- the feasible option set;
- a decision-flip variable;
- the safety, reversibility, or validity of the next action.

If not, proceed and state the assumption.

## Interaction rules

- Ask one question per turn for `QN` skills.
- Explain briefly why a sensitive or non-obvious question matters.
- Do not repeat information the user has already supplied.
- Offer examples or answer shapes when the user may not know what evidence is useful.
- Stop asking when the problem is sufficiently defined for the next meaningful action.
