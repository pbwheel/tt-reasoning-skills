---
name: expert-panel
description: Analyze a problem through genuinely complementary professional models, expose their disagreements and assumptions, and synthesize an actionable view. Use for cross-disciplinary trade-offs; do not use when one domain has a determinate answer or merely to simulate a conversation.
---

# Expert Panel

## Metadata

- Category: Solve
- Primary gap: `solution_gap`
- Input requirements: a problem with at least two materially different professional models or loss functions
- Questions: Conditional—ask only when scope or stakes determine which models matter; follow the [questioning policy](../../protocols/questioning-policy.md)
- Evidence policy: [shared evidence policy](../../protocols/evidence-policy.md), treating generated panel positions as judgment unless sourced
- Recommended predecessors: `first-principles` or `cross-domain` when option generation must precede multidisciplinary critique
- Recommended successors: `steelman-decision` when synthesis leaves a value-weighted choice
- Compatible with: `first-principles`, `cross-domain`, and `steelman-decision`

## Select models

Choose the smallest set of professional models that reveal materially different constraints. Three is a useful default, not a requirement. Explain why each model is relevant and how it differs from the others.

Do not impersonate named living experts or invent quotations. A panel is a structured comparison of models, not theatrical dialogue.

## Analyze

For each model, establish:

- how it defines the problem;
- what it optimizes and constrains;
- its recommended direction;
- what other models tend to miss;
- what evidence would change its view.

Then make the models challenge one another. Identify shared facts, true disagreements, hidden assumptions behind them, and trade-offs that cannot be optimized away.

## Evidence

Follow the [evidence policy](../../protocols/evidence-policy.md). Panel positions are `JUDGMENT` unless supported by sources or user evidence. Do not launder generated opinions into expert consensus.

## Output contract

Include:

- selected models and why they are complementary;
- each model's definition, recommendation, blind spot, and update condition;
- shared facts versus genuine disagreements;
- assumptions driving the disagreements;
- an integrated recommendation or clearly bounded option set;
- major risks, exit conditions, and first action.

## Termination

Stop when the multidisciplinary conflicts are explicit enough to support action or a decision. Do not add more models once they stop changing the synthesis.
