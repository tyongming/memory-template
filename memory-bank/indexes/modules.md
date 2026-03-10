# Module Registry

> **Reading rule:** 📖 FLEXIBLE — Read ONLY sections for modules listed in task_plan.md "Modules Affected". Do NOT read the full file.
> **Update rule:** 🔒 FORCED — Update when you discover new information about a module.
> **Trust policy:** Trust-until-broken. Entries may be stale. If something doesn't match reality, fix the index and log to .learnings/ERRORS.md.

## Format Convention

Each module section follows this structure. Use `## module-{name}` as the heading for grep-based section extraction.

---

## module-{name}

**Path:** `{relative path from project root}`
**Purpose:** {one-line description}
**Spring profiles:** {if applicable}

### Key Classes
- `{ClassName}` — {role}

### Dependencies
- **Imports from:** module-{x}, module-{y}
- **Publishes to:** exchange `{name}` with routing key `{pattern}`
- **Consumes from:** queue `{name}` bound to exchange `{name}`
- **Database tables:** `{table_name}` via `{Entity class}`
- **REST endpoints:** `{method} {path}` — {description}

### Known Gotchas
- {gotcha — promoted from .learnings/}

---

{REPEAT FOR EACH MODULE — agents add sections as they discover modules}
