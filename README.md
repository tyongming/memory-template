# Memory Bank — Structured AI Agent Workflow

A persistent knowledge system that gives AI coding agents long-term memory, SDLC discipline, and multi-agent collaboration. Built for **Claude Code** and **OpenCode (OmO)**.

## The Problem

AI coding agents start every session from scratch. They forget past decisions, repeat mistakes, lose context between tasks, and skip important steps. In large codebases (30+ Spring Boot modules, RabbitMQ messaging), this compounds fast.

## The Solution

A `memory-bank/` directory that acts as shared, persistent memory across sessions — combined with hooks and rules that enforce disciplined development workflows.

**What you get:**

- **Session continuity** — Agents resume exactly where they left off via `progress.md` and task plans
- **SDLC enforcement** — 4 workflow types with defined phases and human review gates
- **Compound learning** — Errors auto-captured, patterns logged, knowledge promoted to permanent memory
- **Multi-agent collaboration** — Specialized agents (tracer, auditor) with performance tracking
- **Token efficiency** — Section-level index reads instead of full-file loads

## Quick Start

```bash
# 1. Clone into your project root (or merge contents)
git clone <this-repo> && cd <this-repo>

# 2. (Optional) Install AST-Grep for dependency tracing
npm install -g @ast-grep/cli

# 3. Start your first task
/ingest-task "JIRA-123: Your task description here"
```

See [PREREQUISITES.md](PREREQUISITES.md) for the full setup guide including Windows/PowerShell steps and optional tooling.

## How It Works

```
You give a task
    ↓
/ingest-task creates task folder (plan + progress + findings)
    ↓
Workflow skill (/workflow-feature, /workflow-bug, etc.) guides phases
    ↓
Hooks enforce discipline:
  • SessionStart  → loads task context, past progress, review feedback
  • PreToolUse    → reminds agent of the current plan before edits
  • PostToolUse   → auto-logs command failures to .learnings/ERRORS.md
  • Stop          → blocks session end if progress wasn't logged
    ↓
Agents trace dependencies (@tracer) and review code (@auditor)
    ↓
Knowledge accumulates in memory-bank/ across sessions
```

## Project Structure

```
├── CLAUDE.md                     # 16 forced rules for Claude Code
├── PREREQUISITES.md              # Post-clone setup guide
│
├── .claude/                      # Claude Code configuration
│   ├── agents/                   # @tracer, @auditor definitions
│   ├── rules/                    # Behavioral rules (index, progress, review, learning)
│   ├── settings.json             # Hooks across 4 lifecycle events
│   └── skills/                   # 12 slash commands
│
├── .opencode/                    # OpenCode / OmO configuration
│   ├── agents/                   # tracer (LSP-powered), reviewer
│   ├── oh-my-opencode.jsonc      # Model routing, ultrawork, hooks
│   └── skills/                   # Skill reference
│
├── .learnings/                   # Cross-session learning capture
│   ├── ERRORS.md                 # Auto-captured command failures
│   ├── LEARNINGS.md              # Patterns, corrections, best practices
│   └── FEATURE_REQUESTS.md       # Missing workflow capabilities
│
└── memory-bank/                  # Shared persistent knowledge
    ├── AGENTS.md                 # Agent role map + cross-tool mapping
    ├── ARCHITECTURE.md           # System overview (populated by /init-project)
    ├── config/                   # Workflow phases, token budgets
    ├── indexes/                  # Module registry, RabbitMQ routing map
    ├── tasks/                    # Per-task folders + INDEX.md + templates
    ├── docs/                     # Design docs, exec plans, ADRs
    ├── reviews/                  # Agent performance tracking
    ├── tests/                    # Per-module test artifacts
    └── decisions/                # Architecture Decision Records
```

## Workflows

| Type | Phases | Use When |
|------|--------|----------|
| **Feature** | Plan → Analysis → Design → Implement → Test → Review → Docs | Building new capabilities |
| **Bug Fix** | Triage → Plan → Implement → Test → Review → Docs | Fixing broken behavior |
| **Investigation** | Observe → Trace → Diagnose → Decide | Understanding a problem (no code changes) |
| **Refactoring** | Scope → Impact → Design → Implement → Test → Review+Docs | Improving code structure |

Review gates (🔑) require human approval before proceeding.

## Agents

| Agent | Tool | Role |
|-------|------|------|
| **Main Agent** | Both | Orchestration + implementation |
| **@tracer** | Claude Code | Cross-module dependency tracing (read-only) |
| **@auditor** | Claude Code | Fresh-eyes code review (read-only) |
| **Tracer** | OpenCode | LSP-powered dependency tracing (read-only) |
| **Oracle** | OpenCode | Architecture review (read-only) |

Agent performance is tracked in `memory-bank/reviews/performance-log.md` with a 5-tier verdict scale. Issues feed back as constraints for future sessions.

## Skills

| Command | Purpose |
|---------|---------|
| `/init-project` | First-run scanner — populates indexes from actual code |
| `/ingest-task` | Create task folder from Jira ticket or description |
| `/workflow-feature` | Guide through 7-phase feature workflow |
| `/workflow-bug` | Guide through 6-phase bug fix workflow |
| `/workflow-investigation` | Guide through 4-phase investigation |
| `/workflow-refactor` | Guide through 6-phase refactoring |
| `/trace-module` | Trace module dependencies |
| `/blast-radius` | Assess change impact across modules |
| `/test-api` | Structured API testing with curl |
| `/write-docs` | Generate documentation and ADRs |
| `/research` | External research via web search |

## Design Principles

- **Evolutionary** — Indexes start as skeletons, populated by agents during real work
- **Nothing off the record** — Every action logged to `progress.md`, every error to `.learnings/`
- **Smart reading** — Agents read index sections by grep, not full files, to minimize token usage
- **Trust-until-broken** — Index entries trusted unless contradicted, then corrected and logged
- **Tool independent** — Same `memory-bank/` works with both Claude Code and OpenCode

## License

MIT
