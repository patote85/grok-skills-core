# Shared Persistent Memory (Knowledge Graph base)

Architectural base for shared, persistent, provenance-carrying memory across agents. This is infrastructure for memory, not a complete production system.

## Role in patterns
- **Orchestrator–Workers**: shared memory. Workers read relevant subgraphs and write new entities/relations. Orchestrator context stays small.
- **Evaluator–Optimizer**: grounding layer. Evaluator fact-checks claims against edges that carry explicit provenance.
- **Persistent world model**: survives context flushes and process restarts. Multi-session agents resume from the graph.

## Core requirements
- Every node and edge must carry provenance (source, timestamp, extraction context).
- Writes must be idempotent. Concurrent writes require explicit concurrency control.
- Schema must be versioned.
- The graph is append-mostly. Destructive updates are high-risk and need human gate + audit.
- LLM calls for extraction/resolution/summarization sit behind circuit breakers, timeouts and bulkheads.
- Least privilege and encryption for sensitive financial entities.

## Storage options (AWS)
- **DynamoDB**: preferred for most Core cases (conditional writes for idempotency, PITR, encryption at rest).
- **Aurora PostgreSQL**: strong when the team already runs Postgres (entities / relations / aliases tables + recursive CTEs).
- **Amazon Neptune**: only when multi-hop volume justifies native graph engine cost.
- **Redis / ElastiCache**: hot read cache only. Never source of truth.
- NetworkX or any in-memory graph is forbidden in production paths.

## Operational discipline
- Maintain gold set + evaluation harness (precision/recall).
- Cap extraction volume per run.
- Sample random nodes daily and verify against sources.
- Prefer incremental updates: resolve new entities against existing canonical set, add only new edges.
