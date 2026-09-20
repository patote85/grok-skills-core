# TypeSafe — typed judgments, not a second agent runtime

Installed skill: `.grok/skills/typesafe-ai/` (MIT, `npx skills add typesafe-ai/skills --skill typesafe-ai`).
Source of truth: https://docs.typesafe.ai/llms.txt  
Do not fork cookbooks into this pack.
Do not commit API keys. Host env: `TYPESAFE_API_KEY` in a 0600 file outside git.

## Default

Code owns the workflow. TypeSafe (Jev / System One) supplies **narrow typed judgments**: Choice, Noul, Score + probabilities.

Not a replacement for:
- `karpathy-code-implementation` (diffs)
- Bend `LAWS`/`PROOF` (invariants executáveis)
- Grok Bot (durable teammate)
- o CRUD Python/SAM no hot path

## When to load `typesafe-ai`

A feature needs programmable common sense that ordinary code cannot parse: route, rank, extract, verify, escalate. Prompt-and-parse of an LLM can become a structured decision.

Financial Core: judgment **never** moves money. Thresholds + HITL (`core-constraints.md`). Credentials server-side. Validate on the institution's data; cookbook numbers are examples.

## Compose

One coherent question per primitive. Independent questions over the same state in one request. Keep inferred state distinct from observed facts.
