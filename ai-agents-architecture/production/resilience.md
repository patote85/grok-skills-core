# Resilience Requirements

- Idempotency on every side-effect (keys + deduplication).
- Circuit breakers and bulkheads around external calls and LLM calls.
- Explicit timeouts, retries with backoff, dead-letter queues.
- Graceful degradation and failover paths.
- Max iterations / hard stopping conditions on every agent loop.
