---
name: explain-two-levels
description: Explain a concept first through an accurate intuitive model and then through its professional mechanism, boundaries, and misconceptions. Use for “what is it,” “why,” or “how does it work” requests; do not use when the real task is fact verification, system design, or option selection.
---

# Explain Two Levels

## Metadata

- Category: Learn
- Primary gap: `knowledge_gap`
- Input requirements: a named concept or mechanism and enough context to calibrate the explanation
- Questions: Q0—proceed without pausing by default; follow the [questioning policy](../../protocols/questioning-policy.md)
- Evidence policy: [shared evidence policy](../../protocols/evidence-policy.md), retrieving sources for current, contested, or versioned mechanisms
- Recommended predecessors: None by default
- Recommended successors: `fact-audit` only when a concrete disputed claim remains blocking
- Compatible with: `reverse-engineer` when a concrete artifact is also central

## Method

Build two connected explanations rather than two unrelated summaries.

### Level 1: intuition

Use plain language and one concrete example. Choose an analogy only when its structure matches the mechanism. State where the analogy stops working.

### Level 2: mechanism

Introduce the accurate terms, components, causal or operational sequence, boundary conditions, and a common misconception. Explicitly map the intuitive elements to the technical ones.

Adjust depth to the user's apparent background. Do not inflate the explanation into a history or market survey.

## Evidence

Apply the [evidence policy](../../protocols/evidence-policy.md). Retrieve sources when the concept is current, contested, or version-dependent. Otherwise explain from stable knowledge and mark uncertainty that affects correctness.

## Output contract

Include:

- an intuitive explanation;
- a concrete example;
- the professional mechanism;
- the intuition-to-terminology mapping;
- applicability boundaries;
- at least one common misconception;
- one or two checks that reveal whether the mechanism—not just the analogy—was understood.

## Termination

Stop when the user has a usable mental model and can distinguish the concept from its nearest misconception.
