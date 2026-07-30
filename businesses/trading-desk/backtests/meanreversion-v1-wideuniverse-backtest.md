# Backtest: Mean-Reversion v1 — Widened Universe Test (15 symbols, 8 sectors)

**Date run:** 2026-07-23 **Base strategy doc:** `../strategies/meanreversion-v1.md`
**Base backtest:** `meanreversion-v1-backtest.md` (5-symbol version)

## Verdict up front

**Widening the universe made every metric worse, not better — and the reason why is the useful
result.** The original 5-symbol backtest's own limitations section suggested a bigger, less-
correlated universe as the natural next test, on the theory that more independent symbols would
let the 3-position cap actually get used and improve returns. That theory was wrong. Going from 5
symbols (mostly tech/broad-market) to 15 across 8 sectors: win rate fell from 68.1% to 62%, average
return per trade got thinner, **max drawdown roughly tripled (2.64% → 6.83%)**, and CAGR collapsed
from ~1.9%/yr to **~0.47%/yr**. The instrumentation added for this run (which the prior backtest
was explicitly missing) shows why: the position cap now blocks a signal **389 times** — nearly as
often as it fills one (408 actual trades) — and those blocks cluster in specific months (Sept 2021,
Jan 2022, Aug 2023, Apr 2024, Oct/Dec 2024) that line up with known broad-market pullbacks. The
mechanic doesn't get "more diversified" opportunities during a real risk-off move — it gets a flood
of simultaneous, correlated signals across every sector at once, competing for the same 3 slots.
Sector-level results confirm this is not just a capital-allocation problem: **Financials,
Consumer Discretionary, Consumer Staples, and Industrials each lost money on average** in this
strategy; only Tech and the broad-market ETFs were actually profitable. No live signals were
generated from this test.

## Why this test was run

Directly from the base backtest's "what would need to change" list: "expand the universe to more,
less-correlated liquid names... to see whether trade frequency and deployed capital actually
improve, or whether the position cap was already binding in ways this run couldn't see." This test
answers that question directly, with the cap-block logging the prior run lacked.

## Methodology

- **Universe:** 15 symbols across 8 sectors — SPY, QQQ, IWM (broad-market/small-cap), AAPL, MSFT,
  NVDA (tech), JPM, BAC (financials), UNH, JNJ (healthcare), HD (consumer discretionary), PG, KO
  (consumer staples), XOM (energy), CAT (industrials). Same liquidity bar as before (large-cap,
  well-known, high daily dollar volume).
- **Period, data source, indicators, slippage, sizing, position cap:** identical to the base
  5-symbol backtest — 2021-01-04 through 2026-07-20, daily bars pulled from 2020-01-02 for SMA(200)
  warm-up, split-adjusted, same SMA(200)/RSI(2)/SMA(5) mechanic, same 6% stop / SMA5 target / 10-day
  time-stop, same 0.2%/0.3%/0.2% slippage assumptions, same `min(10%, 1%/6%)` sizing, same 3-position
  hard cap. **Only the universe changed** — this is a controlled test of that one variable.
- **New instrumentation:** every time an entry signal fires (uptrend + RSI2<10) but the 3-position
  cap is already full, that event is now logged (symbol, date) instead of silently discarded — the
  gap the base backtest flagged as needing to close before trusting the cap's real-world effect.

## Results

**408 closed trades** (up from 213 on 5 symbols) — confirming more symbols does generate more
signals, exactly as expected.

**Win rate: 62% (253/408)**, down from 68.1%.
**Average win: +1.69%** | **Average loss: -2.58%** (both slightly worse than the 5-symbol run).
**Exit reasons:** target 365, stop 41, time-stop 2 (up from 0 — a couple of positions in the wider
universe finally went 10 days without resolving, unlike the narrow universe where every trade
resolved fast).

**Compounded equity: 100 → 102.64 (CAGR ~0.47%/yr, down from ~1.9%/yr).**
**Max drawdown: 6.83%** (up from 2.64% — more than 2.5x worse).

**Position-cap blocks: 389** — almost one block for every trade actually taken. Monthly
distribution is not uniform; blocks cluster heavily in known pullback/correction windows:

| Month | Cap-blocks |
|---|---|
| 2021-09 | 29 |
| 2022-01 | 26 |
| 2024-04 | 23 |
| 2024-12 | 23 |
| 2024-10 | 20 |
| 2023-08 | 19 |
| 2021-06 | 19 |
| 2023-09 | 17 |
| 2024-01 | 17 |

These months correspond to real, known broad-market drawdown/volatility events, not random noise —
confirming that when the market sells off, RSI2<10 fires across most symbols in the universe at
once, regardless of sector, and the fixed 3-slot cap simply can't take more than 3 of them.
"Diversification" across sectors does not desynchronize the entry signal during exactly the periods
it matters most.

**Per-sector breakdown (this is the real finding):**

| Sector | Trades | Win rate | Avg return/trade |
|---|---|---|---|
| Tech | 94 | 70.2% | **+0.73%** |
| Broad-market ETFs | 97 | 69.1% | **+0.37%** |
| Healthcare | 58 | 62.1% | -0.05% |
| Industrials | 23 | 60.9% | -0.22% |
| Consumer Staples | 60 | 51.7% | -0.34% |
| Consumer Discretionary | 22 | 54.5% | -0.59% |
| Financials | 54 | 50.0% | **-0.67%** |

Only Tech and the broad-market ETFs were net profitable per trade on average. Financials,
Consumer Discretionary, Consumer Staples, and Industrials each **lost money on average** running
this exact mechanic. Per-symbol, the best performers were NVDA (+1.41%/trade, 78.4% win), IWM
(+0.64%), MSFT (+0.62%), QQQ (+0.39%); the worst were BAC (-1.01%, 50% win) and HD (-0.59%).

## Reading this honestly

The original 5-symbol universe (SPY, QQQ, AAPL, MSFT, NVDA) wasn't an arbitrary or lazy choice in
hindsight — it happened to be concentrated exactly in the two categories (tech, broad-market) where
this mechanic actually has a real edge. Adding financials, staples, discretionary, healthcare, and
industrials didn't diversify the strategy's risk — it diluted a real, narrower edge with sectors
where the same short-term-oversold-in-an-uptrend read either doesn't apply or actively loses money.
A 2-day RSI dip in a rate-sensitive bank stock or a slow-moving consumer-staples name does not
appear to behave like a 2-day RSI dip in a high-beta growth/tech name — plausible reasons include
different volatility regimes, different investor bases (momentum/retail-heavy vs. income/value-
oriented), and different reasons prices actually drop (a staples or financials name dropping 2 days
in a row is more likely reflecting real news than tech's whippier, sentiment-driven pullbacks).

This also reframes the position-cap question from the original backtest. The cap wasn't
"underused" because the universe was too narrow and correlated — the cap binds hardest in the
wider universe specifically because a real market-wide risk-off event fires the same signal across
every sector simultaneously. More sectors did not desynchronize the signal; a broad drawdown is
broad. The fix for "the cap doesn't get used enough" was never going to be "more sectors" — sector
diversification does not protect against systemic, market-wide moves, which is exactly when this
mechanic's signal is most likely to fire everywhere at once.

## Honest limitations

- **8 sectors is not exhaustive** — real estate, utilities, materials, communications, and small/
  mid-cap-specific names outside IWM's broad basket weren't tested. It's possible some untested
  sector behaves like tech; this test doesn't rule that out, only rules out the 5 tested here that
  underperformed.
- **One symbol per sector for most sectors** (only Tech, Financials, Consumer Staples, and the
  broad-market bucket had 2+ names) — a single name's idiosyncratic behavior (e.g., BAC's -1.01%/
  trade) could be pulling its whole sector's average further than a larger sample would show. Sector
  conclusions here are directional, not proven at the individual-sector level.
- **Same-window caveat as before** — this is still the 2021-2026 window, the same one both momentum
  backtests and the narrow mean-reversion backtest used; a different window could shift which
  sectors look strong or weak.
- **No earnings blackout, same gap as the base version** — still unaddressed, still a real risk,
  now spread across more symbols/sectors than before.
- **Compute environment note:** same PowerShell-script approach as the base mean-reversion
  backtest, not independently cross-checked against a second implementation.

## What would need to change before revisiting this direction

- Test a **tech/growth-tilted expansion** instead of a sector-diverse one — more names *within* the
  categories that actually worked (e.g. add AMD, GOOGL, META, AMZN, more growth-tilted ETFs) rather
  than spreading into sectors this run showed don't fit the mechanic.
- If sector diversification is still wanted for genuine risk-reduction reasons (not
  return-improvement reasons), it should be evaluated on those terms explicitly — accept the
  probable return drag as the price of true diversification — rather than assumed to be a free
  win, which this test disproves.
- Consider whether the position cap should scale with universe size, and if so, confront directly
  that more concurrent positions means more concentrated capital risk on a ~$580 account — this
  is a real trade-off, not a free parameter to raise.

## Conclusion

This test did exactly what it was supposed to: it answered whether "more, less-correlated symbols"
would improve mean-reversion v1's return and capital deployment. It did not — return fell to
roughly a third of the narrow-universe result and drawdown nearly tripled, because the assumed
"less-correlated" premise doesn't hold during the broad market pullbacks that generate this
strategy's busiest signal periods, and because several of the added sectors simply don't share the
edge this mechanic has in tech/broad-market names. The useful output isn't "widening failed" in
isolation — it's that **the edge appears to be sector-specific, not universal**, which is a
falsifiable, actionable finding for the next test rather than a dead end. No live signals were
generated from this version.
