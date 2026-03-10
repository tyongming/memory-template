# RabbitMQ Routing Map

> **Reading rule:** 📖 FLEXIBLE — Read ONLY sections for exchanges listed in task_plan.md "RabbitMQ Flows Involved".
> **Update rule:** 🔒 FORCED — Update when you discover new routing relationships.
> **Trust policy:** Trust-until-broken.

## Format Convention

Each exchange section follows this structure. Use `## exchange: {name}` as the heading for grep-based section extraction.

---

## exchange: {exchange-name}

**Type:** {topic | direct | fanout | headers}
**Durable:** {yes | no}
**Purpose:** {one-line description}

### Routing Keys

| Routing Key Pattern | Publisher Module | Consumer Module(s) | Message Type / DTO | Notes |
|--------------------|-----------------|--------------------|--------------------|-------|
| `{pattern}`        | module-{x}      | module-{y}, module-{z} | `{ClassName}` | |

### Bindings

| Queue Name | Routing Key | Consumer Module | DLQ? |
|-----------|------------|-----------------|------|
| `{queue}` | `{key}`    | module-{x}      | {yes/no → DLQ name} |

### Known Gotchas
- {gotcha — promoted from .learnings/}

---

{REPEAT FOR EACH EXCHANGE}
