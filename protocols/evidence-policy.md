# Evidence Policy

## Epistemic labels

Keep these classes logically distinct even when labels are not printed on every sentence:

| Label | Meaning |
|---|---|
| `FACT` | Directly supported by an identified source or user-provided evidence |
| `INFERENCE` | A conclusion derived from facts through an explicit reasoning step |
| `HYPOTHESIS` | A testable explanation or prediction not yet established |
| `JUDGMENT` | A preference, trade-off assessment, or expert evaluation |
| `UNKNOWN` | Material information that cannot currently be established |

`FACT != INFERENCE`. Repetition, plausibility, specificity, and expert tone do not turn an inference into a fact.

## Source strategy

- Prefer user-provided material when the request concerns that material.
- For current or externally verifiable claims, retrieve sources when tools are available.
- Prefer primary sources for factual claims; use strong secondary sources to synthesize or contextualize.
- Record dates when timeliness affects validity.
- When sources conflict, show the conflict and explain what would resolve it.
- When confirmation is unavailable, use `UNKNOWN`; do not substitute model memory.

The `reason` router diagnoses an evidence gap but should not conduct broad research itself. Delegate that work to `deep-research` or `fact-audit`.

## Skill-specific strictness

- `fact-audit`: identify each material claim and classify its support. Audit the inference from verified facts to the conclusion separately.
- `deep-research`: cite the historical, comparative, and forward-looking basis; label future paths as hypotheses or scenarios.
- `expert-panel`: simulated expert positions are `JUDGMENT` unless independently supported.
- `first-principles`: test alleged constraints; industry conventions and inherited designs are usually assumptions, not irreducible facts.
- `cross-domain`: an analogy is an inference. State both the structural match and the limit of transfer.
- `talent-discovery` and `life-design`: experience reports are evidence about events, not proof of fixed personality traits or guaranteed futures.

## Confidence

Express confidence only when it improves the decision. Base it on source quality, agreement, completeness, and sensitivity to unresolved variables—not rhetorical certainty.
