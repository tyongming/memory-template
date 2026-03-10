---
description: Enforce smart reading of indexes before code modification
globs: ["**/*.java", "**/*.xml", "**/*.yaml", "**/*.yml", "**/*.properties", "**/*.gradle", "**/*.kt"]
---

Before modifying any tracked source file:

1. Identify which module this file belongs to.
2. Check if you have already read that module's section from `indexes/modules.md` THIS SESSION.
3. If NOT → read that section now using grep: `grep -A 50 "## module-{name}" memory-bank/indexes/modules.md`
4. If the task involves RabbitMQ for this module → also read the relevant exchange section from `indexes/routing-keys.md`.
5. Only proceed with the edit after relevant index sections are loaded.

When you discover information not in the index:
- Update the index immediately after your current action.
- Log the discovery to findings.md.

Do NOT read the full index files. Read by section using the module name or exchange name as the grep target.
