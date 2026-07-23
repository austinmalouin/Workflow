# Momentum v2 — Daily-Swing Breakout (Confirmed, Cost-Aware)

**Status:** Documented and backtested (2026-07-23). **Backtest verdict: still not graduating to
live signals — see `../backtests/momentum-v2-backtest.md`.** This revises
[`momentum-v1.md`](momentum-v1.md) (verdict: weak/marginal) by fixing the specific weaknesses its
backtest flagged. It keeps v1's core mechanic — trend filter + breakout + volume + RSI — and adds
realistic costs, an earnings blackout, a stronger breakout confirmation, and an actually-enforced
position cap.

## What changed from v1 (and why)

1. **Slippage/spread modeling** — v1 assumed perfect fills at modeled prices. v2 assumes every
   fill is worse than the signal price: entries 0.2% worse, target exits 0.1% worse, trailing/time
   exits 0.2% worse, and **stop-loss exits 0.3% worse** (stops are the fill most likely to be hit
   in a fast, gapping tape, so they get the worst assumption).
2. **Earnings blackout** — no new entry within **5 calendar days** of a known or projected
   earnings report date for that symbol (ETFs SPY/QQQ have no earnings and are exempt). See
   "Earnings data" below for how dates were sourced/estimated.
3. **Stronger breakout confirmation** — a level break on day T alone is no longer enough. Day T+1's
   close must still be at or above the level that was broken on day T before the trade is taken;
   entry then executes at T+2's open (one day later than v1's T+1 entry). This is a **closing-price**
   hold-through-one-day check, not true intraday confirmation — daily bars can't tell you whether a
   level held throughout the session or was breached and recovered by the close. Documented
   honestly as an approximation, not a claim of intraday validation.
4. **Position cap actually enforced** — a new entry is now skipped outright (not queued, not
   substituted) if 3 positions are already open across the whole 10-symbol universe when its
   entry day arrives. v1's backtest computed the equity curve without this check; v2's simulation
   engine gates every entry on `open_position_count < 3` in real time.

Everything else — trend filter, breakout definition, volume/RSI filters, stop/target/trailing/
time-stop exit logic, and position-sizing formula — is unchanged from v1. See
[`momentum-v1.md`](momentum-v1.md) for the parts not repeated here.

## Timeframe, universe

Same as v1: daily-bar swing trades, 1-15 trading day holds, entries at the next scheduled session's
open. Universe: AAPL, MSFT, NVDA, AMZN, GOOGL, META, TSLA, AMD, SPY, QQQ.

## Entry criteria

Checked on day T's close (the signal day):
1. **Trend filter:** `Close > SMA(50)` AND `SMA(20) > SMA(50)`.
2. **Breakout trigger:** `Close(T) > highest Close of the prior 20 trading days` (closing-price
   Donchian breakout) — call this level `L`.
3. **Volume confirmation:** `Volume(T) >= 1.5x 20-day average volume`.
4. **RSI filter:** `RSI(14)` between 50 and 75.
5. **Not currently in a position, and no other signal already pending confirmation/entry, in that
   symbol.**

Then, new in v2:

6. **Breakout-hold confirmation (day T+1):** `Close(T+1) >= L`. If price closes back below the
   broken level the next day, the signal is cancelled — no entry, no further tracking. If it holds,
   entry executes at **T+2's open**, with the 0.2% entry slippage applied.
7. **Earnings blackout (checked at the T+2 entry date):** skip the entry if a known or projected
   earnings date for that symbol falls within 5 calendar days of T+2, either direction. This blocks
   the *entry*, not the whole holding window — an earnings report can still land mid-hold on a
   position that was already open before the report was scheduled or became known. That risk is
   unchanged from v1 and is not eliminated here.
8. **Position cap (checked at the T+2 entry date):** skip the entry if 3 positions are already open
   across the universe. The signal is not queued or re-tried — it simply doesn't happen.

## Exit criteria (unchanged mechanic from v1, now with slippage)

Checked from the entry day forward, in priority order:
1. **Stop-loss:** `max(entry_price x 0.95, low of signal day T)`. Fill modeled 0.3% worse than the
   stop price.
2. **Take-profit target:** `entry_price x 1.10`. Fill modeled 0.1% worse than the target price.
3. **Momentum-failure trailing exit:** once closed at/above +3% unrealized, if a subsequent close
   is back below `EMA(10)`, exit at the next session's open, 0.2% worse than that open.
4. **Time stop:** 15 trading days with no other exit triggered, close at that day's close, 0.2%
   worse than the close.

Same-day stop/target ambiguity is still resolved conservatively (stop wins), same as v1 — daily
bars can't disambiguate real intraday sequencing.

## Position sizing, risk cap, portfolio limits

Unchanged from v1: size = `min(10% of current equity, 1% of current equity / stop-loss %)`, max
1% account risk per trade, max 3 concurrent positions (now actually enforced in the backtest — see
above), max 2-of-3 slots in the same sector.

**Current real account (Robinhood "Agentic," 798207098), checked 2026-07-23:** total value
**$579.59**, cash/buying power **$59.28**, existing fractional positions in GLDM, QQQ, SPCX, MSFT
(~$520 combined). Materially unchanged from the $584.61 recorded when v1 was documented. At this
equity, 10% sizing is still only ~$58/position, and the account still doesn't have free cash for
more than roughly one new position at a time — the 3-concurrent-position cap remains aspirational
for this account's actual buying power regardless of what the backtest says about the rule.

## Earnings data — real dates vs. a documented assumption

`get_earnings_results` returns only the trailing/upcoming ~8 quarters per symbol — real, verified
report dates from roughly 2025-01 onward for this universe. That covers the last ~1.5 years of the
5.5-year backtest window. For 2021-2024 (the other ~4 years), no historical earnings-date tool
was available, so blackout dates were **back-projected from each symbol's earliest known real date
in ~91.25-day (one quarter) steps**. This is an approximation: real report dates drift by days-to-
weeks quarter to quarter and this projection doesn't capture that drift. Treat the pre-2025 portion
of the earnings blackout as a reasonable estimate, not verified fact — see the backtest's honest
limitations section for how much this could be off.

## What this strategy still does not do

- No options, no leverage from derivatives.
- No true intraday breakout confirmation — the T+1 hold-through check is a closing-price proxy,
  not an intraday one (see point 3 above).
- No blackout coverage for earnings announced *during* an open trade's hold — only entries are
  screened.
- No commission modeling (Robinhood equities are commission-free; likely immaterial, same as v1).
