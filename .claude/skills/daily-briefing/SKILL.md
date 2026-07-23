---
name: daily-briefing
description: Cross-business morning rollup across all of Austin's Business HQ ventures - status, pending approvals, and a trading snapshot. Use when Austin asks for a daily/morning briefing, "what's going on across my businesses", or a status check that spans more than one venture.
---

# Daily Briefing

Produce a short rollup covering all of `businesses/`. This is a status check, not deep work —
delegate to `overseer` for anything requiring judgment calls about priority.

## Steps

1. Read `HQ.md` for the current venture list and status column.
2. For each business folder, read `BUSINESS.md` — note anything changed since last time (new
   goals set, open questions answered, status flipped from onboarding to active).
3. List everything currently in `approvals/queue/` — flag anything that's been sitting more than
   a few days unreviewed.
4. If the trading desk is active, pull a read-only snapshot: `get_portfolio` and
   `get_equity_positions` via the trading-agent's tools (or delegate to `trading-agent` directly)
   — do not place any orders, this is a status read only.
5. Note anything blocked purely on Austin (unanswered open questions in a `BUSINESS.md`) —
   surface these clearly since no agent can make progress past them.

## Output format

One line per business (status + what changed + next concrete step), an approvals-pending count,
a one-line trading snapshot (positions/P&L, no recommendations here — that's `trading-research`'s
job), and anything blocked on Austin's input. Keep it scannable — this should be readable in
under a minute.
