# grok-skills-core

Versioned collection of **Grok skills** designed for building and operating AI agents that produce real production code for high-stakes financial Core systems (zero-downtime tolerance).

These skills follow a **Progressive Disclosure** architecture inspired by Anthropic’s latest context engineering guidance for Claude 5-generation models: keep the entry point lightweight, load detailed guidance only when needed, and never over-constrain the model with rules that newer models can already handle through judgment.

## Design Principles

- **Hard constraints for Core remain non-negotiable** (idempotency, circuit breakers, audit trails, least privilege, human-in-the-loop for high-risk actions).
- Everything else uses progressive disclosure to avoid context bloat and conflicting instructions.
- Skills are complementary and intentionally separated:
  - One decides **architecture and production readiness**.
  - The other disciplines **code implementation quality**.

## Skills

### 1. `ai-agents-architecture`

**Purpose**  
Architectural decision-making and production requirements for AI agents and multi-agent systems in high-stakes environments.

**When to use**  
- Designing or reviewing agentic workflows  
- Deciding whether an agent is needed vs a deterministic workflow  
- Multi-agent orchestration  
- Tool design for agents  
- Any system with side effects in financial Core

**Structure (Progressive Disclosure)**

```
ai-agents-architecture/
├── SKILL.md                    # Lightweight entry point
├── core-constraints.md         # Non-negotiable production rules
├── patterns/
│   ├── when-to-use-agent.md
│   └── shared-memory-kg.md     # Knowledge Graph as persistent shared memory
├── production/
│   ├── resilience.md
│   ├── observability-audit.md
│   └── evaluation.md
└── references/
    ├── anthropic-patterns.md
    ├── andrew-ng-patterns.md
    ├── openai-multiagent.md
    └── code-examples.md
```

**Key concepts**
- Prefer the simplest pattern that meets measured success criteria.
- Knowledge Graph as shared, persistent, provenance-carrying memory (Orchestrator-Workers + Evaluator-Optimizer).
- Explicit storage guidance for AWS (DynamoDB preferred, Aurora PostgreSQL, Neptune only when justified).
- Full production checklist for zero-downtime systems.

### 2. `karpathy-code-implementation`

**Purpose**  
Karpathy-derived discipline for writing and editing code that a senior engineer would respect without rewriting.

**When to use**  
- Producing, reviewing, refactoring or debugging actual source code  
- Feature branches, pull requests, merges  
- Implementation details

**Structure (Progressive Disclosure)**

```
karpathy-code-implementation/
├── SKILL.md                    # Lightweight entry point
├── principles.md               # Detailed principles + self-critique
├── failure-modes.md            # Kitchen Sink, Optimistic Path, etc.
└── examples/
    └── code-examples.md        # Python, Java, Go examples
```

**Core principles (condensed)**
- Read Before You Write
- Think Before You Code
- Simplicity First
- Surgical Changes
- Goal-Driven Execution + Empirical Verification

## How these skills work together

| Concern                        | Skill                          |
|--------------------------------|--------------------------------|
| Should I even use an agent?    | `ai-agents-architecture`       |
| Production constraints (Core)  | `ai-agents-architecture`       |
| Shared memory / Knowledge Graph| `ai-agents-architecture`       |
| Code quality & diffs           | `karpathy-code-implementation` |
| Self-critique before shipping  | `karpathy-code-implementation` |

When generating code for Core systems, **both skills should be active**.

## Origin & Evolution

These skills were developed iteratively with the following primary influences:

- Anthropic – Building Effective Agents + latest context engineering guidance (Claude 5)
- Andrew Ng – Agentic AI patterns + evaluation discipline
- Andrej Karpathy – observations on LLM coding failure modes
- Production requirements for financial Core systems (idempotency, circuit breakers, auditability, least privilege)

The architecture was deliberately moved from monolithic rule sets to progressive disclosure after Anthropic’s public guidance on reducing over-constraint in newer models.

## License

Private repository. For internal use and controlled sharing only.
