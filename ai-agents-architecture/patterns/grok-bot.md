# Grok Bot Runtime Pattern

Grok chat (this environment) is not Grok Bot. Do not collapse the two.

- **Grok chat** — single session, tools in this conversation, no durable cloud computer.
- **Grok Bot** (`x.ai/bot`, `@bot`) — durable teammate with a named job, memory, own cloud computer, connectors, skills, routines, and optional handoff to other Bots.

Official playbooks at `https://x.ai/bot/guides` are capability demos. They are not the default topology.

## When to use a Grok Bot

Use a Bot only when all of the following hold:

1. The work is multi-step inside real apps or connectors (browser, IDE, CRM, design tool, store consoles).
2. The job is long-lived enough to justify a named owner, memory, and an approval boundary.
3. A single Grok-chat call plus tools cannot finish the work without losing the computer session.

Otherwise stay in Grok chat or a fixed workflow.

## Escalation ladder

1. One well-prompted Grok call + retrieval + tools.
2. Fixed workflow (known steps, no dynamic routing).
3. One Grok Bot with one job and the minimum connectors.
4. Group of 2–3 Bots with named handoffs and one human owner of failure.
5. Reject larger rosters (6–10 Bots, “Chief of Staff + department”) unless quota, approval, and measured gain are explicit.

Weekly Grok Bot usage is a hard compute-allocation constraint. Design for quota, not for org-chart cosplay.

## Anatomy of one Bot

Give each Bot:

- **One primary job** in operational language (outcome owned, work refused).
- **Minimum connectors** for that job. Never “sign in to everything”.
- **One approval boundary** (send, purchase, publish, delete, production change).
- **Memory policy** — Bot memory is working context, not system of record. Operational facts that must survive go to an audited store with source, timestamp, and agent.
- **Success criteria** a human can check without reading a novel.

Do not create a Bot named General Helper. Vague jobs poison memory.

Account limits that affect design: about 50 Bots + group chats combined; 50 routines per Bot; recent routine run history is short. Treat these as capacity, not targets.

## Product skill vs project skill

A **Grok Bot skill** (product) is a reusable method the Bot follows on its computer. It must state when to use it, required inputs and access, sequence of work, how to validate, what to return, and what requires approval.

A **project skill** (this repo) is the contract this agent loads. Do not treat a taught-by-demonstration Bot skill as a project skill until a human reviews it and copies the durable rules here.

Lifecycle: one-time task → correct until reviewable → save product skill → only then routine.

## Routines

A routine says *when* a Bot runs a skill. Create a routine only after the skill is reliable. Broad event listeners are forbidden. Deleting a Bot deletes its routines; there is no undo.

## Handoffs and multi-bot

Handoff is allowed only with a named next owner and a defined artifact. Fan-out, god-Bot, studio templates before one measured win, and autonomous send/purchase/deploy are forbidden by default.

## Side effects on the cloud computer

Apply `core-constraints.md` in full. Required HITL: send, purchase, delete, publish, production change, money movement. X plugin is read-only for search. The user posts.

## Contract to emit when asked to set up Bots

```
Bot: <name>
Job: <one sentence outcome + refused work>
Connectors: <minimum list>
Skill: <name + six fields>
Routine: <none | schedule + stale-data policy>
Approval: <actions that stop>
Handoff: <none | next Bot + artifact>
Success: <checkable criterion>
```

One Bot first. Add the second only after the first meets success on real input.
