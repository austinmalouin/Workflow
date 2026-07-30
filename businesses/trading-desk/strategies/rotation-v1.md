# Rotation v1 — Dual-Momentum Asset Rotation (SPY / EFA / Cash)

**Status:** Documented and backtested (2026-07-23). **Backtest verdict: real drawdown control, but
does not beat simple buy-and-hold on absolute return over the tested window — see
`../backtests/rotation-v1-backtest.md`. Not sound for live signals.**

A second genuinely different mechanic tested alongside [`meanreversion-v1.md`](meanreversion-v1.md),
in response to the same direction: momentum v1/v2's breakout-chasing needed a different edge, not
another round of filters. This one is structurally the furthest from momentum of anything tested —
monthly decisions instead of daily, one asset class rotation instead of one-stock-at-a-time entries,
no stop-loss or trailing exit mechanics at all. Loosely based on the published "dual momentum" /
"GEM" (Global Equities Momentum) family of rotation strategies (Antonacci), simplified to use cash
instead of a bond leg — see "why cash instead of bonds" below.

## Timeframe

**Monthly rebalancing.** One decision per month, made at each month-end close, held until the next
month-end. This is the slowest-moving strategy on file for this desk — roughly 12 decisions/year
vs. momentum's dozens of signals/year and mean-reversion's ~40/year.

## Universe

**SPY** (US large-cap equities) and **EFA** (international developed-market equities) — two broad,
liquid, low-fee ETFs representing genuinely different (if still correlated) equity exposures,
plus **cash** as the explicit risk-off holding. This replaces momentum's 10-name universe of mostly
correlated US mega-cap tech + index ETFs, which the momentum backtests never actually achieved real
diversification with.

## Decision rule (evaluated at each month-end close, month M)

1. Compute the **trailing 12-month total price return** for SPY and EFA as of month M's close.
2. **Relative momentum:** whichever of SPY/EFA has the higher trailing 12-month return is the
   "winner" for that month.
3. **Absolute momentum filter:** if the winner's trailing 12-month return is positive, hold the
   winner for the next month (month M+1). If the winner's trailing 12-month return is **zero or
   negative, hold cash instead** — even though it "won" the relative comparison, a negative
   absolute return means the asset class itself is in a downtrend, not just relatively weaker than
   the alternative.
4. Rebalance at month M+1's open if the decision changed from the position already held; no trade
   if the decision is unchanged (holding the same asset, or staying in cash).

## Why cash instead of a bond leg

Classic dual-momentum designs (e.g. GEM) rotate into a bond ETF during risk-off periods rather than
sitting in cash, on the theory bonds usually gain when equities fall. This version deliberately
does **not** do that: `get_equity_historicals` only returns split-adjusted prices for interday bars
(dividend/coupon adjustment is intraday-only per the tool's own documentation), and a bond ETF's
return is dominated by its coupon/yield, not price appreciation — a price-only backtest would
badly understate a bond leg's real return, potentially by more than its entire price-return signal.
Rather than build a strategy around data the tool can't actually provide correctly, this version
uses cash (modeled at a flat 0% return, no interest credited) as the risk-off holding. This is
conservative for the strategy (real cash earns some interest) but does not introduce the systematic
downward bias a mismodeled bond leg would.

## Position sizing

**100% of account equity in the single held position** (or 100% cash) — there is only ever one
holding at a time by design, so the account-size/position-cap mismatch that constrained all three
momentum-family versions doesn't apply here. Both SPY and EFA support fractional shares on
Robinhood, so the ~$580 real account size is not a structural obstacle to running this strategy as
designed.

## Rebalancing costs

0.05% slippage/spread modeled per switch (tighter than momentum's 0.2-0.3%, reflecting that
SPY/EFA have much tighter bid-ask spreads than individual breakout/pullback entries in
faster-moving names) — charged only when the held position actually changes month to month.

## What this strategy does *not* do

- No stop-loss, trailing exit, or intra-month risk control of any kind — a position is held for the
  full month regardless of what happens intra-month (a repeat of a fast single-month crash, like
  March 2020, is absorbed in full before the next month's rebalance can react).
- No true GEM bond leg (see above) — this is a simplified two-asset-plus-cash variant, not a
  faithful reproduction of the published strategy.
- Only two equity legs (SPY, EFA) — a real GEM-style implementation often adds more asset classes
  (small-cap, emerging markets, REITs, commodities) to rotate among; this version deliberately kept
  it to two for a first, tractable test.
- No signal for *how much* momentum, only its sign and relative ranking — a marginal winner (SPY
  ahead of EFA by 0.1%) is treated identically to a decisive one (ahead by 20%).
