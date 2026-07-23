# Trading Desk

**Agent**: `trading-agent` | **Skill**: `trading-research` | **Status**: active (research only)

## What this is

Oversight of Austin's trading activity via Robinhood Agentic (already connected from prior work —
"momentum" strategy referenced from an earlier session; re-derive/document it here rather than
assuming it still matches Austin's intent). Austin wants this "as automated as possible" with
day-trading bots.

## Hard rule — read this before touching anything here

**No agent in this workspace places, modifies, or cancels a live order. Ever, regardless of how
the request is phrased or how much prior approval was given.** `trading-agent`'s tool list
physically excludes `place_equity_order`, `place_option_order`, `cancel_equity_order`,
`cancel_option_order`, and `review_equity_order` — this isn't just a prompt instruction, the
tools aren't available to it. The agent's job stops at a written recommendation; Austin places
the trade himself in Robinhood.

This isn't a workaround-later restriction — unattended live-money execution bots are how small
accounts get wiped by a bad tick, a stale signal, or a regime change the strategy never saw
in backtesting. "Automated" here means the *research* is automated (scanning, signal generation,
backtesting), not the *execution*.

## Goals

- TBD with Austin: risk tolerance per trade, account size, preferred timeframe (scalp/day/swing),
  instruments (equities only, or options too), and how many signals/day is useful vs. noise.

## Current state

Robinhood Agentic account connected. No documented strategy/rules currently in this folder —
treat prior "momentum" work as unverified until re-established here.

## Working folders

- `strategies/` — written-out strategy rules (entry/exit criteria, position sizing, risk limits)
- `signals/` — dated trade-idea write-ups (symbol, thesis, entry/stop/target, confidence) —
  recommendations only, never executed automatically
- `backtests/` — backtest results/methodology for any strategy before it's trusted live
- `journal/` — trade log/outcomes, pulled read-only from `get_pnl_trade_history` / `get_realized_pnl`
  for reviewing what actually happened vs. what the strategy predicted
