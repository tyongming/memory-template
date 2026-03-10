---
name: trace-module
description: Trace cross-module dependencies for a specific Spring Boot module. Scans imports, RabbitMQ connections, shared entities, and REST endpoints using grep/ast-grep. Updates indexes. Use when analyzing module dependencies, preparing blast radius, or the user mentions 'trace' or 'dependencies'.
---

# /trace-module — Module Dependency Tracing

## Trigger
User or agent needs to trace dependencies for a specific module.

## Input
Module name (e.g., `module-auth`)

## Steps

1. **Find module path:**
   ```bash
   find . -type d -name "{module-name}" | head -5
   ```

2. **Scan for cross-module imports:**
   ```bash
   grep -rn "import.*{other-module-package}" {module-path}/src/ --include='*.java'
   ```

3. **Scan for RabbitMQ connections:**
   ```bash
   ast-grep --pattern '@RabbitListener($$$)' --lang java {module-path}/
   grep -rn 'rabbitTemplate\|RabbitTemplate' {module-path}/src/ --include='*.java'
   grep -rn 'routingKey\|routing-key' {module-path}/src/ --include='*.java' --include='*.yaml' --include='*.yml'
   ```

4. **Scan for shared entities:**
   ```bash
   ast-grep --pattern '@Table($$$)' --lang java {module-path}/
   ast-grep --pattern '@Entity' --lang java {module-path}/
   ```

5. **Scan for REST endpoints and clients:**
   ```bash
   grep -rn '@RequestMapping\|@GetMapping\|@PostMapping\|@PutMapping\|@DeleteMapping' {module-path}/src/ --include='*.java'
   grep -rn 'FeignClient\|RestTemplate\|WebClient' {module-path}/src/ --include='*.java'
   ```

6. **Update indexes:**
   - Append/update the module's section in `indexes/modules.md`
   - Append/update exchange sections in `indexes/routing-keys.md`
   - Log to findings.md

7. **Report** structured findings to user.
