# Devlog #2 — "The Plugin Stack: What It Actually Takes to Build a Kingdom Server"

Series: Houses of the Throne (companion devlog, not a numbered episode) | Format: behind-the-scenes
devlog — screen capture (plugin pages, comparison notes, a config file) + narration, no gameplay or
player footage required | Est. runtime: 6-8 minutes | Voice: voiceover (face-optional) |
**Drafted 2026-08-31**

## Why this video, why now

Grounded in research pulled this session (2026-08-31), not assumed:

1. **"Best Minecraft server plugins" / plugin-comparison content is a live, recurring category on
   Minecraft YouTube right now, not a guess.** WebSearch turned up multiple 2026-dated uploads in
   this exact lane — "Best Plugins for Minecraft Servers (2026)" (Jul 2026), "Top 10 FREE Minecraft
   Server Plugins Every Server Needs in 2026," a server-analytics-plugin spotlight (Feb 2026), and a
   minion-plugin spotlight (Apr 2026) — confirming server-owner/admin-facing plugin content has
   steady demand and isn't a one-off niche.
2. **The specific mechanic comparison is real and current.** Fresh research on the actual plugin
   landscape for this genre: Towny is confirmed as the long-standing, actively-developed choice for
   structured towns/nations/taxes/diplomacy (source: Modrinth, Apex Hosting, Space-Node's 2026 Towny
   setup guide); Factions is the classic raid-first/PvP-takeover alternative; Kingdoms/KingdomsX is a
   newer plugin that adds invasion, turret, and structure mechanics directly rather than requiring a
   separate war-window system bolted on top (source: Modrinth, GitHub). This is a real, current
   three-way tradeoff, not invented for the video.
3. **It's the next unblocked decision in the actual build, not a manufactured topic.** CraftHaven's
   own `BUSINESS.md` lists "choose a core plugin stack (Towny or Factions-style + a claims plugin + an
   economy plugin + a cosmetic-only store platform)" as a still-open next step — this devlog narrates
   that live decision-in-progress rather than a decision already locked, which is a different (and
   arguably more engaging) beat than Devlog #1's already-settled hosting/naming/monetization recap.
   **Nothing here locks CraftHaven's actual plugin choice** — that final call stays with
   `crafthaven-agent`/Austin; this video presents the real tradeoffs on camera, explicitly framed as
   "leading plan, not final," and touches neither open blocker (no House names shown, no server or
   player footage needed — everything is plugin-page screen capture and a comparison doc).
4. **It's a distinct beat from every prior script.** Episode -1 is a lore/hype teaser; Devlog #1
   covers *business* decisions (hosting cost, naming/trademark, monetization rules); Explainer #1
   covers the *genre/market* case for kingdom-faction servers broadly. This is the first piece to go
   *technical* — the actual mechanical foundation (claims, taxes, invasions, permissions) that makes
   the "sworn Houses fight over a contested Throne" pitch function as gameplay at all — which is
   exactly the "what it takes to build a server like this" logistics angle the genre hasn't gotten
   from this channel yet.

**Sits in the schedule outside the numbered arc**, alongside the devlog and explainer — see the new
row in `content-calendar/launch-arc-schedule.md`. Functions as a natural follow-up to Devlog #1 for
anyone who already subscribed off that video, and doubles as search-discovery bait for "minecraft
server plugins 2026" / "towny vs factions" traffic that has zero prior CraftHaven awareness.

## Hook (0:00-0:15)

Cold open: a browser with three tabs open side by side — Towny's plugin page, Factions' plugin page,
KingdomsX's plugin page — cursor clicking between them, not settled yet.

**VO:** "A kingdom server isn't a world file and a hosting bill. It's a stack of decisions about what
a player is even allowed to do — claim land, tax a neighbor, invade a rival. None of that exists
until a plugin says it does. This is that decision, and I'm making it on camera."

Title card: **HOUSES OF THE THRONE — DEVLOG #2**

## Beat 1 — Why this decision matters (0:15-1:30)

Screen: a text card pulling the core verbs straight from the CraftHaven concept — "claim land,"
"swear fealty," "ally or rebel," "hold the Throne."

**VO talking points:**
- Every one of those verbs from the pitch has to become a real, working command before a single
  House can exist — this isn't flavor text, it's the literal game engine underneath the story.
- Get this wrong and the fix isn't a patch note, it's migrating land claims and player data after
  Houses already have territory — worth getting closer to right before day one than after.

## Beat 2 — The three real contenders (1:30-3:30)

Screen: side-by-side plugin pages/feature lists for each, cursor highlighting the relevant line as
each is discussed.

**VO talking points:**
- **Towny** — the oldest, most actively developed option: towns, nations, taxes, resident
  permissions, plot protection. Built for structured politics and diplomacy, not built-in war —
  fits the "sworn House" identity side of the pitch very well on its own.
- **Factions** — the classic raid-and-takeover plugin: simpler, extremely well documented, huge
  install base — but built around constant, free-for-all territorial raiding, which doesn't match a
  "war happens in scheduled windows, not nonstop" design and carries a griefier reputation with
  newer players.
- **Kingdoms/KingdomsX** — newer and less battle-tested than either, but the only one of the three
  with invasion, turret, and structure mechanics built in natively — closer out-of-the-box to "a
  House can actually be sieged" than bolting a custom war-window system onto Towny or Factions.

## Beat 3 — What CraftHaven actually needs (3:30-5:00)

Screen: a checklist crossed against the pitch's real requirements — "sworn House identity," "land
claims," "controlled PvP war windows, not free-for-all raiding," "cosmetic-only monetization layer."

**VO talking points:**
- Pure Factions is too raid-first for this design — the whole point of the Throne mechanic is that
  war is a scheduled event with stakes, not background noise every player deals with constantly.
- Pure Kingdoms/KingdomsX gets the invasion mechanic closer to native, but it's the least
  documented and least battle-tested of the three for someone standing up their first real server.
- **Leading plan (not locked):** Towny-style claims/taxes/diplomacy as the everyday layer — it
  matches the "sworn House" politics directly — with a Kingdoms/KingdomsX-style invasion layer
  switched on only during scheduled war windows, an economy plugin bridging both (Vault-compatible,
  matching whatever store platform ends up handling the cosmetic-only monetization from Devlog #1),
  and a cosmetic-only storefront layered on top per the EULA rules already stated on camera in
  Devlog #1.
- Say plainly on camera: this is the leading plan worked out for this video, not a final decision —
  the actual call gets made before the server deploys, and might change.

## Beat 4 — The rest of the foundation (5:00-6:15)

Screen: a quick text-card list — the unglamorous supporting plugins that have to exist regardless of
which claims system wins: **LuckPerms** (permissions), **WorldGuard** (region protection),
**CoreProtect** (rollback/anti-grief logging), **EssentialsX** (core commands/homes/warps).

**VO talking points:**
- None of these make a highlight reel, but a server without them is one griefing incident or one
  permissions mistake away from a bad first impression it can't take back.
- Load-bearing, not exciting — worth naming once so nobody watching assumes the "fun" plugins are
  the whole stack.

## Call to action (6:15-end)

Screen: back to the three-tab browser from the cold open, now with a fourth tab open — a blank
comparison doc titled "Final call: TBD."

**VO:** "None of this is glamorous. Nobody logs into a Minecraft server because the permissions
plugin is well-configured. But it's the difference between a House rivalry that actually holds up
under a real siege and a server that breaks the first time two Houses try to fight. The plumbing's
almost decided. Next: the Houses themselves get named. Subscribe to watch the foundation turn into a
fight."

End card: subscribe prompt, "next: meet the five founding Houses" teaser line (same line used on
Devlog #1 and Explainer #1's end cards — no date promise until Episode -1's naming blocker clears).

---

## Title options (test 2-3 on real CTR once uploaded)

1. "What It Actually Takes to Build a Minecraft Kingdom Server (Plugin Breakdown)"
2. "Devlog #2: The Plugin Decision That Makes or Breaks a Kingdom Server"
3. "Towny vs Factions vs Kingdoms: Which One Actually Builds a War?"

## Thumbnail brief

Composition: three simple stylized icons (a scroll for Towny/diplomacy, crossed swords for Factions/
raiding, a siege tower for Kingdoms/invasion — generic icons, not the plugins' actual trademarked
logos) arranged on branching paths that converge on a single castle/throne icon in the center. Text
overlay, 3-4 words max ("WHICH PLUGIN WINS?" or "THE PLUGIN STACK"). No faces required, no House
sigils shown.

## Description/tags draft

**Description**: 2-3 sentences framing this as the real, in-progress plugin decision behind an
upcoming GoT-adjacent Minecraft kingdom server (CraftHaven) — Towny vs Factions vs Kingdoms/
KingdomsX, and why a hybrid is the current leading plan (not final). One sentence teasing the
House-founding content coming next. Discord link only if Discord exists by publish time.

**Tags**: minecraft server plugins, minecraft towny, minecraft factions plugin, minecraft kingdoms
plugin, minecraft server devlog, minecraft kingdom server, minecraft faction server, best minecraft
plugins 2026

## Notes for Austin

- Fully producible now: every plugin fact cited (Towny/Factions/KingdomsX feature sets, the
  supporting-plugin list) comes from this session's research plus the still-open "choose a plugin
  stack" line already sitting in `crafthaven/BUSINESS.md` — no new approval needed to film this one.
- Like Devlog #1, this has **no blockers** — no House-naming approval required (House names are only
  referenced as "coming next," never shown), no player or server footage needed. Screen capture of
  the three plugins' public pages plus a simple comparison doc/checklist covers the whole thing.
- Unlike Devlog #1, this one presents a decision *in progress* rather than one already locked — be
  careful in the edit not to imply the hybrid plan is final; the script is written to say "leading
  plan, not locked" out loud for exactly this reason. If Austin (or `crafthaven-agent`) settles the
  actual plugin stack before this films, update Beat 3's language to match reality rather than
  reusing this draft's hedge language after the fact.
