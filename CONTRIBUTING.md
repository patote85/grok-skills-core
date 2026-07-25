# Contributing to grok-skills-core

Thank you for considering contributing to this repository!

This project contains Grok skills focused on high-stakes AI agents (financial Core systems). Contributions are welcome, but they must follow a controlled process to maintain the quality and rigor of the skills.

## How to contribute

### 1. Open an Issue first
Before starting any work, open an **Issue** describing:
- What you want to add or improve
- Why it is useful
- Which skill (or both) will be impacted

This avoids duplicated work and allows prior alignment.

### 2. Fork the repository
Click **Fork** in the top-right corner of the repository page.

### 3. Create a branch from `main`
```bash
git clone https://github.com/YOUR-USERNAME/grok-skills-core.git
cd grok-skills-core
git checkout -b feature/your-contribution-name
```

### 4. Make your changes
- Respect the **Progressive Disclosure** architecture (keep `SKILL.md` files lightweight).
- Any change to Core constraints (`core-constraints.md`) must be extremely well justified.
- Follow the existing writing style (direct, technical, and without fluff).
- If adding code examples, keep the pattern: code in en-US + comments in pt-BR.

### 5. Open a Pull Request
- Submit the PR to the `main` branch of the original repository.
- Fill in the PR template (if any) or clearly describe what was changed and why.
- Reference the corresponding Issue (e.g., `Closes #12`).

### 6. Mandatory Code Review
- **No merge into `main` happens without a code review from the maintainer** (`@patote85`).
- Respond to review comments and make the necessary adjustments.
- After approval, the maintainer will perform the merge.

## What is NOT welcome
- Changes that weaken production constraints (idempotency, circuit breakers, audit trail, least privilege, etc.).
- Adding unnecessary complexity or speculative abstractions.
- Oversized PRs without prior discussion in an Issue.

## Questions?
Open an Issue with the `question` tag or mention `@patote85`.

Thank you for helping keep this repository rigorous and useful!
