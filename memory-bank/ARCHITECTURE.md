# ARCHITECTURE.md — System Overview

> **Reading rule:** Read at the start of any new feature or investigation task.
> **Update rule:** Update when architectural changes occur (new modules, new exchanges, infrastructure changes).

## System Identity

- **Type:** Spring Boot monorepo (multi-module Gradle/Maven)
- **Modules:** ~30+ (see indexes/modules.md for full registry)
- **Messaging:** RabbitMQ for inter-module async communication
- **Database:** [TO BE DISCOVERED — update after first task]
- **Deployment:** [TO BE DISCOVERED]

## Module Topology

```
[TO BE POPULATED]
Agents will fill this in as they discover the module dependency graph.
Format: module-name → depends on [list] → publishes to [exchanges] → consumes from [queues]
```

## Key Architectural Patterns

```
[TO BE POPULATED]
Examples of what goes here:
- "All modules use Spring Data JPA with Hibernate"
- "RabbitMQ uses topic exchanges with routing key convention: {domain}.{event}.{version}"
- "Authentication is handled by module-auth issuing JWT tokens verified by Spring Security filters"
- "All REST APIs follow /api/v1/{resource} convention"
```

## Infrastructure

```
[TO BE POPULATED]
- Database(s): type, connection patterns
- Message broker: RabbitMQ topology (exchanges, queues, bindings)
- Cache: Redis/other
- External services: APIs, third-party integrations
```

## Build & Run

```
[TO BE POPULATED]
- Build command:
- Run command:
- Test command:
- Required services for local dev:
```

## Known Constraints & Gotchas

```
[TO BE POPULATED — .learnings/ promotions land here]
```
