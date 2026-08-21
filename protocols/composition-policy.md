# Composition Policy

## Minimum sufficient principle

Select the shortest skill chain that removes the current blocking gap.

- One skill is the default.
- Two skills are common when resolving one gap reveals another.
- Three skills are reserved for genuinely compound tasks.
- Four skills are allowed only for high-stakes or explicitly deep reasoning.
- Five or more skills are prohibited by default.

Do not pre-run an entire chain. After each skill, reassess whether the user can take the next meaningful action.

## Canonical paths

| Path | Chain | Use when |
|---|---|---|
| Problem discovery | `socratic-clarify -> first-principles` | The problem is vague and inherited assumptions may be shaping it |
| Research decision | `deep-research -> fact-audit -> steelman-decision` | A broad evidence model must support a consequential choice |
| Innovation | `first-principles -> cross-domain -> expert-panel` | A redesign benefits from both structural analogies and multidisciplinary critique |
| High-stakes decision | `socratic-clarify -> fact-audit -> steelman-decision -> minimum-experiment` | Clarity, evidence, choice, and empirical validation are all blocking |
| Learn from benchmark | `reverse-engineer -> first-principles -> minimum-experiment` | Transfer principles from an artifact and test the adapted design |
| Personal direction | `talent-discovery -> life-design -> minimum-experiment` | Evidence about strengths should produce testable future paths |

These are defaults, not mandatory pipelines. Skip any step whose gap is already low.

## Negative rules

- Do not recurse into the same skill.
- Avoid `explain-two-levels -> deep-research` unless explanation reveals a real evidence gap.
- Prefer `first-principles -> steelman-decision`, not the reverse, when inherited assumptions determine the option set.
- Avoid `minimum-experiment -> deep-research`; once a cheap decisive test is available, more research needs a specific justification.
- Do not use `expert-panel` merely to produce theatrical dialogue.
- Do not compose two skills that answer the same primary gap unless their boundary matrix identifies distinct, blocking subproblems.

## Parallel work

V1 defines sequential composition. An agent harness may parallelize independent analysis—for example `first-principles` and `cross-domain` after a shared fact audit—but must synthesize their outputs and preserve the same stop condition.
