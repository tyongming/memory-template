# CLAUDE.md — Project Instructions

## Project Identity

This is a Spring Boot multi-module monorepo (~30+ modules) with RabbitMQ inter-module messaging.
Your persistent knowledge lives in `memory-bank/`. Read before you act. Write after you act. Nothing happens off the record.

## Active Plugins

- **ScopeCraft MCP** — Multi-task management (fallback: memory-bank/tasks/INDEX.md)

## Self-Improving Behavior (No Plugin — Rules-Based)

There is no self-improving-agent plugin. Instead, this behavior is enforced by rules:
- Failed bash commands are auto-logged to `.learnings/ERRORS.md` by the PostToolUse hook in settings.json
- At session end, evaluate `.learnings/` capture per `.claude/rules/learning-promotion.md`
- Learnings, gotchas, and workflow gaps should be manually logged to `.learnings/LEARNINGS.md`

## 🔒 Forced Rules (Always Follow)

### Memory-Bank Discipline
1. **Read reviews/{your-name}.md** at session start. Apply known issues as constraints.
2. **Read task_plan.md** at session start and before every edit (PreToolUse hook enforces this).
3. **Read progress.md** (latest entry) at session start for cold-start resumption.
4. **Log to progress.md** after every significant action. Nothing happens off the record.
5. **Update indexes** when you discover new information about modules, routing keys, or architecture.
6. **Do NOT modify code in a module** without first reading that module's section from indexes/modules.md.
7. **Do NOT skip SDLC phases.** The Stop hook will block you if phases are incomplete.

### Smart Reading (Token Efficiency)
8. Read index files **by section, not in full**. Use grep/search to extract only sections for modules listed in task_plan.md "Modules Affected".
9. Read routing-keys.md **by exchange section** — only exchanges listed in task_plan.md "RabbitMQ Flows Involved".
10. Read analysis/{topic}.md **only if** the task touches that domain.
11. Read other agents' reviews **only if** you're delegating to them this session.

### SDLC Discipline
12. Follow the phase sequence defined in config/workflow-phases.md. Do not jump ahead.
13. At User review gates (🔑), **stop and present your work**. Do not proceed without approval.
14. Split implementation into the **smallest possible subtasks**. One subtask = one logical change.
15. After Implementation, run tests BEFORE requesting review. Do not skip Testing phase.

### Documentation Tags
16. Design docs use verification tags: `[VERIFIED]`, `[UNVERIFIED]`, `[OUTDATED]`. Update tags when you verify or invalidate information.

## 📖 Flexible Reading Guide

When you read task_plan.md, extract:
- **"Modules Affected"** → grep those module names from indexes/modules.md
- **"RabbitMQ Flows Involved"** → grep those exchange names from indexes/routing-keys.md
- **"Domain Topics"** → check if indexes/analysis/{topic}.md exists, read if relevant

## Available Skills

| Skill | Purpose |
|-------|---------|
| `/init-project` | First-run scanner: populates ARCHITECTURE.md, modules.md, routing-keys.md from code |
| `/ingest-task` | Create task folder from Jira ticket or description |
| `/trace-module` | Trace module dependencies via grep/find/ast-grep |
| `/blast-radius` | Assess impact of changes across modules |
| `/test-api` | Execute structured API tests with curl |
| `/write-docs` | Generate/update documentation and ADRs |
| `/research` | External research via web search and docs |
| `/workflow-feature` | Feature workflow: 7 phases |
| `/workflow-bug` | Bug fix workflow: 6 phases |
| `/workflow-investigation` | Investigation workflow: 4 phases |
| `/workflow-refactor` | Refactoring workflow: 6 phases |

## Available Agents

| Agent | When to Use |
|-------|------------|
| `@tracer` | Cross-module dependency tracing, RabbitMQ routing discovery, blast radius |
| `@auditor` | Code review after Implementation + Testing phases complete |

## Build & Test

```
[TO BE POPULATED after first task — exact commands for this project]
```

## Known Issues

```
[TO BE POPULATED — .learnings/ promotions land here]
```
