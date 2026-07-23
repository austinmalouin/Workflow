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

**SEO audit completed 2026-07-22** (per Austin's request, ahead of the zero-search-traffic
problem). Pulled actual title/tags for all 10 active listings directly from Shop Manager (not
guessed) and did keyword research on current Etsy demand in this niche. Key findings:

- 6 of 10 listings already use all 13 available tags; **Payday Checklist Printable was only using
  7/13** (biggest single gap found); **No-Shame Weekly Budget Check-In was at 12/13** (one empty
  slot).
- No listing anywhere in the shop uses "cash stuffing" — confirmed via research to be a currently
  hot, fast-growing search term tightly matched to the Sinking Fund Tracker and Savings Goal
  Tracker products.
- The ADHD-specific listings (ADHD Debt Payoff Kit, No-Shame Weekly Budget Check-In) are the
  best-optimized mechanically but were missing validated emotional-intent phrases ("shame-free,"
  "gentle finance") that competing ranking listings in this sub-niche actually use.
- Full research-backed revisions (new title + 13-tag set + meta description each) were drafted for
  the 6 highest-leverage listings, prioritized by sales potential, in
  `businesses/etsy-shop/listings/`:
  `debt-free-starter-kit-seo-revision.md`, `adhd-debt-payoff-kit-seo-revision.md`,
  `no-shame-weekly-budget-checkin-seo-revision.md`, `payday-checklist-seo-revision.md`,
  `sinking-fund-tracker-seo-revision.md`, `savings-goal-tracker-seo-revision.md`. The remaining 4
  listings (Annual Budget Overview, Monthly Bill Tracker, Debt Snowball Tracker, Weekly Budget
  Planner) already use all 13 tags with reasonable keyword coverage and were judged lower priority
  — not revised this round.
- The unpublished draft ("ADHD Reset Routine & No-Shame Cleaning Kit") turned out to already have
  a complete title/tags/description/price — contrary to the original assumption. The real blockers
  are structural: **it's configured as a "Physical item" instead of "Digital files"** (wrong
  shipping/returns flow), it has **no digital file attached** and **no photos/video uploaded**, and
  its description has a **branding inconsistency** ("Solera Palms" instead of the shop's actual
  name) that needs fixing before publish. Full pre-publish checklist in
  `businesses/etsy-shop/listings/adhd-reset-routine-draft.md`.
- Nothing was changed live — all of the above is drafted for Austin's review per the
  approval-queue/draft-and-recommend model.

**All 6 SEO revisions published live 2026-07-23** (Austin approved). Debt-Free Starter Kit,
ADHD Debt Payoff Kit, No-Shame Weekly Budget Check-In, Payday Checklist, Sinking Fund Tracker, and
Savings Goal Tracker all now carry the researched titles/tags on the live shop — "cash stuffing"
added to the two savings listings, Payday Checklist went from 7/13 to 13/13 tags, and the
shame-free/gentle-finance emotional-intent language is live on the ADHD listings. One deviation
from the draft: the Savings Goal Tracker title couldn't use "&" twice (Etsy validation) — used
"and" for the added phrase instead, keeping the pre-existing "US Letter & A4" ampersand. The ADHD
Reset Routine draft (missing digital file, photos, wrong item type) is still unpublished — Austin
hasn't actioned that checklist yet.

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
