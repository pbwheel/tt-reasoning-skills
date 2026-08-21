# Research Examples

## Technology landscape

**Request:** “Research the evolution, current landscape, and future of solid-state batteries.”

**Path:** `deep-research`

Bound chemistry, application, geography, and time horizon. Build a sourced timeline of turning points, compare relevant technology families on meaningful dimensions, and present future paths with prerequisites and warning signals. Future paths are hypotheses, not predictions presented as facts.

## Claim inside a landscape

**Request:** “Research vector databases and verify whether filtered search is always slower in product X.”

**Path:** `deep-research -> fact-audit`

The broad study creates the landscape model. The audit then isolates the bounded performance claim and checks documentation, benchmark conditions, versions, and counterexamples. Do not re-audit every fact in the landscape.

## Understand before verifying

**Request:** “Explain differential privacy, then tell me whether it makes data collection risk-free.”

**Path:** `explain-two-levels -> fact-audit`

First connect an intuitive privacy-budget model to the formal mechanism and its boundaries. Then audit “risk-free” as a specific claim, including implementation, auxiliary information, composition, and non-privacy risks.
