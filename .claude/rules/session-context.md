When the user asks a question about the current task, active APIs, or anything covered in the SessionStart hook output:

1. Answer from the hook-provided context FIRST.
2. Do NOT launch agents, explore the codebase, or re-read task files.
3. Only explore if the hook context genuinely lacks the needed detail.