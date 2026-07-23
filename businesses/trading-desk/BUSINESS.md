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

Robinhood Agentic account connected (798207098, "Agentic"; total value $579.59, cash $59.28 as of
2026-07-23). Two documented/backtested strategy versions on file, both still short of the bar for
live signals:

- `strategies/momentum-v1.md` / `backtests/momentum-v1-backtest.md` — 100 trades, 38% win rate,
  ~1.2%/yr compounded, no slippage/earnings/cap modeling. Verdict: weak/marginal.
- `strategies/momentum-v2.md` / `backtests/momentum-v2-backtest.md` — same core mechanic, adds
  slippage, an earnings blackout, a stronger breakout-hold confirmation, and an actually-enforced
  3-position cap. 63 trades, 42.9% win rate, ~0.45%/yr compounded (lower than v1 — the added
  realism removed more return than it added). Verdict: still not sound for live signals.

No live signals have been generated from either version. Next step, if pursued, would need a
different edge or filter set rather than another round of cost-realism fixes on this same
mechanic — see each backtest's "what would need to change" / limitations sections.

## Working folders

- `strategies/` — written-out strategy rules (entry/exit criteria, position sizing, risk limits)
- `signals/` — dated trade-idea write-ups (symbol, thesis, entry/stop/target, confidence) —
  recommendations only, never executed automatically
- `backtests/` — backtest results/methodology for any strategy before it's trusted live
- `journal/` — trade log/outcomes, pulled read-only from `get_pnl_trade_history` / `get_realized_pnl`
  for reviewing what actually happened vs. what the strategy predicted
