---
name: deep-research
description: Build a source-backed model of a broad topic across historical evolution, current alternatives, and plausible future paths. Use for technologies, companies, industries, people, or trends that need landscape research; do not use merely to verify one or a few claims.
---

# Deep Research

## Metadata

- Category: Research
- Primary gap: `evidence_gap`
- Input requirements: a broad research question and any material scope constraints supplied by the user
- Questions: Q0—define a reasonable scope and proceed by default; follow the [questioning policy](../../protocols/questioning-policy.md)
- Evidence policy: [shared evidence policy](../../protocols/evidence-policy.md), with primary-source preference and dated support
- Recommended predecessors: `socratic-clarify` only when the research question itself is not actionable
- Recommended successors: `fact-audit` for a bounded disputed claim or `steelman-decision` for a supported choice
- Compatible with: `fact-audit`, without re-auditing the entire landscape

Apply the [evidence policy](../../protocols/evidence-policy.md) strictly.

## Scope

Turn the request into a bounded research question. State material assumptions about geography, time horizon, comparison set, or meaning of ambiguous terms. Ask only when choosing incorrectly would invalidate most of the work.

## Research model

### Vertical: evolution

Trace origin, early state, key actors, turning points, successes and failures, path dependencies, and the present state.

### Horizontal: landscape

Compare the target with meaningful alternatives on dimensions that follow from the user's goal. Do not manufacture symmetry or include competitors merely to lengthen a table.

### Forward: paths

Develop a small set of plausible paths. For each, state prerequisites, leading indicators, counter-signals, and what remains unknown. Treat paths as scenarios, not predictions presented as facts.

## Source discipline

- Search or inspect authoritative material rather than relying on memory for external facts.
- Prefer primary sources and record relevant dates.
- Use secondary synthesis where it adds context.
- Surface conflicting evidence and explain its implications.
- Mark unsupported points `UNKNOWN`.

## Output contract

Include:

- research question and scope;
- concise executive synthesis;
- historical timeline and causal turning points;
- current comparative landscape;
- disagreements, uncertainties, and source limitations;
- plausible future paths with indicators;
- implications for the user's actual goal;
- citations close to supported claims.

## Termination

Stop when additional sources are unlikely to change the model or the user's next action. State remaining high-value research gaps instead of pursuing exhaustiveness.
