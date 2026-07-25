---
name: karpathy-code-implementation
description: Enforce Karpathy-derived discipline for writing and editing code. Prioritize minimal diffs, simplicity, surgical changes, read-before-write, goal-driven verification and empirical checks. Use progressive disclosure for detailed principles, failure modes and language-specific examples. Use whenever producing, reviewing, refactoring or debugging actual source code. Do not use for high-level agent architecture decisions.
---

# Karpathy Code Implementation

**Hierarchy**
1. Code quality is non-negotiable.
2. Communication clarity is secondary and must never compromise technical rigor.

Produce code that a senior engineer would respect without rewriting.

## Core Principles (condensed)

- **Read Before You Write** — Read the real files, patterns, imports and tests before changing anything.
- **Think Before You Code** — State assumptions and tradeoffs. Ask when unclear. Do not fill gaps with plausible code.
- **Simplicity First** — Minimum code that solves the stated problem. No speculative abstraction or future-proofing.
- **Surgical Changes** — Smallest possible diff. Touch only what the request requires. Match existing style.
- **Goal-Driven + Verify** — Define success criteria first. Prefer empirical verification (tests, diffs, types) over model opinion. Self-critique before presenting.

## Progressive Disclosure

- Detailed principles and self-critique checklist → `principles.md`
- Common failure modes → `failure-modes.md`
- Language-specific examples → `examples/` (or `references/code-examples.md`)

## Posture

When editing existing code the diff must be justifiable line by line.  
Prefer verification over confidence.  
If a simpler approach exists, say so.
