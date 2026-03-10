---
description: Guide for promoting learnings from .learnings/ to permanent memory
globs: ["**/*"]
---

At session end, evaluate if any discoveries should be captured:

## Tier 1 → Tier 2 (.learnings/)

**Location:** `.learnings/`. There are exactly 3 category files:

- `.learnings/ERRORS.md` — auto-populated by PostToolUse hook; also log manually
- `.learnings/LEARNINGS.md` — corrections, knowledge gaps, patterns, best practices
- `.learnings/FEATURE_REQUESTS.md` — missing workflow capabilities

**IMPORTANT:** Always **append** entries to the existing category files above. NEVER create individual files (e.g.,
`2026-03-03-my-learning.md`). One file per category, not one file per learning.

Capture to category files when:

- A bash command fails (the PostToolUse hook auto-logs to ERRORS.md)
- You discover something that contradicts what's in the indexes (→ append to LEARNINGS.md)
- You identify a missing capability in the workflow (→ append to FEATURE_REQUESTS.md)
- You notice a pattern that could save time in future tasks (→ append to LEARNINGS.md)

**Note:** There is no self-improving-agent plugin. You are responsible for logging learnings manually to the category
files. The only automated capture is the error logger hook.

## Tier 2 → Tier 3 (Permanent Memory)

**Propose** promotion (do not auto-promote) when:
- A learning applies broadly across tasks (not just this one)
- An error has recurred 3+ times (check ERRORS.md for recurrence count)
- A pattern has proven useful across 2+ tasks

Promotion targets — see `.learnings/LEARNINGS.md` header for the full target map.what

Format your proposal:
```
**Promote:** {learning summary}
**From:** .learnings/{file}
**To:** {target file and section}
**Reason:** {why it's broadly applicable}
```

User will approve or defer.
