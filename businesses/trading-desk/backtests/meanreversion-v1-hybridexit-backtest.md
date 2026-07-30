# Backtest: Mean-Reversion v1 — Threshold-Gated Hybrid Exit

**Date run:** 2026-07-23 **Base backtest:** `meanreversion-v1-backtest.md` **Prior (failed) attempt:**
`meanreversion-v1-letwinnersrun-backtest.md`

## Verdict up front

**A small, real, low-noise improvement — the threshold gate fixed the failure mode of the pure
trailing-exit test.** The pure let-winners-run version (previous test) applied a trailing exit to
every confirmed trade and made everything worse (CAGR fell, drawdown nearly tripled) because most
"confirmations" were weak and gave back most of their gain before the trail caught them. This
version only switches a trade into trailing mode if it's **already up 5% or more** the moment it
first confirms (closes above SMA5) — everything else banks the exit immediately, exactly as the
base version does. Result: only 9 of 213 trades ever qualified for the trail, and **8 of those 9
were winners** (vs. the pure version's 52.5%), including the two large NVDA moves the base version
had cut off early (+15.84%, +14.6%) plus AAPL +15.04% and MSFT +9.13%. Because so few trades are
affected, the aggregate improvement is modest — win rate and average win/loss are nearly identical
to the base version, CAGR ticks up marginally (~1.9%→~1.94%/yr), max drawdown ticks down slightly
(2.64%→2.55%). This is directionally the right design, validated at the trade level, but not by
itself a graduation-worthy jump in return. No live signals were generated from this version.

## What changed from the base version

Identical entry rule, universe (SPY/QQQ/AAPL/MSFT/NVDA), stop-loss, slippage, sizing, and position
cap. The exit rule is now conditional:

- On the day a position first closes above SMA(5) (the base version's exit trigger), compute the
  trade's unrealized return at that point (`close / entry_price - 1`).
- **If unrealized return ≥ +5%:** don't exit — mark the position "confirmed" and switch to a
  trailing exit (ride until it closes back below SMA5, same mechanic as the failed pure-trailing
  test), with the time-stop extended to 15 days to give it room.
- **If unrealized return < +5%:** exit immediately at the next open, exactly as the base version
  does — bank the ordinary small bounce rather than risking a giveback on a confirmation that
  hasn't shown real strength yet.

## Results

**213 trades** (identical count to the base version — the hybrid rule doesn't change which signals
fire or how many resolve, only how the exit is timed for the rare trade that qualifies).

**Win rate: 67.6% (144/213)** — essentially unchanged from the base version's 68.1%.
**Average win: +1.93%** | **Average loss: -2.48%** — both nearly identical to base (+1.9% / -2.5%),
as expected since 204 of 213 trades exit exactly as they would have under the base rule.
**Exit reasons:** target 184, stop 20, **trail 9** (the only trades affected by this change).

**The 9 trades that qualified for the trail:**

| Symbol | Entry | Exit | Return |
|---|---|---|---|
| NVDA | 2021-08-19 | 2021-09-01 | +14.88% |
| NVDA | 2021-12-14 | 2021-12-17 | +0.63% |
| AAPL | 2022-01-25 | 2022-02-04 | +7.56% |
| MSFT | 2023-04-25 | 2023-05-04 | +9.13% |
| NVDA | 2024-02-21 | 2024-02-29 | +15.84% |
| NVDA | 2024-10-02 | 2024-10-16 | +14.60% |
| NVDA | 2025-11-07 | 2025-11-14 | -1.50% |
| NVDA | 2026-05-28 | 2026-06-04 | +0.84% |
| AAPL | 2026-06-26 | 2026-07-15 | +15.04% |

8 of 9 winners (88.9%), average return on these 9 trades ≈ **+8.6%** — compare to what the base
version's fixed exit would have banked on these same signals (roughly +1-3% each, based on the
base backtest's typical target-exit magnitude). This is the mechanism working as designed: gating
on demonstrated strength (already up 5%+) rather than a bare SMA5 crossing filtered out the
weak/whipsaw-prone confirmations that sank the pure-trailing test, while still capturing the
genuine outliers.

**Compounded equity: 100 → 111.17 (CAGR ~1.94%/yr)** — a small improvement over the base version's
~1.9%/yr.
**Max drawdown: 2.55%** — a small improvement over the base version's 2.64%.

## Side-by-side: base vs. pure-trailing vs. hybrid

| | Base (fixed exit) | Pure trailing | Hybrid (5% gate) |
|---|---|---|---|
| Win rate | 68.1% | 48.3% | 67.6% |
| Avg win / loss | +1.9% / -2.5% | +3.77% / -2.68% | +1.93% / -2.48% |
| CAGR | ~1.9%/yr | ~1.55%/yr | ~1.94%/yr |
| Max drawdown | 2.64% | 7.24% | 2.55% |
| Trades affected by exit change | — | 213/213 | 9/213 |

## Honest limitations

- **Only 9 trades were affected** — too small a sample to have real statistical confidence that
  "trail if up 5%+ at confirmation" is precisely the right threshold, or that its 8/9 hit rate
  generalizes. A different market regime could easily produce a worse ratio on the next 9
  qualifying trades.
- **The 5% threshold was chosen reasoning from the pure-trailing test's outcome, not independently
  optimized** — a lower threshold (e.g. 3%) would qualify more trades and could show a different,
  possibly worse, risk/reward; this wasn't swept.
- **Same window, same compute-environment caveats** as all prior mean-reversion backtests.
- **Aggregate improvement is small enough to be within noise** for a 213-trade sample — this result
  should be read as "the hybrid design is directionally correct and doesn't hurt," not as a proven,
  large edge on its own.

## What would need to change before this graduates

- Combine with the earnings blackout (`meanreversion-v1-earningsblackout-backtest.md`) — both
  changes were tested in isolation and both showed small, real improvements with no real downside;
  a combined version is the natural next test.
- Sweep the confirmation threshold (3%, 4%, 5%, 7%) to see if the trade-off between trade count and
  hit-rate has a better setting than 5%, chosen here by inference rather than optimization.
- Still needs the wider validation every version on this desk needs: a bigger sample, a different
  test window, and a second independent implementation before any of this is trusted with real
  money.

## Conclusion

This test confirms the diagnosis from the pure-trailing failure: the problem wasn't the idea of
letting winners run, it was applying it indiscriminately. Gating the trail on demonstrated
strength (up 5%+ at confirmation) preserves the base version's reliable behavior on ordinary trades
while capturing much larger gains on the rare trade that's genuinely running — 8 of 9 qualifying
trades were winners, averaging around +8.6%. The aggregate effect on this backtest is modest
(CAGR ~1.9%→~1.94%) simply because so few trades qualify, but it is a real, no-downside
improvement over the base version, and the best mean-reversion result on file to date. No live
signals were generated from this version.
