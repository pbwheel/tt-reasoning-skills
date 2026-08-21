# Reasoning Skill Contract

## Purpose

Each atomic skill solves one defined cognitive task. The `reason` router either selects atomic skills or returns a direct outcome when no cognitive gap blocks the requested work. Neither form may expand into a comprehensive analysis when the user only needs the next meaningful action.

## Required metadata

Every skill must make these properties discoverable in its frontmatter or body:

- `name`, `category`, and `summary`
- `use_when` and `do_not_use_when`
- `input_requirements` and `output_contract`
- `question_policy`
- `evidence_policy`
- composition: `recommended_predecessors`, `recommended_successors`, `compatible_with`
- `termination`

The YAML frontmatter remains intentionally small: `name` and a discriminating `description`. The description supplies `summary`, `use_when`, and `do_not_use_when`. The body's `Metadata` section supplies the remaining routing properties. Use `None by default` rather than omitting a composition field; this keeps the interface explicit without inventing a relationship.

Composition fields are directional:

- `recommended_predecessors`: skills that should run before the current skill when their gap blocks it;
- `recommended_successors`: skills that may run after the current skill when a new blocking gap appears;
- `compatible_with`: skills that may participate in the same workflow without implying order.

## Behavioral requirements

### Preserve the user's task

- Treat the user's goal, constraints, provided material, and authorization as controlling inputs.
- State a necessary assumption when it could materially change the result.
- Do not use a reasoning method to silently replace the user's requested deliverable.

### Reduce one primary gap

Each atomic skill names one primary cognitive gap internally:

- `clarity_gap`
- `knowledge_gap`
- `evidence_gap`
- `solution_gap`
- `decision_gap`
- `direction_gap`

A skill may reveal another gap. It should hand off or recommend a next skill only when that new gap blocks progress.

### Ask proportionately

Follow [`questioning-policy.md`](questioning-policy.md). Ask only when the answer has enough information value to alter the method, conclusion, or safety of the next action.

### Maintain epistemic integrity

Follow [`evidence-policy.md`](evidence-policy.md). Do not present remembered, inferred, simulated, or generated material as verified fact.

### Compose minimally

Follow [`composition-policy.md`](composition-policy.md). Use one skill by default and stop when the user can take the next meaningful action.

## Output contract

Outputs need not use a rigid template, but they must:

1. answer the skill's defined cognitive task;
2. preserve material uncertainty and conflicting evidence;
3. distinguish evidence from interpretation where confusion would matter;
4. end with a usable conclusion, next action, or precisely defined open question;
5. avoid adding unrelated analysis merely because another skill could be applied.

## Termination

Stop when all required output elements are present and the user can take the next meaningful action. Do not continue for exhaustiveness alone.
