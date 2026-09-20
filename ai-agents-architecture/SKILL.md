---
name: ai-agents-architecture
description: Enforce architectural and production best practices for AI agents and multi-agent systems in high-stakes environments. Decide whether an agent is needed, choose the simplest viable pattern, and enforce non-negotiable Core constraints (idempotency, circuit breakers, audit, least privilege). Use when designing or reviewing Grok Bot teammates, product skills, routines, templates, or multi-bot handoffs. Use when deciding guidance vs full security audit — load Cloudflare security-audit-skill, do not fork it. Use progressive disclosure for detailed patterns and production guidance. Do not use for pure code-quality or diff-level implementation rules.
---

# AI Agents Architecture

Apply these principles when designing, reviewing or operating agentic systems. Prefer measured simplicity. Complexity is the enemy of reliability.

## Core Decision Framework

1. **Is an agent actually required?**
   - Prefer a single well-prompted LLM call + retrieval + tools.
   - Use predefined workflows (fixed control flow) whenever steps are known in advance.
   - Escalate to dynamic agents only when the sequence cannot be predetermined and environment feedback is available.
   - Escalate to a Grok Bot only when the job needs a durable owner, a cloud computer, and connectors that a single Grok-chat call cannot hold. See `patterns/grok-bot.md`.
   - Measure the gain. Reject the agent if latency, cost, quota or failure surface increases without clear improvement.

2. **Simplicity is non-negotiable**
   - Prefer explicit loops, clear state and visible routing over opaque orchestrators.
   - Minimum viable pattern that meets the measured success criteria.

3. **Transparency of planning**
   - Intermediate reasoning and plans must be inspectable and logged.
   - Never bury critical decisions in opaque chain-of-thought.

## Non-negotiable Core Constraints

See `core-constraints.md`. These rules are hard requirements for any agent that can cause side effects in financial Core systems. They are not optional guidance.

## Progressive Disclosure

Load only what the current task requires:

- **Patterns & when to use agents** → `patterns/`
- **Grok Bot runtime (teammate, computer, skills, routines)** → `patterns/grok-bot.md`
- **Security audit routing (Cloudflare skill, do not fork)** → `patterns/security-audit.md`
- **Bend laws gate (not a default runtime)** → `patterns/bend-laws.md`
- **Shared persistent memory (Knowledge Graph base)** → `patterns/shared-memory-kg.md`
- **Resilience, observability, evaluation** → `production/`
- **Code examples** → `references/code-examples.md`

Detailed Anthropic, Ng and OpenAI pattern references remain in `references/`.

## Operational Posture

When in doubt, simplify.  
Long-running agents are compute allocation decisions — justify the cost.  
Plans that humans do not actually read are useless. Prefer short, structured, diffable plans with explicit success criteria.
