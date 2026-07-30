# Solera — Supplier Dealer/Dropship Application Research (2026-07-24)

**Why this exists**: Part 3 of `BUSINESS.md` flagged that MVP Disc Sports' and Disc Golf Deals
USA's exact dealer/dropship application requirements weren't retrievable in the original research
pass. Austin approved reaching out to both. Before any contact form gets submitted, this document
answers the actual question: **what does each supplier require, does Solera meet it today, and
what — if anything — does Austin need to set up first?**

**No application, contact form, or email was submitted during this research.** Solera currently has
no domain, no registered business entity, no EIN, and no resale certificate — submitting an
application today would mean either leaving required fields blank/generic or inventing
credentials that don't exist. Neither is acceptable. This pass is reconnaissance only, done by
reading each supplier's live pages directly (not guessing from memory).

---

## 1. MVP Disc Sports

**Source pages checked directly**: `mvpdiscsports.com/wholesale/`, `mvpdiscsports.com/contact/`
(FAQ), `mvpproshop.com/pages/dealer-application-page` ("Become a Dealer" form — confirmed to be
MVP's own retail arm: same phone number, 844-687-3472, and same Marlette, MI address as MVP Disc
Sports HQ).

### What's actually on the page

- **Who can apply**: "We offer wholesale pricing to any stores, organizations, or event-runners
  looking to buy golf discs, bags, baskets, and accessories in bulk." No online-only exclusion is
  stated (contrast with Innova Discs below, which explicitly excludes online-only stores — checked
  as a comparison point, not a target supplier here).
- **Minimum order**: 32 discs per wholesale order (can mix models/plastics across MVP, Axiom, and
  Streamline). Custom stamping has a separate 150-disc minimum (not relevant to the accessories
  angle).
- **Dropship program**: "Some of our most popular Baskets, Bags, and Accessories will be available
  to drop ship... For the complete list of items available to drop ship, please sign into the Drop
  Ship Portlet." The portlet itself is dealer-gated — no public page shows what's needed to unlock
  it beyond becoming a dealer first.
- **Actual application form** (`mvpproshop.com/pages/dealer-application-page`, verified by reading
  the live page's form fields directly): **Full Name, Business Name, Email, Phone Number, Message**
  — protected by hCaptcha. That's the entire form. No field for EIN, resale certificate number,
  business license, or website URL.
- **No published application fee. No published approval timeline.** "Looking for Rates? Contact
  sales@mvpdiscsports.com for wholesale rates and further information about the wholesale program."
  Phone: 844-MVP-DISC (844-687-3472).
- One unrelated-but-notable policy: "we are not permitting any new Amazon Sellers at this time" —
  doesn't affect Solera (a Shopify store), just flagging it's there.

### Is a business entity/EIN/resale certificate actually required?

**Not for the initial contact form** — it only asks for name/business name/email/phone/message.
**Likely required before an actual wholesale account is activated**, though this is inference, not
something MVP states publicly: legitimate US wholesalers generally need a resale certificate (seller's
permit) on file to sell tax-exempt for resale, and it would be unusual for MVP to ship at wholesale
pricing indefinitely without ever asking for one. This should be flagged to Austin as a strong
probability, not a confirmed requirement — the page itself never says so.

---

## 2. Disc Golf Deals USA

**Source pages checked directly**: `discgolfdealsusa.com/pages/wholesale-signup`,
`discgolfdealsusa.com/pages/wholesale-login`, plus a direct DOM inspection of the signup page's
HTML (not just the rendered text) to look for the application form's actual fields.

### What's actually on the page — and a real problem found

The wholesale signup page's visible text says: *"Get signed up to secure wholesale pricing on a
variety of different disc golf brands. Just submit the application below and we will reach out to
you via email/phone to confirm when you are approved as to receive dealer pricing."*

**But there is no application form on the page.** This isn't a guess — I inspected the page's live
DOM directly (via a browser session, not just a text scrape) and enumerated every `<form>` element
on the page: the only forms present are the site's currency/localization selector, the site search
box, and a footer email-newsletter opt-in. None of them collect business name, tax ID, or any
dealer-specific information. The "application below" that the page's own copy promises is not
present in the page as of 2026-07-24 — it may have been removed, may depend on an app/widget that
isn't loading, or may require a separate step (e.g., logging into a wholesale customer account
first) that isn't documented anywhere on the public page. **This is a real finding worth flagging
directly to Austin, not something to paper over**: the stated self-serve application path doesn't
currently work.

- **Practical path given that**: contact them directly. Footer contact info: **(980) 549-0509**
  (text), **(844) 850-1105** (phone), **info@discgolfdealsusa.com**, open 9am–5pm EST Monday–Friday.
- **No minimum order quantity, application fee, or approval timeline published anywhere** on the
  site that this pass could find.
- A separate `/collections/wholesale-products` page exists showing wholesale-priced items, but
  that's a product listing, not the dealer-application mechanism.

### Is a business entity/EIN/resale certificate actually required?

**Unknown — not stated anywhere on the site**, and the broken/missing application form means there's
no field list to check the way there was for MVP. This can only be resolved by direct contact
(phone or email), which is exactly why this pass stopped short of guessing.

---

## 3. Industry comparison point (context only, not a target supplier)

To sanity-check whether "no EIN/resale-cert field on the form" is normal or unusual for disc golf
wholesale, I checked **Innova Discs'** retail dealer form (`innovadiscs.com/dealers/become-a-dealer/retail-dealer-form/`)
as a comparison, since Innova is the largest brand in the sport:

- Innova's form has a **mandatory "Resale License #" field**.
- Innova's page states: *"you must have and maintain a valid State sales license (other local
  licenses and permits may also be required)."*
- Innova **explicitly excludes online-only or mobile stores**: *"Innova is not accepting
  applications for online only or mobile stores at this time."* — which would disqualify a
  Shopify-only store like Solera outright, one more reason Innova was never on the target list.

Takeaway: resale licenses **are** a normal ask in this industry — MVP and Disc Golf Deals USA
simply don't surface that requirement on their public-facing pages the way Innova does. That
doesn't mean they won't ask for one once real contact happens; it means their initial applications
are lighter-weight and their tax-ID requirements (if any) aren't publicly documented.

---

## 4. Draft outreach — NOT SENT, for Austin's review only

**Updated 2026-07-24**: Austin has now picked the brand name — **Flight Path Disc Co.** — so the
drafts below use that name instead of the "Solera" placeholder used when this research was first
written. No business name is presented as a registered legal entity — the store is still pre-launch
with no domain or business registration yet, and the drafts say so plainly.

### Draft A — MVP Disc Sports "Become a Dealer" form

> **Full Name**: Austin Malouin
> **Business Name**: Flight Path Disc Co. (new store, pre-launch)
> **Email**: austinmalouin@gmail.com
> **Phone**: [Austin to provide — not in this workspace]
> **Message**: Hi — I'm setting up a new Shopify store, Flight Path Disc Co., focused on disc golf
> accessories (bags, baskets, mini markers, apparel, and pre-dyed discs/dye supplies), currently
> pre-launch with no live site yet. I'm interested in your dropship program for baskets, bags, and
> accessories, and wanted to understand the requirements to become an approved dealer —
> specifically whether a registered business entity, EIN, or state resale certificate is needed to
> get started, and what the typical approval timeline looks like. Happy to provide any
> documentation needed once I have it in place. Thank you!

**Status: NOT SENT.** One gap before this should go out for real: a phone number (the form
requires one). The brand-name blocker is now resolved — Flight Path Disc Co. is locked in as of
2026-07-24, so this draft no longer needs to be redone under a different name.

### Draft B — Disc Golf Deals USA (email, since the web form doesn't currently work)

> **To**: info@discgolfdealsusa.com
> **Subject**: Wholesale/dealer inquiry — new disc golf accessories store
>
> Hi — I tried your Wholesale Signup page (discgolfdealsusa.com/pages/wholesale-signup) but the
> application form didn't appear to load. I'm setting up a new Shopify store, Flight Path Disc Co.,
> in the disc golf accessories space (bags, baskets, apparel, and your dye-supplies line
> specifically), currently pre-launch. Could you let me know what's required to get set up as a
> wholesale dealer — business registration, EIN, resale certificate, minimum orders, and anything
> else — and whether that can be done before the store has a live domain? Thanks, and happy to hop
> on a call if that's easier.
>
> Austin Malouin
> austinmalouin@gmail.com

**Status: NOT SENT.** Brand name is locked in (Flight Path Disc Co., 2026-07-24), so this draft is
ready pending Austin's send-it go-ahead. This one explicitly surfaces the broken-form finding so
Austin can decide whether to mention it or just call/text the numbers listed above instead.

---

## 5. What Austin needs to do first (his decision, not something to fabricate around)

Neither supplier's own page makes a registered business/EIN/resale certificate a hard blocker for
the *initial* inquiry — both are reachable with nothing more than a name, email, and message. But
getting an actual wholesale/dropship account **activated** (not just an inquiry answered) will very
likely require real paperwork, based on standard practice in this industry (see the Innova
comparison above) and general US wholesale-tax norms. None of the following can be produced by this
workspace — they're Austin's calls and Austin's actions:

1. **Pick the final brand name** (Flight Path Supply Co. / Chains & Grip / Basket Case Disc Co. /
   other — see Part 3) before reaching out anywhere, so the inquiry doesn't need to be redone under
   a different name later.
2. **Decide on a business structure** — even a sole proprietorship (no formal registration required
   in most states to start operating, but this is state-dependent and Austin's call) versus an LLC.
3. **Get an EIN** if going the LLC/formal route (free, direct from IRS.gov — a five-minute online
   application once the entity decision is made), or confirm operating as a sole proprietor under
   Austin's SSN if that's the path chosen.
4. **Register for a state sales tax permit / resale certificate** — this is very likely what either
   supplier will ask for once a real wholesale relationship starts, and it's also generally required
   to legally collect sales tax on Solera's own future sales. State-specific; Austin's home state's
   department of revenue site handles this.
5. **A domain/live site is not confirmed as required** by either supplier's public pages (MVP's
   language doesn't exclude online-only, unlike Innova) — but having one ready before contacting
   suppliers presents better and avoids the awkward "pre-launch" framing in both drafts above.

**Bottom line for right now**: Austin can send a lightweight inquiry to either supplier today with
just his name/email — the forms don't demand more than that up front. But he cannot complete a real
dealer/dropship *account setup* without at minimum picking a business structure and very likely
obtaining a resale certificate — that's paperwork this workspace cannot produce or fabricate, so
it's listed here as his action item, not done.

---

## Sources consulted

- `mvpdiscsports.com/wholesale/`, `mvpdiscsports.com/contact/`, `mvpproshop.com/pages/dealer-application-page`
  — read directly (page text and, for the application form, live DOM field inspection).
- `discgolfdealsusa.com/pages/wholesale-signup`, `discgolfdealsusa.com/pages/wholesale-login` — read
  directly, including DOM inspection to confirm no application form is actually present on the page.
- `innovadiscs.com/dealers/become-a-dealer/retail-dealer-form/` — checked as an industry comparison
  point only (Innova is not a target supplier for Solera; excluded by its own online-only ban).
- General web search cross-checks on MVP's dropship/referral program pages and Disc Golf Deals USA's
  wholesale-products collection, used to confirm nothing material was missed outside the pages
  above.

**What wasn't verified**: whether either supplier would actually approve Solera once real contact
happens, what documentation they'd request beyond what's publicly stated, and Disc Golf Deals USA's
minimum order size / fees / timeline — none of that is published anywhere this pass could find, and
the broken application form means it can only be resolved by Austin (or an agent under his explicit
go-ahead) actually calling or emailing them.
