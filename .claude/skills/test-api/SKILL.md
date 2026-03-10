---
name: test-api
description: Execute structured API tests with curl against task acceptance criteria. Logs results to progress.md. Checks downstream RabbitMQ effects. Use during Testing phase or when the user asks to test endpoints, validate API, or run integration tests.
---

# /test-api — Structured API Testing

## Trigger
Testing phase of any workflow, or user requests API validation.

## Steps

1. Read task_plan.md acceptance criteria to determine what to test.
2. For each endpoint to test, execute:
   ```bash
   curl -s -w "\n%{http_code}" -X {METHOD} {URL} \
     -H "Content-Type: application/json" \
     -d '{body}' 2>&1
   ```
3. Log each test to progress.md:
   ```
   - {HH:MM} — API Test: {METHOD} {path}
     - Expected: {status code, response shape}
     - Actual: {status code, response body snippet}
     - Result: ✅ PASS / ❌ FAIL — {reason}
   ```
4. If RabbitMQ is involved, check downstream effects:
   - Wait appropriate time for async processing
   - Verify downstream state (DB, other API endpoints)
5. Run regression tests from `memory-bank/tests/{module}/` if they exist.
6. Summary: X passed, Y failed, Z skipped.
