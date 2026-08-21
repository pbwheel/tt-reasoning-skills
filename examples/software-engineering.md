# Software Engineering Examples

## Legacy rewrite decision

**Request:** “Our Java service is increasingly hard to maintain. Should we rewrite it in Rust?”

**Path:** `first-principles -> steelman-decision -> minimum-experiment`

1. `first-principles` separates symptoms from facts, validates performance and compatibility constraints, and derives the minimum capabilities without assuming either repair or rewrite.
2. `steelman-decision` compares incremental repair, strangler migration, and rewrite under delivery, hiring, reliability, and opportunity-cost criteria.
3. `minimum-experiment` tests the decision-flip variable—for example whether a representative slice can meet operability and development-speed thresholds.

Stop after step 1 if the alleged need for a rewrite disappears. Stop after step 2 if the evidence is decisive and an experiment would not change the choice.

## Agent memory design

**Request:** “We are designing agent memory. What can we borrow from other fields?”

**Path:** `cross-domain`

Abstract the problem as a limited-capacity system deciding what to retain, retrieve, decay, and consolidate. Candidate analogues might include CPU caches, library indexes, human memory, and inventory control. Each mechanism must include a structural mapping and transfer limit; a poetic similarity is not sufficient.

## Framework performance claim

**Request:** “This post says the framework makes every API 10x faster. Is it reliable?”

**Path:** `fact-audit`

Audit the benchmark setup, baseline, workload, hardware, warm-up, percentile selection, and generalization from the tested endpoint to “every API.” The likely deliverable is a narrowed claim, not a framework survey.
