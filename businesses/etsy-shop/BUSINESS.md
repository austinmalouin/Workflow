# Etsy Shop — SteadyLedgerPrints

**Agent**: `etsy-agent` | **Skill**: `etsy-ops` | **Status**: active | **Shop**: [steadyledgerprints.etsy.com](https://steadyledgerprints.etsy.com)

## What this is

Austin's Etsy store, "Steady Ledger Co." Goal: automate, operate, manage, advance, and market it —
full ownership of the storefront's growth, not just occasional help.

## Shop profile (pulled directly from the live shop, 2026-07-22)

- **Niche**: undated, printable budget & debt-payoff planners — digital downloads (PDF, US Letter
  & A4), print-at-home, reusable.
- **Sub-lines**: Budget (weekly/monthly/annual planners), Debt Payoff (snowball trackers, visual
  thermometers), Savings (goal trackers, sinking funds). A distinct thread: several listings are
  framed for ADHD/neurodivergent budgeting ("No-Shame Weekly Budget Check-In," "ADHD Debt Payoff
  Kit") — this is a real differentiator worth leaning into, not incidental.
- **Fulfillment**: instant digital download, zero production/shipping cost per sale.
- **Location**: North Carolina, US.
- **Status on Etsy**: New shop, opened 2026. 10 active listings + 1 draft not yet published
  ("ADHD Reset Routine & No-Shame Cleaning Kit"), 0 sales, 0 reviews yet.
- **Pricing**: everything currently at an intro 40%-off sale price, ranging $0.75 (single
  checklist) to $7.20 (Debt-Free Starter Kit bundle); original prices $1.25–$12.

## Stats check — 2026-07-23 (month to date, Jul 1–23)

- **19 visits, 0 orders, 0% conversion, $0.00 revenue** — no change in sales since shop opened.
- **1 abandoned cart** this month — first real buyer-intent signal, no purchase yet.
- Only **6 total listing views** across all visits (0.32 views/visit) — most visitors aren't
  clicking into any listing at all. Most-viewed: Savings Goal Tracker (5 views), Debt-Free Starter
  Kit (1 view). The other 8 listings got zero views this month.
- **Traffic mix**: Etsy search sent **0** visits — everything came from Etsy app/other Etsy pages
  (7), Etsy marketing/SEO (3), and direct/other traffic (8, largely Austin/testing likely). Zero
  search visits for a shop with 10 SEO-able listings is the single most concerning number here —
  worth an SEO/tag audit before anything else.

## Current listings (10 active)

| Listing | Sale price | Original |
|---|---|---|
| Payday Checklist Printable — 5-Minute Money Routine | $0.75 | $1.25 |
| ADHD Debt Payoff Kit — Visual Debt Thermometer + Impulse Spend Log | $3.00 | $5.00 |
| No-Shame Weekly Budget Check-In (ADHD/neurodivergent) | $2.40 | $4.00 |
| Annual Budget Overview — 12-Month Planner | $3.30 | $5.50 |
| Sinking Fund Tracker — Cash Envelope System | $2.40 | $4.00 |
| Debt-Free Starter Kit (Budget + Snowball + Savings bundle) | $7.20 | $12.00 |
| Monthly Bill Tracker — Undated Payment Organizer | $2.10 | $3.50 |
| Savings Goal Tracker — Visual Savings Challenge | $2.10 | $3.50 |
| Debt Snowball Tracker — Payoff Planner | $2.70 | $4.50 |
| Weekly Budget Planner — Undated Financial Tracker | $2.70 | $4.50 |

## Goals (proposed — confirm/adjust with Austin)

- First sale, then first 10 reviews — a 0-sale/0-review shop's biggest lever right now is proof
  of quality, not more listings.
- Expand the ADHD/neurodivergent-finance angle — it's differentiated and underserved relative to
  generic budget-planner listings, which are extremely saturated on Etsy.
- Get all 10 listings SEO-checked (titles/tags) since none have sales data yet to validate current
  keyword choices.

## Current state

Real shop, freshly launched, pre-revenue. No open questions blocking work — `etsy-agent` should
re-check the live shop via browser whenever it needs current state rather than asking Austin to
repeat it here.

## How the agent works today

No Etsy API/MCP connector is available yet (checked 2026-07-22). Until one exists, `etsy-agent`:
- Uses the Claude in Chrome browser tools to check the live shop/Shop Manager directly for
  current state (listings, prices, sales) instead of asking Austin — see `etsy-ops` skill.
- Researches keywords/trends/competitors via web search.
- Drafts listing titles, tags, descriptions, and pricing into `listings/`.
- Briefs Canva for mockups/thumbnails.
- Leaves finished drafts in `inbox/` for Austin to paste into Etsy directly (or, once comfortable,
  pastes them in directly via the browser — confirm with Austin before publishing anything live).

Ask to search `mcp-registry` periodically for a real Etsy connector.

## Working folders

- `listings/` — drafted/researched listing content, organized by product or batch
- `marketing/` — social/promo copy, seasonal campaign plans
- `finance/` — cost/pricing notes (real bookkeeping lives with `finance-agent` once QuickBooks is authorized)
- `inbox/` — anything ready for Austin to review/paste/post
