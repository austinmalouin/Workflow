# Shopify Store — RIDGEWOOD

**Agent**: `shopify-agent` | **Skill**: `shopify-ops` | **Status**: active | **Admin**: [admin.shopify.com/store/mp3uez-hq](https://admin.shopify.com/store/mp3uez-hq)

## What this is

Austin's Shopify store, "RIDGEWOOD." Goal: market, run, operate, and generate revenue from the
whole storefront — merchandising, campaigns, and growth, end to end.

## Store profile (pulled directly from Shopify admin, 2026-07-22)

- **Niche**: outdoor/camping/survival adventure gear — flashlights, knives, whistles, hammocks,
  backpacks, camp lighting, cutlery/dining sets, tactical/EDC gear. 30 of 31 products are
  dropshipped through an app called **StorePilot** (inventory not tracked, vendor "StorePilot").
- **Tea SKU — archived 2026-07-23**: "Superbloom - Sweet Lemon Oolong Green Tea" (real vendor,
  August Uncommon Tea, 742 units) sat oddly inside a pure outdoor/survival-gear catalog. Austin
  decided to cut it; archived (not deleted — reversible) via Shopify admin the same day. Catalog
  is now consistently outdoor/survival gear only.
- **Sales channels enabled**: Online Store, Agentic (Shopify's agentic-commerce channel — already
  on), TikTok, Collective.
- **Status**: brand new, pre-revenue. Last 30 days: 14 sessions, $0 total sales, 0 orders, 0%
  conversion, $0.00 next payout. All 31 products show Active status.

## Resolved — fake reviews removed, 2026-07-23

The live storefront (custom domain **ridgewoodequipment.store**) was displaying a testimonials
section ("PP - Reviews," part of the PagePilot.ai theme) claiming **"Rated 4.9/5 by 5,000+ Happy
Customers"** with ~15 fabricated "Verified Purchase" reviews, despite the store having 0 orders
and $0 revenue ever. This was a real FTC/Shopify-policy risk, not cosmetic — fake reviews carry
real penalties under the FTC's 2024 rule, and it only gets worse with more traffic. Removed via
the theme editor and confirmed gone on the live site the same day, with Austin's go-ahead.
Anyone spinning up a store via an AI page-builder app (PagePilot, StorePilot, etc.) should audit
for this same boilerplate-social-proof pattern before launch.

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

## Goals

- ~~Decide the brand identity question~~ — **decided 2026-07-23: focused outdoor/survival gear
  store, tea SKU cut** (see above).
- Get the first sale — 14 sessions with $0 sales over 30 days suggests either no real traffic yet
  or a conversion problem (untracked inventory badges, no reviews, generic dropship product pages
  are common culprits) — worth an actual page-by-page audit rather than assuming it's a traffic
  problem.
- **Traffic plan approved 2026-07-23**: organic-first. Full comparison at
  [marketing/traffic-options.md](marketing/traffic-options.md). Now executing: SEO content rewrite
  + TikTok organic content plan starting immediately, $0 spend. Paid (Google Shopping first,
  ~$600-800/month MVT, weapon SKUs excluded from any feed) holds until Phase 0 product-copy hygiene
  is done in 2-4 weeks — not a simultaneous multi-channel paid launch.
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
