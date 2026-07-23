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

## Urgent finding — 2026-07-23

The live storefront (custom domain **ridgewoodequipment.store**) displays a testimonials section
claiming **"Rated 4.9/5 by 5,000+ Happy Customers"** with ~15 named "Verified Purchase" reviews.
The store has **0 orders and $0 revenue, ever**, per Shopify's own Analytics/Growth data. These
reviews are fabricated — almost certainly boilerplate shipped by the dropshipping theme/app and
never removed. This is a real legal/policy problem, not a cosmetic one: the FTC's 2024 rule against
fake reviews carries real penalties, and Shopify's own policies prohibit deceptive claims — this
gets more dangerous the more traffic the store gets, not less. **Recommended: remove this section
immediately**, before any traffic/growth push. Flagged to Austin directly rather than queued,
given urgency — see chat.

## Growth diagnosis — 2026-07-23

Checked Shopify's Growth/Analytics tabs directly: **0 marketing running**. Last 30 days' 14
sessions break down as 12 Direct + 2 Organic (Google) — no ads, no email, no social campaigns,
$0 attributed to marketing. This is a traffic problem, not (primarily) a conversion problem — 14
monthly visits is roughly nobody, and no amount of page optimization fixes zero real visitors.
Shopify is currently pushing a waitlist for "Campaign Autopilot" (early access) — worth considering
once real budget is on the table, but not a substitute for a deliberate plan.

Secondary factors once traffic exists: some products ("Adventure Ready Tactical Axe," knives) are
the kind of listing that gets rejected or restricted by Meta/Google ad policy for weapons-adjacent
content — worth knowing before planning paid social. The catalog is also generic AliExpress-style
dropship gear identical to thousands of other "StorePilot"-built stores — real differentiation
(a narrower niche, real brand voice, actual customer proof once it exists) matters more here than
in a more defensible niche.

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
