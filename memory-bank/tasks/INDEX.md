# Task Index

> **Managed by:** /ingest-task skill (creates rows), agents (update status/phase)
> **Reading rule:** Read at session start to check active tasks.

| Task ID | Type | Status | Current Phase | Created | Updated | Notes |
|---------|------|--------|---------------|---------|---------|-------|
| | | | | | | |

## Status Values
- `Active` — work in progress
- `Blocked` — waiting on User or external dependency
- `Done` — all phases complete, session ended cleanly
- `Abandoned` — no longer needed

## Phase Format
`{number}-{name}` — e.g., `3-Design`, `4-Implementation`

## Management Rules

1. **/ingest-task** appends a new row with Status=Active, Phase=1-{first phase}
2. **Phase transitions:** Agent updates "Current Phase" column when moving to next phase
3. **Completion:** Agent changes Status to "Done" and records completion date in Updated
4. **Context switching:** Agent reads INDEX.md to find all Active tasks, then reads the target task's progress.md for resumption

## Context Switch Procedure

When User says "switch to {TASK-ID}":
1. Write session summary for current task's progress.md
2. Update current task's phase in INDEX.md
3. `echo "{NEW-TASK-ID}" > .current-task`
4. Read new task's task_plan.md + latest progress.md entry
5. Announce: "Switched to {TASK-ID}. Phase: {current phase}. Last session ended at: {summary}."
