# Shopify Store — RIDGEWOOD

**Agent**: `shopify-agent` | **Skill**: `shopify-ops` | **Status**: active | **Admin**: [admin.shopify.com/store/mp3uez-hq](https://admin.shopify.com/store/mp3uez-hq)

## What this is

Austin's Shopify store, "RIDGEWOOD." Goal: market, run, operate, and generate revenue from the
whole storefront — merchandising, campaigns, and growth, end to end.

## Store profile (pulled directly from Shopify admin, 2026-07-22)

- **Niche**: outdoor/camping/survival adventure gear — flashlights, knives, whistles, hammocks,
  backpacks, camp lighting, cutlery/dining sets, tactical/EDC gear. 30 of 31 products are
  dropshipped through an app called **StorePilot** (inventory not tracked, vendor "StorePilot").
- **One outlier product**: "Superbloom - Sweet Lemon Oolong Green Tea" — real vendor (August
  Uncommon Tea), 743 units actually in stock across 3 variants. This is a genuinely different
  supply model (real inventory) sitting inside an otherwise pure-dropship catalog — worth deciding
  deliberately whether it belongs, since mixing outdoor gear and specialty tea under one brand is
  an odd fit unless there's a reason (e.g. "trail tea," camp-brew angle).
- **Sales channels enabled**: Online Store, Agentic (Shopify's agentic-commerce channel — already
  on), TikTok, Collective.
- **Status**: brand new, pre-revenue. Last 30 days: 14 sessions, $0 total sales, 0 orders, 0%
  conversion, $0.00 next payout. All 31 products show Active status.

## Goals (proposed — confirm/adjust with Austin)

- Decide the brand identity question first: is this a focused outdoor/survival gear store (drop
  the tea SKU or spin it out separately), or intentionally broader? A 31-SKU catalog with no
  sales yet benefits more from a tight, credible niche than breadth.
- Get the first sale — 14 sessions with $0 sales over 30 days suggests either no real traffic yet
  or a conversion problem (untracked inventory badges, no reviews, generic dropship product pages
  are common culprits) — worth an actual page-by-page audit rather than assuming it's a traffic
  problem.
- The "Agentic" sales channel being already enabled is worth understanding/using deliberately —
  confirm what it's currently configured to do.

## Current state

Real store, freshly launched, pre-revenue. No open questions blocking work — `shopify-agent`
should check the live admin via browser whenever it needs current state rather than asking Austin
to repeat it here.

## How the agent works today

No Shopify API/MCP connector is available yet (checked 2026-07-22). Until one exists,
`shopify-agent` has direct browser access to the live admin (admin.shopify.com/store/mp3uez-hq)
via Claude in Chrome — it reads current state itself and, once Austin approves a specific change,
can go make it directly in admin rather than requiring manual paste-in.

## Working folders

- `products/` — product page copy, collection/merchandising plans
- `marketing/` — campaign plans, ad copy drafts, email sequences
- `finance/` — margin/cost notes (real bookkeeping lives with `finance-agent` once QuickBooks is authorized)
- `inbox/` — anything ready for Austin to review/approve
