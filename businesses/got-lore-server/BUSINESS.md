# Medieval/GoT-Themed Minecraft Server

**Agent**: `lore-server-agent` | **Skill**: `lore-server-growth` | **Status**: onboarding (concept locked 2026-07-22)

## What this is

A real, joinable **Minecraft Java Edition multiplayer server** — medieval-fantasy /
Game-of-Thrones-adjacent in theme (Seven-Kingdoms-style houses, sworn banners, castle-building,
faction warfare, a contested throne) — that Austin wants to grow into a profitable server business.
This is a game server people log into and play on, not a Discord-only fan community.

**CORRECTED 2026-07-22**: earlier drafts of this file assumed "lore server" meant a Discord
community for ASOIAF discussion/theorizing. That was wrong. The core product is the Minecraft
server itself (gameplay: building, factions, land claims, PvP/war, progression). A Discord almost
certainly still exists or should exist alongside it — that's standard practice for Minecraft
servers (support, ban appeals, community, announcements, selling ranks via a storefront linked
from Discord) — but Discord is the support/community layer, not the product.

**IP-naming note**: "Game of Thrones" and related terms are actively defended HBO trademarks
(100+ registered marks). Precedent exists for non-commercial fan builds operating for years
(WesterosCraft, running since 2011, free-to-join, no cash shop), but this server *is* meant to be
monetized, which is a materially different risk profile. Recommendation: keep the marketing
positioning "if you love Game of Thrones, you'll love this" (comparison/inspiration is normal and
low-risk) but give the server and its houses/lore original names rather than licensed
terms — "Seven Kingdoms," "Iron Throne," "House Stark" etc. reskinned to original equivalents.
This avoids a takedown risk to a revenue-generating product. Final naming is Austin's call; this
is a flagged risk, not a blocker.

## Concept (see full reasoning + monetization plan in `../../.claude/skills/lore-server-growth/SKILL.md`
and the research notes below)

**Format**: a persistent medieval-fantasy survival server built around **player-run Houses**
(factions) that claim land, build keeps, swear fealty or rebel, and compete for seasonal control
of a central "Throne" holding via a mix of building competitions, economy, and controlled PvP
war windows. Structurally close to the proven "Empires SMP" / kingdom-faction genre (see
research below) but running as a real public server (anyone can join and found/join a House)
rather than a closed cast of pre-cast creators.

### Why this format (research-grounded, not assumed)

- **Precedent that it works as gameplay**: Kingdom/faction-war servers are an established,
  populated genre — MoxMC, TheCrownSMP, ArkOfRulers, Last Realm, "Medieval SMP" and others are
  live, monetized servers right now built on kingdoms + factions + custom economy plugins
  (Towny/Factions-style). This is not an unproven mechanic.
- **Precedent that it works as content**: Empires SMP (fWhip and cast — GeminiTay, Pixlriffs,
  LDShadowLady, Smallishbeans, etc.) turned "everyone owns an empire, empires ally/trade/war" into
  one of the most-watched SMP formats in Minecraft YouTube, precisely because kingdom rivalry
  produces natural narrative stakes (rises, betrayals, sieges) that a plain survival server
  doesn't.
- **The gap**: nobody found in research combines (a) explicit GoT-adjacent medieval/political
  theming (succession, sworn houses, a throne worth fighting over — not generic "kingdoms"),
  (b) a real public monetized server anyone can join (not a closed influencer cast), and (c) a
  serialized YouTube narrative built around that server as the throughline. WesterosCraft proves
  the GoT-Minecraft audience is real and durable (12+ years, active today) but it's a build/tourism
  server with no factions, no war, no monetization, and no ongoing content series — it's a museum,
  not a game people compete on. That's the specific opening.
- **Genuine risk, stated plainly**: this is a competitive niche (faction/kingdom servers are
  common) and a new server has zero player base at launch — the channel's job (see
  `businesses/minecraft-channel/BUSINESS.md`) is specifically to solve that cold-start problem by
  giving people a story to want to join, not just a server IP to try.

## Monetization plan (EULA-compliant)

Mojang's Commercial Usage Guidelines allow real money only for: cosmetic items, non-gameplay
perks (extra homes/warps, cosmetic pets/particles/nicknames), and time-limited convenience (queue
priority). **Prohibited**: anything sold that gives a paying player a real combat/economic edge a
free player can't ever match (pay-to-win kits, exclusive OP items, buyable land-claim advantages in
a PvP context). Free players must be able to reach parity through play, just slower.

Planned revenue stack, in build order:
1. **Cosmetic rank tiers** (one-time purchase, e.g. Sellsword / Knight / Lord) — cosmetic
   nicknames/colors, particle trails, pet mounts, extra `/home` warps, cosmetic banners/capes.
   No combat stats, no exclusive tools.
2. **Cosmetic crate keys** — purely visual loot (banner designs, building-skin cosmetics, title
   badges) sold or earned equally through play; never gear.
3. **Land-claim convenience, not advantage** — sell claim-block convenience (faster claiming,
   more claim slots) capped so it never lets a paying House out-build a free one at war-relevant
   scale; keep actual war/PvP mechanics untouched by payment.
4. **Server-name-adjacent merch / Patreon-style supporter tier** tied to the YouTube channel
   (early video access, Discord supporter role, name in credits) — content-side revenue that
   doesn't touch the EULA at all.
5. **Sponsorships once traffic exists** — Minecraft hosting companies (the kind that show up in
   "best medieval servers" round-ups) sometimes sponsor creators; realistic only after the channel
   has real numbers.

Do not sell: kits with unique combat stats, faction-war advantages, or anything free players can't
eventually earn. This is the single most common way monetized Minecraft servers get community
backlash or a Mojang warning — keep this list visible to anyone pricing new store items later.

## Content <-> server funnel (the two businesses are one funnel)

- **Content drives players to the server**: launch/announcement video (see
  `businesses/minecraft-channel/scripts/`), House-founding videos, siege/war-day narrative
  recaps, "a free player rose to Lord with zero purchases" success-story episodes — every video
  ends with a concrete reason and a server IP to go try it.
- **Server drives the next videos**: real House rivalries, betrayals, alliances, sieges, and
  build reveals that happen on the server become the next episode's raw footage — the server
  *is* the writers' room. Austin should watch for these moments and hand them to
  `minecraft-agent` as they happen: a House flipping allegiance, a contested Throne-holding
  election, a first successful siege, a big build reveal.

## Current state

Concept locked 2026-07-22. No server infrastructure (host, plugins, world) yet, no Discord yet,
no players. Next concrete steps: pick final (non-trademarked) naming, choose a host and core
plugin stack (Towny or Factions-style + a claims plugin + an economy plugin + a cosmetic-only
store platform e.g. Tebex), stand up Discord as the support hub, and time the public launch to
land right after the channel's launch/announcement video goes up.

## How the agent works today

No Minecraft server-hosting or Discord bot connector is available yet (checked 2026-07-22). Until
one exists, `lore-server-agent` works by:
- Researching the medieval/faction-server landscape and monetization norms (WebSearch), keeping
  this file current as the concept firms up
- Drafting the server's lore/House framework, rules, and store item list into `marketing/`
- Maintaining a content/event calendar in `content-calendar/` (House elections, war windows,
  build contests) synced with the YouTube channel's release schedule
- Leaving ready-to-post Discord/announcement copy in `inbox/` for Austin to post manually

## Working folders

- `content-calendar/` — planned in-server events (war windows, elections, build contests) timed
  against the YouTube upload schedule
- `marketing/` — lore/House framework, server rules draft, store/monetization copy,
  cross-promotion drafts
- `inbox/` — finished posts/announcements awaiting Austin
