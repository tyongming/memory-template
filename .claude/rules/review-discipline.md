---
description: Read own review file at session start to apply accumulated feedback
globs: ["**/*"]
---

At the start of every session:

1. Determine your agent name (used as your review filename):
   - If you were spawned with a name (e.g., "researcher", "coder", "tracer") → use that.
   - If your system prompt or tool config gives you a name (e.g., "Sisyphus") → use that.
   - Otherwise → use your model ID (e.g., "claude-opus-4-6").
2. Check if `memory-bank/reviews/{your-agent-name}.md` exists.
3. If it exists, read the **full file**. Apply the feedback as constraints on your behavior this session.
4. Known issues from past reviews should influence your approach:
   - If a past review noted you "missed error handling" → pay extra attention to error handling.
   - If a past review noted "scope creep" → stick strictly to task_plan.md subtasks.
