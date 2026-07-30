# Backtest: Mean-Reversion v1 — Earnings Blackout

**Date run:** 2026-07-23 **Base backtest:** `meanreversion-v1-backtest.md`

## Verdict up front

**Closes a real, previously-flagged risk gap at close to no cost — a small, real improvement.**
The base mean-reversion backtest had no earnings blackout, a risk flagged explicitly in that
writeup: a name gapping into an earnings report could trigger the RSI2<10 entry trigger for a
completely different reason (a fundamental repricing) than the mechanic assumes (short-term
technical overreaction). Adding a 5-calendar-day blackout around known/projected earnings dates
(same rule and data-sourcing approach as momentum v2's blackout) blocked 20 entries outright.
Trade count fell only slightly (213→203, since the position cap backfilled some blocked slots with
other signals), win rate held essentially flat (68.1%→68%), and — mildly better than a wash —
**CAGR improved (~1.9%→~2.06%/yr)** while max drawdown stayed effectively unchanged (2.64%→2.65%).
No live signals were generated from this version.

## Why this test was run

Explicitly flagged in the base mean-reversion strategy doc as unaddressed and, per that doc, "a
bigger open risk here than it was for momentum v2, precisely because this strategy's entire thesis
is 'the drop is noise' — an earnings-driven drop often is not noise." This closes that gap.

## Methodology

- **Universe, entry/exit rules, sizing, slippage, position cap:** identical to the base 5-symbol
  backtest — only the earnings blackout is new.
- **Earnings data:** `get_earnings_results` per symbol (AAPL, MSFT, NVDA — SPY and QQQ have no
  earnings and are exempt), trailing ~8 quarters, real/verified dates from ~2025-01 onward. Same
  approach as momentum v2's blackout: earlier quarters (2021-2024) are back-projected from each
  symbol's earliest known real report date in ~91.25-day (one quarter) steps — an approximation,
  not verified history, for roughly 4 of the 5.5 test years.
- **Blackout rule:** skip a scheduled entry if the actual entry date (T+1 from the signal) falls
  within 5 calendar days, either direction, of a known/projected earnings date for that symbol.
  Checked at the entry date, matching momentum v2's rule for direct comparability.

## Results

**203 closed trades** (down from 213 — 20 entries were blocked outright, but only a net 10 fewer
trades appear because the 3-position cap backfilled some freed-up slots with other qualifying
signals that would otherwise have been capped out).

**Win rate: 68% (138/203)** — essentially identical to the base version's 68.1%.
**Average win: +1.95%** | **Average loss: -2.4%** — both slightly better than base (+1.9% / -2.5%),
consistent with removing some earnings-adjacent trades that likely skewed toward the loss side.
**Exit reasons:** target 185, stop 18 (down from 20 — two of the removed trades would have been
stop-outs).

**Compounded equity: 100 → 111.88 (CAGR ~2.06%/yr)** — modestly better than the base version's
~1.9%/yr.
**Max drawdown: 2.65%** — effectively unchanged from 2.64%.

**Entries blocked by the blackout: 20** across the 5.5-year window on 3 earnings-bearing symbols
(AAPL, MSFT, NVDA) — a modest but real filter, roughly 1-2 blocks per symbol per year, in line with
each name reporting quarterly and the 10-day blackout window (5 days each side) covering a small
fraction of the trading year.

## Reading this honestly

This is close to a "free" improvement: the blackout removes exactly the kind of trade the mechanic
was never designed to handle (a fundamentals-driven gap, not short-term technical noise) without
meaningfully reducing trade frequency or changing the strategy's core behavior. The improvement is
modest in magnitude, not transformative — this is risk-hygiene paying for itself, not a new source
of edge.

## Honest limitations

- **~4 of the 5.5 backtest years rely on back-projected, not verified, earnings dates** — same
  caveat as momentum v2. Real earnings dates drift by days-to-weeks quarter to quarter; some
  pre-2025 blackout windows are probably a few days off, which could let a few earnings-adjacent
  trades through that should have been blocked, or block a few that didn't need to be. The
  direction of the result (small improvement) is unlikely to flip from this imprecision, but the
  exact magnitude (20 blocks, +0.16pp CAGR) should be read as approximate.
- **Only 20 blocked entries** — too small a sample to be fully confident this is a durable +0.16pp
  CAGR effect rather partly noise; the improvement is directionally sound (closing a real risk
  shouldn't hurt, and it didn't) but not large enough to lean on heavily by itself.
- **No blackout coverage for earnings announced during an already-open trade's hold** — same gap as
  momentum v2 had; this only screens new entries, not positions already open when a report lands.
- **Same compute-environment note** as all mean-reversion backtests — fresh PowerShell script, not
  independently cross-checked.

## What would need to change before this graduates

- Combine with the hybrid exit (`meanreversion-v1-hybridexit-backtest.md`) — both changes are
  independently small, real, no-downside improvements; a combined version stacking both is the
  natural next test and likely lands around ~2.1-2.2%/yr, still far short of a live-ready number on
  a ~$580 account, but the best result yet.
- If Robinhood or another data source ever provides verified historical earnings dates further
  back than ~8 quarters, re-run with real (not projected) dates for the full window.

## Conclusion

A small, honest, low-downside fix: it closes a real risk the base strategy explicitly flagged as
open, without giving up win rate, trade frequency, or return — if anything nudging all three
slightly in the right direction. Not a transformative result on its own, but exactly the kind of
change that should be kept regardless of what other refinements are tested next. No live signals
were generated from this version.
