# Token Budget & Model Routing

> **Referenced by:** Agents when choosing models for delegation, User when evaluating costs.

## Claude Code Token Strategy

| Component              | Model       | Estimated Tokens | Notes                           |
|------------------------|-------------|------------------|---------------------------------|
| Main Agent             | Opus 4.6    | Full context     | Worth it — complex reasoning    |
| @tracer agent          | Opus 4.6    | Isolated context | Deep tracing needs strong model |
| @auditor agent         | Sonnet 4.5  | Isolated context | Review doesn't need Opus        |
| Agent Teams teammates  | Sonnet 4.5  | Isolated context | Exploration is parallelizable   |
| Skills (on-demand)     | Main context| ~200-500 each    | Loaded only when invoked        |
| Hooks (per edit cycle) | N/A         | ~150-200         | Fixed overhead, unavoidable     |
| Smart reading (forced) | N/A         | ~1,000-1,300     | Session start cost              |
| Smart reading (flexible)| N/A        | ~500-2,000       | Depends on task scope           |

**Monitor:** Run `/context` once per session. If total overhead exceeds 10k tokens, check which indexes have grown too large and consider splitting.

## OpenCode Token Strategy

| Component              | Model       | Notes                            |
|------------------------|-------------|----------------------------------|
| Orchestration (Sisyphus)| Claude Opus | Worth it for complex reasoning   |
| Explore agents         | Gemini 3.1  | Fast, cheap codebase exploration |
| Oracle (review)        | Codex 5.3   | Good for architecture reasoning  |
| Librarian (research)   | Gemini/GPT  | Save Claude tokens               |
| Document Writer        | Gemini/GPT  | Documentation doesn't need Opus  |
| Hephaestus (coding)    | Claude      | Implementation needs strong model |

**Advantage:** OmO model routing automatically sends cheap tasks to cheap models.

## Cost Targets

| Metric                        | Target        |
|-------------------------------|---------------|
| Monthly subscription cost     | $0-40         |
| Average tokens per session    | < 50k         |
| Hook overhead per session     | < 4k tokens   |
| Forced reading per session    | < 1,500 tokens|
| Skills loaded per session     | 2-4 average   |

## When to Upgrade Model

- If agent consistently produces incorrect analysis → upgrade from Sonnet to Opus
- If Gemini Explore agents miss dependencies → switch to Claude for that agent
- If token budget exceeded → check if indexes need splitting, not model downgrade
