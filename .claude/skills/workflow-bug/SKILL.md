---
name: workflow-bug
description: Initialize and guide a Bug Fix workflow through all 6 phases (Triage, Reproduce, Fix, Test, Review, Document). Use when starting a bug fix task or the user mentions 'bug workflow' or 'fix a bug'.
---

# /workflow-bug — Bug Fix Workflow (6 Phases)

## Trigger
After /ingest-task creates a Bug task, this skill displays the phase sequence and guides the agent.

## Phase Sequence

| # | Phase          | Gate    | Outputs                                    |
|---|----------------|---------|---------------------------------------------|
| 1 | Triage         | 🔑 User | Root cause hypothesis in findings.md       |
| 2 | Plan           |         | Fix strategy + blast radius in task_plan.md|
| 3 | Implementation |         | Bug fix code, progress.md updated          |
| 4 | Testing        |         | Regression test confirming fix + no regressions |
| 5 | Review         | 🔑 User | Review notes                               |
| 6 | Documentation  |         | Indexes updated, ADR if architectural      |

## Steps

1. Read `config/workflow-phases.md` for full phase definitions.
2. Display the Bug Fix phase table above.
3. Confirm current phase with the user.
4. Guide agent through phase requirements:
   - Phase 1 (Triage): Reproduce the bug, identify root cause, document in findings.md
   - Phase 2 (Plan): Define fix strategy, assess blast radius
   - Phase 3 (Implementation): Apply the fix
   - Phase 4 (Testing): Write regression test, run existing tests
   - Phase 5 (Review): @auditor reviews at User gate
   - Phase 6 (Documentation): Update indexes, write ADR if needed
5. After each phase completion, mark `[x]` in task_plan.md.
