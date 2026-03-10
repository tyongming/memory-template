# Project Learnings

> **Scope:** Cross-task, cross-session knowledge. Persists indefinitely.
> **Write rule:** Add entries when you discover corrections, knowledge gaps, or best practices.
> **Promotion rule:** Agent proposes promotion to permanent memory (indexes, CLAUDE.md, skills). User approves.

## Format

Each entry:

### {YYYY-MM-DD} — {short title}
**Task:** {TASK-ID or "general"}
**Category:** {correction | knowledge-gap | best-practice | pattern}
**Detail:** {what was learned}
**Promotion target:** {modules.md section X | routing-keys.md | CLAUDE.md Build section | new skill | none yet}
**Promoted:** {yes — date | no}

## Promotion Target Reference

| Learning Type                  | Promote To                          | Example                                           |
|-------------------------------|-------------------------------------|----------------------------------------------------|
| Module-specific gotcha        | modules.md → that module's section  | "module-auth token refresh has 5s race condition"  |
| RabbitMQ routing discovery    | routing-keys.md → that exchange     | "order.created also goes to notification service"  |
| Cross-module dependency       | modules.md → both modules' sections | "module-gateway imports DTOs from module-auth"     |
| Build/test environment issue  | CLAUDE.md → Build section           | "Redis must be running for gateway integration tests" |
| Tool usage pattern            | Agent .md prompt                    | "ast-grep pattern for @RabbitListener: ..."        |
| Same error 3+ times           | CLAUDE.md → Known Issues            | "Always check Spring profile before running tests" |
| Recurring workflow pattern    | New skill or skill enhancement      | "Extraction of /trace-redis-keys skill"            |
| Architectural constraint      | ARCHITECTURE.md                     | "All REST APIs must go through module-gateway"     |
| Decision with broad impact    | decisions/ADR-{NNN}.md              | "Chose eventual consistency over distributed tx"   |

---

{entries appear here, newest first}
