# Mean-Reversion v1 — Pullback-in-Uptrend (RSI2)

**Status:** Documented and backtested (2026-07-23). **Backtest verdict: promising risk profile,
still not sound enough for live signals — see `../backtests/meanreversion-v1-backtest.md`.**

This is a deliberately different mechanic from [`momentum-v1.md`](momentum-v1.md) /
[`momentum-v2.md`](momentum-v2.md), not a third revision of the same one. Both momentum versions
buy *strength* (a new closing high, chasing continuation) and both showed a 57% stop-out rate —
most breakout signals were false starts that reversed. This strategy instead buys *weakness within
strength*: a sharp short-term pullback inside an established long-term uptrend, betting on
reversion back toward the recent average rather than continuation to new highs. Loosely based on
the "Connors RSI2" family of published mean-reversion systems.

## Timeframe

Daily-bar swing trades, but shorter-lived than the momentum versions: designed to resolve in a
handful of sessions (the backtest shows almost all trades exit within 10 trading days, most
sooner), not the 1-15 day range momentum used.

## Universe

Same liquidity bar as the momentum strategies, but a smaller set for this initial test: **SPY,
QQQ, AAPL, MSFT, NVDA** — 3 mega-cap tech names plus the two broad index ETFs. Smaller than
momentum's 10-symbol universe on purpose to keep the first test tractable; see the backtest's
limitations on what a 5-symbol, tech-heavy universe does to the position cap.

## Entry criteria (checked on daily close, day T)

1. **Long-term uptrend filter:** `Close(T) > SMA(200)` — only buy dips in names that are, in the
   big picture, still going up. This is a much longer/slower filter than momentum's SMA(50)/SMA(20)
   pair.
2. **Short-term oversold trigger:** `RSI(2) < 10` — a 2-period RSI is deliberately twitchy; it
   demands a sharp 1-2 day drop, not a gentle drift down. This is the entry signal itself, the
   opposite of momentum's "new closing high" trigger.
3. **Not currently in a position in that symbol.**
4. **Position cap:** skip if 3 positions are already open across the universe (same hard-gated cap
   as momentum v2).

Entry executes at the **next session's open (T+1)**, slippage 0.2% worse than that open — same
assumption as momentum v2, no reason to assume better fills just because the mechanic changed.

## Exit criteria (checked from entry day forward, in priority order)

1. **Stop-loss (hard, intraday):** `entry_price x 0.94` (-6%, wider than momentum's -5% — mean-
   reversion trades need more room to be wrong before the read is invalidated, since the entry
   itself is a bet that a falling price stops falling, and it can keep falling before it doesn't).
   Checked against the day's **low**, not just the close, so a stop can trigger intraday same as a
   real resting order would. Fill modeled 0.3% worse than the stop price.
2. **Mean-reversion target:** `Close(T) > SMA(5)` — the pullback is considered "reverted" once
   price closes back above its own 5-day average. This is a much shallower target than momentum's
   fixed +10%; it's designed to bank the bounce, not ride a new trend. Exit executes at the next
   session's open, 0.2% worse than that open.
3. **Time stop:** 10 trading days with neither the stop nor the target triggered, exit at that
   day's close, 0.2% worse than the close. (In the backtest this never actually fired — every trade
   resolved via stop or target well inside 10 days.)

Same-day stop/target ambiguity: not really applicable here the way it was for momentum (the stop
is an intraday low-touch check, the target is a closing-price check evaluated after the stop check
each day, so a day that would touch both resolves stop-first by construction of the sequencing,
same conservative bias as the momentum backtests).

## Position sizing, risk cap

Identical formula to momentum v1/v2: `min(10% of current equity, 1% of current equity / stop-loss
%)`. At a 6% stop, the risk-capped size is 1%/6% ≈ 16.7%, so the 10%-of-equity cap binds — every
trade sizes at 10% of equity, same as momentum's typical binding case.

**Current real account (Robinhood "Agentic," 798207098), checked 2026-07-23:** total value
$579.59, cash $59.28. Same constraint as both momentum versions: 10% sizing is roughly $58/trade,
and the account cannot actually fund 3 concurrent positions right now.

## What this strategy does *not* do

- No options, no leverage.
- No earnings blackout modeled yet (unlike momentum v2) — a name gapping down hard into earnings
  could trigger the RSI2<10 entry trigger for exactly the wrong reason (a fundamental repricing,
  not short-term noise) and this version doesn't screen for that. Flagged as a real gap before any
  live use, not just a backtest footnote.
- No sector-concentration limit — the 5-symbol universe here is itself concentrated (4 of 5 names
  are large-cap tech / tech-heavy index funds), so the "no more than 2-of-3 same sector" rule from
  momentum isn't meaningfully enforceable on a universe this narrow.
- Only tested on 5 symbols instead of momentum's 10 — see the backtest for what a larger, more
  sector-diverse universe would likely do to trade frequency and the position cap.
