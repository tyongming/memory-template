---
name: ingest-task
description: "Create a task folder from a Jira ticket or verbal description. Determines workflow type, generates TASK-ID, creates three-file structure, registers in ScopeCraft MCP or INDEX.md. Use when starting any new task, receiving a Jira ticket, or the user says 'new task' or 'ingest'."
---

# /ingest-task — Task Ingestion

## Trigger
User provides a Jira ticket ID + description, or describes a task verbally.

## Steps

1. **Determine workflow type** from the description:
   - New capability → Feature (7 phases)
   - Something broken → Bug (6 phases)
   - Understanding needed → Investigation (4 phases)
   - Code improvement → Refactoring (6 phases)

2. **Determine TASK-ID:**
   - From Jira ticket → `{JIRA-ID}-{short-slug}`

3. **Create task folder:**
   ```bash
   mkdir -p memory-bank/tasks/{TASK-ID}
   ```

4. **Create three files** from templates (see config for templates):
   - `task_plan.md` — pre-fill phases based on workflow type, paste Jira description into Objective
   - `findings.md` — empty template
   - `progress.md` — first entry: "Task created from {source}"

5. **Register task in ScopeCraft** (primary registry):
   ```
   mcp__scopecraft__task_create:
     title: "{TASK-ID}: {short description}"
     type: feature|bug|chore|spike
     status: in_progress
     priority: high|medium|low
     area: {primary module, e.g. "lott-eai"}
     tags: ["{Jira ticket}", "{domain keywords}"]
     location: current
   ```
   - One task per Jira ticket. No subtasks — SDLC phases live in task_plan.md.
   - If ScopeCraft unavailable: fall back to appending row to `memory-bank/tasks/INDEX.md`.

6. **Set current task:**
   - **Primary:** ScopeCraft tracks it via `status: in_progress` — SessionStart hook queries ScopeCraft for the active task.
   - **Fallback:** `echo "{TASK-ID}" > .current-task` (used when ScopeCraft is disabled)

7. **Announce:** "Task {TASK-ID} created as {type}. Starting Phase 1: {phase name}."
