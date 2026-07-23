# Backtest: Momentum v1 (Daily-Swing Breakout)

**Date run:** 2026-07-22 **Strategy doc:** `../strategies/momentum-v1.md`

## Verdict up front

**Weak / marginal. Not graduating to live signals on this backtest.** Raw per-trade expectancy is
technically positive, but the win rate is low (38%), the compounded equity growth over 5+ years is
close to negligible once realistic position sizing is applied, and none of slippage, spread,
commissions-on-stops, or earnings-gap risk are modeled — all of which would erode, not help, a
result this thin. Per the trading-research skill's own rule, a strategy only produces live signals
once its backtest is documented *and looks genuinely sound* — this one doesn't clear that bar yet.
No scan was run for live candidates as a result (see step 3 of the task this was produced for).

## Methodology

- **Universe:** AAPL, MSFT, NVDA, AMZN, GOOGL, META, TSLA, AMD, SPY, QQQ — 10 liquid large-cap
  names and index ETFs.
- **Period:** 2021-01-04 through 2026-07-21 (~5.5 years, 1,393 daily bars per symbol). This spans
  the 2021 bull run, the 2022 rate-hike bear market, the 2023-2024 recovery/bull, and 2025-2026 —
  a full cycle, not a cherry-picked bull stretch.
- **Data source:** `get_equity_historicals`, daily bars, split-adjusted (not dividend-adjusted;
  immaterial at a 1-15 day holding period).
- **Execution:** Rules from `momentum-v1.md` applied mechanically bar-by-bar in a script (indicators
  computed from data through day T only — no look-ahead in the signal; entry always at day T+1's
  actual open). One open trade per symbol at a time; a new signal in a symbol is ignored while a
  prior trade in that same symbol is still open.
- **Ambiguity rule:** on any day where both the stop and target would be touched (day's low ≤ stop
  and day's high ≥ target), the stop is assumed to trigger first. This is a conservative modeling
  choice, not a fact about real intraday order flow — see limitations.
- **Position sizing in the equity curve:** each trade sized at `min(10% of equity, 1% risk / stop%)`
  per the strategy's own rule, applied to a single hypothetical account, trades compounded in
  chronological order of entry date across all 10 symbols combined (start value 100).

## Results

**Sample size: 100 closed trades** across the 10 symbols, 2021-04 through 2026-06.

| Symbol | Trades |
|---|---|
| AAPL | 10 |
| AMD | 10 |
| AMZN | 16 |
| GOOGL | 14 |
| META | 10 |
| MSFT | 13 |
| NVDA | 14 |
| QQQ | 3 |
| SPY | 3 |
| TSLA | 7 |

QQQ and SPY have too few trades (3 each) to trust individually — the index-ETF leg of the universe
is essentially unvalidated on its own; the aggregate result leans on the single-stock trades.

**Win rate: 38% (38 wins / 62 losses)**
**Average win: +6.17%** | **Average loss: -2.74%**
**Raw per-trade expectancy: ≈ +0.65%** (0.38 x 6.17 − 0.62 x 2.74), before any costs
**Approx. profit factor: ≈ 1.38** (gross wins ÷ gross losses)

**Exit reason breakdown:**
- Stopped out: 57 trades (majority — frequent false breakouts/whipsaws)
- Target hit (+10%): 15 trades
- Trailing (momentum-failure) exit: 15 trades
- Time stop (15 trading days): 13 trades

**Compounded equity curve** (start = 100, 10%-of-equity sizing per trade, sequential by entry
date): **final value ≈ 106.5 — a ~6.5% total return over 5.5 years (~1.2%/year annualized).**
**Max drawdown ≈ 4.4%.**

That headline return is weak on its face: it is far below what simply holding SPY or QQQ (or most
of the individual mega-cap names) returned over the same 2021-2026 window, and it's before any
transaction costs. The low max drawdown is partly an artifact of the sizing (only 10% of equity per
trade, sequential compounding) rather than evidence the strategy is low-risk in practice — see
limitations.

## Honest limitations

- **No slippage or spread modeled.** 57 of 100 trades exit via a hard stop; many stops land at
  exactly the modeled -5% or the signal-day low. Real stop fills, especially on gap-throughs, are
  routinely worse than the resting stop price. This is the single biggest reason to distrust the
  raw expectancy — it's the part of the edge most likely to be costs, not real edge.
- **No commission modeling**, though Robinhood equities are commission-free, so this one is
  probably immaterial.
- **No earnings-date filter was applied or tested** — some entries likely fell inside an earnings
  window, where a gap can blow straight through the 5% stop before it can fill at the modeled
  price. The strategy doc flags this as a live-trading requirement; the backtest does not account
  for it, which likely makes the backtest optimistic on tail-risk trades.
- **Same-day stop/target ambiguity resolved conservatively (stop-first)** without intraday bars to
  confirm — could understate wins on days that actually ran to target first.
- **Sequential compounding assumption**: the equity curve treats all 100 trades as if they share
  one capital pool trade-by-trade in time order. In reality, several of these signals overlap in
  calendar time across different symbols (e.g., broad-market pullbacks stopping out AMZN, GOOGL,
  META, and NVDA within days of each other in Feb 2023 and Nov 2025) — a real portfolio holding
  those concurrently would see a sharper simultaneous drawdown than this curve shows, because the
  "3 concurrent positions" cap wasn't actually enforced in this simulation. **The 4.4% max
  drawdown figure is likely understated for that reason.**
- **Small per-symbol samples for QQQ and SPY (3 trades each)** — not statistically meaningful on
  their own.
- **Look-ahead bias check:** signal computed from data through close of day T only; entry at T+1's
  actual open — this part is clean. But indicator warm-up, breakout definition (closing-price
  Donchian rather than intraday-high Donchian), and the RSI implementation (Wilder smoothing) are
  design choices that could shift results meaningfully if changed — this is one specific rule set,
  not "momentum trading" in general.
- **100 trades over 5.5 years is a modest sample** for a system with only ~38% of trades winning;
  a handful of different market regimes are represented, but this is not enough to rule out that
  the modest positive edge is noise.

## What would need to change before this graduates

- Model realistic slippage on stop fills (e.g., assume an extra 0.3-0.5% worse than the resting
  stop) and re-check whether expectancy survives.
- Add an earnings-blackout filter and re-run to see how much of the tail risk that removes.
- Test whether requiring intraday-high (not just closing-price) breakout confirmation reduces the
  57% stop-out rate — the current definition may be catching too many one-day closing pops that
  reverse.
- Re-run the equity curve enforcing the actual 3-concurrent-position cap (reject a signal if 3
  slots are already full) to get an honest concurrent-drawdown estimate instead of the sequential
  approximation used here.

## Conclusion

Positive raw expectancy, low win rate, thin realistic returns, and an understated drawdown estimate
add up to "not there yet," not "broken." Per step 4 of the assignment this backtest was written
for: this is the honest answer — no live signals were generated from this version of the strategy.
