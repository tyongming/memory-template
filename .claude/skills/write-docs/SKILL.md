---
name: write-docs
description: Generate or update documentation after task completion. Updates indexes, ARCHITECTURE.md, design docs, and creates ADRs. Use during Documentation phase or when the user asks to update docs, write ADR, or document changes.
---

# /write-docs — Documentation Generation

## Trigger
Documentation phase of any workflow.

## Steps

1. Read task_plan.md and progress.md to understand what was built.
2. Update these files as applicable:
   - `indexes/modules.md` — any new module info discovered during implementation
   - `indexes/routing-keys.md` — any new RabbitMQ routing
   - `ARCHITECTURE.md` — if architectural patterns changed
   - `docs/design-docs/` — create or update design doc with [VERIFIED] tag
   - `decisions/ADR-{NNN}.md` — if architectural decisions were made
3. Move exec-plan from `docs/exec-plans/active/` to `docs/exec-plans/completed/`
4. ADR template:
   ```
   # ADR-{NNN}: {Title}
   **Date:** {YYYY-MM-DD}
   **Status:** Accepted
   **Context:** {why the decision was needed}
   **Decision:** {what was decided}
   **Consequences:** {trade-offs and implications}
   ```
