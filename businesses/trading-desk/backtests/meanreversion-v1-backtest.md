# Backtest: Mean-Reversion v1 (Pullback-in-Uptrend, RSI2)

**Date run:** 2026-07-23 **Strategy doc:** `../strategies/meanreversion-v1.md`
**Prior versions (different mechanic, for comparison):** `momentum-v1-backtest.md`,
`momentum-v2-backtest.md`

## Verdict up front

**A genuinely different risk profile from the momentum versions — and directionally more
promising — but still not sound enough for live signals.** Win rate jumps from momentum's 38-43%
to **68.1%**, and max drawdown falls from momentum's 3-4% to **2.64%**. That confirms the core
hypothesis: buying oversold dips inside an uptrend behaves very differently from chasing breakout
highs, on the same names, over the same kind of window. But the win rate improvement comes from
many small wins (+1.9% average) against a smaller number of real losses (-2.5% average, plus a
harder -6.28% modeled stop-loss tail on 20 of 213 trades), and only 10% of equity is deployed per
trade — so the *absolute* return is thin: **+10.95% total over 5.5 years, ~1.9%/year annualized.**
That's better than momentum v2 (~0.45%/yr) and roughly on par with momentum v1 (~1.2%/yr), on a
much smoother equity curve, but it does not clear the bar for live signals on its own. No live
signals were generated from this version.

## Why this test was run

Both momentum v1 and v2 share one mechanic (trend filter + closing-price breakout + volume + RSI,
buying strength) and both cleared roughly the same 57% stop-out rate — the entries are reliably
getting faded. v2 added realistic costs and the paper edge shrank further. Per the standing
direction (a different edge, not another round of filters on the same mechanic), this backtest
tests the structural opposite: fading short-term weakness inside a long-term uptrend, instead of
chasing short-term strength.

## Methodology

- **Universe:** SPY, QQQ, AAPL, MSFT, NVDA — 5 symbols (smaller than momentum's 10; see
  limitations for what this does to the position cap).
- **Period:** entries from 2021-01-04 through 2026-07-20 (~5.5 years, matching momentum v1/v2's
  window for comparability). Data pulled from 2020-01-02 to give the 200-day SMA a full warm-up
  before the test window starts.
- **Data source:** `get_equity_historicals`, daily bars, split-adjusted, fetched per-call for all
  5 symbols together (1,644 daily bars each).
- **Compute environment:** no Python/Node runtime is available in this workspace session, so the
  simulation was written and run as a PowerShell script (`meanreversion_backtest.ps1`,
  reproducible, not hand-computed) rather than the script language used for prior backtests. Same
  bar-by-bar, no-look-ahead discipline: indicators computed through day T's close only, entries and
  exits fill at the next session's actual open (except the intraday stop-loss, which checks the
  day's low directly, same as a real resting stop order would behave).
- **Execution engine:** single chronological day-by-day simulation across all 5 symbols together
  (shared, real-time position count), same structural approach as momentum v2: each day, (0)
  execute any target-exit that was signaled on a prior day's close, (1) enact entries scheduled
  from a prior day's close, (2) resolve today's exits (stop via intraday low, mean-reversion target
  via today's close signaling tomorrow's exit, time-stop via day count), (3) scan for new entry
  signals at today's close.
- **Indicators:** SMA(200) and SMA(5) (simple moving averages), RSI(2) with standard Wilder
  smoothing (seeded from the first 2 daily deltas, then smoothed).
- **Slippage:** entries 0.2% worse than the open, stop-loss exits 0.3% worse than the stop price,
  target/time exits 0.2% worse than their reference price — identical assumptions to momentum v2,
  not loosened for this test.
- **Position sizing:** identical formula to momentum v1/v2 — `min(10% of running equity, 1% of
  running equity / stop-loss %)`, computed per trade, applied sequentially by entry date to a
  single hypothetical account starting at 100.
- **Position cap:** 3 concurrent positions, hard-gated (an entry due while 3 are already open is
  skipped outright), same as momentum v2.
- **No earnings blackout modeled** for this version (see strategy doc's "what this does not do").

## Results

**Sample size: 213 closed trades** across the 5 symbols, 2021-01 through 2026-07.

| Symbol | Trades |
|---|---|
| AAPL | 49 |
| MSFT | 26 |
| NVDA | 46 |
| QQQ | 45 |
| SPY | 47 |

Trades by year: 2021: 49, 2022: 14, 2023: 39, 2024: 51, 2025: 35, 2026 (partial, through July): 25.
**2022's trade count drops by more than half** relative to the surrounding years — the SMA(200)
uptrend filter correctly locked most symbols out of new entries for most of the 2022 bear market,
since price was below its 200-day average for extended stretches. That's the uptrend filter doing
its job structurally, not a data artifact.

**Win rate: 68.1% (145 wins / 68 losses)**
**Average win: +1.9%** | **Average loss: -2.5%**
**Exit reason breakdown:**
- Mean-reversion target hit (`Close > SMA5`): 193 trades, average +1.19% (net of slippage) — most
  trades exit this way, and most exits are modest bounces, not major reversals. A handful of
  outliers rode much further than a typical bounce (best trades: NVDA +18.32% on 2024-02-21→23,
  +12.02% on 2021-12-14→16) — cases where the "reversion" signal actually caught the start of a
  larger continuation move.
- Stopped out: 20 trades, **every single one at almost exactly -6.28%** (the modeled -6% stop plus
  0.2% entry slippage plus 0.3% stop slippage) — this is a useful sanity check that the simulation
  code is applying the stop and slippage consistently, not a sign every stop is identically timed
  in the market.
- Time stop (10 trading days): **0 trades** — no position in this backtest ever went 10 days
  without hitting either the stop or the mean-reversion target. This confirms the mechanic resolves
  fast, as designed, but also means the time-stop rule is untested here.

**Compounded equity curve** (start = 100, sizing per trade's own risk formula, sequential by entry
date): **final value ≈ 110.95 — a ~10.95% total return over 5.5 years (~1.9%/year annualized).**
**Max drawdown ≈ 2.64%.**

## Side-by-side vs. momentum v1/v2

| Metric | Momentum v1 | Momentum v2 | Mean-reversion v1 |
|---|---|---|---|
| Mechanic | Buy breakout strength | Buy breakout strength (cost-aware) | Buy pullback weakness in uptrend |
| Universe | 10 symbols | 10 symbols | 5 symbols |
| Sample size | 100 trades | 63 trades | 213 trades |
| Win rate | 38% | 42.9% | **68.1%** |
| Avg win / avg loss | +6.17% / -2.74% | +5.36% / -3.30% | +1.9% / -2.5% |
| Compounded return (test window) | +6.5% | +2.5% | +10.95% |
| Annualized | ~1.2%/yr | ~0.45%/yr | ~1.9%/yr |
| Max drawdown | 4.4% (cap not enforced) | 3.0% (cap enforced) | **2.64%** |
| Stop-out rate | 57% | 57% | 9.4% (20/213) |

Reading this straight: the mean-reversion mechanic really is structurally different, not a
relabeled version of the same edge — dramatically higher win rate, dramatically lower drawdown,
much lower stop-out rate. But the per-trade win size shrank along with it (average win +1.9% vs.
momentum's +5-6%), so on pure compounded return this version is better than v2 and roughly level
with v1 — an improvement in risk-adjusted terms, not yet a graduation-worthy result in absolute
terms.

## Honest limitations

- **Only 5 symbols, and 4 of them are large-cap tech / tech-heavy index funds** (AAPL, MSFT, NVDA,
  QQQ, plus SPY). These names are highly correlated — a broad tech selloff can plausibly hit the
  RSI2<10 trigger on several of them within the same day or two, meaning the 3-position cap likely
  binds more often here than it would on a more sector-diverse universe, capping the strategy's
  actual deployed capital during exactly the moves where the edge (if real) would compound fastest.
  This backtest did not log how often the cap actually blocked a signal (unlike the momentum v2
  backtest, which logged 0 cap-blocks explicitly) — that instrumentation gap should be closed
  before trusting this version further.
- **No earnings blackout.** A stock gapping down hard into an earnings report will trip RSI2<10 for
  a completely different reason (repricing on new information, not short-term technical
  overreaction) than the mechanic assumes. This is a bigger open risk here than it was for momentum
  v2, precisely because this strategy's entire thesis is "the drop is noise" — an earnings-driven
  drop often is not noise.
- **Time stop never fired (0/213)** — the 10-day time-stop rule is written into the mechanic but
  completely unvalidated by this sample. If a future market regime produces pullbacks that neither
  bounce nor blow through the stop, this rule's behavior is unknown.
- **Compute environment note:** this backtest was run as a PowerShell script rather than whatever
  scripting environment produced the momentum v1/v2 numbers (no Python or Node runtime is
  available in this session). The simulation logic was written fresh for this test and is not a
  reused, previously-validated engine — treat it as new code, sanity-checked here (the exact
  -6.28% stop-loss consistency across all 20 stop-outs, and the SMA(200)-driven drop in 2022 trade
  count) but not independently cross-checked against a second implementation.
- **Same-day stop/target ambiguity, sequential-compounding assumption, and split-only (no
  dividend) price data** — same caveats as momentum v1/v2, not re-derived here.
- **Small per-symbol samples relative to the aggregate** — MSFT (26 trades) is thinner than the
  other four (45-49 each); no single symbol's result should be trusted in isolation.
- **No commission modeling** (Robinhood equities are commission-free, immaterial as before).
- **Real account check (2026-07-23):** $579.59 total, $59.28 cash — same sizing/cap mismatch as
  momentum v1/v2 applies here too; this account cannot actually fund 3 concurrent 10%-of-equity
  positions today regardless of what the backtest's cap logic assumes.

## What would need to change before this graduates

- ~~Expand the universe to more, less-correlated liquid names... and re-run with cap-block
  logging~~ **Tested 2026-07-23, see `meanreversion-v1-wideuniverse-backtest.md`.** Result:
  widening to 15 symbols across 8 sectors made every metric worse (CAGR 1.9%→0.47%, max drawdown
  2.64%→6.83%) — the position cap blocked signals 389 times, clustered in known broad-market
  pullback months, because a real risk-off move fires this signal across every sector at once
  regardless of "diversification." Per-sector breakdown showed the edge is concentrated in Tech and
  broad-market ETFs specifically; Financials, Consumer Discretionary, Consumer Staples, and
  Industrials each lost money on average running the identical mechanic. Next test should expand
  *within* tech/growth names, not spread across sectors.
- Add the earnings blackout from momentum v2 — this mechanic's exposure to earnings-day gaps is a
  real, unaddressed risk, arguably a bigger one here than for the breakout mechanic.
- Consider whether letting winners run past the SMA(5) exit (e.g. a trailing rule, similar to
  momentum's momentum-failure exit) captures more of the occasional larger continuation moves (the
  NVDA +18.32% and +12.02% outliers) without giving up the fast, high-win-rate resolution on
  ordinary bounces — the current fixed shallow target may be leaving return on the table precisely
  because it doesn't distinguish "reverted" from "reverted and about to keep running."
- Independently re-implement the simulation (ideally in a different tool/session) to cross-check
  this backtest's numbers before treating them as load-bearing.

## Conclusion

This test did what it was asked to do: prove or disprove that a structurally different mechanic
behaves differently from the momentum family's breakout-chasing. It behaves very differently — far
higher win rate, far lower drawdown, far lower stop-out rate — which is real evidence the "genuinely
different edge" direction is sound in kind, even though this specific parameterization's absolute
return (~1.9%/yr) is still too thin, on too narrow and correlated a universe, with earnings risk
still unaddressed, to trust with live money. Per the trading-research standard (documented and
genuinely sound before signals get generated), this doesn't clear the bar yet either — but it is
the most promising direction on file so far, and the recommended one to keep refining rather than
returning to more momentum-mechanic tuning. No live signals were generated from this version.
