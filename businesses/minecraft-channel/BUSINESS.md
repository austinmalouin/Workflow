# Minecraft YouTube Channel

**Agent**: `minecraft-agent` | **Skill**: `minecraft-content` | **Status**: onboarding

## What this is

A new, automated-as-possible Minecraft YouTube channel, built to make money (ad revenue,
sponsorships, and/or affiliate) **and to drive players into `businesses/got-lore-server/`**, a
monetized medieval/GoT-adjacent Minecraft server. The two businesses are one funnel: this channel's
content exists to make people want to join that server, and events on that server become this
channel's content. Read `../got-lore-server/BUSINESS.md` alongside this file — decisions here
assume that server exists as the destination.

## Format decision (locked 2026-07-22)

**Format: a serialized "Houses of the Throne" faction-war narrative series**, filmed on and
promoting the medieval/GoT-adjacent server — not generic let's-plays, not tutorials/redstone,
not disconnected shorts. Concretely:

- **Launch arc**: a documentary-style "founding" video (world/lore reveal, server rules, how to
  join) — see `scripts/` for the first draft — followed by 3-5 "House founding" episodes as early
  players/creators stake claims and build seats of power.
- **Ongoing series**: episodic recaps of real server events — House rivalries, sieges, betrayals,
  Throne-holding contests, big build reveals — cut like a serialized drama (cold open, stakes,
  cliffhanger) rather than a raw unedited stream.
- **Shorts**: cut from the same footage — single dramatic moments (a siege breach, a betrayal
  reveal, a build reveal) — for discovery/top-of-funnel, always pointing back to the full episode
  and the server IP.
- **Voice**: face-optional; a narrator/commentary voiceover over gameplay + cinematic build
  shots works fine and is the norm for this genre (Empires SMP creators mix face-cam and
  voiceover-over-gameplay).

### Why this, not something else (reasoning, not enthusiasm)

Verified via WebSearch (2026-07-22), not assumed:

1. **The mechanic is proven as content.** Kingdom/faction-war SMPs are one of the most-watched
   Minecraft formats — Empires SMP (fWhip + cast: GeminiTay, Pixlriffs, LDShadowLady,
   Smallishbeans, etc.) built a huge audience purely on "everyone owns an empire; empires ally,
   trade, and go to war." Rivalry produces built-in narrative stakes a plain survival series
   doesn't have.
2. **The GoT-adjacent audience is real and durable, but under-monetized/under-served as content.**
   WesterosCraft (running since Dec 2011, still active, mc.westeroscraft.com, free to join) proves
   there's a large, patient GoT-Minecraft audience — but it is a build/tourism server (warps
   between static recreations of Winterfell, King's Landing, etc.), no factions, no war, no
   ongoing YouTube series, no monetization. It's a museum, not a game with a story being told.
   Separately, several *generic* medieval/kingdom-faction servers (MoxMC, TheCrownSMP, ArkOfRulers,
   Last Realm) are live and monetized right now, proving the gameplay/business model works — but
   none of them carry explicit GoT-style political/succession theming or a serialized narrative
   channel built around them.
3. **The gap is the specific combination, not any one piece alone**: GoT-adjacent political
   theming (sworn houses, succession, a throne worth fighting over) + a real public server anyone
   can join (not a closed influencer cast like Empires SMP) + a serialized documentary-style
   YouTube series turning real server events into episodes. That combination did not turn up
   anywhere in research — it's "out of the loop" in the sense of uncommon, not unprecedented in
   its parts.
4. **Real risk, stated honestly**: faction/kingdom servers are a crowded gameplay category, and a
   brand-new server starts with zero population — a launch video alone doesn't solve that. The
   series has to keep manufacturing reasons to join (visible House rivalries, a fair path for a
   new player to rise) or it stalls like any other small server. This is a bet on serialized
   narrative solving server cold-start, not a guaranteed win.
5. **IP caution**: "Game of Thrones" is an actively enforced HBO trademark. Plan to market as
   GoT-*adjacent*/*inspired* ("if you love Game of Thrones...") while using original names for the
   server, houses, and throne mechanic — see the naming note in `../got-lore-server/BUSINESS.md`.

## Goals

- Launch arc live (announcement video + 3-5 House-founding episodes) timed to the server's public
  launch.
- Monetization eligibility (1,000 subs / 4,000 watch hours) as the first concrete milestone;
  revisit growth targets once the launch arc's real performance data exists — no invented numbers
  before that.

## Current state

Not yet created. No channel, no uploaded content. Format decided (above) and a first draft
launch-video script exists at `scripts/server-launch-announcement.md`, written to premiere
alongside the server's public launch.

**Voice + gear decided 2026-07-23**: voiceover-only (no face cam) — confirmed as the right call for
this genre and lowest barrier to actually start. Austin is starting from zero on recording/editing
gear. Recommended budget stack, real and current as of 2026-07-23:
- **Recording**: OBS Studio — free, no watermark, records gameplay at whatever resolution the
  machine can handle (720p on modest hardware, 1080p/1440p on stronger).
- **Editing**: CapCut (free, beginner-friendly, good for cuts/subtitles/export) as the starting
  point; DaVinci Resolve as a free but steeper-learning-curve upgrade once comfortable.
- **Voiceover**: record real narration directly; AI narration tools (e.g. ElevenLabs) are a viable
  fallback if Austin doesn't want to voice it himself, quality is genuinely close to human now.
- Total new-software cost: **$0** — everything above is free at the tier a new channel needs.

## How the agent works today

No YouTube upload/analytics connector is available yet (checked 2026-07-22). Until one exists,
`minecraft-agent` works by:
- Generating video/series ideas and titles with real search-demand backing (web research on
  trending Minecraft content, not guessing)
- Writing scripts/outlines into `scripts/`
- Briefing Canva for thumbnails
- Maintaining an upload schedule in `content-calendar/`
- Leaving a ready-to-upload package (title, description, tags, thumbnail brief) in `inbox/` —
  Austin (or Austin's recording setup) still needs to actually capture/edit gameplay footage and
  upload; that part isn't automatable without a connector and a video source

## Working folders

- `content-calendar/` — schedule of planned videos/series
- `scripts/` — outlines/scripts/talking points per video
- `inbox/` — finished upload packages awaiting Austin
