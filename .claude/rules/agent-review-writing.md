---
description: After delegating to any agent, the main agent evaluates and logs their performance
globs: [ "**/*" ]
---

After receiving results from a delegated agent (@tracer, @auditor, Oracle, Reviewer, Coder, Document Writer):

1. Evaluate the agent's output against these criteria:
    - **Completeness:** Did it cover everything asked?
    - **Accuracy:** Were findings correct? Any false positives/negatives?
    - **Scope:** Did it stay within bounds or scope creep?
    - **Usefulness:** Did the output actually help the task?

2. Append an entry to `memory-bank/reviews/performance-log.md`:
   ```
   ### {YYYY-MM-DD} — {agent-name} — {task-id}
   **Verdict:** {STRONG | GOOD | ADEQUATE | NEEDS IMPROVEMENT | POOR}
   **Strengths:** {what went well}
   **Issues:** {what needs improvement}
   **Action items:** {specific changes for next session}
   ```
   Verdict scale (5-tier):
    - **STRONG** — exceeded expectations, no issues
    - **GOOD** — met expectations, minor issues only
    - **ADEQUATE** — met minimum bar, notable issues
    - **NEEDS IMPROVEMENT** — fell short, significant issues
    - **POOR** — failed to deliver, fundamental problems

3. If issues were found, update or create `memory-bank/reviews/{agent-name}.md`:
   ```
   ## Known Issues (apply as constraints next session)
   - {date}: {issue description — e.g. "missed error handling in 3 files"}
   ```
    - This file is read by the agent at next session start via review-discipline.md rule.
    - **Purpose is constraints only** — list what the agent must NOT do. No strengths or positive reinforcement.

4. Update the **Scorecard** table at the top of `performance-log.md`:
    - Increment the agent's review count and verdict tally.
    - Format: `| {agent-name} | {total} | {STRONG} | {GOOD} | {ADQ} | {NI} | {POOR} |`

5. If the agent performed well with no issues, skip the individual review file update.

6. **Archival:** When performance-log.md exceeds 50 entries, move entries older than 3 months to
   `memory-bank/reviews/archive/{YYYY}.md`. Keep the Scorecard in the main file (cumulative).

Do NOT skip this step. The Stop hook checks if agent performance was logged.
