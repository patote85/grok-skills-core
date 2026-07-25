# OpenAI Practical Guide — Multi-Agent & Guardrails Summary

Source: OpenAI "A Practical Guide to Building Agents".

## Multi-Agent Patterns

1. **Manager (Agents-as-Tools)**
   Central manager agent calls specialized agents as tools. Manager retains control of user interaction and final synthesis.
   Preferred when a single coherent experience is required.

2. **Decentralized (Handoffs)**
   Agents are peers. One agent hands off execution (and often conversation ownership) to another specialized agent.
   Preferred for triage / routing scenarios where specialization takes over completely.

Model multi-agent systems as graphs: nodes = agents, edges = tool calls or handoffs.

## Tool Design Categories
- Data tools (retrieve context)
- Action tools (mutate external state)
- Orchestration tools (call other agents)

Rate tools by risk (low/medium/high) based on reversibility, permissions and blast radius. High-risk tools require human approval or strong guardrails.

## Guardrails (Layered)
- Relevance / safety classifiers
- PII filters
- Tool-level risk gates
- Output validation
- Rules-based (blocklists, length limits)
- Human-in-the-loop escalation on high-risk actions or repeated failures

Optimistic execution + concurrent guardrail checks is common. Fail closed on critical violations.
