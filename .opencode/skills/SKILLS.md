# OmO Skills — Memory Bank Operations

All skills follow the same logic as Claude Code equivalents but use OmO's tool ecosystem (LSP, AST-Grep, Tmux) instead of bash-only alternatives.

## Skill: /init-project

**Difference from Claude Code:** Delegates module discovery scans to Explore agent (parallel execution via ultrawork). LSP `workspace_symbols` supplements grep-based scans for more precise module mapping. Librarian agent handles infrastructure config discovery (Eureka, Redis, datasources). Main agent assembles results into ARCHITECTURE.md, modules.md, and routing-keys.md.

Same 7-phase structure as Claude Code version. See `.claude/skills/init-project/SKILL.md` for full phase details.

## Skill: /ingest-task

Same as Claude Code version. Identical behavior — creates task folder, three files, registers in INDEX.md.

## Skill: /trace-module

**Difference from Claude Code:** Uses LSP tools (goto_definition, find_references) IN ADDITION to grep/AST-Grep. LSP gives structured, precise results.

Steps:
1. Use LSP `document_symbols` to map the module's public API
2. Use LSP `find_references` to find all callers across the monorepo
3. Use AST-Grep for annotation patterns (@RabbitListener, @Entity, @Table)
4. Use grep for config-file patterns (routing-key, spring.datasource)
5. Update indexes with findings

## Skill: /blast-radius

Same as Claude Code. Uses /trace-module results + one level deeper tracing.

## Skill: /test-api

**Difference from Claude Code:** Uses Tmux terminal integration for curl execution. Can keep test sessions running in background and check results asynchronously.

## Skill: /write-docs

**Difference from Claude Code:** Delegates to Document Writer agent for heavy documentation tasks. Main agent handles index updates.

## Skill: /research

**Difference from Claude Code:** Delegates to Librarian agent, which has native access to context7 MCP (library docs) and web search. Richer than Claude Code's web-search-only approach.

## Skill: /workflow-*

Same as Claude Code. Reads workflow-phases.md, displays phase sequence, guides through phases.
