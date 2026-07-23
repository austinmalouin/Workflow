---
name: shopify-ops
description: Shopify store workflow - product pages, merchandising, campaign planning, and email drafts for businesses/shopify-store/. Use when working on Austin's Shopify store specifically.
---

# Shopify Ops

Workflow for `businesses/shopify-store/` (RIDGEWOOD — outdoor/camping/survival gear). Read
`BUSINESS.md` there first for niche/goals/state — then, if you need anything current (products,
orders, sessions, channels), check the live admin yourself via the browser tools rather than
treating `BUSINESS.md` as always up to date or asking Austin to re-report it.

## Product/merchandising

1. Research the category's current competitive landscape (WebSearch) before writing copy —
   pricing bands, common objections handled in competitor copy, what collection structures
   similar outdoor/survival-gear stores use.
2. Draft product page copy into `products/<product-slug>.md`: title, description, key
   selling points, suggested price with reasoning, SEO title/meta description.
3. Note collection/navigation structure suggestions in `products/collection-structure.md` if the
   store's organization needs work.

## Campaigns

1. Draft campaign plans into `marketing/<campaign-slug>.md`: goal, audience, offer, channels,
   timeline, and copy for each channel.
2. For email specifically: use `ToolSearch` for the Gmail MCP tools and create a **draft** via
   `create_draft` (subject + body). Tell Austin it's ready in Gmail Drafts — there is no send
   tool, so this is where the agent's part ends.
3. For paid ad copy: draft into the same campaign file; actual ad account access isn't connected,
   so this is copy-ready-to-paste, not launched.

## Before handing off to inbox/

Every draft should be complete enough that Austin can paste it directly into Shopify admin (or
send the Gmail draft as-is) with zero editing needed.

## Publishing (after approval only)

Drafting is unrestricted; publishing/editing the live store is external-facing and always needs
Austin's explicit go-ahead first (route through the `approval-queue` skill, or get direct
confirmation in chat for a specific change). Once approved, use the browser tools to actually make
the change in Shopify admin yourself rather than making Austin paste it in. Take a screenshot
after publishing to confirm it landed as intended.
