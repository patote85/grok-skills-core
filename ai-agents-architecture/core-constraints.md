# Core Constraints (Non-negotiable)

These rules apply to every agent that can cause side effects in financial Core systems. Violation is not allowed.

## Side-effect Safety
- **Idempotency** on all write/actions (idempotency keys + deduplication).
- **Circuit breakers** and bulkheads around external calls.
- **Explicit timeouts**, retries with backoff, and dead-letter handling.
- **Graceful degradation / failover** paths when the LLM or tools fail.

## Observability & Audit
- Structured logs of every planning step, tool call, input/output and decision.
- **Audit trail** sufficient for regulatory review.
- Provenance on every fact written to shared memory (source, timestamp, agent).

## Access & Control
- **Least privilege**: tools and credentials scoped to the minimum required.
- **Human-in-the-loop** checkpoints for high-risk or high-value actions (money movement, irreversible state changes, external side effects).
- Max iterations / hard stopping conditions on every agent loop.

## Schema & Memory
- Schema versioning for any persistent shared memory (Knowledge Graph).
- Entities extracted under different schema versions must be distinguishable.
- Writes to shared memory must be concurrent-safe and idempotent.

Never deploy an agent that can spend money, move data, or change system state without the above.
