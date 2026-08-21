# Skill Metadata and Boundary Matrix

This file is the source of truth for routing boundaries. Individual skill files contain the executable detail.

## Metadata matrix

| Skill | Category | Primary gap | Use when | Do not use when | Questions | Required output |
|---|---|---|---|---|---|---|
| `reason` | Router | highest blocking gap or none | The user needs reasoning help but the right method is unclear, or requests a routing plan | An explicitly selected atomic skill is sufficient | Inherits first selected skill | Direct action, minimum sufficient workflow, or routing plan in plan-only mode |
| `socratic-clarify` | Clarify | `clarity_gap` | Goal, facts, assumptions, or constraints are mixed | The problem is clear and only facts or a choice are missing | QN | Actionable problem statement, facts, assumptions, variables, next question |
| `explain-two-levels` | Learn | `knowledge_gap` | A concept or mechanism needs intuitive and technical explanation | The real task is verification, design, or selection | Q0 | Intuition, precise mechanism, boundary, misconception, comprehension check |
| `reverse-engineer` | Learn | `knowledge_gap` | A concrete artifact is available as a benchmark | No specific artifact exists | Conditional | Problem, principles, decisions, structure, transferable and local lessons |
| `deep-research` | Research | `evidence_gap` | A broad topic needs historical, comparative, and future analysis | Only one or a few claims need verification | Q0 | Scope, timeline, landscape, conflicts, scenarios, sources, unknowns |
| `fact-audit` | Research | `evidence_gap` | Claims or an argument need verification | The goal is broad domain orientation | Q0 | Claim ledger, evidence verdicts, inference audit, corrected conclusion |
| `expert-panel` | Solve | `solution_gap` | The problem has genuine cross-disciplinary trade-offs | A single professional model gives a determinate answer | Conditional | Complementary models, disagreements, assumptions, synthesis, risks |
| `first-principles` | Solve | `solution_gap` | Legacy complexity or convention hides the real design space | The task is simply to choose among already sound options | Conditional | Facts, assumptions, goal, constraints, redefinition, derived design |
| `cross-domain` | Solve | `solution_gap` | Distant domains may contain structurally similar mature mechanisms | A known same-domain solution or direct fact is sufficient | Conditional | Abstract structure, analogues, mappings, transfer limits, adapted options |
| `steelman-decision` | Decide | `decision_gap` | Two or more plausible options have real trade-offs | The problem or factual basis is still too unclear | Q1 | Strongest cases, conditions, trade-offs, flip variables, recommendation |
| `minimum-experiment` | Decide | `decision_gap` | Thinking cannot cheaply resolve a decision-critical uncertainty | The answer is already knowable from available evidence | Q1 | Assumptions, highest-value uncertainty, reversible test, thresholds, first action |
| `talent-discovery` | Self | `direction_gap` | The user wants evidence-based patterns in strengths and energizing conditions | They only need possible future paths | QN | Experience evidence, recurring patterns, capabilities, conditions, hypotheses |
| `life-design` | Self | `direction_gap` | The user needs multiple plausible future paths | They first need evidence about their strengths or values | QN | Current state, values, constraints, futures, trade-offs, tests |

## User-language boundary matrix

| User question | Prefer | Do not prefer first | Boundary reason |
|---|---|---|---|
| What is my real problem? | `socratic-clarify` | `first-principles` | Define the problem before redesigning it |
| What does this concept mean? | `explain-two-levels` | `deep-research` | Understanding does not require a landscape study |
| Why is this product excellent? | `reverse-engineer` | `expert-panel` | The artifact, not hypothetical experts, is the evidence |
| Give me a complete view of this technology | `deep-research` | `fact-audit` | The scope is a domain, not a claim set |
| Is this claim reliable? | `fact-audit` | `deep-research` | Test the claim without expanding the whole field |
| Reconcile technical, legal, and commercial concerns | `expert-panel` | `cross-domain` | The key is conflicting professional models, not analogy |
| Why has this system become so complex? | `first-principles` | `steelman-decision` | Rebuild the option set before choosing |
| How do other fields solve this structure? | `cross-domain` | `expert-panel` | Seek isomorphic mechanisms rather than viewpoints |
| A or B? | `steelman-decision` | `first-principles` | The option set is already adequate unless assumptions say otherwise |
| How can we tell whether this is worth doing? | `minimum-experiment` | `steelman-decision` | The blocker is empirical uncertainty, not argument quality |
| What am I genuinely good at? | `talent-discovery` | `life-design` | Infer strengths before designing futures |
| What should my next chapter look like? | `life-design` | `talent-discovery` | Generate paths when strengths and values are sufficiently known |

## Router state model

| State | Missing ingredient | Family |
|---|---|---|
| `DIRECT` | No cognitive ingredient; perform the requested deliverable or action | No skill |
| `UNCLEAR` | The actual problem | Clarify |
| `UNDERSTANDING` | A concept, mechanism, or artifact model | Learn |
| `EVIDENCE` | Facts, evidence, or history | Research |
| `SOLUTION` | A good solution path | Solve |
| `DECISION` | A justified choice or validation method | Decide |
| `DIRECTION` | Personal strengths or future direction | Self |

`DIRECTION` maps to `direction_gap`. A bounded personal choice can instead map to `DECISION`; prefer `DIRECTION` only when constructing or understanding longer-term paths is itself blocking the choice.
