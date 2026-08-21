---
name: socratic-clarify
description: Turn a vague, mixed, or incorrectly framed concern into an actionable problem by separating goals, facts, interpretations, assumptions, and constraints. Use when the user does not yet know the real question; do not use for a clear factual query or an already-defined A/B choice.
---

# Socratic Clarify

## Metadata

- Category: Clarify
- Primary gap: `clarity_gap`
- Input requirements: a concern, goal, or problem statement whose actionable form is unclear
- Questions: QN—multi-turn, one focused question at a time; follow the [questioning policy](../../protocols/questioning-policy.md)
- Evidence policy: [shared evidence policy](../../protocols/evidence-policy.md), with facts separated from interpretations and assumptions
- Recommended predecessors: None by default
- Recommended successors: `deep-research`, `first-principles`, or `steelman-decision` only when the clarified problem reveals that blocking gap
- Compatible with: `fact-audit` when disputed claims emerge during clarification

## Use when

- The stated problem combines several concerns.
- The desired outcome or success condition is missing.
- Facts, interpretations, and value judgments are being treated as the same thing.
- A hidden premise or missing constraint could change which problem matters.

Do not use when the problem is already precise and the user only lacks information, a solution, or a choice.

## Method

Maintain a working distinction among:

- desired outcome;
- directly known facts;
- interpretations of those facts;
- value judgments;
- assumptions;
- constraints;
- alternative explanations;
- variables that could change the framing.

Ask the single question with the highest expected effect on the problem definition. Use the answer to update the model, then ask again only if ambiguity still blocks an actionable formulation. Do not conduct a disguised interrogation or force a predetermined conclusion.

When the user's initial message already contains enough evidence, synthesize directly instead of asking performative questions.

## Output contract

Conclude with:

- the original concern in neutral language;
- the actionable problem or decision;
- confirmed facts;
- unverified assumptions;
- key constraints and variables;
- the next question only if one remains blocking;
- otherwise, the most appropriate next reasoning action.

## Termination

Stop when the problem is specific enough to research, solve, decide, or act on. Do not keep clarifying details that will not change the next step.
