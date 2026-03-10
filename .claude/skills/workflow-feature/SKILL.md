---
name: workflow-feature
description: Initialize and guide a Feature workflow through all 7 phases (Plan, Analyze, Design, Implement, Test, Review, Document). Displays phase table, confirms current phase, guides through requirements. Use when starting a feature task or the user mentions 'feature workflow'.
---

# /workflow-feature — Feature Workflow (7 Phases)

## Trigger
After /ingest-task creates a Feature task, this skill displays the phase sequence and guides the agent.

## Phase Sequence

| # | Phase          | Gate    | Agent / Skill              | Outputs                                    |
|---|----------------|---------|----------------------------|--------------------------------------------|
| 1 | Plan           | 🔑 User | Main + /workflow-feature   | User stories, acceptance criteria in task_plan.md |
| 2 | Analysis       |         | @tracer / Explore          | findings.md populated, indexes updated     |
| 3 | Design         | 🔑 User | Main                       | Subtask breakdown in task_plan.md, exec-plan created |
| 4 | Implementation |         | Main (Builder) / Hephaestus| Source code changes, progress.md updated    |
| 5 | Testing        |         | Main + /test-api           | Test results in progress.md, regression tests run |
| 6 | Review         | 🔑 User | @auditor / Oracle          | Review notes in docs/quality/              |
| 7 | Documentation  |         | Main + /write-docs / Doc Writer | API docs, indexes, ADRs, ARCHITECTURE.md updated |

## Steps

1. Read `config/workflow-phases.md` for full phase definitions.
2. Display the Feature phase table above.
3. Confirm current phase with the user.
4. Guide agent through phase requirements:
   - What outputs are expected for the current phase
   - Which agents/skills to invoke
   - Where User review gates (🔑) are — stop and present work at these gates
5. After each phase completion, mark `[x]` in task_plan.md.

## Completion Criteria
ALL 7 phases must be marked `[x]` in task_plan.md before the Stop hook allows session end.
