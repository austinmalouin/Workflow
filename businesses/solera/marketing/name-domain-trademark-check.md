# Flight Path Disc Co. — Domain, Trademark, and Name-Collision Check (2026-07-29)

**Why this exists**: `BUSINESS.md` locked the brand name "Flight Path Disc Co." on 2026-07-24 and
flagged two things as required before supplier outreach went out under that name: a domain
availability check and a basic trademark search. Neither had been done. This is that pass.

**Headline finding: the name has a real problem.** "Flight Path" is not an open lane in disc golf —
it is already occupied by at least four distinct entities, one of which is sponsored by MVP Disc
Sports, one of the two suppliers we're about to contact. Recommendation is to change the name before
any outreach goes out. Details below, all verified against live pages, not assumed.

---

## 1. Name collisions found (this is the blocker)

| Entity | What it is | Where | Why it matters |
|---|---|---|---|
| **Flightpath Disc Golf** | 501(c)(3) nonprofit in **Redding, CA**, disc-golf youth education ("18 Aces" program). Sells branded merch: t-shirts $20–25, hoodies $35, hats $20, **towels $15**, jerseys $35. | `flightpathdiscgolf.org` | **The worst collision.** Same sport, and it sells *apparel and towels* — two of the exact product lines in `products/initial-sku-list.md`. And see the MVP note below. |
| **Flight Path Discs** | Registered `.com`, currently a WordPress "Coming Soon" placeholder — no products, no business info. Unclear whether abandoned or mid-setup. | `flightpathdiscs.com` → redirects to `flightpathdiscs.wordpress.com` | Someone already holds the closest `.com` to our name, in our exact niche. Even if dormant, it's taken and could wake up. |
| **The Flight Paths Disc Golf Podcast** | Active disc golf podcast | `flightpathsdg.podbean.com` | Occupies the *content* lane — which is Flight Path Disc Co.'s entire pillar #1. Direct competition for search and social handles. |
| **Flightpath Golf, LLC** | Company with live USPTO trademark activity (e.g. "GOLF PENS", serial 99671601) | USPTO / Justia | An entity actively filing trademarks under the Flightpath name in the golf space. |

### The MVP problem specifically

**Flightpath Disc Golf's corporate sponsors include MVP Disc Sports** — along with OTB Discs, Grip
EQ, and Pizza Factory. MVP is supplier target #1 in
[supplier-outreach-research.md](supplier-outreach-research.md).

So the current plan would have us emailing MVP Disc Sports to introduce a brand new business called
"Flight Path Disc Co." — when MVP already sponsors an organization called "Flightpath Disc Golf."
That is a bad first impression at best and a trademark conversation at worst. This is the single
most concrete reason to settle the name before sending anything.

---

## 2. Trademark search (basic, not a legal clearance)

- **FLIGHTPATH** — Serial 87753421, **Registration 5544935**, status **registered/live** as of
  2018-08-21, first use 2017-11-24. **International Class 028** — "Games and playthings; gymnastic
  and sporting articles." Goods described as **golf tees**.
- **Why Class 028 matters**: disc golf discs, baskets, and most disc golf hardgoods fall in **the
  same class 028**. A live registered mark in the identical class, in an adjacent sport (golf), is
  exactly the fact pattern that produces a likelihood-of-confusion objection. It is not a guaranteed
  bar — the goods differ (golf tees vs. disc golf accessories) — but it is a real risk, not a clean
  search.
- **No mark found** for "Flight Path" registered specifically for *disc golf* goods. The absence is
  weak evidence though: this was a search of Justia's index plus general web search, and the
  USPTO's own TESS/`tmsearch.uspto.gov` database was not queryable directly in this pass.

**This is not a legal clearance opinion and shouldn't be treated as one.** A real clearance search
for a name you're going to put on merchandise is a flat-fee service from a trademark attorney
(commonly a few hundred dollars) and is worth it *before* printing apparel, not after. Flagging that
as Austin's call, not something this workspace can do.

---

## 3. Domain availability

Checked by DNS lookup — **none of these resolve**, which means no live site:

- `flightpathdisc.com` — no DNS record
- `flightpathdiscco.com` — no DNS record
- `flightpathsupply.com` — no DNS record
- `flightpathdiscgolf.com` — no DNS record
- `throwflightpath.com` — no DNS record

**Important caveat, stated plainly**: "no DNS record" means *not in use*. It does **not** prove the
domain is unregistered — a domain can be registered and parked with no DNS configured. A real
availability check requires a registrar WHOIS lookup, which needs Austin at a registrar (and is the
same screen where he'd buy it). So: treat these as *promising, unconfirmed*.

And note the one that **is** taken: `flightpathdiscs.com` (plural) is registered and redirecting to
WordPress. That's the domain a customer would most likely guess.

---

## 4. North Carolina business structure — sole prop vs. LLC

Researched because a wholesale account almost certainly needs a resale certificate, which needs a
tax registration, which is downstream of this decision.

| | Sole proprietorship | LLC |
|---|---|---|
| **State formation cost** | $0 — no state filing required to operate | **$125** (Articles of Organization) |
| **Annual cost** | $0 | **$200/yr** annual report, due **April 15** |
| **3-year state cost** | $0 | **$525** ($125 + $200 + $200) |
| **Liability** | None — personal assets exposed | Separates personal assets from business debts |
| **EIN** | Optional; can operate under SSN | Effectively required (free, ~10 min at IRS.gov) |
| **How suppliers read it** | Fine for an inquiry; thinner for a wholesale account | Reads as a real business |

**NC's $200 annual report fee is high** — many states charge $50–100.

### Resale certificate path (needed either way, and it's free)

This is the piece suppliers will actually ask for, and it's independent of the LLC decision:

1. Register for a **Certificate of Registration** (sales & use tax account) with NCDOR — **no fee**,
   online via NCDOR's Business Registration portal, or by mailing Form NC-BR. Account ID typically
   issued instantly, written confirmation within ~5 business days.
2. Once you have that Account ID, complete **Form E-595E** (Streamlined Sales and Use Tax
   Certificate of Exemption) — this is the actual "resale certificate."
3. **Give E-595E to the supplier**, not to NCDOR. Keep records 3+ years.

### Recommendation

**Start as a sole proprietor and get the free NCDOR sales tax registration + E-595E now; form the
LLC when there's real revenue or real liability.** Reasoning:

- The resale certificate is the actual unlock for wholesale, and it costs **$0** and doesn't require
  an LLC.
- $525 over three years is real money against a venture at $0 revenue, and every other venture in
  this workspace is also pre-revenue (see `HQ.md`).
- Liability exposure on selling towels, bags, and apparel is low. It would change if the catalog
  ever includes anything load-bearing — note `initial-sku-list.md` already flags carabiner-style
  safety caveats in the RIDGEWOOD catalog; if a disc golf SKU ever carries injury risk, revisit
  immediately.
- The LLC is easy to add later. It's not a door that closes.

**Not legal or tax advice** — entity choice has personal tax consequences this workspace can't see.
Worth one conversation with a CPA before filing anything, especially since NC's annual fee is on the
higher end.

---

## 5. What this means for the plan

The naming problem gates items that were queued to happen today:

- **Supplier outreach: HOLD.** Both drafts in `supplier-outreach-research.md` name the business
  "Flight Path Disc Co." Sending them to MVP — who sponsors Flightpath Disc Golf — under that name
  is the wrong first move. Rename first, then send. This is a one-day delay, not a real setback.
- **Domain purchase: HOLD.** Don't buy a Flight Path domain that may need to be abandoned.
- **Trademark clearance: worth paying for**, once a name survives a collision check.
- **Content launch: NOT blocked.** The Week 1 content is category education ("do you need a mini
  marker disc?") and doesn't need the brand name on screen. That work can proceed today under a
  neutral handle, which is exactly why it's the right thing to start on while naming resolves. See
  [first-video-shooting-script.md](first-video-shooting-script.md).

---

## Sources consulted

- `flightpathdiscgolf.org` and `/shop` — read live; confirmed 501(c)(3), Redding CA, merch lineup,
  and the MVP Disc Sports sponsorship.
- `flightpathdiscs.com` → `flightpathdiscs.wordpress.com` — read live; confirmed registered but a
  "Coming Soon" placeholder with no products.
- `flightpathsdg.podbean.com` — surfaced in search as an active disc golf podcast.
- `trademarks.justia.com` — FLIGHTPATH Reg. 5544935 / Serial 87753421, Class 028, golf tees;
  Flightpath Golf LLC's "GOLF PENS" application (Serial 99671601). Justia's detail page returned
  HTTP 403 on direct fetch, so specifics come from search-result summaries — **worth re-verifying
  directly at `tmsearch.uspto.gov`** before relying on them.
- NCDOR (sales & use tax registration, Form E-595E), plus LLC-cost roundups (llcuniversity.com,
  creditdonkey, bizreport, certumsolutions) cross-checked against each other for the $125/$200
  figures.

**What wasn't verified**: actual registrar-level availability of any candidate domain (needs WHOIS);
whether `flightpathdiscs.com`'s owner has any trademark claim or intent to operate; and a full
USPTO TESS search across all spelling variants and classes.
