---
name: workflow-investigation
description: Initialize and guide an Investigation workflow through all 4 phases (Scope, Explore, Synthesize, Report). Use when starting an investigation task, researching unknowns, or the user mentions 'investigation workflow' or 'explore this'.
---

# /workflow-investigation — Investigation Workflow (4 Phases)

## Trigger
After /ingest-task creates an Investigation task, this skill displays the phase sequence and guides the agent.

## Phase Sequence

| # | Phase    | Gate    | Outputs                                    |
|---|----------|---------|---------------------------------------------|
| 1 | Observe  |         | Symptoms documented in findings.md         |
| 2 | Trace    |         | Dependency chain, data flow in findings.md |
| 3 | Diagnose |         | Root cause analysis in findings.md         |
| 4 | Decide   | 🔑 User | Recommendation: fix now, defer, or accept risk |

## Steps

1. Read `config/workflow-phases.md` for full phase definitions.
2. Display the Investigation phase table above.
3. Confirm current phase with the user.
4. Guide agent through phase requirements:
   - Phase 1 (Observe): Document symptoms, gather evidence
   - Phase 2 (Trace): Use @tracer or /trace-module to follow dependency chains
   - Phase 3 (Diagnose): Analyze findings, determine root cause
   - Phase 4 (Decide): Present recommendation to User — fix now, defer, or accept risk
5. After each phase completion, mark `[x]` in task_plan.md.

## Important
Investigation does NOT produce code changes. Output is a decision + optional new Feature/Bug task.
