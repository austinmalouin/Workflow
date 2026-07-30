# Backtest: Mean-Reversion v1 — Combined (Hybrid Exit + Earnings Blackout)

**Date run:** 2026-07-23 **Base backtest:** `meanreversion-v1-backtest.md`
**Component tests:** `meanreversion-v1-hybridexit-backtest.md`, `meanreversion-v1-earningsblackout-backtest.md`

## Verdict up front

**The two independently-validated fixes stack cleanly — this is the best result on file, and it is
still not sound enough for live signals.** Combining the threshold-gated hybrid exit (trail only
if already up 5%+ at confirmation) with the 5-day earnings blackout on the same 5-symbol universe
(SPY, QQQ, AAPL, MSFT, NVDA) produces **CAGR ~2.09%/yr**, win rate 67.5%, max drawdown 2.55% — each
metric landing close to what adding the two independent effects would predict, with no negative
interaction between them. That's a genuinely better number than either fix alone (hybrid: ~1.94%/yr,
blackout: ~2.06%/yr) and meaningfully better than the original base version (~1.9%/yr). It is still
a roughly 2%/year paper return on a ~$580 account, still resting on a 5.5-year, 5-symbol,
single-implementation backtest with the usual caveats. No live signals were generated from this
version, and none should be until a materially larger sample, an independent re-implementation, and
real-money-scale considerations (below) are addressed.

## Methodology

Exactly the union of the two component tests — no new design decisions:

- **Universe, entry rule, position sizing, position cap:** unchanged since the original base
  backtest (SPY/QQQ/AAPL/MSFT/NVDA, `Close>SMA200` + `RSI(2)<10`, `min(10%, 1%/6%)` sizing, 3-position
  cap).
- **Exit rule (from the hybrid-exit test):** bank the trade immediately at the first close above
  SMA(5) unless unrealized return at that moment is already ≥5%, in which case switch to a
  trailing exit (ride until closing back below SMA5), time-stop extended to 15 days for trades in
  trailing mode.
- **Entry filter (from the earnings-blackout test):** skip a scheduled entry if it would fall within
  5 calendar days of a known/projected earnings date for AAPL, MSFT, or NVDA (SPY/QQQ exempt;
  real dates from `get_earnings_results` for ~2025 onward, back-projected in ~91.25-day steps for
  2021-2024, same approximation as momentum v2 and the standalone blackout test).
- Slippage (0.2%/0.3%/0.2%), stop-loss (-6%, intraday low check), and the 2021-01-04 to 2026-07-20
  test window are unchanged throughout.

## Results

**203 closed trades** — matching the standalone earnings-blackout test's trade count exactly (the
blackout removes the same 20 entries regardless of which exit rule is layered on top; the exit rule
change doesn't alter which signals fire, only how a handful resolve).

**Win rate: 67.5% (137/203)** — essentially the midpoint of the two component tests (67.6% hybrid,
68% blackout), as expected from a clean combination.
**Average win: +1.99%** | **Average loss: -2.38%** — both slightly better than either component
test alone, and clearly better than the base version's +1.9% / -2.5%.
**Exit reasons:** target 176, stop 18, **trail 9** — the identical 9 trades that qualified for the
trailing exit in the standalone hybrid test (none of them fall inside an earnings blackout window,
so the two fixes don't interact or conflict on this sample).

**Compounded equity: 100 → 112.1 (CAGR ~2.09%/yr).**
**Max drawdown: 2.55%** — matching the hybrid-only test's improvement, unaffected by the blackout
(which didn't change the drawdown in its standalone test either).
**Entries blocked by earnings blackout: 20** — identical to the standalone blackout test.

## Full comparison across every mean-reversion variant tested

| Version | Trades | Win rate | Avg win/loss | CAGR | Max DD |
|---|---|---|---|---|---|
| Base (fixed SMA5 exit) | 213 | 68.1% | +1.9% / -2.5% | ~1.9%/yr | 2.64% |
| Widened universe (15 sym, 8 sectors) | 408 | 62.0% | +1.69% / -2.58% | ~0.47%/yr | 6.83% |
| Pure let-winners-run (trail everything) | 201 | 48.3% | +3.77% / -2.68% | ~1.55%/yr | 7.24% |
| Hybrid exit only | 213 | 67.6% | +1.93% / -2.48% | ~1.94%/yr | 2.55% |
| Earnings blackout only | 203 | 68.0% | +1.95% / -2.4% | ~2.06%/yr | 2.65% |
| **Combined (hybrid + blackout)** | **203** | **67.5%** | **+1.99% / -2.38%** | **~2.09%/yr** | **2.55%** |

The combined version is the best on every return-related metric and ties for the best drawdown,
confirming that two independently-motivated, isolated fixes (one about exit timing, one about
entry-risk filtering) can be stacked without one undoing the other — not a guarantee that's always
true, but the case here.

## Honest limitations

- **All limitations from both component tests still apply and don't cancel out**: the 5%
  confirmation threshold was chosen by inference from the pure-trailing failure, not independently
  optimized; ~4 of 5.5 backtest years use back-projected (not verified) earnings dates; only 9
  trades ever exercise the hybrid exit logic and only 20 entries are blocked by the blackout — both
  are thin samples to lean on for their specific claimed effect sizes.
- **This is still a 5-symbol, 5.5-year, single-implementation backtest.** Every version tested on
  this desk shares this ceiling — a bigger sample, a different test window, and an independently
  re-implemented simulation (not just this same PowerShell approach re-run with different rules)
  are still needed before any number here should be trusted with real capital.
- **~2%/year on a ~$580 account is a small number in dollar terms** even if the backtest holds up
  exactly as measured — roughly $12/year before considering any further real-world friction (partial
  fills, wider real-world slippage than modeled, tax treatment of short-term gains). This was never
  going to be a way to meaningfully grow a sub-$600 account quickly; the value of this whole research
  thread has been in the process of finding *any* real, honestly-measured edge, not in the absolute
  dollar amount at this account size.
- **No independent verification.** Every backtest in this desk's history (momentum v1/v2, rotation
  v1, and all five mean-reversion variants) has been run in this same session-level PowerShell
  approach. A transcription error or subtle look-ahead bug shared across all of them would not be
  caught by any of the honest-limitations sections written so far, because they were all written by
  the same process that ran the code.

## What would need to change before this graduates

- Independent re-implementation of this exact rule set (ideally by a different tool/process/session)
  to catch any shared implementation bug before trusting the ~2.09%/yr number.
- A larger sample — either a longer historical window (if data permits) or accepting that 203 trades
  over 5.5 years is close to the ceiling of what this universe/timeframe can produce, and that
  further confidence requires waiting for more real time to pass, not more backtesting.
- A explicit, honest reckoning with position sizing at this account size: 10%-of-equity sizing on
  a ~$580 account is single-digit dollars per trade before the position even moves — worth
  discussing directly with Austin whether a strategy graduating at this account size is worth the
  operational overhead (daily monitoring, signal write-ups) relative to its realistic dollar payoff,
  separate from whether the backtest itself is "sound."

## Conclusion

This is the best mean-reversion result produced on this desk to date, and it got there by stacking
two narrow, well-isolated, honestly-tested fixes rather than one large speculative change. That is
the right way to have gotten here. It is also still short of a live-signal-worthy result — not
primarily because the backtest numbers look bad (they don't, relative to where this research
started), but because the sample is still thin, the implementation is still unverified by a second
process, and the realistic dollar return at this account size is small enough that "sound" and
"worth doing" are two different questions Austin should weigh separately. No live signals were
generated from this version.
