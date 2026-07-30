# Draft Prep — ADHD Reset Routine & No-Shame Cleaning Kit

**Listing ID**: 4541666400 | **Status**: Draft (last updated Jul 21, 2026) | Checked live via
Shop Manager 2026-07-22.

## Correction to the original brief

Austin's brief assumed this draft was missing title/tags/description/price. **It isn't** — all
four already exist and are in reasonably good shape. What's actually blocking publish is
different, and more structural. Details below.

## What's already there (verified in Shop Manager)

- **Title** (115/140 chars): "ADHD Reset Routine & No-Shame Cleaning Kit, Printable Home
  Organization Planner PDF, Neurodivergent Chore Checklist" — good, front-loads the differentiator,
  uses "printable" and "PDF," reasonable length.
- **Tags** (13/13 used): adhd cleaning, reset routine, chore checklist, dopamine tasks, home
  organization, printable pdf, cleaning schedule, self care reset, digital download,
  neurodivergent, brain dump sheet, adhd planner, executive function — this is a strong tag set,
  already better-targeted than several of the *active* listings (uses "dopamine tasks" and
  "executive function," both specific, real ADHD-search-behavior terms not used anywhere else in
  the shop).
- **Description**: present and well-written — explains the reset-routine-card system, room-by-room
  breakdown, dopamine-friendly checkboxes, and brain dump page; mentions A4/US Letter/A5 sizing and
  GoodNotes/Notability compatibility.
- **Price**: $7.00 set.

## What's actually blocking this from being publish-ready

1. **Item type is set to "Physical item," not "Digital files."** Every other active listing in the
   shop is categorized as "Digital files." This draft is currently configured with a physical-item
   fulfillment flow: it shows a "Processing profile — Ready to ship, 1-2 days," a shipping option
   selector, "item weight and size," and a 30-day physical returns policy — none of which apply to
   a PDF download. **If published as-is, buyers would be asked for a shipping address and the
   listing would misrepresent itself as a physical product.** This needs to be changed to "Digital
   files" in Item Details before anything else.
2. **No digital file is attached.** The other 10 listings all have a PDF uploaded (e.g.
   `adhd_debt_payoff_kit.pdf`). This draft has nothing uploaded — the actual product file needs to
   be attached once the item type is corrected to Digital (the upload option only appears in that
   mode).
3. **No photos or video uploaded.** The photo/video section is empty ("Drag and drop files or
   Upload," 0 of 20 used). Etsy requires at least one photo to publish, and every active listing
   has 2 mockup images + 1 video — this one needs the same before it can go live.
4. **Description contains a branding inconsistency that should be fixed before publish**: the
   current description text reads *"Part of the Steady Ledger collection by **Solera Palms** —
   pairs perfectly with our ADHD budget & debt trackers."* "Solera Palms" does not match the shop
   name anywhere else (shop is SteadyLedgerPrints / "Steady Ledger Co." per BUSINESS.md) — this
   reads like a leftover placeholder from a template or an unrelated draft and should be corrected
   to the actual shop name before this goes live. Suggested fix: *"Part of the Steady Ledger Co.
   collection — pairs perfectly with our ADHD budget & debt trackers."*

## Optional polish (not blockers, but worth considering)

- **Price consistency**: every other active listing in the shop is set up as a "sale price" shown
  against a higher "original price" at a consistent ~40%-off intro discount (e.g. the comparable
  Debt-Free Starter Kit bundle is $7.20 sale / $12.00 original). This draft's $7.00 is a flat price
  with no original/sale framing. Given this kit is similarly scoped (multiple components: reset
  cards, room sheets, checkboxes, brain dump page) to the $12/$7.20 bundle, consider setting it up
  the same way — e.g. **$12.00 original / $7.20 sale** (matching the bundle exactly) or
  **$11.00 original / $6.60 sale** — rather than a flat $7.00, so it's visually consistent with the
  rest of the shop's intro-sale merchandising and shows buyers a "deal."
- Tag set is strong as-is; no changes recommended.
- Title is strong as-is; no changes recommended.

## Recommended pre-publish checklist for Austin

1. ~~Change Item Details → category/type from "Physical item" to "Digital files."~~ **Done,
   2026-07-23** — changed in Shop Manager and saved as draft, with Austin's go-ahead. Confirmed
   live in the draft (still unpublished): "Digital files • 2020 - 2026."
2. Upload the actual PDF file — **finalized & exported, delivered to Austin; only the literal
   attach step is blocked, 2026-07-23.** The first generation (`design_type: document`) had lost
   the real content to AI paraphrasing and left placeholder text; fixed by regenerating the exact
   copy with `design_type: doc` + `verbatim: true`, then merging that verbatim text back into the
   styled 10-page design (ID `DAHQQdTPRhY`, [edit](https://www.canva.com/d/v7T8Q6qLs3hFWAT) ·
   [view](https://www.canva.com/d/LHivfhBqurAs46H)). All 10 pages now carry the approved checklist
   content verbatim, placeholder text removed, and the cover's title/subtitle/byline spacing was
   nudged so nothing overlaps. Exported to a 10-page US-Letter PDF, saved at
   `listings/adhd-reset-routine-assets/adhd-reset-routine.pdf` and sent to Austin directly.
   **Not attached to the listing:** the browser file-upload tool only accepts files the *user*
   shared with the session (dragged-in attachments / connected folders) — agent-generated files are
   refused regardless of local path (scratchpad, repo, and outputs folders all rejected). So Austin
   drags the PDF into the draft's "Digital files" box himself (1 min).
3. Add mockup photos (and ideally a video) — **2 photos finalized & exported, delivered; attach
   blocked same as #2, 2026-07-23.** Cover photo (ID `DAHQQRz1bTw`) needed no changes. "What's
   Included" photo (ID `DAHQQWAAUzU`) had garbled text ("pr tudz prompts") + a duplicate row on
   review; text corrected and committed (Austin OK'd accepting a minor row-overlap to nudge later).
   Both exported to PNG at `listings/adhd-reset-routine-assets/listing-photo-1-cover.png` and
   `listing-photo-2-whats-included.png`, saved in-repo and sent to Austin — he drags them into
   "Photo and video." **Video still not covered** — Canva's generator has no video type, so the
   scroll-through video needs a separate manual screen recording.
4. ~~Fix the description's "Solera Palms" reference to the correct shop name.~~ **Done, 2026-07-23**
   — description now reads "Part of the Steady Ledger Co. collection — pairs perfectly with our
   ADHD budget & debt trackers." Saved as draft, confirmed live in the editor.
5. Optional: restructure price to a sale/original pair consistent with the rest of the shop — not
   actioned, still just a suggestion.
6. Then it's ready for Austin to hit Publish himself — no further copy work needed.

**Current status, 2026-07-23:** #1 and #4 done live in the draft; #2 and #3 fully produced,
exported, saved in `listings/adhd-reset-routine-assets/`, and sent to Austin — the only remaining
work is the manual file-attach (blocked for the agent by the upload sandbox) plus the optional
video and price framing. Nothing has been published; the draft is still a draft. Once Austin drags
the 3 files in, the listing is publish-ready on his say-so.
