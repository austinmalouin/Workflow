# Business HQ Dashboard

Last restructured: 2026-07-22

**Visual dashboard**: [claude.ai/code/artifact/1c603ab1-a189-41ca-a283-5ff643234823](https://claude.ai/code/artifact/1c603ab1-a189-41ca-a283-5ff643234823) — the actual "app" view of everything below. Ask to have it regenerated whenever venture status changes meaningfully; it's a snapshot, not a live feed.

**Repo**: [github.com/austinmalouin/Workflow](https://github.com/austinmalouin/Workflow) — this workspace is now a git repo, pushed. Pull before assuming local state is current; cloud routines below commit and push their own work back here.

**Permanent automation (cloud routines, run whether or not this session is open)**:

| Routine | Cadence | Covers | Connector used |
|---|---|---|---|
| [business-hq-trading-research](https://claude.ai/code/routines/trig_01CG1U9mLCpUFYJkwYSQW8Me) | Weekdays 9:24am ET | Trading desk: scans, backtests, signals — read-only, no order-placement tool exists in this routine | Robinhood_Agentic (read-only tools only) |
| [business-hq-content-research](https://claude.ai/code/routines/trig_01PSuKAiNvzfua299kBZAowX) | Mondays 9:17am ET | Minecraft channel + lore server: research, scripts, content calendar, thumbnail briefs | Canva |

**Not yet possible in the cloud**: Etsy and Shopify checks need your actual logged-in Chrome
(Claude-in-Chrome), which only exists locally — those stay on the local session cron below.
Finance/QuickBooks cloud automation needs QuickBooks connected as a claude.ai connector first
(it isn't yet) — ask to set that up once it's authorized.

**Local session cron (only while this Claude Code session stays open, expires in 7 days)**:
- Etsy shop check — daily 8:47am
- Cross-business rollup (nudges Minecraft/lore-server/Shopify progress) — daily 6:13pm

## Ventures

| Business | Folder | Agent | Status |
|---|---|---|---|
| Etsy shop (SteadyLedgerPrints) | [businesses/etsy-shop](businesses/etsy-shop/BUSINESS.md) | `etsy-agent` | Active — 10 listings, pre-revenue |
| Shopify store (RIDGEWOOD) | [businesses/shopify-store](businesses/shopify-store/BUSINESS.md) | `shopify-agent` | Active — 31 listings, pre-revenue |
| Trading desk | [businesses/trading-desk](businesses/trading-desk/BUSINESS.md) | `trading-agent` | Active — Robinhood Agentic connected |
| Minecraft YouTube channel | [businesses/minecraft-channel](businesses/minecraft-channel/BUSINESS.md) | `minecraft-agent` | Onboarding — needs channel name |
| GoT/Lore server | [businesses/got-lore-server](businesses/got-lore-server/BUSINESS.md) | `lore-server-agent` | Onboarding — needs platform (Discord?) |
| Cross-business books | [businesses/](businesses/) (shared) | `finance-agent` | Blocked — QuickBooks not yet authorized |

Overseer agent (`overseer`) sits above all of these — use it for cross-business prioritization,
weekly rollups, and deciding where your attention/budget should go next.

## How to use this

Ask the assistant to act as an agent by name, e.g.:

> "Have the etsy-agent draft five new listing titles for the fall niche."
> "Get the trading-agent to scan for momentum setups and write up the top 3."
> "Ask the overseer for this week's priority across all five businesses."

**How this actually works** (confirmed 2026-07-23): these aren't separately dispatchable
subagents — `.claude/agents/*.md` files don't register in this environment's `Agent` tool, restart
or not. When you name an agent, the assistant reads that file as a playbook and does the work
directly in the same conversation, with the same real tools (browser, files, Robinhood, etc.) —
functionally the same result, just not an isolated process. See `.claude/agents/<name>.md` for
each one's intended scope. The one place this matters: `trading-agent`'s file lists a restricted
tool set (no order placement) as a *design intent*, but that restriction isn't technically
enforced without real subagent isolation — what actually prevents trade execution is the
assistant's own standing rule to never place a trade, which holds regardless. None of the "agents"
spend money, send external messages, or publish content without it either being a Gmail *draft*
(never sent) or landing in `approvals/` for your sign-off.

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
| `lore-server-growth` | Community content calendar, growth/marketing drafts |

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

Ask to search the MCP registry (`mcp-registry` tools) any time you want to check whether a new
connector for one of these has become available.
