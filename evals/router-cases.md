# Router Cases

These fixtures test routing behavior, not exact wording. A result passes when the selected path matches the expected path or a documented acceptable alternative, respects the maximum chain length, and stops after the blocking gap is removed.

## Single-skill cases

| # | Input | Expected |
|---:|---|---|
| 1 | “I keep saying our onboarding is bad, but I cannot define what bad means.” | `socratic-clarify` |
| 2 | “We need to improve collaboration, though I am not sure what outcome I actually want.” | `socratic-clarify` |
| 3 | “My cofounder says growth is the problem; I think retention is. Help us frame it.” | `socratic-clarify` |
| 4 | “What are React Server Components?” | `explain-two-levels` |
| 5 | “Why does public-key cryptography work?” | `explain-two-levels` |
| 6 | “Explain eventual consistency to a product manager, then precisely.” | `explain-two-levels` |
| 7 | “Why is Stripe's API design considered good?” | `reverse-engineer` |
| 8 | “Analyze this dashboard and extract design principles we can reuse.” | `reverse-engineer` |
| 9 | “What makes this incident-response playbook effective?” | `reverse-engineer` |
| 10 | “Research the evolution, competitors, and likely future of solid-state batteries.” | `deep-research` |
| 11 | “Give me a source-backed landscape of vector databases.” | `deep-research` |
| 12 | “How did the creator economy develop, and where might it go next?” | `deep-research` |
| 13 | “Someone says RSC reduces every frontend bundle by 90%. Is that credible?” | `fact-audit` |
| 14 | “Check whether the evidence in this memo supports its conclusion.” | `fact-audit` |
| 15 | “Audit these three claims about our competitor's revenue.” | `fact-audit` |
| 16 | “Reconcile privacy, ML quality, and product growth for this personalization feature.” | `expert-panel` |
| 17 | “Our launch has technical, regulatory, and insurance trade-offs. Analyze them together.” | `expert-panel` |
| 18 | “Why has our approval workflow accumulated twelve layers, and what is actually necessary?” | `first-principles` |
| 19 | “Ignore the industry template and derive the simplest system from our constraints.” | `first-principles` |
| 20 | “If we designed billing from zero, which capabilities are irreducible?” | `first-principles` |
| 21 | “What can agent memory learn from caches, libraries, and human memory?” | `cross-domain` |
| 22 | “Find distant fields that solve allocation under uncertain demand.” | `cross-domain` |
| 23 | “How might immune-system mechanisms inspire abuse detection, and where does the analogy fail?” | `cross-domain` |
| 24 | “We can buy or build; both are feasible. Which should we choose?” | `steelman-decision` |
| 25 | “Should I accept the stable role or the riskier role with more learning?” | `steelman-decision` |
| 26 | “Compare monolith and microservices for these stated constraints.” | `steelman-decision` |
| 27 | “We cannot tell whether customers will pay. What is the cheapest useful test?” | `minimum-experiment` |
| 28 | “How can I validate demand before building the integration?” | `minimum-experiment` |
| 29 | “Design a one-week reversible test of this pricing assumption.” | `minimum-experiment` |
| 30 | “Help me find what I am repeatedly good at from my past work.” | `talent-discovery` |
| 31 | “I want to examine when I enter flow without taking a personality test.” | `talent-discovery` |
| 32 | “People ask me to untangle projects. Is that a transferable strength?” | `talent-discovery` |
| 33 | “Help me design several plausible versions of my next five years.” | `life-design` |
| 34 | “I know my values and strengths; what could my next career chapter look like?” | `life-design` |
| 35 | “Create different future paths that preserve family time and financial stability.” | `life-design` |

## Composed cases

| # | Input | Expected path | Stop/reassessment note |
|---:|---|---|---|
| 36 | “Our old Java service is hard to maintain. Should we rewrite it in Rust?” | `first-principles -> steelman-decision -> minimum-experiment` | Skip the experiment if the decision becomes one-way and evidence is already decisive |
| 37 | “I do not know whether low sales are a product or positioning problem; help me decide what to change.” | `socratic-clarify -> minimum-experiment` | Clarification may reveal that existing data can answer it, replacing the experiment with `fact-audit` |
| 38 | “Research the carbon-credit market and tell us whether to enter.” | `deep-research -> steelman-decision` | Add `fact-audit` only for a decision-critical disputed claim |
| 39 | “This acquisition memo claims the market will triple. Audit it and recommend proceed or pass.” | `fact-audit -> steelman-decision` | Stop after audit if the claim is decisively false and no choice remains |
| 40 | “Learn from Linear's product design, then propose one low-risk way to test the principle in our tool.” | `reverse-engineer -> minimum-experiment` | Do not require `first-principles` unless adaptation exposes inherited assumptions |
| 41 | “Our queueing design is stuck in industry convention. Derive the need, borrow mechanisms elsewhere, then reconcile ops and product concerns.” | `first-principles -> cross-domain -> expert-panel` | Stop before panel if no disciplinary conflict remains |
| 42 | “I am unsure what I am best at or what career to try next.” | `talent-discovery -> life-design -> minimum-experiment` | The interaction may span multiple turns before paths are ready |
| 43 | “Clarify what success means for our reorg, then compare centralized and embedded teams.” | `socratic-clarify -> steelman-decision` | Add `expert-panel` only if disciplinary models genuinely block the comparison |
| 44 | “Explain differential privacy, then check the claim that it makes data collection risk-free.” | `explain-two-levels -> fact-audit` | The second task is explicit, so composition is justified |
| 45 | “Research browser-agent security, then audit our claim that confirmation dialogs eliminate prompt injection.” | `deep-research -> fact-audit` | Stop if research already directly and conclusively settles the claim |
| 46 | “This benchmark product is excellent. Extract its principles and redesign our bloated version without copying it.” | `reverse-engineer -> first-principles` | Preserve target constraints rather than importing the artifact wholesale |
| 47 | “We need a retention design inspired by other domains, then a cheap test of the leading mechanism.” | `cross-domain -> minimum-experiment` | Test one translated mechanism, not the analogy as a whole |
| 48 | “Legal says no, engineering says feasible, sales says urgent. Help us choose launch or delay.” | `expert-panel -> steelman-decision` | Do not conflate model synthesis with the final value-weighted choice |
| 49 | “I suspect our incident process is cargo cult. Redesign it and compare gradual migration with replacement.” | `first-principles -> steelman-decision` | Experiment only if a critical empirical uncertainty remains |
| 50 | “I know two career directions; help me choose and design a reversible trial.” | `steelman-decision -> minimum-experiment` | Use `life-design` only if the option set is underdeveloped |
| 51 | “I have a broad concern that AI will replace my work. Help me identify the real decision, examine my evidence, and choose a response.” | `socratic-clarify -> fact-audit -> steelman-decision` | Maximum three unless the user explicitly asks for deeper work |
| 52 | “Should we adopt this new database? First show me only your reasoning plan.” | `reason --plan`: likely `socratic-clarify` or `fact-audit -> steelman-decision` | Do not execute child skills in plan mode |
| 53 | “$reason Summarize the attached paper in five bullets.” | `direct`, selected skills `[]` | A deliverable is requested; no cognitive gap blocks it |
| 54 | “$reason --plan Reformat this supplied table as CSV.” | `direct`, selected skills `[]` | Name the direct action but do not execute it in plan mode |
| 55 | “I have compared the known trade-offs. Should I move to Berlin or stay?” | `steelman-decision` | This is a bounded personal choice among formed options |
| 56 | “I may move, but I do not know what kind of next life chapter or locations would fit.” | `life-design` | Construct personal paths before making a bounded location decision |
| 57 | “After one clarification answer, the desired outcome and constraints are now actionable.” | terminate `socratic-clarify`, then reassess | Do not ask another QN question merely because the skill supports multiple turns |
| 58 | “$reason What is the capital of France?” | `direct`, selected skills `[]` | A simple answer needs no reasoning skill |

## Non-routing checks

- A simple factual answer that requires no reasoning workflow should be answered directly; `$reason` must not force a skill.
- A direct deliverable such as summarization or reformatting should return `outcome: direct` unless a cognitive gap actually blocks execution.
- An explicit atomic-skill invocation should use that skill unless doing so is impossible or unsafe.
- The router must not expose its internal YAML diagnosis in ordinary mode merely because it generated one.
