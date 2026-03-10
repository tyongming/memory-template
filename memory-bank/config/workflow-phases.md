# Workflow Phase Definitions

> **Referenced by:** planning-with-files Stop hook (checks all phases complete),
> /workflow-* skills (display phase sequence), /ingest-task (sets initial phase)

## Feature — 7 Phases

| # | Phase          | Gate    | Agent / Skill              | Outputs                                    |
|---|----------------|---------|----------------------------|--------------------------------------------|
| 1 | Plan           | 🔑 User | Main + /workflow-feature   | User stories, acceptance criteria in task_plan.md |
| 2 | Analysis       |         | @tracer / Explore          | findings.md populated, indexes updated     |
| 3 | Design         | 🔑 User | Main                       | Subtask breakdown in task_plan.md, exec-plan created |
| 4 | Implementation |         | Main (Builder) / Hephaestus| Source code changes, progress.md updated    |
| 5 | Testing        |         | Main + /test-api           | Test results in progress.md, regression tests run |
| 6 | Review         | 🔑 User | @auditor / Oracle          | Review notes in docs/quality/              |
| 7 | Documentation  |         | Main + /write-docs / Doc Writer | API docs, indexes, ADRs, ARCHITECTURE.md updated |

**Completion criteria:** ALL 7 phases must be marked `[x]` in task_plan.md before Stop hook allows session end.

## Bug Fix — 6 Phases

| # | Phase          | Gate    | Outputs                                    |
|---|----------------|---------|---------------------------------------------|
| 1 | Triage         | 🔑 User | Root cause hypothesis in findings.md       |
| 2 | Plan           |         | Fix strategy + blast radius in task_plan.md|
| 3 | Implementation |         | Bug fix code, progress.md updated          |
| 4 | Testing        |         | Regression test confirming fix + no regressions |
| 5 | Review         | 🔑 User | Review notes                               |
| 6 | Documentation  |         | Indexes updated, ADR if architectural      |

## Investigation — 4 Phases

| # | Phase    | Gate    | Outputs                                    |
|---|----------|---------|---------------------------------------------|
| 1 | Observe  |         | Symptoms documented in findings.md         |
| 2 | Trace    |         | Dependency chain, data flow in findings.md |
| 3 | Diagnose |         | Root cause analysis in findings.md         |
| 4 | Decide   | 🔑 User | Recommendation: fix now, defer, or accept risk |

**Note:** Investigation does NOT produce code changes. Output is a decision + optional new Feature/Bug task.

## Refactoring — 6 Phases

| # | Phase           | Gate    | Outputs                                    |
|---|-----------------|---------|--------------------------------------------|
| 1 | Scope           |         | What to refactor, boundaries in task_plan.md |
| 2 | Impact Analysis | 🔑 User | Blast radius, affected modules in findings.md |
| 3 | Design          |         | Refactoring strategy, subtask breakdown    |
| 4 | Implementation  |         | Refactored code, progress.md updated       |
| 5 | Testing         |         | Full regression — refactoring must not change behavior |
| 6 | Review + Docs   | 🔑 User | Review + indexes/docs updated together     |
