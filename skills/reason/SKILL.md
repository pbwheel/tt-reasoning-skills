---
name: reason
description: Diagnose what is blocking progress and select the shortest sufficient chain from this reasoning-skill library. Use when the right reasoning method is unclear or the user explicitly requests reasoning routing; do not route through it when the user already selected an applicable atomic skill. Use plan-only mode to show routing without execution.
---

# Reason

Route by cognitive state and gap reduction, not by keyword matching.

## Shared rules

Before routing, read:

- [skill boundaries](../../protocols/skill-boundaries.md)
- [composition policy](../../protocols/composition-policy.md)

Apply the [evidence policy](../../protocols/evidence-policy.md) and [questioning policy](../../protocols/questioning-policy.md) when executing the selected workflow.

## Metadata

- Category: Router
- Primary gap: highest blocking gap, or none for direct work
- Use when: the user wants reasoning help but the appropriate method is unclear, or explicitly requests the router
- Do not use when: the user explicitly selected an applicable atomic skill
- Input requirements: the user's requested outcome and available context
- Questions: inherit the first selected skill; ask none for direct work
- Evidence policy: [shared evidence policy](../../protocols/evidence-policy.md)
- Recommended predecessors: None; `reason` is an entry point
- Recommended successors: the selected atomic skill or skill chain
- Compatible with: all skills in this repository

## Diagnose

Build a compact internal diagnosis and routing result:

```yaml
outcome: direct | skill | chain
state: DIRECT | UNCLEAR | UNDERSTANDING | EVIDENCE | SOLUTION | DECISION | DIRECTION
problem: <the progress-blocking problem>
known: []
unknown: []
decision_required: true | false
clarity_gap: low | medium | high
knowledge_gap: low | medium | high
evidence_gap: low | medium | high
solution_gap: low | medium | high
decision_gap: low | medium | high
direction_gap: low | medium | high
```

Do not expose this structure unless it helps the user or plan-only mode was requested.

Ask: **What is preventing progress?** Distinguish the primary gap from gaps that are merely present. A requested deliverable is not automatically a cognitive gap.

Derive `state` from the selected outcome and primary gap: direct -> `DIRECT`, clarity -> `UNCLEAR`, knowledge -> `UNDERSTANDING`, evidence -> `EVIDENCE`, solution -> `SOLUTION`, decision -> `DECISION`, and direction -> `DIRECTION`. The state is a readable summary of the diagnosis, not a second routing signal that may contradict the gap ratings.

## Select

Select from the diagnosis rather than walking a fixed family list:

1. If the user requests a direct deliverable or simple answer and no cognitive gap blocks it, set `outcome: direct`, select no skill, and perform the task normally. Examples include answering a simple factual question, summarizing supplied material, reformatting text, or carrying out an otherwise supported action.
2. Otherwise, select the highest blocking gap. Ignore low gaps. A medium gap may be selected only when no high gap blocks progress.
3. Resolve tied blocking gaps with dependency precedence:
   - `clarity_gap` first when the problem, outcome, or option set cannot yet be defined;
   - `evidence_gap` before `solution_gap` or `decision_gap` when missing facts determine feasibility or eliminate options;
   - `solution_gap` before `decision_gap` when inherited assumptions make the option set unsound;
   - `direction_gap` before `decision_gap` when the user needs to construct or understand longer-term personal paths; use `decision_gap` for a bounded choice among already-formed personal options;
   - otherwise prefer the gap whose reduction most directly enables the next meaningful action, and state the tie assumption internally.
4. Map the selected gap to one atomic skill:
   - `clarity_gap` -> `socratic-clarify`;
   - `knowledge_gap` -> `explain-two-levels` for a concept or mechanism, or `reverse-engineer` for a concrete artifact;
   - `evidence_gap` -> `fact-audit` for one or a few claims, or `deep-research` for a broad topic;
   - `solution_gap` -> `first-principles` for inherited assumptions, `cross-domain` for structural transfer, or `expert-panel` for conflicting professional models;
   - `decision_gap` -> `steelman-decision` for plausible options, or `minimum-experiment` when empirical evidence has more value than analysis;
   - `direction_gap` -> `talent-discovery` for evidence about strengths, or `life-design` for future paths.
5. Set `outcome: skill` for one selected skill. Set `outcome: chain` only when completing it is expected to reveal another blocking gap.

Prefer one skill. Add another only when completing the first is expected to reveal a second blocking gap. Three skills are exceptional; four require a high-stakes or explicitly deep task. Do not select five.

## Execute

In normal mode:

1. For `outcome: direct`, perform the requested work normally, do not load an atomic reasoning skill, and stop.
2. For `outcome: skill` or `outcome: chain`, briefly name the approach only when the workflow is complex or the method helps orient the user.
3. Read and follow the selected skill's `SKILL.md`.
4. Reassess after each skill. Stop the chain when the user can take the next meaningful action.
5. Do not fabricate a child skill's output. If it requires research, tools, source material, or user answers, obtain them under that skill's rules.

For a QN skill, the child skill owns the interview and its termination condition. After each answer, reassess whether that child skill can now terminate or whether its next question remains necessary. Return to router-level selection only when the answer materially changes the user's requested outcome or primary state; do not reroute merely because the child skill is multi-turn.

In plan-only mode, do not execute child skills. Return only:

- problem state;
- primary gaps;
- outcome: `direct`, `skill`, or `chain`;
- selected skills and order;
- why each is necessary;
- important missing inputs;
- stop condition.

For `outcome: direct`, return `selected skills: []`, explain why no reasoning skill is needed, and identify the direct action. Do not execute that action in plan-only mode.

## Output contract

- For `direct`, perform the requested work in normal mode without forcing a reasoning skill.
- For `skill` or `chain`, return the selected child skill's required output, not a substitute router summary.
- For plan-only mode, return the routing fields above and do not execute the work.
- Preserve material uncertainty and the stop condition inherited from the selected child skill.

## Boundary checks

- Do not use broad research to answer a simple explanation.
- Do not use an expert panel as decorative role-play.
- Do not choose between options before checking whether inherited assumptions made the option set false or incomplete.
- Do not continue researching after a cheap, decisive, reversible test is available without explaining the value of more evidence.
- Do not turn personal exploration into fixed personality labels or deterministic advice.

## Termination

Stop once the user can take the next meaningful action. Completeness is not a reason to extend the chain.
