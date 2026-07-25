# Andrew Ng / DeepLearning.AI Agentic Patterns

Primary source: Agentic AI course (DeepLearning.AI) + public statements.

## Four Core Design Patterns

1. **Reflection**
   Agent examines its own output, critiques it, and improves. Self-critique loop before finalizing.

2. **Tool Use**
   LLM decides which external functions/APIs to call (search, code execution, databases, calendars, etc.). Tool choice is model-driven.

3. **Planning**
   Agent produces an explicit multi-step plan before execution, then follows/adapts it.

4. **Multi-Agent**
   Specialized agents coordinate (orchestrator or peer handoff) to solve different parts of a complex workflow.

## Critical Differentiator (Ng)
The single biggest difference between teams that succeed with agentic systems and those that struggle is a **disciplined process of evals and error analysis**.

- Build component-level and end-to-end evaluations early.
- Perform systematic error analysis on failure cases.
- Iterate on the basis of measured failure modes, not intuition.
- Prefer raw Python implementations first so the control flow is fully visible and debuggable.

## Practical Stance
- Agentic workflows improve accuracy, modularity and capability on complex tasks.
- Always measure the gain against the increase in latency, cost and failure surface.
