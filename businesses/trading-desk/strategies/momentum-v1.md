# Momentum v1 — Daily-Swing Breakout

**Status:** Documented and backtested (2026-07-22). **Backtest verdict: weak/marginal — see
`../backtests/momentum-v1-backtest.md`. Do not treat this as validated for live signals yet.**

This supersedes the undocumented "momentum" strategy referenced from a prior session, which was
never written down and is treated as unverified/discarded. This is a fresh design, built to be
testable and falsifiable.

## Timeframe

**Daily-bar swing trading.** One clear commitment: signals are generated off daily closes, entries
execute at the next session's open, and trades are held anywhere from 1 to 15 trading days. This is
not a scalp/day-trade system (no intraday bars) and not a position-trade system (no multi-month
holds) — it sits deliberately in between so a single account can watch it once per day after the
close.

## Universe

Liquid, well-known large-cap equities and broad-market ETFs only — names where a small account can
get filled near the quoted price without moving the market. Examples used in the backtest: AAPL,
MSFT, NVDA, AMZN, GOOGL, META, TSLA, AMD, SPY, QQQ. Any candidate should have comparable liquidity
(multi-billion dollar daily dollar volume) before this strategy is applied to it.

## Entry criteria (all must be true on a daily close, checked after the close, day T)

1. **Trend filter:** `Close > SMA(50)` AND `SMA(20) > SMA(50)` — price is in an established
   intermediate uptrend, not just spiking against a downtrend.
2. **Breakout trigger:** `Close(T) > highest Close of the prior 20 trading days` (a 20-day
   closing-price Donchian breakout) — momentum is making a new short-term high, not just drifting.
3. **Volume confirmation:** `Volume(T) >= 1.5 x 20-day average volume` — the breakout is backed by
   participation, not a thin print.
4. **RSI filter:** `RSI(14)` between 50 and 75 — momentum present but not deep into blow-off/
   overbought exhaustion (RSI > 75 is skipped, not chased).
5. **Not currently in a position in that symbol** (one open trade per symbol at a time).

Entry executes at the **next session's open** (day T+1), never at day T's close — this avoids
look-ahead bias (you can't buy the close that generated the signal).

## Exit criteria (in priority order, checked from entry day forward)

1. **Stop-loss** (hard rule, always live): `max(entry_price x 0.95, low of the signal day T)` —
   i.e. -5% from entry, or the signal day's low if that's tighter (closer to entry). Whichever
   loses less money is used. This stop is placed immediately on entry and never widened.
2. **Take-profit target:** `entry_price x 1.10` (+10%, a ~2:1 reward-to-risk versus the 5% stop).
3. **Momentum-failure trailing exit:** once a trade has closed at or above +3% unrealized, if price
   subsequently closes back below `EMA(10)`, exit at the next session's open — the move has lost
   steam before hitting target.
4. **Time stop:** if neither the stop, target, nor trailing exit has triggered within 15 trading
   days of entry, close the position at that day's close. Momentum setups that go nowhere for three
   weeks are not working and tie up capital/attention.

If a single day's range would hit both the stop and the target (gap/whipsaw day), the backtest
conservatively assumes the **stop hit first** — this is a modeling assumption, not a guarantee of
real intraday sequencing.

## Position sizing — fixed % of real account equity

Position size (dollars) = **the smaller of:**
- **10% of current account equity**, and
- **1% of current account equity ÷ the trade's stop-loss %** (the risk-capped size)

Pull current equity from `get_accounts` / `get_portfolio` before sizing every trade — never invent
a number. As of 2026-07-22, the connected agentic account (798207098, "Agentic") had:
- Total account value: **$584.61**
- Cash / buying power: **$59.28**
- Existing equity positions: fractional GLDM, QQQ, SPCX, MSFT (~$525 combined)

At that equity, 10% sizing = **~$58** per position. **This account currently only has enough
buying power for roughly one position at a time** — the "max 3 concurrent positions" rule below is
aspirational until either more cash is added or existing holdings are trimmed. Flagging this
explicitly rather than pretending the sizing rule and the account's actual cash line up.

## Max risk per trade

**Hard cap: 1% of current account equity**, enforced via the position-sizing formula above (never
overridden upward regardless of how good a setup looks).

## Portfolio-level risk limits

- **Max concurrent open positions:** 3 (diversification / correlation control) — currently
  constrained by account cash, see above.
- **Max same-sector concentration:** no more than 2 of the 3 concurrent slots in the same sector
  (e.g., not 3 mega-cap tech names at once — NVDA/AMD/MSFT all reacting to the same semiconductor
  headline isn't 3 independent bets).

## What this strategy does *not* do

- No options — equities only, no leverage from derivatives.
- No earnings-date filter is backtested (no earnings calendar data was pulled for the backtest
  period) — before trading this live, cross-check `get_earnings_calendar` and skip/tighten around
  any signal with earnings inside the holding window; earnings gaps blow through the 5% stop
  routinely.
- No slippage, spread, or commission modeling — see the backtest's honest limitations section.
