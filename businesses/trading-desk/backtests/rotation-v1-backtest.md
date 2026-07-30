# Backtest: Rotation v1 (Dual-Momentum SPY/EFA/Cash, Monthly)

**Date run:** 2026-07-23 **Strategy doc:** `../strategies/rotation-v1.md`

## Verdict up front

**Real, structural drawdown control — but it does not beat simply buying and holding SPY on
absolute return over this window, so it does not clear the bar for live signals either, for a
different reason than the momentum family did.** Max drawdown falls to **24.56%** vs. buy-and-hold
SPY's **52.2%** over the identical 23.4-year window — the strategy sat out virtually the entire
2008 crash and most of the 2022 bear market in cash. But CAGR comes in at **7.7%/year** against
buy-and-hold SPY's **9.67%/year** — in a window this dominated by a long US equity bull run, giving
up equity exposure during drawdowns cost more upside than the crash-avoidance was worth, on a pure
return basis. No live signals were generated from this version.

## Why this test was run

Same standing direction as `meanreversion-v1-backtest.md`: momentum v1/v2 needed a genuinely
different edge, not another filter pass on the same breakout mechanic. This tests the structural
opposite of momentum in almost every respect — monthly instead of daily, relative/absolute
momentum across asset classes instead of single-stock breakout signals, and no stop-loss/trailing
mechanics at all.

## Methodology

- **Universe:** SPY, EFA.
- **Period:** decisions from 2003-01 through 2026-06 (23.4 years, 281 monthly decisions) — data
  pulled from 2002-01 to give the 12-month lookback a full year of warm-up before the first
  decision. This is a much longer window than the momentum backtests' 5.5 years, made practical
  because monthly bars (294 per symbol) are two orders of magnitude fewer data points than the
  daily bars (1,400+ per symbol) momentum's window required.
- **Data source:** `get_equity_historicals`, monthly bars, split-adjusted (see the strategy doc's
  "why cash instead of bonds" for why dividend adjustment wasn't available/used here).
- **Compute environment:** same note as the mean-reversion backtest — no Python/Node runtime is
  available in this session, so this was run as a PowerShell script (`rotation_backtest.ps1`),
  reproducible and inspectable, not hand-computed and not a reused prior engine.
- **Decision rule:** at each month-end M, compute trailing-12-month return for SPY and EFA; hold
  whichever is higher if that return is positive, else hold cash (0% modeled return), for month
  M+1. Rebalance only on a change of position.
- **Slippage:** 0.05% per position change (SPY/EFA are tight-spread, liquid ETFs — a smaller
  assumption than momentum's stock-level 0.2-0.3%, justified by the asset class, not loosened
  arbitrarily).
- **Benchmarks computed over the identical window:** buy-and-hold SPY, buy-and-hold EFA, and a
  50/50 SPY/EFA blend rebalanced monthly (a naive diversification comparison with no momentum
  logic at all).

## Results

**281 monthly decisions, 2003-01 through 2026-06.**

**Final equity (start = 100): 568.66 → CAGR 7.7%**
**Max drawdown: 24.56%** | **Annualized volatility: 11.66%**
**Win rate (months): 52.3% (147/281)**
**Allocation:** SPY held 145 months, EFA held 82 months, cash held 54 months.
**Position switches (slippage events): 44** over 23.4 years — roughly 1.9/year, confirming this is
genuinely a low-turnover strategy, not a relabeled daily system.

**Benchmarks, same window:**

| | Final (start=100) | CAGR | Max drawdown |
|---|---|---|---|
| **Rotation v1** | 568.66 | 7.7% | **24.56%** |
| Buy & hold SPY | 867.73 | **9.67%** | 52.2% |
| Buy & hold EFA | 328.91 | 5.22% | — |
| 50/50 SPY/EFA, rebalanced monthly (no momentum) | 546.32 | 7.52% | 56.0% |

Two things stand out. First, the strategy's return is barely ahead of the naive, momentum-free
50/50 blend (7.7% vs. 7.52%) — most of rotation's value here isn't return enhancement, it's
drawdown reduction (24.56% vs. that same blend's 56.0% drawdown). Second, buy-and-hold SPY alone
beats the strategy on raw CAGR by exactly the margin that crash-avoidance cost in upside — this
window (2003-2026) contains an unusually long, strong US bull run, and any strategy that spends
time in cash during selloffs gives up some of the snapback that followed each one.

**What actually happened during the three big drawdowns in the window** (pulled directly from the
decision log):
- **2008-2009 GFC:** cash from June 2008 through at least June 2009 — the strategy sat out the
  entire crash and the initial recovery months, both trailing-12-month returns having gone
  decisively negative.
- **2020 COVID crash:** held SPY into February 2020 (the crash month itself, -13% that month),
  rotated to cash for March-April 2020, then back into SPY by May 2020 in time to capture most of
  the V-shaped recovery (+1.28%, +5.89%, +6.98% the following three months).
- **2022 bear market:** held SPY through Q1 2022 (still riding positive trailing momentum, losing
  ~9% in March), rotated to cash by April 2022 and stayed there through December 2022 as both legs'
  trailing momentum stayed negative.

This is exactly the mechanism the strategy is supposed to provide — it reacted with roughly a
one-month lag to each regime change, avoided the worst of two of the three drawdowns almost
entirely, and took a partial hit on the fastest one (2020, because a one-month-lagged monthly
signal cannot react to a crash that happens within a single month).

## Honest limitations

- **No dividend adjustment.** SPY and EFA's actual total returns (price + dividends) are higher
  than what this backtest measures — SPY's dividend yield has run roughly 1.3-1.8%/year over this
  window, EFA's closer to 2.5-3%/year. Both benchmarks and the strategy's held-asset returns are
  understated by a similar amount in most months, so the *relative* comparison between strategy and
  buy-and-hold is less distorted than the absolute CAGR figures — but the effect on relative
  momentum rankings (SPY vs. EFA) is not zero, since EFA's higher yield could occasionally flip a
  close relative-momentum call that a total-return calculation would call the other way. This is a
  real, unresolved gap, not a rounding error.
- **This window is dominated by an unusually strong, long US equity bull market.** A test that
  instead emphasized 2000-2002 or a hypothetical extended sideways/choppy regime would likely show
  this strategy in a much better relative light — crash-avoidance strategies are structurally
  disadvantaged in backtests over strong-bull windows and structurally advantaged over
  choppy/bearish ones. This is a property of the test period, not a flaw in the method, but it
  means the 7.7%-vs-9.67% CAGR gap should not be read as "the strategy doesn't work" so much as
  "this window didn't reward giving up equity exposure."
- **One-month decision lag is a real, structural cost.** The strategy cannot react faster than
  monthly, so any single-month shock (2020 being the clearest example) is absorbed in full before
  the next rebalance can respond. A faster-reacting variant would trade off this cost against much
  higher turnover and transaction-cost drag — not obviously a better trade for a small account.
- **Only 2 equity legs.** A richer asset universe (adding small-cap, EM, REITs, commodities per
  classic GEM-family variants) could change both the return and drawdown numbers meaningfully in
  either direction; untested here.
- **Cash modeled at a flat 0% return.** Real idle cash in a Robinhood account earns some interest;
  modeling it at 0% is conservative (understates the strategy's real-world return by the interest
  the 54 cash-months would have earned) but not by a large amount at typical short-term rates.
- **Absolute-momentum threshold fixed at exactly 0%.** No sensitivity testing was done on this
  threshold (e.g., requiring 12-month return above a small positive hurdle, or comparing against a
  T-bill rate instead of zero, as classic GEM does) — untested here.
- **Compute environment note:** same caveat as mean-reversion v1 — this was run as fresh
  PowerShell code in this session (no Python/Node available), sanity-checked (the concrete
  crash-period allocation history above matches known market history) but not independently
  cross-checked against a second implementation.

## What would need to change before this is worth reconsidering

- Re-run with dividend-adjusted (total return) data if a data source that supports it becomes
  available — the current price-only comparison is the single biggest open question on these
  results.
- Test over a window that includes more of the pre-2003 or a genuinely choppy/sideways regime, to
  see whether the drawdown-control benefit shows up as *net positive* return advantage outside a
  strong-bull window, not just a smoother ride through the same one.
- Consider whether this strategy has a role as a **capital-preservation sleeve** rather than a
  return-generating signal — i.e., not something graduated to "live signals" in the trading-desk
  sense, but a candidate answer if Austin ever wants a lower-maintenance, lower-drawdown holding for
  part of the account instead of active single-stock signals.

## Conclusion

The mechanic works as designed — it measurably avoided most of two major drawdowns and reacted
sensibly to a third — but on raw return, over this specific 23-year, bull-dominated window, it does
not beat simply holding SPY, and only barely beats a momentum-free 50/50 blend. That is a different
kind of "not there yet" than momentum v1/v2's thin, cost-eroded edge or mean-reversion v1's promising-
but-narrow result: this strategy isn't broken, it's solving for a different objective
(drawdown control) than "beat a simple index buy-and-hold," and this window didn't reward that
trade-off. Per the trading-research standard, this does not graduate to live signals. Of the three
non-breakout directions tested so far, mean-reversion v1 remains the more promising one to keep
refining for this desk's actual goal (a signal-generating edge), with this rotation result kept on
file as a documented, honestly-negative-on-return alternative rather than a discarded one.
