# Backtest: Mean-Reversion v1 — Let-Winners-Run Exit Variant

**Date run:** 2026-07-23 **Base strategy doc:** `../strategies/meanreversion-v1.md`
**Base backtest:** `meanreversion-v1-backtest.md` (5-symbol version, the confirmed-edge universe)

## Verdict up front

**Worse on every headline number, and the reason why is directly useful for the next test.**
Replacing the base version's fixed "exit on first close above SMA5" target with a trailing rule
("once confirmed above SMA5, ride until it closes back below SMA5") did what it was designed to
do — average win size nearly doubled (+1.9% → +3.77%) — but win rate collapsed (68.1% → 48.3%),
max drawdown nearly tripled (2.64% → 7.24%), and CAGR came in *lower* than the base version
(~1.9%/yr → ~1.55%/yr) despite the bigger average win. The trailing exit is too loose for this
setup: of 177 trades that reached the "confirmed" state, only 52.5% still finished as winners —
the rest gave back most or all of the bounce before closing back below SMA5 finally triggered the
exit, in a few cases losing almost as much as the hard stop would have (worst trail exits: -6.84%,
-6.47%, -5.93%) without ever tripping the actual stop-loss. No live signals were generated from
this version.

## Why this test was run

The base 68.1%-win backtest's single clearest weakness was the asymmetry between average win
(+1.9%) and average loss (-2.5%) — a high win rate carrying a thin per-trade edge. Two outlier
trades in that backtest (NVDA +18.32%, +12.02%) resolved via the fixed SMA5 target but kept running
well past it, suggesting the fixed shallow target might be cutting off real continuation moves
early. This test replaces that fixed target with a trailing exit to see if it captures more of
those moves without giving up too much of the win rate.

## What changed from the base version

Everything is identical to `meanreversion-v1-backtest.md` (same 5-symbol universe — SPY, QQQ,
AAPL, MSFT, NVDA; same entry rule; same 6% hard stop; same slippage assumptions; same position
sizing and 3-position cap) **except the exit mechanic**:

- **Base version:** exit at the next open the first time `Close(T) > SMA(5)`. One-shot, banks the
  bounce immediately.
- **This version:** track a `confirmed` flag per open position. The first time `Close(T) > SMA(5)`,
  the position is marked confirmed but **not exited** — it keeps riding. From that point forward,
  exit at the next open the first time `Close(T) < SMA(5)` again (a genuine trailing stop using the
  same short moving average, rather than a one-time crossing signal).
- **Time-stop extended 10 → 15 trading days**, since the position is now deliberately meant to be
  held longer if it keeps confirming above its trailing average.
- Stop-loss mechanic (intraday low touch, -6%, 0.3% slippage) is unchanged and still checked before
  the trailing-exit logic each day.

## Results

**201 closed trades** (down slightly from the base version's 213 — a few trades that would have
resolved separately under fixed exits now overlap differently under the trailing rule's timing,
and the position cap interacts slightly differently with longer average holding periods).

**Win rate: 48.3% (97/201)**, down sharply from 68.1%.
**Average win: +3.77%** | **Average loss: -2.68%** — the win/loss asymmetry did flip in the right
direction (unlike the base version, which had a bigger win rate but a much thinner average win).
**Average days held: 6.2** (up from a strategy that, in the base version, never once needed its
full 10-day time-stop).

**Exit reasons:**
- Trailing exit (confirmed, then closed back below SMA5): 177 trades, **only 52.5% winners**
  (93 wins / 84 losses-or-flat). Average winning trail exit +3.44%; average losing/giveback trail
  exit -1.82%.
- Stopped out: 20 trades (similar count to the base version's 20).
- Time stop (15 days): 4 trades (up from 0 in the base version — a few positions now genuinely ride
  long enough to hit the extended window).

**Compounded equity: 100 → 108.86 (CAGR ~1.55%/yr)** — lower than the base version's ~1.9%/yr.
**Max drawdown: 7.24%** — nearly triple the base version's 2.64%.

**Best and worst trailing exits**, for concrete texture:

| Best | Return | Days held |
|---|---|---|
| NVDA 2024-02-21→29 | +15.84% | 5 |
| NVDA 2026-05-04→18 | +15.72% | 9 |
| AAPL 2026-06-26→07-15 | +15.04% | 11 |
| NVDA 2024-10-02→16 | +14.60% | 9 |

| Worst | Return | Days held |
|---|---|---|
| AAPL 2021-05-03→11 | -6.84% | 5 |
| NVDA 2023-09-07→18 | -6.47% | 6 |
| NVDA 2021-05-04→11 | -5.93% | 4 |
| AAPL 2025-02-28→03-11 | -5.92% | 6 |

The upside case is real — four trades above +14%, versus the base version's best of +18.32% (a
single outlier) — but the downside case shows the actual mechanism problem: a position can confirm
(close above SMA5 once), then reverse hard over the following days, and by the time it closes back
below SMA5 to trigger the trailing exit, it has given back nearly as much as the hard stop would
have cost — without the hard stop (a fixed price level) ever being touched, because the reversal
happened gradually in closing-price terms rather than through a single sharp intraday move.

## Reading this honestly

The base version's fixed, immediate SMA5-cross exit wasn't a naive or lazy design — it was
implicitly doing real work: banking the reversion the moment it was confirmed, before the market
had a chance to take it back. A pure trailing rule removes that discipline entirely; it only exits
on weakness, so anything that confirms and then chops sideways-to-down for a few days bleeds back
most of its gain before the trail fires. The net effect: bigger winners, yes, but roughly half the
previously-reliable base-rate wins turned into flat-to-losing trades waiting for the trail to
finally catch up. This is a case where "let winners run" as a blanket rule works against a strategy
whose actual edge is in exiting quickly, not in riding trends — mean-reversion and trend-following
have different natural exit disciplines, and this test mixed the two by importing a trend-following-
style trailing exit onto a mean-reversion entry.

## Honest limitations

- **Only one trailing-exit design tested** (immediate trail on the same SMA5 used for entry
  confirmation) — a looser trailing MA (e.g., SMA10 or EMA10, matching momentum's trailing-exit
  precedent) or a percent-based trailing stop from the peak price might behave differently; this
  result doesn't rule those out.
- **No partial-profit-taking tested** — a hybrid (bank some of the position at the original SMA5
  target, let the remainder ride with a trailing stop) was not tested here and is a natural next
  step; see below.
- **Same window, same compute-environment caveats** as the base and wide-universe backtests — fresh
  PowerShell script, not independently cross-checked.
- **20 stop-outs, similar to the base version** — the hard stop's behavior is essentially unchanged
  by this test, as expected (it's checked identically in both versions).

## What would need to change before revisiting this direction

- **Test a threshold-gated hybrid**: keep the base version's immediate SMA5-cross exit as the
  default, but *only* switch to a trailing exit for trades already up some minimum amount (e.g.,
  +5% or more) by the time they first confirm — banking the ordinary small bounces immediately
  (as the base version does well) while giving the genuinely strong movers room to keep running.
  This directly targets the mechanism identified above: don't apply trend-following discipline to
  trades that haven't shown trend-following-caliber strength yet.
- Test a looser trailing reference (SMA10/EMA10) to see if it reduces the whipsaw-driven giveback
  on the 84 losing/flat trail exits without giving up as much of the upside capture.

## Conclusion

Letting winners run, applied uniformly to every confirmed trade, made this strategy worse — lower
CAGR, nearly triple the drawdown — despite successfully increasing average win size. The mechanism
is clear and instructive: this strategy's edge lives in exiting quickly on confirmation, and a
blanket trailing exit gives that discipline up on the majority of trades in exchange for outsized
gains on a minority. The direction isn't dead, but the design needs to be selective (hybrid,
threshold-gated) rather than universal. No live signals were generated from this version; the base
68.1%-win, 5-symbol version remains the best result on file to date.
