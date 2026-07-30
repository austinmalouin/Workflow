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

## Stats check — 2026-07-23, daily recheck (month to date, Jul 1–23)

- **20 visits, 0 orders, 0% conversion, $0.00 revenue** — still no sales since shop opened.
- **1 abandoned cart** this month, unchanged — no new one, no purchase yet.
- **7 total listing views** (up from 6 earlier today) — the one new view landed on Savings Goal
  Tracker (now 6), still the only listing with real traction. Too soon to see any effect from
  yesterday's SEO title/tag updates — normal day-to-day noise, not a signal yet.
- No new messages, reviews, or favorites.
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
"and" for the added phrase instead, keeping the pre-existing "US Letter & A4" ampersand.

**ADHD Reset Routine draft — 2 of 4 pre-publish blockers fixed, 2026-07-23**: Austin actioned the
checklist above. Verified live via Shop Manager first (all four blockers still present, unchanged
since Jul 22). With explicit go-ahead:
- Item type switched from "Physical item" to "Digital files" in Shop Manager, saved as draft.
- Description's "Solera Palms" branding typo fixed to "Part of the Steady Ledger Co. collection —
  pairs perfectly with our ADHD budget & debt trackers."
- Both confirmed live in the (still-unpublished) draft after saving — draft count unchanged at 1,
  nothing published.
Still open: no digital PDF file or mockup photos/video exist for this listing anywhere — Austin
chose "design from scratch" for these, so full page-by-page product content (3 reset cards, 5
room-by-room sheets, a brain dump page) plus a Canva mockup/video brief has been drafted in
[adhd-reset-routine-content-draft.md](listings/adhd-reset-routine-content-draft.md).

## Search-visibility work applied live — 2026-07-23

Austin asked for "as much automated stuff as possible… anything to boost my views and sales" while
he handles the manual file-attach himself. Everything below was **applied live** to the shop (all
reversible; before/after recorded here).

**1. Etsy's own search-visibility dashboard was flagging a real problem.** Checked
`Shop Manager → Etsy search visibility` directly: "1 factor risks lowering your search visibility —
2 listings have new title recommendations." Etsy's algorithm had flagged two titles as
keyword-stuffed/unclear. This is the highest-signal input available (it's Etsy telling us what its
own ranking thinks), and it had never been actioned.

- **Debt-Free Starter Kit** — accepted Etsy's suggestion as-is. It only stripped low-value filler
  ("Printable", "Undated", "Instant Download", "Bundle") while keeping the real keywords.
  - Before: `Debt-Free Starter Kit | Printable Budget Planner, Debt Snowball & Savings Tracker Bundle | Undated PDF Instant Download`
  - After: `Debt-Free Starter Kit | Budget Planner, Debt Snowball, Savings Tracker (PDF Download)`
- **Savings Goal Tracker** — did **not** accept Etsy's suggestion verbatim. Etsy wanted to drop
  "Cash Stuffing," which is a deliberately-added, genuinely-searched term from the earlier keyword
  research (see the 6-listing SEO revision work). Edited the recommendation instead to keep Etsy's
  shorter/clearer structure *and* retain the keyword.
  - Before: `Savings Goal Tracker | Visual Savings Challenge and Cash Stuffing PDF Instant Download | US Letter & A4`
  - Etsy proposed: `Savings Goal Tracker | Visual Savings Challenge PDF (US Letter)` ← drops "cash stuffing"
  - Published: `Savings Goal Tracker | Cash Stuffing & Savings Challenge PDF (US Letter)`
- Both published via Etsy's own flow; verified live afterward.

**Worth internalizing for future sessions:** Etsy's title recommendations optimize for *buyer
clarity*, and it will happily strip a high-intent keyword to get there. Don't bulk-accept them —
accept the structure, hand-edit to keep researched keywords. The edit box in that flow allows it.

**2. Shop sections created and all 10 listings assigned.** The shop had **zero** sections — every
listing was unsectioned, so the storefront had no browsable navigation and Etsy had one less
relevance signal. Created 4 keyword-bearing sections and assigned all 10 active listings:
- **ADHD & Neurodivergent (2)** — ADHD Debt Payoff Kit, No-Shame Weekly Budget Check-In
- **Debt Payoff Trackers (2)** — Debt-Free Starter Kit, Debt Snowball Tracker
- **Budget Planners (4)** — Payday Checklist, Annual Budget Overview, Monthly Bill Tracker,
  Weekly Budget Planner
- **Savings & Sinking Funds (2)** — Savings Goal Tracker, Sinking Fund Tracker
- No Section: **0**. (The ADHD Reset Routine draft is still unsectioned — assign it to
  "ADHD & Neurodivergent" when it publishes.)

**Etsy admin quirks learned (save future time):**
- In the listings bulk editor, **scrolling clears your checkbox selection.** Select and act without
  scrolling in between. The reliable pattern: filter the list down (search box, or the sidebar
  Sections filter) until the whole group fits on screen → click select-all → Editing options →
  Change section.
- The sidebar Sections filter set to "No Section" is the fastest way to find unassigned listings.
- `form_input` on the section dropdown needs the numeric section **value**, not the label, when the
  label contains an ampersand. Section IDs: ADHD & Neurodivergent `59591046`, Debt Payoff Trackers
  `59607435`, Budget Planners `59591076`, Savings & Sinking Funds `59607455`.

**3. Attributes turned out to be a dead end — correcting an earlier assumption.** The previous
note here flagged "fill in listing attributes" as the next win, based on Etsy's generic advice that
attributes are "an important factor in helping items appear in relevant Etsy searches." Checked the
actual listing editor: for this category (**Personal Finance Templates**, digital), the Attributes
section contains **only Tags** — there are no structured attribute dropdowns (no Occasion, Style,
Color, Holiday, etc.). Etsy's generic guidance doesn't apply to this category. Nothing to fill.
Don't re-add this to the backlog.

**4. The real gap, found instead: the shop's own differentiator was missing from 80% of the
catalog.** Pulled every listing's tag set directly (fetched each listing-editor page and parsed the
embedded tag JSON — much faster than opening 10 editors by hand). Result: only **2 of 10** listings
carried any ADHD/neurodivergent tag. The other 8 were competing purely on the most saturated terms
on Etsy — "instant download" (all 10), "budget tracker" (8), "financial planner", "personal
finance", "printable tracker", "undated planner". A zero-sale shop cannot rank for those; meanwhile
the low-competition, fast-growing, genuinely-differentiated ADHD terms were sitting unused.

Fixed via Etsy's bulk tag editor, section by section (the sections built earlier made this clean —
each section maps to a tag group). Two passes per section, because the bulk dialog only does one
operation at a time:
- Pass 1: **Remove "instant download"** (frees a slot; all 8 were at 13/13)
- Pass 2: **Add "adhd friendly"**

Verified live afterward via the listings-page tag filter: **"adhd friendly" went 2 → 10**,
**"instant download" went 10 → 2** (the 2 remaining are the two originally-ADHD listings, untouched).

**Etsy bulk-tag-editor quirks (save future time):**
- The Add/Remove dropdown is a **native `<select>` styled to look custom** — `form_input` and JS
  `querySelector('select')` don't find it in the dialog. Click it, then press **Down** (Remove) or
  **Up** (Add).
- **Switching mode clears the queued tag.** You cannot stage an add and a remove together — apply
  the remove, re-select, then do the add.
- Same selection-fragility as before: **no `find` calls between selecting and acting**, and the
  first select-all click right after a page load often doesn't register — click, screenshot to
  confirm the count chip, then proceed.

**5. Closing the consistency gap — 8 description rewrites drafted AND published live, 2026-07-23.**
The tag work above left 8 listings tagged `adhd friendly` with descriptions that never mentioned
ADHD — a conversion leak and a tag-stuffing look. Drafted fixes for all 8 in
[adhd-description-rewrites.md](listings/adhd-description-rewrites.md), then applied and published
all 8 with Austin's go-ahead. Verified live afterward by re-fetching each listing's description —
all 8 now mention ADHD in the opening. Payday Checklist, Annual Budget Overview, Sinking Fund
Tracker, Debt-Free Starter Kit, Monthly Bill Tracker, Savings Goal Tracker, Debt Snowball Tracker,
Weekly Budget Planner. Every listing on the shop now both tags and speaks to the ADHD angle.

**Mechanics used**: per listing, triple-click on the opening paragraph in the description textarea
selects exactly that paragraph (stops at the real `\n\n`, not just the wrapped visual line) —
reliable for swapping just the hook without touching *What's included*/*How it works*/*Details*
below it. Two of the eight listings (Sinking Fund Tracker, Debt Snowball Tracker, Weekly Budget
Planner) use ALL CAPS section headers ("WHAT'S INCLUDED" not "What's included") — matched that
per-listing instead of a single template, so the inserted "Why it works" block doesn't look like a
different hand wrote it. First edit lost the blank line before the next section (typed text ending
without a trailing newline collapsed into the following heading) — fixed by ending each typed block
with a trailing blank line; verified via screenshot before publishing each one, not just after.

Key finding that changed the approach: the existing descriptions are **already good** — consistent
structure (hook → *What's included* → *How it works* → *Details*), concrete, no fluff. A wholesale
rewrite would have destroyed working copy. So each edit is surgical: **replace the opening hook**
with an ADHD/executive-function-led one, and **insert a `Why it works for ADHD brains:` block**
after it. Everything below stays untouched. Voice modeled on the ADHD Debt Payoff Kit, which
already nails it.

Honest calls recorded in that file: strongest fit is Payday Checklist / Debt Snowball / Savings
Goal / Monthly Bill Tracker (genuinely ADHD-native — short horizon, visual progress, early wins).
**Weakest is Annual Budget Overview** — a 12-month planning page is the least ADHD-native product
in the shop; if any listing should drop the `adhd friendly` tag instead of leaning in, it's that
one. No therapeutic/medical/diagnostic claims anywhere — the copy only describes *design choices*.

**Also still untouched:** the optional price/sale-framing consistency item, and the 15 free listing
credits sitting unused (relevant if new listings get created).

**Content draft reviewed, 2026-07-23**: checked the mockup/video brief directly against the real
shop, not just assumption — opened the live shop grid and the ADHD Debt Payoff Kit listing's
actual photos. The original brief's guess ("soft pastels, rounded corners, bursting-star
checkboxes") didn't match reality; corrected it to the shop's real, consistent system: deep
forest-green header band, warm cream background, bold serif/slab headline, mustard-gold divider
line, plain black-outline square checkboxes.

**Canva briefed, 2026-07-23**: with Austin's go-ahead, generated three editable Canva drafts from
the reviewed content (10-page PDF `DAHQQdTPRhY`, cover photo `DAHQQRz1bTw`, "What's Included" photo
`DAHQQWAAUzU`).

**Finalized, exported & delivered — 2026-07-23 (Austin: "nudge the cover spacing then do everything
else, no questions asked").** Reviewing the generated designs caught real defects, all fixed:
- The PDF's first pass (`design_type: document`) had let Canva's AI paraphrase the checklist into
  generic marketing prose and leave "[Your Name Here]" placeholders. Fixed by regenerating the exact
  copy with `design_type: doc` + `verbatim: true` and merging that verbatim text back into the
  styled 10-page layout; placeholders removed; cover title/subtitle/byline spacing nudged so nothing
  overlaps. All 10 pages now verbatim-correct.
- The "What's Included" photo had garbled text ("pr tudz prompts") + a duplicate row — corrected.
- All three exported (10-page US-Letter PDF + 2 PNGs), saved in-repo at
  `listings/adhd-reset-routine-assets/`, and **sent to Austin directly**.

**One genuine blocker, not a judgment call:** the browser file-upload tool only accepts files the
*user* shared with the session; agent-generated files are refused from every local path tried
(scratchpad, repo, session outputs). So the literal "attach to the Etsy draft" step can't be done by
the agent — Austin drags the PDF into "Digital files" and the 2 PNGs into "Photo and video" (a
~1-minute drag-and-drop). **Video** still needs a manual screen recording (Canva can't generate it).
Nothing was published; the draft remains a draft, publish-ready on Austin's say-so once the 3 files
are attached.

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
