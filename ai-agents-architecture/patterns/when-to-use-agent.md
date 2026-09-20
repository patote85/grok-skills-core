# When to Use an Agent

Prefer the simplest pattern that meets measured success criteria.

**Use a workflow (fixed control flow)** when:
- The sequence of steps is known in advance.
- Deterministic routing or validation is sufficient.
- Latency and cost must stay minimal.

**Escalate to a dynamic agent** only when:
- The sequence of steps cannot be predetermined.
- The agent needs to react to environment feedback (tool results, external state).
- Multi-hop reasoning or exploration across tools is required.

**Reject multi-agent** when a single well-prompted LLM call + tools solves the problem.

**Escalate to a Grok Bot** only as a third step, after a fixed workflow and a single dynamic agent in Grok chat are insufficient:

- The job needs a durable named owner, memory, and a cloud computer inside real apps.
- Connectors and session state cannot live in one Grok-chat turn.
- A routine is justified only after a reviewed product skill exists.

**Reject large Grok Bot rosters** (studio / department templates with many specialists) unless quota, approval boundaries, and a measured win from one Bot are already explicit. Official SpaceXAI guides are examples, not the default topology. Details → `grok-bot.md`.

**TypeSafe** — not an agent loop. Load `typesafe-ai` + `patterns/typesafe.md` when a step is a typed Choice/Noul/Score. Code keeps control; uncertain cases HITL. Docs: https://docs.typesafe.ai/llms.txt. Never commit `TYPESAFE_API_KEY`.

**Bend / leis executáveis** — not a default runtime. Load `patterns/bend-laws.md` only for a concrete pure-core invariant job. Evidence from `crud-api-bend`: contract parity yes, production TPS no. Do not generate the hot path of a financial service in Bend because an agent can emit it.

**Security review** — do not invent a local audit methodology. Guidance by default. Load `cloudflare/security-audit-skill` for attack classes and the six-phase workflow. Full audit only on an explicit audit/pen-test/report request plus a named target. Missing OS sandbox → `needs_validation`, do not run target code. Routing → `security-audit.md`.

Always measure: if the agent increases latency, cost, quota or failure surface without clear accuracy/reliability gain, discard it.
