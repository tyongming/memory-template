# {TASK-ID}: {Title}

> **Source:** {Jira ticket URL or "ad-hoc"}
> **Type:** {Feature | Bug | Investigation | Refactoring}
> **Created:** {YYYY-MM-DD}
> **Status:** Phase 1 — {first phase name}

## Objective

{One-paragraph description of what this task achieves. Paste or summarize from Jira.}

## Phases

{Populated by /ingest-task based on workflow type. Example for Feature:}

- [ ] 1. Plan — User stories + acceptance criteria
- [ ] 2. Analysis — Dependency tracing + feasibility
- [ ] 3. Design — Subtask breakdown + exec plan
- [ ] 4. Implementation — Code changes
- [ ] 5. Testing — API tests + regression
- [ ] 6. Review — Code review (auditor)
- [ ] 7. Documentation — Docs + index updates

## Acceptance Criteria

{Filled during Plan phase}

1. {criterion}
2. {criterion}

## Modules Affected

{Filled during Plan/Analysis. THIS IS THE SMART READING GUIDE.}

- `module-{name}` — {why it's affected}
- `module-{name}` — {why it's affected}

## RabbitMQ Flows Involved

{Filled during Analysis. THIS IS THE SMART READING GUIDE.}

- Exchange: `{exchange-name}` / Routing key: `{pattern}` — {role in this task}

## Domain Topics

{Filled during Analysis. Points to indexes/analysis/ files.}

- `analysis/{topic}.md` — {relevance}

## Blast Radius

{Filled during Analysis by @tracer or /blast-radius.}

- **Direct:** {modules directly modified}
- **Indirect:** {modules affected by message/DB changes}
- **Test scope:** {which test suites must pass}

## Subtasks

{Filled during Design phase. Smallest possible MVP increments.}

- [ ] 4.1: {subtask description}
- [ ] 4.2: {subtask description}

## Design Decisions

{Filled during Design. Brief notes on why, not just what.}

## Notes

{Anything else — constraints, open questions, links.}
