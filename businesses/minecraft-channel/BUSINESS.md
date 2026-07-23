# Minecraft YouTube Channel

**Agent**: `minecraft-agent` | **Skill**: `minecraft-content` | **Status**: onboarding

## What this is

A new, automated-as-possible Minecraft YouTube channel, built to make money (ad revenue,
sponsorships, and/or affiliate).

## Open questions (fill in / answer in chat, then delete this section)

- Channel name / handle (or need ideas)?
- Content format: let's-plays, shorts/clips, tutorials, builds, redstone, modded, SMP/roleplay?
- Face-on-camera or faceless/voiceover?
- Upload cadence target?
- Existing footage/recording setup, or starting from zero?

## Goals

- TBD once format is chosen (e.g. "N subscribers by <date>", "monetization eligibility
  (1,000 subs / 4,000 watch hours) by <date>").

## Current state

Not yet created. No channel, no content.

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
