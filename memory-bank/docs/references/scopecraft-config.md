# ScopeCraft MCP Configuration

## If ScopeCraft MCP is available:

Add to Claude Code MCP settings:
```json
{
  "mcpServers": {
    "scopecraft": {
      "command": "npx",
      "args": ["-y", "scopecraft-mcp"],
      "env": {
        "SCOPECRAFT_ROOT": "./memory-bank/tasks"
      }
    }
  }
}
```

Available commands:
- `task_create` — Create new task with type and phases
- `task_update` — Update task status, phase, or metadata
- `task_list` — List tasks with filters (active, type, phase)
- `phase_list` — Show phases for current task

## Fallback: INDEX.md

If ScopeCraft is not installed, use `memory-bank/tasks/INDEX.md`:

```markdown
# Task Index

| Task ID | Type | Status | Current Phase | Created | Updated |
|---------|------|--------|---------------|---------|---------|
| FEAT-20260301-example | Feature | Active | 3-Design | 2026-03-01 | 2026-03-01 |
```

Management rules:
- /ingest-task appends rows
- Phase updates: agent edits "Current Phase" column
- Completion: agent changes Status to "Done"
- Context switching: agent reads INDEX.md to find active tasks
