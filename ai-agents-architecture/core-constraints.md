# Core Constraints (Non-negotiable)

These rules apply to every agent that can cause side effects in financial Core systems. Violation is not allowed.

Also apply, on every decision in this project (not only agent deploy):

- **Resource cost** — session tokens plus create-and-run cost of the chosen infra. Reject the heavier pattern when a cheaper one meets the measured bar.
- **Living agent-friendly** — source of truth outside chat, proof in the artifact, constraints in CI. Update maps and skills when models change; do not freeze a year-old checklist or add slop docs.

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
- On Grok Bot, connectors and logins are per Bot. Do not share a god-account across jobs.
- **Human-in-the-loop** checkpoints for high-risk or high-value actions (money movement, irreversible state changes, external side effects).
- On Grok Bot this includes send, purchase, delete, publish, production change, and any spend via Link. Drafts may be prepared; the human posts and pays.
- Max iterations / hard stopping conditions on every agent loop.
- Weekly Grok Bot quota is a stopping condition. Do not add Bots or routines that cannot fit measured usage.

## Schema & Memory
- Schema versioning for any persistent shared memory (Knowledge Graph).
- Entities extracted under different schema versions must be distinguishable.
- Writes to shared memory must be concurrent-safe and idempotent.
- Grok Bot memory is working context, not source of truth. Operational facts require provenance (source, timestamp, agent) in the audited store.

Never deploy an agent that can spend money, move data, or change system state without the above.
