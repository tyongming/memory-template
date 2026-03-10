---
name: blast-radius
description: Assess change impact across Spring Boot modules. Runs trace-module then traces one level deeper to find indirect dependents. Categorizes into Direct, Indirect, and Test scope. Use when planning changes, evaluating risk, or the user asks 'what will this affect' or 'impact analysis'.
---

# /blast-radius — Change Impact Assessment

## Trigger
User or agent needs to understand the impact of changing a specific module or class.

## Steps

1. Run /trace-module for the target module.
2. For each dependency found, trace ONE level deeper (direct dependents of dependents).
3. Categorize:
   - **Direct:** Modules where code changes are needed
   - **Indirect:** Modules affected via RabbitMQ message changes, shared DB schema changes, or DTO changes
   - **Test scope:** Test suites that must pass (based on direct + indirect modules)
4. Update task_plan.md "Blast Radius" section.
