# Security Audit — when to load Cloudflare

Do not fork `cloudflare/security-audit-skill`. That repo is the methodology. This file is only the routing rule.

Source of truth: `https://github.com/cloudflare/security-audit-skill`  
Skill path: `skills/security-audit/SKILL.md`  
Not the same as `cloudflare/skills` (Workers / platform build).

## Default

**Guidance mode.** Answer the security question. Do not run six phases, do not create `~/security-audit-skill/...`, do not write REPORT.md.

Load from Cloudflare only the companion file that matches the surface (web/auth, AI/LLM, cloud, supply chain, isolation, etc.).

## Full audit

Use Cloudflare's complete workflow only when the user explicitly asks to audit, pen-test, or produce report artifacts **and** names a target repo.

Then follow their contract, not a local paraphrase:

- Parent owns shared files; hunters/verifiers are isolated.
- Hunter that found a candidate must not be the verifier.
- `confirmed` needs a trust-boundary failure, source trace, and bounded result.
- No sandbox (no external net, allowlisted env, scratch-only writes, resource limits) → `needs_validation`, never execute target code.
- No live/prod probe, no paid quota burn, no availability test against shared processes.
- Profiles: `quick` / `standard` / `deep`. Budget is agent-invocation count. One run is not coverage.

In this Grok chat, assume sandbox and isolated sub-agents are missing unless proven otherwise. Full audit here degrades to guidance + a validation plan.

## Fixes after a finding

A confirmed finding does not authorize a drive-by refactor. Patch under `karpathy-code-implementation`: read the real files, smallest diff, verify.

## Do not add to this skill pack

Attack-class prompts, JSON schema, and Node validators stay upstream. Copying them here guarantees drift.
