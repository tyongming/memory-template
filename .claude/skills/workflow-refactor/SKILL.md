---
name: workflow-refactor
description: Initialize and guide a Refactoring workflow through all 6 phases (Identify, Analyze, Plan, Refactor, Test, Document). Use when starting a refactoring task or the user mentions 'refactor workflow' or 'clean up code'.
---

# /workflow-refactor — Refactoring Workflow (6 Phases)

## Trigger
After /ingest-task creates a Refactoring task, this skill displays the phase sequence and guides the agent.

## Phase Sequence

| # | Phase           | Gate    | Outputs                                    |
|---|-----------------|---------|--------------------------------------------|
| 1 | Scope           |         | What to refactor, boundaries in task_plan.md |
| 2 | Impact Analysis | 🔑 User | Blast radius, affected modules in findings.md |
| 3 | Design          |         | Refactoring strategy, subtask breakdown    |
| 4 | Implementation  |         | Refactored code, progress.md updated       |
| 5 | Testing         |         | Full regression — refactoring must not change behavior |
| 6 | Review + Docs   | 🔑 User | Review + indexes/docs updated together     |

## Steps

1. Read `config/workflow-phases.md` for full phase definitions.
2. Display the Refactoring phase table above.
3. Confirm current phase with the user.
4. Guide agent through phase requirements:
   - Phase 1 (Scope): Define refactoring boundaries clearly
   - Phase 2 (Impact Analysis): Use /blast-radius, present to User
   - Phase 3 (Design): Break into smallest possible subtasks
   - Phase 4 (Implementation): Apply refactoring incrementally
   - Phase 5 (Testing): FULL regression — behavior must not change
   - Phase 6 (Review + Docs): @auditor reviews, then update all indexes and docs
5. After each phase completion, mark `[x]` in task_plan.md.
