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

Always measure: if the agent increases latency, cost or failure surface without clear accuracy/reliability gain, discard it.
