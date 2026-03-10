# AGENTS.md — Agent Role Map

> **Reading rule:** Read this file at the start of any session involving delegation or multi-agent work.
> **Update rule:** Update when a new agent is added or an agent's role changes significantly.

## Claude Code Agents

### Main Agent (You)
- **Model:** Opus 4.6
- **Role:** Orchestration + Implementation (Builder)
- **Context:** Full codebase + memory-bank + all skills
- **Writes to:** All memory-bank files, source code
- **Phases:** Plan, Design, Implementation, Testing, Documentation
- **Skills available:** /ingest-task, /trace-module, /blast-radius, /test-api, /write-docs, /research, /workflow-*

### @tracer
- **Model:** Opus 4.6
- **Role:** Deep cross-module dependency tracing
- **Context:** Isolated — sees only what it reads (no implementation noise)
- **Tools:** Read, Grep, Glob, Bash (read-only: grep, find, ripgrep, ast-grep)
- **No Write/Edit access**
- **Writes to:** findings.md (via Main agent relay), proposes index updates
- **Phases:** Analysis
- **When to use:** Cross-module dependency chains, RabbitMQ routing discovery, shared DTO identification, blast radius assessment
- **Trigger patterns:** `@RabbitListener`, `@Exchange`, `@Table`, cross-module imports, shared entity classes

### @auditor
- **Model:** Sonnet 4.5
- **Role:** Fresh-eyes code review
- **Context:** Isolated — deliberately blind to implementation reasoning
- **Tools:** Read, Grep, Glob (no Write, no Edit, no Bash)
- **Writes to:** docs/quality/ (via Main agent relay)
- **Phases:** Review
- **Review checklist:**
  1. Does the code match what task_plan.md specified?
  2. Error handling — are failures caught and logged?
  3. RabbitMQ — are messages acknowledged correctly? Dead-letter handling?
  4. Spring Boot — are transactions scoped correctly? Entity lifecycle?
  5. Security — authentication checks, input validation?
  6. Are there files changed that aren't in the blast radius?

---

## OpenCode Agents (OmO Built-In)

### Sisyphus (Orchestrator)
- **Role:** Delegates to built-in agents, manages conversation flow
- **Equivalent to:** Main Agent in Claude Code

### Explore (×3, parallel via ultrawork)
- **Role:** Codebase exploration using LSP + AST-Grep
- **Equivalent to:** Agent Teams in Claude Code (but with native LSP advantage)

### Tracer (Custom Explore Variant)
- **Role:** Deep dependency tracing with LSP tools
- **Config:** `.opencode/agents/tracer.jsonc`
- **Equivalent to:** @tracer in Claude Code (but with native LSP)

### Oracle
- **Role:** Architecture review, read-only advisory
- **Equivalent to:** @auditor in Claude Code

### Librarian
- **Role:** External research via context7 + web search
- **Equivalent to:** /research skill in Claude Code

### Hephaestus / Coder
- **Role:** Code implementation with full write access
- **Equivalent to:** Main Agent (Builder role) in Claude Code

### Document Writer
- **Role:** Documentation generation with full write access
- **Equivalent to:** /write-docs skill in Claude Code

---

## Cross-Tool Role Mapping

| Phase        | Claude Code              | OpenCode                |
|--------------|--------------------------|-------------------------|
| Plan         | Main Agent + /workflow-* | Sisyphus                |
| Analysis     | @tracer + Agent Teams    | Explore×3 + Tracer      |
| Design       | Main Agent               | Sisyphus + Oracle       |
| Implement    | Main Agent (Builder)     | Hephaestus              |
| Testing      | Main Agent + /test-api   | Sisyphus + Tmux         |
| Review       | @auditor                 | Oracle                  |
| Documentation| Main Agent + /write-docs | Document Writer         |
| Research     | Main Agent + /research   | Librarian               |
