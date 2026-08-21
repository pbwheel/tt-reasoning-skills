---
name: reverse-engineer
description: Analyze a specific successful artifact to recover the problem, principles, decisions, structure, and transferable lessons behind it. Use when a concrete product, design, process, or work is available as a benchmark; do not use without a specific artifact.
---

# Reverse Engineer

## Metadata

- Category: Learn
- Primary gap: `knowledge_gap`
- Input requirements: the artifact itself, or enough reliable material to inspect its observable design
- Questions: Conditional—ask only when the artifact or evaluation goal cannot be identified; follow the [questioning policy](../../protocols/questioning-policy.md)
- Evidence policy: [shared evidence policy](../../protocols/evidence-policy.md), with observed properties separated from inferred intent
- Recommended predecessors: None by default
- Recommended successors: `first-principles` for target-specific redesign or `minimum-experiment` for a transfer test
- Compatible with: `explain-two-levels` when the artifact's mechanism also needs explanation

## Input requirements

Obtain the artifact itself or enough reliable material to inspect it. If access is impossible, state what is missing and avoid pretending to reverse-engineer from reputation alone.

## Method

Work backward from observable results:

```text
outcome -> success criteria -> key choices -> structure/process -> target user -> underlying problem
```

For each inferred choice:

1. identify the observable evidence;
2. explain the problem it likely solves;
3. identify the trade-off accepted;
4. separate a transferable principle from implementation detail;
5. note plausible alternative explanations.

Do not copy surface features without recovering their conditions of success.

## Evidence

Apply the [evidence policy](../../protocols/evidence-policy.md). Observed properties are facts; intentions and design rationales are inferences unless supported by primary material.

## Output contract

Include:

- the underlying user and problem;
- the artifact's apparent success criteria;
- the key structural and process decisions;
- evidence-backed principles;
- what is transferable and under which conditions;
- what is artifact-specific or uncertain;
- a concise adaptation checklist or practice exercise.

## Termination

Stop when the analysis can guide an adaptation decision without encouraging superficial imitation.
