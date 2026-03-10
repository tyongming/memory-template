---
description: Enforce append-only progress logging after every significant action
globs: ["**/*"]
---

After every significant action (file creation, code change, test execution, discovery, decision):

1. Append an entry to `memory-bank/tasks/{current-task}/progress.md`.
2. Entry format:
   ```
   - {HH:MM} — {action description}
     - Files changed: `{path}`
     - Result: {outcome}
   ```
3. **Task-related only.** Only log actions that advance the task: code changes, analysis, test results, design decisions, phase transitions. Do NOT log agents performance reviews, learnings, or workflow meta-actions — those have their own destinations defined by other rules.
4. At session end, write a Session Summary with "Next step:" for the next session's cold-start.
5. **Session header must include start and end times** for time tracking:
   ```
   ## {YYYY-MM-DD} — Session {N} ({title})
   **Start:** {HH:MM} | **End:** {HH:MM}
   ```
   Ask user for start time at session start if not obvious. Record end time when writing session summary.

Progress.md is append-only. Never delete or modify previous entries.
