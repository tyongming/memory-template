# {TASK-ID}: Findings

> **Update rule:** Write to this file after every 2 search/read operations during Analysis.
> **Reading rule:** On-demand — read when you need context from earlier exploration.

## Dependencies Discovered

{Each entry: what was found, where, and why it matters.}

### Module Dependencies
| Source Module | Depends On | Type | Discovery Method |
|--------------|-----------|------|-----------------|
| | | import / RabbitMQ / shared-DB / REST | grep / LSP / ast-grep |

### RabbitMQ Routing
| Exchange | Routing Key | Publisher | Consumer(s) | Pattern |
|----------|------------|-----------|-------------|---------|
| | | | | topic / direct / fanout |

### Shared Entities / DTOs
| Class | Used By Modules | Table/Collection |
|-------|----------------|-----------------|
| | | |

## Root Cause Analysis

{For Bug/Investigation workflows. Filled during Triage/Diagnose.}

- **Symptom:**
- **Hypothesis:**
- **Evidence:**
- **Confirmed root cause:**

## Key Discoveries

{Anything surprising or undocumented that was found during exploration.}

- {discovery} — Found in {file:line} via {method}

## Questions / Unknowns

{Things that couldn't be resolved during Analysis. May need User's input.}

- [ ] {question}

## Index Update Proposals

{Discoveries that should be promoted to indexes. Reviewed at session end.}

- [ ] modules.md: {proposed addition}
- [ ] routing-keys.md: {proposed addition}
- [ ] analysis/{topic}.md: {create new / update existing}
