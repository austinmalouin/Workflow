# Trading Desk

**Agent**: `trading-agent` | **Skill**: `trading-research` | **Status**: active (research only)

## What this is

Oversight of Austin's trading activity via Robinhood Agentic (already connected from prior work —
"momentum" strategy referenced from an earlier session; re-derive/document it here rather than
assuming it still matches Austin's intent). Austin wants this "as automated as possible" with
day-trading bots.

## Hard rule — read this before touching anything here

**No agent in this workspace places, modifies, or cancels a live order. Ever, regardless of how
the request is phrased or how much prior approval was given.** `trading-agent`'s tool list
physically excludes `place_equity_order`, `place_option_order`, `cancel_equity_order`,
`cancel_option_order`, and `review_equity_order` — this isn't just a prompt instruction, the
tools aren't available to it. The agent's job stops at a written recommendation; Austin places
the trade himself in Robinhood.

This isn't a workaround-later restriction — unattended live-money execution bots are how small
accounts get wiped by a bad tick, a stale signal, or a regime change the strategy never saw
in backtesting. "Automated" here means the *research* is automated (scanning, signal generation,
backtesting), not the *execution*.

## Goals

- TBD with Austin: risk tolerance per trade, account size, preferred timeframe (scalp/day/swing),
  instruments (equities only, or options too), and how many signals/day is useful vs. noise.

## Current state

Robinhood Agentic account connected (798207098, "Agentic"; total value $579.59, cash $59.28 as of
2026-07-23). Four documented/backtested strategy versions on file across three distinct mechanics,
all still short of the bar for live signals:

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
total exposure, not advice on averaging down. Recommendation only, not executed.

## Working folders

- `strategies/` — written-out strategy rules (entry/exit criteria, position sizing, risk limits)
- `signals/` — dated trade-idea write-ups (symbol, thesis, entry/stop/target, confidence) —
  recommendations only, never executed automatically
- `backtests/` — backtest results/methodology for any strategy before it's trusted live
- `journal/` — trade log/outcomes, pulled read-only from `get_pnl_trade_history` / `get_realized_pnl`
  for reviewing what actually happened vs. what the strategy predicted
