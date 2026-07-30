# Business HQ Dashboard

Last restructured: 2026-07-22

**Visual dashboard**: [claude.ai/code/artifact/fe9b1927-a3ab-4b04-ba2e-c2781ca4a8b9](https://claude.ai/code/artifact/fe9b1927-a3ab-4b04-ba2e-c2781ca4a8b9) — "The Bridge," the actual "app" view of everything below (source: `hq-brain.html`). Kept in sync at the end of every substantive session per the standing rule in [CLAUDE.md](CLAUDE.md); it's a snapshot, not a live feed.

**Repo**: [github.com/austinmalouin/Workflow](https://github.com/austinmalouin/Workflow) — this workspace is now a git repo, pushed. Pull before assuming local state is current; cloud routines below commit and push their own work back here.

**Permanent automation (cloud routines, run whether or not this session is open)**:

| Routine | Cadence | Covers | Connector used |
|---|---|---|---|
| [business-hq-trading-research](https://claude.ai/code/routines/trig_01CG1U9mLCpUFYJkwYSQW8Me) | Weekdays 9:24am ET | Trading desk: scans, backtests, signals — read-only, no order-placement tool exists in this routine | Robinhood_Agentic (read-only tools only) |
| [business-hq-content-research](https://claude.ai/code/routines/trig_01PSuKAiNvzfua299kBZAowX) | Mondays 9:17am ET | Minecraft channel + CraftHaven server: research, scripts, content calendar, thumbnail briefs | Canva |

**Not yet possible in the cloud**: Etsy and Shopify checks need your actual logged-in Chrome
(Claude-in-Chrome), which only exists locally — those stay on the local session cron below.
Finance/QuickBooks cloud automation needs QuickBooks connected as a claude.ai connector first
(it isn't yet) — ask to set that up once it's authorized.

**Local session cron (only while this Claude Code session stays open, expires in 7 days)**:
- Etsy shop check — daily 8:47am
- Cross-business rollup (nudges Minecraft/CraftHaven/Shopify progress) — daily 6:13pm

## Ventures

| Business | Folder | Agent | Status |
|---|---|---|---|
| **Automation Studio** (AI consulting) | [businesses/automation-studio](businesses/automation-studio/BUSINESS.md) | `automation-agent` | **Onboarding — the cash engine; next step is 10 validation calls** |
| Etsy shop (SteadyLedgerPrints) | [businesses/etsy-shop](businesses/etsy-shop/BUSINESS.md) | `etsy-agent` | Active — 10 listings, pre-revenue |
| Shopify store (RIDGEWOOD) | [businesses/shopify-store](businesses/shopify-store/BUSINESS.md) | `shopify-agent` | Active — 31 listings, pre-revenue |
| Shopify store (Flight Path Disc Co., disc golf — folder still named "solera") | [businesses/solera](businesses/solera/BUSINESS.md) | none yet (would reuse `shopify-agent`) | Build-out — niche + name decided, supplier outreach drafted (not sent), no products/store yet |
| Trading desk | [businesses/trading-desk](businesses/trading-desk/BUSINESS.md) | `trading-agent` | Active — Robinhood Agentic connected |
| Minecraft YouTube channel | [businesses/minecraft-channel](businesses/minecraft-channel/BUSINESS.md) | `minecraft-agent` | Onboarding — needs channel name |
| CraftHaven (Minecraft server) | [businesses/crafthaven](businesses/crafthaven/BUSINESS.md) | `crafthaven-agent` | Onboarding — name locked, no hosting/Discord yet |
| **Acting & Modeling** (Austin as talent) | [businesses/acting-modeling](businesses/acting-modeling/BUSINESS.md) | `talent-agent`, `casting-scout-agent`, `talent-brand-agent` | **Founding — modeling-led; needs stats sheet + Flair Magazine images uploaded** |
| Cross-business books | [businesses/](businesses/) (shared) | `finance-agent` | Blocked — QuickBooks not yet authorized |

**Portfolio note (2026-07-26, updated 2026-07-28)**: six of the eight ventures are *asset plays* —
they compound over months and every one sits at $0 today. Automation Studio was founded
specifically because none of them produce income this month; it trades hours for money at $100+/hr
to fund the rest. Treat it as the priority venture until it has a paying client.

Acting & Modeling (added 2026-07-28) is the only other venture with a near-term cash path — NC
non-union background work pays ~$100–200/day and needs no portfolio — but its real value is the
longer arc: representation, then volume, then rate. It is the one venture where the product is
Austin himself, which is also why its scam-avoidance constraints are the strictest in the
workspace. See its `BUSINESS.md`; nobody here pays an agency to be represented.

Overseer agent (`overseer`) sits above all of these — use it for cross-business prioritization,
weekly rollups, and deciding where your attention/budget should go next.

## How to use this

Ask the assistant to act as an agent by name, e.g.:

> "Have the etsy-agent draft five new listing titles for the fall niche."
> "Get the trading-agent to scan for momentum setups and write up the top 3."
> "Ask the overseer for this week's priority across all five businesses."

**How this actually works** (updated 2026-07-23, later session): these agents now do dispatch as
real, isolated subagents via the `Agent` tool — `shopify-agent` and others were confirmed running
independently in the background this session. (An earlier session that same day found the
opposite — that project-local `.claude/agents/*.md` files didn't register — but that no longer
holds; whatever caused it seems to have been fixed or was environment-specific.) See
`.claude/agents/<name>.md` for each one's intended scope and tool list. One thing not yet
re-verified since the fix: whether `trading-agent`'s restricted tool list (no order placement) is
now actually enforced by real subagent isolation, or still just a design intent backstopped by the
assistant's own standing rule never to place a trade — treat the standing rule as the real
guarantee either way. None of the "agents" spend money, send external messages, or publish content
without it either being a Gmail *draft* (never sent) or landing in `approvals/` for your sign-off.

## Approval queue

Anything an agent prepares that needs your yes — a listing to publish, a campaign to launch, a
trade idea to act on, a video to upload — goes through [approvals/README.md](approvals/README.md).
Check `approvals/queue/` for what's waiting on you.

## Skills available to all agents

| Skill | Purpose |
|---|---|
| `daily-briefing` | Cross-business morning rollup: status, approvals pending, trading snapshot |
| `approval-queue` | Convention for drafting an action for human sign-off |
| `etsy-ops` | Listing creation, SEO, pricing, seasonal calendar |
| `shopify-ops` | Product pages, campaigns, email drafts |
| `trading-research` | Scans, backtests, signal write-ups — never order placement |
| `minecraft-content` | Video ideas, scripts, thumbnail briefs, upload checklist |
| `crafthaven-growth` | CraftHaven event calendar, House/lore framework, growth/marketing drafts |
| `talent-ops` | Acting/modeling: agency + casting vetting checklist, submission packages, asset build order |

## Known gaps (integrations not yet connected)

These businesses are designed to plug into live tools once connected — until then, agents work
from research + drafts you execute manually:

- **Etsy**: no Etsy API/MCP connector yet, but `etsy-agent` has direct browser access to your
  logged-in shop (steadyledgerprints.etsy.com) — it reads live state itself and can publish
  approved changes directly, no manual paste-in needed.
- **Shopify**: no Shopify MCP connector yet, but `shopify-agent` has direct browser access to your
  logged-in admin (admin.shopify.com/store/mp3uez-hq) — it reads live state itself and can
  publish approved changes directly, no manual paste-in needed.
- **YouTube**: no upload/analytics connector yet. Agent preps scripts/thumbnails; you upload.
- **Discord**: no bot/server connector yet. Agent drafts posts/announcements; you post them.
- **QuickBooks**: connected but not authorized — authorize via your connector settings to unblock `finance-agent`.
- **Casting platforms**: no connector exists for Casting Networks / Actors Access / Backstage, and
  none is likely to. `casting-scout-agent` works by live web research and drafts submissions for
  Austin to send; profile creation and submissions are always his hands on the keyboard.

Ask to search the MCP registry (`mcp-registry` tools) any time you want to check whether a new
connector for one of these has become available.
