# Error Log

> **Scope:** Auto-captured command failures + manually logged errors.
> **Write rule:** PostToolUse hook in settings.json auto-logs bash failures. Agents manually log other errors.
> **Promotion rule:** If same error appears 3+ times → promote to CLAUDE.md as permanent rule.

## Format

Each entry:

### {YYYY-MM-DD HH:MM} — {short title}
**Task:** {TASK-ID}
**Command:** `{command that failed}`
**Error:** `{error message}`
**Context:** {what the agent was trying to do}
**Resolution:** {how it was fixed, or "unresolved"}
**Recurrence:** {first | 2nd | 3rd+ → PROMOTE}

---

{entries appear here, newest first}
