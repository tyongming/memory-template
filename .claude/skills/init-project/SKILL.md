---
name: init-project
description: First-run project scanner. Scans all source repos to populate ARCHITECTURE.md, modules.md, and routing-keys.md from actual code. Run once after cloning memory-bank into a new project. Use when indexes are empty or the user says 'initialize', 'scan project', or 'bootstrap'.
---
# /init-project — First-Run Project Scanner
## Trigger
Memory-bank indexes are empty (skeleton templates only). Run ONCE to bootstrap.
## Prerequisites
1. **Ask the user which directories to scan** — could be one repo (`"."`) or multiple.
   Store their answer as `SCAN_DIRS`. All commands below loop over `$SCAN_DIRS`.
2. `.claude/` symlink working (verify: `cat .claude/settings.json`)

```bash
# Set once at the start — replace with the user's answer
SCAN_DIRS="dir1 dir2 dir3"
```

## Phase 1: Discover Modules (~5 min)
Scan for Maven modules across all directories:
```bash
# Find all pom.xml files (each = a module)
for d in $SCAN_DIRS; do find "$d" -name "pom.xml" -maxdepth 3; done | sort
# Extract module names and parent relationships
for d in $SCAN_DIRS; do
  for pom in $(find "$d" -name "pom.xml" -maxdepth 3); do
    DIR=$(dirname "$pom")
    NAME=$(basename "$DIR")
    LAYER=$(echo "$DIR" | cut -d'/' -f1)
    echo "$LAYER | $NAME | $DIR"
  done
done
```
For each module found:
1. Identify its type from the naming convention: `-data`, `-dao`, `-srv`, `-rest-itf`, `-rest-dto`, `-rest-webapp`, `-srv-webapp`
2. Identify which layer it belongs to the directories
3. Create a section in `memory-bank/indexes/modules.md`
## Phase 2: Discover RabbitMQ Topology (~5 min)
Scan for all messaging infrastructure:
```bash
for d in $SCAN_DIRS; do
  # Find all exchanges
  grep -rn "TopicExchange\|DirectExchange\|FanoutExchange\|HeadersExchange" \
    "$d"/*/src/ --include='*.java'
  # Find all @RabbitListener consumers
  grep -rn "@RabbitListener" "$d"/*/src/ --include='*.java'
  # Find all publishers (AmqpTemplate / RabbitTemplate)
  grep -rn "amqpTemplate\|rabbitTemplate\|AmqpTemplate\|RabbitTemplate" \
    "$d"/*/src/ --include='*.java' | grep -i "send\|convert"
  # Find routing key constants
  grep -rn "ROUTING_KEY\|routingKey\|routing.key" "$d"/*/src/ --include='*.java'
  # Find ConsumerConfiguration classes
  find "$d" -name "*ConsumerConfiguration*" -o -name "*AmqpConfig*"
done | head -80
```
For each exchange/routing-key found:
1. Create a section in `memory-bank/indexes/routing-keys.md`
2. Map publisher → exchange → routing key → consumer
## Phase 3: Discover Database Entities (~3 min)
```bash
for d in $SCAN_DIRS; do
  grep -rn "@Entity" "$d"/*/src/ --include='*.java'
  grep -rn "@Table" "$d"/*/src/ --include='*.java'
  grep -rn "spring.datasource\|spring.jpa" "$d"/*/src/ \
    --include='*.yaml' --include='*.yml' --include='*.properties'
done | head -80
```
## Phase 4: Discover REST Endpoints (~3 min)
```bash
for d in $SCAN_DIRS; do
  grep -rn "@RestController\|@Controller" "$d"/*/src/ --include='*.java'
  grep -rn "@FeignClient" "$d"/*/src/ --include='*.java'
  grep -rn "@RequestMapping\|@GetMapping\|@PostMapping\|@PutMapping\|@DeleteMapping" \
    "$d"/*/src/ --include='*.java'
done | head -80
```
## Phase 5: Discover Infrastructure (~2 min)
```bash
for d in $SCAN_DIRS; do
  # Find Docker/deployment configs
  find "$d" -name "Dockerfile" -o -name "docker-compose*" -o -name "*.Dockerfile"
  # Find application configs
  find "$d" -name "application*.yaml" -o -name "application*.yml" -o -name "application*.properties"
  # Find Eureka/discovery config
  grep -rn "eureka\|spring.cloud.discovery" "$d"/*/src/ \
    --include='*.yaml' --include='*.yml' --include='*.properties'
  # Find Redis config
  grep -rn "spring.redis\|spring.data.redis" "$d"/*/src/ \
    --include='*.yaml' --include='*.yml' --include='*.properties'
done | head -60
```
## Phase 6: Populate Files
With all scan results, populate:
### 1. `memory-bank/ARCHITECTURE.md`
Fill in ALL sections:
- System Identity (database type, deployment method)
- Module Topology (layer → module → dependencies diagram)
- Key Architectural Patterns (from what the scans revealed)
- Infrastructure (DB, RabbitMQ topology, Redis, Eureka)
- Build & Run (from project CLAUDE.md if documented, or discover from pom.xml/gradle)
### 2. `memory-bank/indexes/modules.md`
One `## module-{name}` section per module discovered.
Include: path, purpose, layer, key classes, dependencies, publishes/consumes, DB tables.
### 3. `memory-bank/indexes/routing-keys.md`
One `## exchange: {name}` section per exchange discovered.
Include: type, routing keys, publishers, consumers, bindings.
## Phase 7: Verify & Log
1. Count populated entries:
   ```bash
   grep -c "^## module-" memory-bank/indexes/modules.md
   grep -c "^## exchange:" memory-bank/indexes/routing-keys.md
   ```
2. Log to progress.md: modules found, exchanges found, entities found
3. Mark any sections as `[UNVERIFIED]` if the scan was ambiguous
4. Log unknowns to `.learnings/LEARNINGS.md` for future investigation
## Expected Duration
~20-30 minutes for a 30+ module project. Delegate scanning to Gemini if available to save Claude tokens.
## After Init
The indexes are now populated. Future tasks use smart reading (grep by section) instead of full scans.