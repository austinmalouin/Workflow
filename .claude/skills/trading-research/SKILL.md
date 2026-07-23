---
name: trading-research
description: Market research workflow for businesses/trading-desk/ - scans, technical/fundamental analysis, backtesting, and trade-idea write-ups via Robinhood read-only data. Never places, modifies, or cancels orders - that tool does not exist in this workflow. Use for anything about generating or reviewing trade signals.
---

# Trading Research

Workflow for `businesses/trading-desk/`. This produces recommendations only — order placement is
a human action in Robinhood, always. There is no step in this skill that ends in an executed
trade.

## Before generating any new signal

Read every file in `strategies/` — a signal should trace back to a documented, backtested
strategy, not an ad-hoc pattern that looked good today. If no strategy is documented yet, that's
the actual first task: write one down (entry/exit criteria, position sizing rule, risk limit per
trade, timeframe) before producing signals from it.

## Backtesting a strategy

1. Pull historical data (`get_equity_historicals` / `get_option_historicals`) covering enough
   history and market regimes to mean something — a strategy that only worked in one bull run
   isn't validated.
2. Apply the strategy's rules mechanically against the historical data; compute win rate, average
   win/loss, max drawdown, and sample size.
3. Write results to `backtests/<strategy-slug>-<date>.md` including the caveats (data limitations,
   look-ahead bias risk, transaction costs/slippage not modeled, etc.) — don't present a clean
   number without the honest asterisks.
4. A strategy only graduates to producing live signals once its backtest is documented and
   Austin's seen it — don't skip straight to signals from an unvalidated idea.

## Scanning for candidates

Use `get_scanner_filter_specs` to see available filters, `create_scan`/`run_scan` to find
candidates matching the strategy's entry criteria systematically, rather than manually picking
tickers.

## Writing a signal

`signals/YYYY-MM-DD-<symbol>.md`:
- **Thesis**: why this setup, tied to the documented strategy
- **Entry / stop / target**: specific levels
- **Position size**: as a % of account (pull real account value via `get_accounts`/`get_portfolio`
  — never invent a dollar figure)
- **Confidence**: honest, not inflated
- **Invalidation**: what would prove this wrong
- Explicit line: "Recommendation only — place manually in Robinhood if you agree."

## Reviewing past signals

Periodically compare `journal/` entries (pulled from `get_pnl_trade_history`/`get_realized_pnl`)
against what the signal predicted. If a strategy is consistently underperforming its backtest,
say so and stop issuing new signals from it until it's revisited.
