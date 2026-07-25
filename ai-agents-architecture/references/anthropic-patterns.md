# Anthropic Building Effective Agents — Core Patterns (Primary Reference)

Source: Anthropic Engineering, "Building effective agents" (Dec 2024). Most consolidated production experience available.

## Definitions
- **Workflows**: LLMs + tools orchestrated through predefined code paths. Predictable, consistent.
- **Agents**: LLMs dynamically direct their own processes and tool usage. Higher flexibility, higher cost/latency/risk of compounding errors.
- **Augmented LLM**: LLM + retrieval + tools + memory.

## When to Use What
- Start with optimized single LLM call (prompt + retrieval + examples).
- Use workflows for well-defined, predictable tasks.
- Use agents only for open-ended problems where steps cannot be predetermined and environment feedback is available.
- Add complexity only when measurement proves it improves outcomes.

## The Five Patterns (increasing complexity)

### 1. Prompt Chaining
Decompose into fixed sequence of LLM calls. Programmatic gates between steps.
Use when: task decomposes cleanly into subtasks; trade latency for accuracy.

### 2. Routing
Classify input → route to specialized prompt/tool/model.
Use when: distinct categories of input exist and classification is reliable.

### 3. Parallelization
- Sectioning: independent subtasks run concurrently, then aggregate.
- Voting: same task multiple times, majority or threshold.
Use when: speed or higher confidence needed.

### 4. Orchestrator-Workers
Central LLM breaks task dynamically, delegates to workers, synthesizes.
Use when: subtasks are unpredictable in number or nature (e.g., multi-file coding).

### 5. Evaluator-Optimizer
Generator produces → Evaluator critiques → loop until criteria met.
Use when: clear evaluation criteria exist and iterative refinement adds value.

## Core Principles
1. **Simplicity** — Prefer simple composable patterns. Complex frameworks often hide the real control flow.
2. **Transparency** — Explicitly surface the agent's planning steps.
3. **Agent-Computer Interface (ACI)** — Tool definitions and docstrings are part of the prompt. Engineer them with the same rigor as system prompts. Prefer formats easy for the model to generate (avoid heavy escaping or complex diffs).

## Tool Engineering Notes
- Documentation quality of tools is first-class prompt engineering.
- Test tools thoroughly; bad tool interfaces destroy agent reliability.
- Prefer natural, low-overhead formats.
