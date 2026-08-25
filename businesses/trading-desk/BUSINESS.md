# Trading Desk

**Agent**: `trading-agent` | **Skill**: `trading-research` | **Status**: active (research only)

## What this is

Oversight of Austin's trading activity via Robinhood Agentic (already connected from prior work —
"momentum" strategy referenced from an earlier session; re-derive/document it here rather than
assuming it still matches Austin's intent). Austin wants this "as automated as possible" with
day-trading bots.

## Hard rule — read this before touching anything here

**No agent in this workspace places, modifies, or cancels a live order. Ever, regardless of how
the request is phrased or how much prior approval was given.** `trading-agent`'s tool list is
*designed* to physically exclude `place_equity_order`, `place_option_order`,
`cancel_equity_order`, `cancel_option_order`, and `review_equity_order`. **Update 2026-08-21:** the
weekday cloud routine's actual session that day found those tools (and option/crypto equivalents)
present and loadable via `ToolSearch` on the `Robinhood_Agentic` connector, contradicting the
"tools aren't available to it" claim below and the routine's own hard-rule text — see
`journal/2026-08-21-check.md` for the detail. They were not called, and the routine's own
overriding instruction (never place/modify/cancel an order regardless of tool availability) was
followed — but the real backstop in this environment is that standing behavioral rule, not tool
absence, until Austin confirms otherwise. The agent's job stops at a written recommendation;
Austin places the trade himself in Robinhood.

This isn't a workaround-later restriction — unattended live-money execution bots are how small
accounts get wiped by a bad tick, a stale signal, or a regime change the strategy never saw
in backtesting. "Automated" here means the *research* is automated (scanning, signal generation,
backtesting), not the *execution*.

## Goals

- TBD with Austin: risk tolerance per trade, account size, preferred timeframe (scalp/day/swing),
  instruments (equities only, or options too), and how many signals/day is useful vs. noise.

## Current state

Robinhood Agentic account connected (798207098, "Agentic"; total value $579.59, cash $59.28 as of
2026-07-23; **total value $430.54, cash $0 / buying power $0 as of 2026-08-06**, total value
$435.58 as of 2026-08-19, total value $432.50 as of 2026-08-20, total value $435.96, cash/buying
power $0.11 as of 2026-08-25 (first non-zero reading since 2026-08-06, but not a functionally
different number) — see the 2026-08-06 update below for why).
Four documented/backtested strategy versions on file across
three distinct mechanics, all still short of the bar for live signals:

- `strategies/momentum-v1.md` / `backtests/momentum-v1-backtest.md` — daily breakout-chasing, 100
  trades, 38% win rate, ~1.2%/yr compounded, no slippage/earnings/cap modeling. Verdict:
  weak/marginal.
- `strategies/momentum-v2.md` / `backtests/momentum-v2-backtest.md` — same breakout mechanic, adds
  slippage, an earnings blackout, a stronger breakout-hold confirmation, and an actually-enforced
  3-position cap. 63 trades, 42.9% win rate, ~0.45%/yr compounded (lower than v1 — the added
  realism removed more return than it added). Verdict: still not sound; both versions run a 57%
  stop-out rate, evidence the breakout mechanic itself (not just missing cost realism) is the
  weak point.
- `strategies/meanreversion-v1.md` / `backtests/meanreversion-v1-backtest.md` — **genuinely
  different mechanic:** buy oversold dips inside a long-term uptrend (RSI2 < 10 above SMA200)
  instead of chasing breakouts. 213 trades, 5 symbols (SPY/QQQ/AAPL/MSFT/NVDA), **68.1% win rate**,
  ~1.9%/yr compounded, max drawdown 2.64% (vs. momentum's 3-4%), stop-out rate down to 9.4%.
  Verdict: most promising direction on file — confirms a different edge behaves very differently.
  **Widened-universe test (2026-07-23, `backtests/meanreversion-v1-wideuniverse-backtest.md`):**
  expanding to 15 symbols across 8 sectors made everything worse (CAGR 1.9%→0.47%, max drawdown
  2.64%→6.83%) — the position cap blocked 389 signals, clustered in known market-wide pullback
  months, and per-sector results show the edge is real in **Tech and broad-market ETFs only**;
  Financials, Consumer Discretionary, Consumer Staples, and Industrials each lost money on average
  running the identical rules. Sector diversification doesn't help this mechanic — a real risk-off
  move fires the signal everywhere at once regardless of sector.
  **Let-winners-run test (2026-07-23, `backtests/meanreversion-v1-letwinnersrun-backtest.md`):**
  replaced the fixed SMA5 exit with a trailing version on the same 5-symbol universe. Average win
  grew (+1.9%→+3.77%) as hoped, but win rate collapsed (68.1%→48.3%) and drawdown nearly tripled
  (2.64%→7.24%) — net CAGR came in *lower* (~1.9%→~1.55%/yr). Mechanism: only 52.5% of trades that
  confirmed a reversion still finished as winners; many gave back most of the bounce before the
  trail finally triggered.
  **Two follow-up fixes, both tested 2026-07-23, both small real improvements with no downside:**
  - Hybrid exit (`backtests/meanreversion-v1-hybridexit-backtest.md`): only trail a trade if it's
    already up 5%+ at confirmation, bank everything else immediately like the base version. Only
    9/213 trades qualified, 8 of them winners (avg ≈+8.6%, incl. NVDA +15.84%, AAPL +15.04%). Win
    rate/avg win/loss essentially unchanged from base; CAGR nudges up (~1.9%→~1.94%/yr), drawdown
    down slightly (2.64%→2.55%).
  - Earnings blackout (`backtests/meanreversion-v1-earningsblackout-backtest.md`): 5-day blackout
    around AAPL/MSFT/NVDA earnings (SPY/QQQ exempt), same data/methodology as momentum v2. Blocked
    20 entries; win rate held (68.1%→68%), CAGR improved (~1.9%→~2.06%/yr), drawdown flat
    (2.64%→2.65%). Close to a free improvement — removes exactly the trade type the mechanic was
    never designed to handle.
  **Combined version (2026-07-23, `backtests/meanreversion-v1-combined-backtest.md`):** both fixes
  stacked cleanly, no negative interaction — 203 trades, 67.5% win rate, **CAGR ~2.09%/yr** (best on
  file), max drawdown 2.55%. Still short of the live-signal bar: 5-symbol/5.5-year sample is thin,
  every backtest on this desk has been run by the same single implementation (no independent
  re-check yet), and ~2%/yr on a ~$580 account is a small number in dollar terms regardless of
  whether the backtest holds up — "sound" and "worth doing at this account size" are separate
  questions worth discussing directly with Austin before pursuing this further.
- `strategies/rotation-v1.md` / `backtests/rotation-v1-backtest.md` — **also genuinely different:**
  monthly dual-momentum rotation across SPY/EFA/cash (no single-stock signals at all). 23.4-year
  backtest: 7.7%/yr, max drawdown 24.56% vs. buy-and-hold SPY's 52.2% — real crash-avoidance (sat
  out most of 2008 and 2022) but doesn't beat simple buy-and-hold SPY (9.67%/yr) on this bull-
  dominated window. Verdict: not a signal-generating edge for this desk's goals, but worth keeping
  on file as a possible lower-maintenance capital-preservation option, separate from "live
  signals."

No live signals have been generated from any version.

## Account-size reality check (2026-07-23)

Before pursuing further technical refinement, a spot-check and a plain dollar-economics review,
because "the backtest is sound" and "this is worth doing at this account size" are different
questions:

**Spot-check on the combined backtest:** manually re-derived (from raw price data, not by
re-running the same script) the entry/exit math for one trade of each exit type — a trailing exit
(NVDA 2021-08-19→09-01, +14.88%), a stop-loss (QQQ 2021-02-22→23, -6.28%, confirmed the day's
actual low of $311.00 did breach the computed stop level of $311.78), and an ordinary target exit
(AAPL 2021-01-05→08, +2.34%). All three matched the backtest's recorded numbers exactly. This is a
partial check (3 trades, hand-verified arithmetic against raw bars), not a full independent
re-implementation — it rules out an arithmetic or slippage-application bug in the sample checked,
it does not rule out a shared design flaw (e.g. look-ahead bias) that would affect every trade
identically and every version tested on this desk equally, since all of them were written by the
same process in the same session.

**The dollar math, plainly:** ~2.09%/yr CAGR on the current $579.59 account is **≈$12/year** —
before any real-world friction beyond what's modeled (partial fills, real-world slippage worse than
assumed, tax treatment of short-term gains). To turn this exact edge into $500/year would take
about **$23,900** in capital; $1,200/year (~$100/month) would take about **$57,400**. At this
CAGR, the account would take about **34 years** to double. None of this is a knock on the backtest
work — it's a statement about what a ~2%/year edge is worth at this scale, which no amount of
further strategy refinement changes. Separately, **cash is the binding constraint today regardless
of the strategy**: $59.28 free cash means one 10%-of-equity position (~$58) consumes nearly all of
it — the "3 concurrent positions" cap written into every version tested here has been aspirational
since the very first backtest and remains so.

**What this means going forward:** the technical research has been genuinely productive — a real,
if small, validated edge exists where none did at the start (momentum's dead end) — but growing
this account meaningfully was never going to come from strategy refinement at $580. The honest
options, for Austin to weigh (not decided here): (1) treat this as a research/skill-building line
rather than an income line — the automated weekday routine is cheap to keep running and the
strategy is in good shape for if/when more capital gets added; (2) if trading income actually
matters, the prerequisite is capital, not a better strategy — revisit at whatever account size
would make the payoff worth the ongoing attention; (3) reconsider whether the ~$520 already sitting
in legacy fractional positions (GLDM, QQQ, SPCX, MSFT) should just stay simple buy-and-hold rather
than being folded into an active strategy, since none of this research was built around them.

**Update 2026-07-23 — Austin's decision:** can't add capital for a few weeks, wants to start now
with the current ~$600 anyway, explicitly accepting the thin-edge/small-dollar picture above.
Manually checked all 5 symbols against the combined strategy's live entry rule that day — none
qualified (SPY/QQQ/AAPL not oversold, MSFT below its SMA200 so ineligible regardless, NVDA
overbought) — no signal was invented to have something to act on. Going forward:
`business-hq-trading-research` (the weekday cloud routine) is now instructed to write a dated
signal to `signals/` whenever the combined strategy's entry rule genuinely fires, using real data
each run, and to skip writing anything on days nothing qualifies rather than force a signal. Every
signal it writes must still say explicitly that it's a recommendation only — Austin places any
resulting trade himself in Robinhood; no agent here has an order-placement tool, regardless of any
permission given in chat.

**First live signal (2026-07-28, `signals/2026-07-28-QQQ.md`):** QQQ — 6 straight down sessions
(708.97→675.49, -4.7%) while still well above its SMA200 (643.88), RSI(2)=3.5. Entry ~next open,
stop -6%, size 10% of equity (~$57.51). Austin already holds a separate legacy QQQ lot (0.38 shares
@ $709.83 avg cost) from before this research — this signal is an independent position under the
strategy's rules, not a management action on the existing lot; flagged to Austin as a fact about
total exposure, not advice on averaging down. Recommendation only, not executed. **Confirmed
2026-08-06: it stayed unexecuted** — the QQQ position on file is still the identical pre-signal
legacy lot (same quantity, same $709.83 avg cost), so this strategy has effectively produced zero
real trades to date.

**Update 2026-08-17 — both signals to date have actually resolved, by rule, on paper:** a
2026-08-17 check caught that neither prior signal's outcome had ever been tracked to completion.
QQQ (7/28) hit its target one trading day after entry (7/30 close $683.55 > SMA5 $677.42; exit at
the 7/31 open ≈$690.73, **+2.25%**) — this happened back on 7/31 and no journal entry ever recorded
it. AAPL (8/13) hit its target on 8/14 (close $305.93 > SMA5 $305.32, a thin margin; exit at the
8/17 open, roughly **+0.3%** after slippage). Neither was ever executed in the real account — both
remain paper-only, and the position cap has been at 0/3 real positions the whole time regardless.
**2 signals generated, 2 resolved, 2 wins** — directionally consistent with the backtest's 67.5%
win rate but far too small a sample to mean anything on its own. See
`journal/2026-08-17-check.md` for the full math on both.

**First entry-rule fire since 7/28 (2026-08-18, `signals/2026-08-18-MSFT.md`):** MSFT's RSI(2) hit
7.73 (deep oversold) on a sharp pullback from its 8/10 post-earnings high, while still well above
its SMA200 — a clean, unambiguous fire of the entry rule, clear of the earnings blackout (next
report 2026-10-28, 71 days out). Signal written per the standing rule. **But it can't actually be
acted on today:** cash and buying power are still $0 (see the 2026-08-06 note below — now 12
sessions unchanged), so even though the strategy produced a real signal on a real qualifying
symbol for the first time, there's nothing to size a position with. Worth raising directly with
Austin: is a cash deposit worth making now that the strategy has actually fired, or does this stay
a paper-only research line until/unless that changes?

**Second signal, MSFT still open (2026-08-19, `signals/2026-08-19-QQQ.md`):** QQQ's RSI(2) hit 9.94
(just inside the <10 threshold) on the 8/18 close after a sharp one-day drop (729.87→717.51,
-1.69%), still well above its SMA200 (651.51) — QQQ is ETF-exempt from the earnings blackout. SPY
(10.17) and NVDA (10.25) both sat just above the cutoff — no signal on either, this was close.
Checked the 8/18 MSFT signal for resolution: still open, no stop breach (low $477.15 vs. stop
≈$452.65), target not yet hit (close $481.63 still below SMA5 $489.34), time stop nowhere close (1
session elapsed of 10). **Two open paper signals now (MSFT 8/18, QQQ 8/19), occupying 2 of 3
strategy slots by convention — neither funded.** Cash/buying power still $0 (13 sessions unchanged;
see below). Full detail in `journal/2026-08-19-check.md`.

**Third signal, all 3 slots now filled on paper (2026-08-20, `signals/2026-08-20-NVDA.md`):**
NVDA's RSI(2) hit 5.98 on the 8/19 close — the deepest, cleanest oversold read this desk has
produced (deeper than MSFT's 7.73 or QQQ's 8.33/9.94), on a two-day drop (225.01→219.74→217.56)
while still well above its SMA200 (195.18). QQQ's RSI(2) also refired (8.33) but was skipped —
it already has an unresolved open signal from 8/19 and the strategy doesn't stack same-symbol
entries. **Earnings-blackout call worth flagging:** NVDA reports 2026-08-26 (pm, verified); entry
(8/20) is 6 calendar days out, just outside the 5-day blackout window — clears the rule, but close
enough that the position could still be open heading into the print. Checked both prior signals for
resolution: MSFT (8/18) still open, no stop breach (lows $477.15/$479.36 vs. stop ≈$452.65), target
not yet hit (SMA5 still above close both sessions); QQQ (8/19) still open, no stop breach (low
$712.61 vs. stop ≈$677.17), target not yet hit, only 1 session elapsed. **All 3 strategy slots are
now occupied on paper (MSFT, QQQ, NVDA) — 0 of 3 are actually funded.** Cash/buying power still $0
(14 sessions unchanged). The strategy has now fired on 3 straight trading days — signal generation
is clearly not the bottleneck anymore; cash is. Worth raising directly with Austin. Full detail in
`journal/2026-08-20-check.md`.

**2026-08-25 check (`journal/2026-08-25-check.md`):** no new entry — SPY/AAPL/MSFT/QQQ didn't
qualify on RSI(2), and NVDA hit its deepest oversold read yet (RSI(2) **0.48**, beating its own
8/21 record of 2.06) but is excluded, already carrying an open signal with no same-symbol stacking;
moot regardless since 2 of 3 slots are occupied. **MSFT (8/18) resolution confirmed final:** the
8/24 official open settled at $483.205, exit fill ≈$482.24 after slippage, entry $481.54 — **+0.15%
confirmed**, matching the prior provisional estimate almost exactly. QQQ (8/19) and NVDA (8/20)
remain open, both still within their stops — but **NVDA's stop buffer has narrowed to $1.86**, the
tightest of any open signal here, and **NVDA earnings are now only 1 trading session away** (reports
2026-08-26 pm, tomorrow evening) with the position still open. This is the sharpest version yet of
the standing "hold through the print or not" question flagged on 8/21 and 8/24 — worth a direct
decision from Austin before the report, even though no real capital is at risk (still unfunded).
Paper record now 3 signals resolved, 3 winners (QQQ 7/28 +2.25%, AAPL 8/13 +0.3%, MSFT 8/18 +0.15%
confirmed). Cash/buying power effectively still $0 ($0.11, first movement in 17 sessions but not
functionally different), total value $435.96, real P&L unchanged at -$75.72 all-time; no new real
trades. Full detail in the journal file.

**2026-08-24 check (`journal/2026-08-24-check.md`):** no new entry — SPY/AAPL/QQQ/MSFT didn't
qualify on RSI(2), and NVDA mathematically re-qualified with its deepest oversold read yet
(RSI(2) 2.06) but is excluded (already carrying an open signal, no same-symbol stacking); moot
regardless since the 3-slot cap was already full. **MSFT (8/18) resolved on paper — target hit:**
8/21 close ($483.24) closed back above its 5-day SMA ($482.14), the standard mean-reversion exit
condition, with no stop breach beforehand. Exit executes at today's open (0.2% worse); provisional
paper return using the pre-market reference ≈+0.15% (will confirm exact figure once today's open
settles). QQQ (8/19) and NVDA (8/20) remain open, both still within their stops, neither target hit.
**Paper record now 3 signals resolved, 3 winners** (QQQ 7/28 +2.25%, AAPL 8/13 +0.3%, MSFT 8/18
≈+0.15%) — directionally consistent with the 67.5% backtest win rate, still too small to mean
anything. **NVDA earnings flag escalating:** report is 2026-08-26 pm, now only 2 trading sessions
away, and the open NVDA signal is still unresolved — worth a direct decision from Austin before
8/26. Cash/buying power still $0 (16 sessions unchanged), total value $436.12, real P&L unchanged at
-$75.72 all-time; no new real trades. Full detail in the journal file.

**2026-08-21 check (`journal/2026-08-21-check.md`):** no new entry — SPY/AAPL didn't qualify on
RSI(2), and QQQ/NVDA both mathematically qualified again but are excluded (already carrying open
signals, no same-symbol stacking); moot regardless since all 3 slots are already full. All three
open signals (MSFT 8/18, QQQ 8/19, NVDA 8/20) remain unresolved — no stop breach, no target hit on
any. **NVDA earnings-proximity flag now live:** today is the date that signal's invalidation
conditions called out as "reconsider holding through the print" if still open — NVDA reports
2026-08-26 pm, 4 trading sessions out, and the position is still open on paper (no real risk today
since it was never funded, but worth a direct decision from Austin before 8/26 in case cash arrives
first). Cash/buying power still $0 (15 sessions unchanged), total value $436.13, real P&L unchanged
at -$75.72 all-time. **New safety note:** this run's tool catalog actually includes order-placement
tools (`place_equity_order` etc.) as loadable via `ToolSearch` on the `Robinhood_Agentic` connector,
contradicting the routine's documented assumption that no such tool exists in-session — none were
called, the standing behavioral rule was followed regardless, but the "tool is physically absent"
backstop this desk's docs describe does not currently hold in this environment. Worth confirming
with Austin whether that's expected. Full detail in the journal file.

**2026-08-06 check (`journal/2026-08-06-check.md`):** no signal — RSI(2) on all five symbols was
nowhere near the <10 oversold trigger as of the 2026-08-05 close (SPY 85.1, QQQ 70.2, AAPL 49.6,
MSFT 71.8, NVDA 97.5; MSFT/NVDA in fact deeply overbought). No file written, per the standing rule
against inventing a signal. Also pulled real account P&L for the honest comparison Austin asked
for: all-time realized -$75.72 (-15.66%), but every one of those four closed trades (SPCX, SOFI,
SMCI, IONQ) is pre-existing/manual activity outside this strategy's 5-symbol universe — none of
it is attributable to meanreversion-v1, and with the one signal produced so far never executed,
"is it tracking the backtest" still isn't a real question yet — there's no live strategy trade on
the books to check it against. **Same-day post-close recheck** (routine fired twice today; see
journal addendum) reconfirmed no signal — the indicator feed still hadn't posted a finalized
2026-08-06 daily bar as of ~90 minutes after close, so RSI/SMA readings were identical to the
morning check — and surfaced a new, more urgent fact: **account buying power is now $0** (cash
$0, unsettled funds $0, confirmed via `get_accounts`/`get_portfolio`), down from the $59.28 free
cash this whole live-signal plan was scoped around on 2026-07-23. Total account value is $430.54
(down from $579.59), driven by the same four pre-existing manual trades noted above realizing
-$75.72, not by anything this strategy did. **Practical implication: even on a day the entry rule
fires, there is currently no cash to size a position with under the 10%-of-equity rule.** This is
a capital-availability problem, not a strategy problem, and is worth a direct conversation with
Austin about whether to add cash, pause signal generation until cash is available, or keep
generating recommendations regardless (since they cost nothing to write and he may add funds
before acting on one).

## Working folders

- `strategies/` — written-out strategy rules (entry/exit criteria, position sizing, risk limits)
- `signals/` — dated trade-idea write-ups (symbol, thesis, entry/stop/target, confidence) —
  recommendations only, never executed automatically
- `backtests/` — backtest results/methodology for any strategy before it's trusted live
- `journal/` — trade log/outcomes, pulled read-only from `get_pnl_trade_history` / `get_realized_pnl`
  for reviewing what actually happened vs. what the strategy predicted
