# Boundary Cases

Each case tests a likely confusion between neighboring skills.

| Input | Prefer | Reject or defer | Reason |
|---|---|---|---|
| “What is CRDT?” | `explain-two-levels` | `deep-research` | Concept understanding, not landscape research |
| “How have CRDT systems evolved, and which implementations exist?” | `deep-research` | `explain-two-levels` | Historical and comparative scope |
| “Is this CRDT performance claim true?” | `fact-audit` | `deep-research` | A bounded claim set |
| “Why does this particular editor's collaboration feel seamless?” | `reverse-engineer` | `explain-two-levels` | Concrete artifact and design decisions |
| “Our goal says ‘delight users.’ What does that mean operationally?” | `socratic-clarify` | `first-principles` | The goal is not yet actionable |
| “The goal is a two-minute approval; derive the minimum process.” | `first-principles` | `socratic-clarify` | Goal is clear; solution is blocked by convention |
| “A and B are both viable under known constraints.” | `steelman-decision` | `first-principles` | Choose within an adequate option set |
| “A and B are the only options because our old architecture assumes so.” | `first-principles` | `steelman-decision` | Repair the option set before choosing |
| “What would a lawyer, security engineer, and PM each optimize?” | `expert-panel` | `cross-domain` | Conflicting professional models |
| “What can rate limiting learn from traffic control?” | `cross-domain` | `expert-panel` | Structural mechanism transfer |
| “Is there demand?” with reliable sales data attached | `fact-audit` | `minimum-experiment` | Existing evidence may settle it more cheaply |
| “Is there demand?” with no behavioral evidence | `minimum-experiment` | `steelman-decision` | The blocker is empirical uncertainty |
| “What strengths recur in my experiences?” | `talent-discovery` | `life-design` | Build an evidence-based self-model |
| “Given these established strengths, what futures fit?” | `life-design` | `talent-discovery` | Generate paths from known inputs |
| “Explain why this analogy is useful.” | `explain-two-levels` | `cross-domain` | Explanation of an existing analogy, not solution search |
| “Find analogies that generate new designs.” | `cross-domain` | `explain-two-levels` | Analogy is the solution method |
| “Review whether this report's conclusion follows.” | `fact-audit` | `expert-panel` | Evidence and inference integrity, not perspectives |
| “The evidence is agreed; disciplines value different outcomes.” | `expert-panel` | `fact-audit` | The conflict is judgment and optimization |
| “How does this product work internally?” | `explain-two-levels` | `reverse-engineer` | Mechanism understanding unless design excellence is the target |
| “Which choices made this product outperform alternatives?” | `reverse-engineer` | `explain-two-levels` | Recover design rationale and transferable principles |

## Failure conditions

- Routing from a trigger word while ignoring the actual blocking gap.
- Selecting two adjacent skills that perform the same job.
- Asking a question in a Q0 skill when a bounded assumption would preserve validity.
- Treating a generated expert view, analogy, personal pattern, or future scenario as fact.
- Continuing a clarification or self-exploration interview after the next action is already clear.
