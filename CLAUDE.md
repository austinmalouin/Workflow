# Business HQ

This directory is Austin's multi-business agent workspace ("Business HQ"). It hosts several
independent ventures, each with its own folder under `businesses/`, plus a shared roster of
subagents (`.claude/agents/`) and skills (`.claude/skills/`) that operate them.

Start at [HQ.md](HQ.md) for the navigation dashboard.

## How the "agents" actually work (read this before assuming otherwise)

The files in `.claude/agents/*.md` and `.claude/skills/*/SKILL.md` do **not** register as
dispatchable subagents or skills in this environment — confirmed 2026-07-23, this was a wrong
assumption when this workspace was built. Only a fixed catalog tied to installed plugins shows up
in the `Agent`/`Skill` tools; project-local files aren't picked up, restart or not.

In practice: when Austin asks for "the etsy-agent" or similar, the assistant reads that file as a
**playbook** and does the work directly in the main conversation — same browser access, same
constraints, same output, just not an isolated subagent process. This works fine for everything
except one thing worth knowing: any tool-list restriction written into an agent file (e.g.
`trading-agent` deliberately not listing order-placement tools) is **not actually enforced**,
because that file's tool list never gets applied to a real sandboxed session. The thing that
actually holds the line on trading is the assistant's own standing rule to never execute a trade —
see hard constraint 1 below, which is real regardless of this limitation.

## Operating model: parallel rooms

Austin asks questions per-business ("rooms"), often several in quick succession. Don't serialize
them: dispatch each room's work as an independent background task and keep reading his next
message, so an answer about trading doesn't block a question about Minecraft. One exception —
Etsy and Shopify work both drive his single real Chrome session, so those two serialize against
*each other* (tab-freeze risk, learned 2026-07-23) while running freely in parallel with
everything else.

## Operating model: draft-and-recommend

Every agent here researches, plans, drafts, and prepares — humans approve anything that leaves
the building or touches money. Concretely:

- Content (listings, posts, videos, emails) gets drafted into a business's `inbox/` folder or as
  a Gmail draft, never posted/sent directly.
- Trade ideas get written to `businesses/trading-desk/signals/` as a recommendation, never
  auto-executed. Live order placement is a human action in Robinhood, full stop — no agent in
  this workspace has that tool.
- Anything requiring real money, new accounts, or public posting goes through
  `approvals/` (see [approvals/README.md](approvals/README.md)) or gets asked about directly.

## Standing rule: sync the Bridge at the end of every substantive session

The HQ dashboard is a published Artifact ("The Bridge", source: `hq-brain.html` at the workspace
root, URL: https://claude.ai/code/artifact/fe9b1927-a3ab-4b04-ba2e-c2781ca4a8b9 — always update
in place, never mint a new URL). It cannot update itself, so any session that materially changes
a business's state (new backtest, new draft, a decision made, a blocker cleared) **must end by
syncing the Bridge before wrapping up**, without Austin having to ask:

1. Update that venture's entry in `hq-brain.html` — gauges, mission log, the "awaiting
   authorization" question (it should always reflect the *current* open decision, never one
   already answered), and the console-command quick actions (the concrete next steps).
2. Update the Overseer's cross-business log/priorities if the change is significant.
3. Republish via the Artifact tool to the same URL.
4. Keep `BUSINESS.md` and the Bridge telling the same story — BUSINESS.md remains the source of
   truth; the Bridge is its dashboard view.

The point: when Austin opens the Bridge, the forged prompts should always ask the next *new*
question, not re-ask one a prior session already resolved.

## Hard constraints (do not relax these when adding agents/skills)

1. No agent places live trades, transfers funds, or executes purchases. Ever.
2. No agent sends external email, DMs, or publishes public content without an explicit go-ahead
   in that specific conversation.
3. New integrations (YouTube, Discord, Shopify, Etsy APIs, etc.) get connected by Austin via his
   connector settings — agents can prep the work but not the OAuth handshake.
4. Every business folder's `BUSINESS.md` is the source of truth for that venture's goals/state —
   keep it current instead of letting context drift into chat history.

## Layout

```
HQ.md                        <- dashboard / navigation
businesses/<venture>/         <- one folder per business, BUSINESS.md + working subfolders
approvals/                    <- pending-action queue for anything needing a human yes
.claude/agents/                <- subagent definitions (who does what)
.claude/skills/                <- reusable workflows the agents (and you) invoke
```
