# Backtest: Momentum v2 (Confirmed, Cost-Aware Daily-Swing Breakout)

**Date run:** 2026-07-23 **Strategy doc:** `../strategies/momentum-v2.md` **Prior version:**
`momentum-v1-backtest.md`

## Verdict up front

**Still not graduating to live signals — and by the headline number, worse than v1, not better.**
Adding realistic slippage, an earnings blackout, and a stricter breakout confirmation is exactly
what v1's own "what would need to change" list asked for, and it worked as a filter: win rate
improved (38% -> 42.9%) and modeled max drawdown fell (4.4% -> 3.0%), but the compounded return
over the same 5.5-year window dropped from a already-weak ~6.5% total (~1.2%/yr) to **~2.5% total
(~0.45%/yr)** — a smaller number, not a bigger one. That is the honest result of taking the costs
seriously: a meaningful slice of v1's raw edge was the part most likely to be fees, slippage, and
false breakouts, and v2 shows what's left once that's stripped out. What's left is still barely
above doing nothing, on a much smaller sample (63 trades vs. 100). No live signals were generated
from this version either.

## Methodology

- **Universe:** same 10 symbols as v1 — AAPL, MSFT, NVDA, AMZN, GOOGL, META, TSLA, AMD, SPY, QQQ.
- **Period:** 2021-01-04 through 2026-07-21, matching v1 (data was pulled from 2020-10-01 to give
  indicators a warm-up window; the ~3 trades that would have entered before 2021-01-04 were
  excluded from the reported stats below so the two backtests cover the identical window).
- **Data source:** `get_equity_historicals`, daily bars, split-adjusted. Fetched per-symbol
  (1,456 daily bars each) rather than in one combined call — the combined response exceeded the
  tool's output size limit.
- **Indicators:** SMA20/SMA50 (simple), EMA10 (standard exponential, SMA-seeded), RSI14 (Wilder
  smoothing), 20-day volume average, 20-day closing-price Donchian channel — all computed
  identically to v1's implementation.
- **Execution engine:** a single chronological day-by-day simulation across all 10 symbols
  together (not per-symbol in isolation), because the position cap requires a shared, real-time
  count of open positions. Each day: (1) resolve exits for open positions, (2) resolve breakout
  confirmations due that day, (3) open any entries scheduled for that day (subject to the cap and
  earnings blackout), (4) scan for brand-new signals. This ordering means a position that closes
  today can free a slot that a new entry uses later the same day, which is the realistic reading of
  "3 concurrent positions."
- **Slippage:** entries 0.2% worse than the modeled open; target exits 0.1% worse than target;
  trailing/time exits 0.2% worse than their reference price; **stop-loss exits 0.3% worse** than the
  stop price (worst of the four, reflecting that stops fire in the fastest-moving, least favorable
  conditions). All within the 0.1-0.3% range specified for this revision, with stops deliberately
  at the high end.
- **Earnings blackout:** 5 calendar days each side of a known/projected earnings date, checked at
  the scheduled entry date. Real report dates came from `get_earnings_results` (trailing ~8
  quarters per symbol, so real/verified from ~2025-01 onward); 2021-2024 dates are back-projected
  in ~91.25-day steps from each symbol's earliest known real date — a documented approximation, not
  verified history (see limitations). SPY/QQQ have no earnings and were never blacked out.
- **Breakout confirmation:** entry deferred from T+1 (v1) to T+2, gated on day T+1's close holding
  at or above the level broken on day T.
- **Position cap:** hard-gated in the simulation — an entry whose day arrives while 3 positions are
  already open is skipped outright, not deferred or queued.
- **Position sizing in the equity curve:** identical formula to v1 — `min(10% of running equity,
  1% of running equity / that trade's actual stop-loss %)` — computed per trade from its own actual
  entry/stop prices (not a flat assumption), applied sequentially by entry date, single hypothetical
  account, start value 100.
- **Ambiguity rule:** same as v1 — if a day's range would touch both stop and target, the stop is
  assumed to trigger first (conservative, not a fact about real intraday sequencing).

## Results

**Sample size: 63 closed trades** across the 10 symbols, 2021-01 through 2026-06 (down from v1's
100 — the confirmation requirement and earnings blackout both remove trades that v1 would have
taken).

| Symbol | Trades |
|---|---|
| AAPL | 7 |
| AMD | 9 |
| AMZN | 10 |
| GOOGL | 8 |
| META | 4 |
| MSFT | 7 |
| NVDA | 8 |
| QQQ | 2 |
| SPY | 3 |
| TSLA | 5 |

QQQ (2 trades) and SPY (3 trades) are, if anything, thinner than in v1 — still not individually
meaningful; the aggregate leans on the single-stock trades, same caveat as v1.

**Win rate: 42.9% (27 wins / 36 losses)**
**Average win: +5.36%** | **Average loss: -3.30%**
**Per-trade expectancy (net of modeled slippage): ≈ +0.42%** (0.429 x 5.36 − 0.571 x 3.30)
**Approx. profit factor: ≈ 1.22** (down from v1's ~1.38 — expected, since v1's expectancy was
computed with zero transaction costs and v2's is not)

**Exit reason breakdown:**
- Stopped out: 36 trades (57% of trades — same proportion as v1, average loss -3.05% before
  counting a few break-even-ish time exits elsewhere)
- Target hit (+10%): 12 trades, average return when it hit target-side: +9.89% (near the nominal
  +10% target, less the 0.1% target slippage)
- Trailing (momentum-failure) exit: 5 trades, average +0.08% — essentially break-even, consistent
  with "gave back the move before hitting target but still exited near flat"
- Time stop (15 trading days): 10 trades, average +1.46%

**Signal pipeline (full simulated range, including the few pre-2021 warm-up trades excluded from
the stats above):** 116 raw breakout signals detected -> 17 failed the next-day hold-through
confirmation and were cancelled -> 99 confirmed -> 33 blocked by the earnings blackout -> 0 blocked
by the position cap -> 66 entered (63 of which fall inside the reported 2021-2026 window).

**The position cap never actually bound in this data** — concurrent open positions never reached 3
at the moment a new entry was due, so the cap-enforcement fix (item 2 of the assignment) is real
and correctly wired into the simulation, but this particular 10-symbol universe and signal
frequency didn't generate enough overlap to test it under stress. That's a fact about this sample,
not a claim that concurrency risk is a non-issue — a bigger universe or a more sensitive strategy
would be expected to hit the cap more often.

**Compounded equity curve** (start = 100, sizing per trade's own risk-based formula, sequential by
entry date): **final value ≈ 102.5 — a ~2.5% total return over 5.5 years (~0.45%/year
annualized).** **Max drawdown ≈ 3.0%.**

## v1 vs. v2, side by side

| Metric | v1 | v2 |
|---|---|---|
| Sample size | 100 trades | 63 trades |
| Win rate | 38% | 42.9% |
| Avg win | +6.17% | +5.36% |
| Avg loss | -2.74% | -3.30% |
| Per-trade expectancy | +0.65% (**no costs modeled**) | +0.42% (**net of slippage**) |
| Profit factor | ~1.38 | ~1.22 |
| Compounded return (5.5y) | +6.5% | +2.5% |
| Annualized | ~1.2%/yr | ~0.45%/yr |
| Max drawdown | 4.4% (position cap **not** enforced) | 3.0% (position cap enforced, but never actually triggered) |
| Position-count cap | Aspirational only — equity curve let unlimited concurrent trades stack | Actually gates entries in the simulation |
| Breakout confirmation | Same-day close only | Requires next-day close to hold the level, entry pushed to T+2 |
| Earnings blackout | Not modeled | 5-day blackout around known/projected earnings |
| Slippage/spread | Not modeled | 0.1-0.3% worse fills, stops worst |

Reading this table straight: v2 is the more honest number, and the honest number is smaller. The
higher win rate and lower drawdown are real improvements in *risk-adjusted* terms, but the strategy
makes less money, on fewer trades, than v1 did — because v1's headline return was partly built on
costs and false-breakout noise that v2 correctly removes.

## Honest limitations (carried over or new)

- **Earnings blackout dates are mostly projected, not historical**, for 2021-2024 (~4 of the 5.5
  years). Real earnings-date drift (a company reporting a week earlier or later than a strict
  91-day cadence) means some pre-2025 blackout windows are probably a few days off in either
  direction. This could let a small number of earnings-adjacent trades through that should have
  been blocked, or block a few that didn't need to be — the net effect on the results above is
  unknown and not something this backtest can bound without real historical earnings-calendar
  access.
- **Breakout-hold confirmation is still closing-price only.** Requiring T+1's close to hold above
  the T breakout level is a meaningfully stronger filter than v1's same-day check (it did cancel 17
  of 116 raw signals, ~15%), but it is not true intraday confirmation — a level could be broken,
  breached back below, and recovered by the close on T+1, and this method would still call it
  "held." Daily bars cannot resolve this; it would take intraday data to do better.
- **Position cap validated in code, not in stress.** As noted above, concurrency never reached 3 in
  this sample, so the fix is correctly implemented but effectively untested against the exact
  failure mode (correlated drawdowns across simultaneously-open positions) that motivated it. A
  larger universe or a looser signal (more trades/year) would exercise this more.
- **Same-day stop/target ambiguity still resolved conservatively (stop-first)** without intraday
  bars to confirm, same caveat as v1.
- **No commission modeling** (still immaterial — Robinhood equities are commission-free).
- **Small per-symbol samples for QQQ (2) and SPY (3)** — thinner than v1's already-thin 3-and-3,
  not individually meaningful.
- **63 trades over 5.5 years is a modest sample**, smaller than v1's already-modest 100 — the
  confirmation and blackout filters that improved the win rate also shrank the evidence base for
  trusting that win rate. A higher win rate on fewer trades is not obviously more reliable than a
  lower win rate on more trades; both are within range of noise for a system this size.
- **Real account check (2026-07-23):** total value $579.59, cash $59.28 — essentially unchanged
  from the $584.61 on file when v1 was tested. The sizing/cap mismatch flagged in v1 (this account
  can't actually fund 3 concurrent positions at 10%-of-equity sizing) is unchanged and still
  applies here.

## Conclusion

The v2 revision did what it was supposed to do: it replaced v1's unrealistic assumptions
(free fills, same-day-only breakout confirmation, no earnings risk, an uncapped equity curve) with
more defensible ones, and the strategy's paper edge shrank in response — from an already-marginal
~1.2%/year to ~0.45%/year, on a smaller, still-thin sample. That is the expected and correct
direction for a real fix to move the numbers; it is also the reason this version does not clear the
bar for live signals any better than v1 did. Per the trading-research standard (backtest documented
*and* genuinely sound before signals get generated) — this one still isn't sound. No live signals
were written from this version of the strategy.
