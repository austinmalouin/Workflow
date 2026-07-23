# AI-Assisted Production Workflow — Houses of the Throne

Companion to `BUSINESS.md`. This is the operating playbook for where AI genuinely speeds up
production of this channel and where it must stay hands-off. Grounded in a July 2026 WebSearch
pass on what CapCut, Canva, VidIQ/TubeBuddy, and clipping tools (Opus Clip, Vizard) actually do
today — not assumed capabilities. Sources cited per section.

## The one-line rule for every stage below

**AI drafts, filters, and repurposes. Austin decides what the story is and performs the voice.**
This channel's entire value proposition (per `BUSINESS.md`) is that the drama is real — a rival
House really did betray an ally, a siege really did happen on the server. The moment AI is allowed
to invent or embellish a story beat, the channel becomes indistinguishable from any generic
Minecraft roleplay channel and the "genuine server events" differentiator is gone. Every stage
below names the line explicitly.

---

## 1. Research — tracking real server events into episode-worthy beats

**What AI does well:** AI is good at *organizing and structuring* information Austin already has,
not at *sourcing* it. There is no tool that watches a Minecraft server and knows a betrayal
happened — that has to come from Austin (or the server's Discord/chat logs, screenshots, build
timestamps) as raw input.

Concrete workflow:
- Austin keeps a running **event log** (a simple running note — Discord export, voice memo, or
  quick bullet list) of what actually happened each week: who founded what House, who allied with
  whom, any sieges/wars scheduled and their outcome, notable builds finished, drama in
  Discord/in-game chat.
- Feed that raw log to an LLM (Claude/ChatGPT) with an explicit instruction: *"Only use the events
  I list below. Do not invent details, dialogue, or outcomes I didn't describe. Group these into
  candidate episode beats (cold open / rising stakes / climax / cliffhanger) and flag which real
  events could serve each slot."*
- The AI's job is pattern-matching real events onto dramatic structure (which siege is the climax,
  which betrayal is the cold-open hook) — not generating any event itself.

**Where this breaks if misused:** asking an AI to "make the story more exciting" invites it to
invent stakes, dialogue, or outcomes that didn't happen on the server. That is the one failure
mode that would gut this channel's premise. Guardrail: never paste a prompt that asks the AI to
add drama — only to *organize and prioritize* drama that already occurred.

---

## 2. Scripting — AI-assisted outline/draft, human polish required

**What AI does well:** turning a real-events log into a first-pass structured draft fast. Current
practice (per 2026 sources) — Claude/ChatGPT at the ~$20/mo tier is what most solo creators
actually use for this, not specialized "AI script writer" SaaS products, which mostly wrap the
same underlying models. A capable prompt: hook (0:00-0:15), setup, rising action, climax,
cliffhanger/CTA, using the real event log from Stage 1 and matching the tone of
`scripts/server-launch-announcement.md`.

**Human pass required, non-negotiable:**
- Fact-check every claim against the real event log — cut anything the AI phrased as more certain
  or more dramatic than what actually happened.
- Rewrite all VO lines in Austin's actual voice/cadence — an AI draft is a skeleton, not
  narration-ready copy. First-draft AI phrasing tends toward generic YouTube-narrator cliché
  ("in a world where...") that will make every episode sound like every other faction-war channel.
- Austin makes the final call on which real moments *matter* enough to be the episode's climax —
  that's a creative/editorial judgment call about what the story means, not a summarization task.

**Practical workflow:** AI produces outline v1 in minutes → Austin edits/rewrites the VO copy →
Austin (or ElevenLabs as the stated fallback per `BUSINESS.md`) performs the narration.

---

## 3. Editing — where automation earns its keep in CapCut/DaVinci

Per 2026 research on CapCut's current AI toolset:

- **Auto captions**: genuinely fast and accurate for clear narration (roughly 94-96% accuracy on
  clean English speech, ~15-20 sec processing for a 10-minute video) — use this every time, then
  spot-check for Minecraft/fantasy proper nouns (House names, player usernames) the model won't
  recognize.
- **Silence removal / auto jump-cuts**: CapCut's Auto-Edit and similar tools (AutoCut for
  Premiere/DaVinci) will trim dead air and jump-cut between segments automatically. This is a
  genuine time-saver for removing "um," dead air, and false starts in one pass, but the automation
  is reported as *aggressive* — it can clip the front of words. Treat auto-cut output as a rough
  assembly to review, never as a final cut.
- **AI Auto-Edit ("draft timeline from raw footage")**: useful only as a first-pass assembly for
  gameplay B-roll selection (pick clean flythrough shots, cut dead travel time) — not for deciding
  the *narrative* cut. The dramatic pacing choices (when to hold on a build reveal, when to cut to
  black before a cliffhanger, how long to let a siege breach breathe) are Austin's editorial voice
  and are exactly what separates "serialized drama" from "raw stream footage," per the format
  decision in `BUSINESS.md`. Automating that away would flatten the show's actual differentiator.

**Recommended split:** let automation handle mechanical cleanup (captions, silence, rough
assembly) so Austin's edit time goes into the parts that make it feel like a show — pacing,
music sync, cliffhanger placement, cold-open structure.

---

## 4. Thumbnails — AI concepts via Canva, human final call

Canva is confirmed as a connected tool (its MCP server is available in this environment) and has
a Magic Media AI thumbnail generator that produces multiple concepts from a text prompt/style
preset at YouTube's 1280x720 size.

Workflow:
- Brief Canva with the thumbnail brief format already used in `scripts/server-launch-announcement.md`
  (composition, focal point, 3-4 word max text overlay, legibility at mobile size).
- Generate 2-4 concept variants (different focal image, different text treatment) to compare, not
  to auto-publish.
- Human final call on: which real screenshot/build shot actually represents the episode's true
  climax (AI has no way to know which in-game moment was the emotionally real one), whether a
  face/silhouette figure reads as "this House's story" to a returning viewer, and legibility at
  actual mobile thumbnail size (test small before finalizing — a 2026 CTR data point: thumbnails
  with strong emotional expression can lift CTR 20-30%, but only if genuinely legible).
- Never let AI invent a scene that didn't happen in-game for the thumbnail — the thumbnail is a
  promise to the viewer about what's inside; a fabricated hero shot breaks trust the same way an
  invented plot beat would.

---

## 5. Title generation — AI options tested against real title mechanics

Per 2026 research: title and thumbnail together account for the large majority of a video's CTR,
and current data supports front-loading the hook/keyword in the first 40-50 characters, keeping
the primary keyword in the first 3-5 words, and treating everything past ~60 characters as
SEO-supporting context rather than the click driver (there's genuine debate in the data on ideal
total length — some analyses favor 40-60 characters, others show 70-100 outperforming by 10-14%,
so this is a genuine test-and-learn area, not a solved formula).

Workflow:
- Ask AI for 8-10 title variants against the real episode content (not invented hooks) — vary
  structure (question, statement, number/stakes-forward) rather than just synonym-swapping one
  phrasing.
- Filter mechanically first: keyword position, character count, no clickbait that overpromises
  vs. what the episode delivers (overpromising kills retention/session time, which YouTube's
  algorithm penalizes).
- Human picks the 2-3 finalists and, once the channel has any view data, A/B tests them (TubeBuddy
  has a built-in thumbnail/title A/B test feature) rather than guessing which "feels" better.
- `scripts/server-launch-announcement.md` already has 3 title options in this exact
  draft-then-test format — carry that pattern forward per episode.

---

## 6. SEO — keyword/tag research grounded in real search demand

Per 2026 research, the realistic free/cheap stack is **YouTube Studio** (baseline free analytics,
what's actually driving traffic to existing videos), **VidIQ** (keyword research, search volume,
competition scores, trending-topic surfacing), and **TubeBuddy** (SEO Studio checklist scoring,
bulk tag/description optimization). These are the two dominant tools creators actually use in 2026
— not a single "AI SEO" black box.

Workflow:
- Before naming an episode/series, pull actual search-volume data from VidIQ/TubeBuddy for
  candidate keyword phrases ("minecraft faction server," "minecraft kingdom smp," "medieval
  minecraft roleplay," etc.) — this is exactly the kind of "verified via WebSearch, not assumed"
  discipline already used to lock the channel's format in `BUSINESS.md`; apply the same standard
  to keyword choices.
- Use AI (ChatGPT/Claude) only to *draft* description copy and tag lists from that verified
  keyword list — never to invent keyword volume or trends from its own training data, which will
  be stale and unverified.
- Reuse tag/description scaffolding already established in
  `scripts/server-launch-announcement.md` (tags: "minecraft server," "medieval minecraft," "game
  of thrones minecraft," etc.) as the seed list, then expand using real tool data per episode.

---

## 7. Shorts production — repurposing long-form efficiently

Per 2026 research, dedicated AI clipping tools (Opus Clip, Vizard) are the mainstream solution:
they ingest a long-form video, auto-detect highlight-worthy moments (a "Virality Score" in Opus
Clip's case), and export vertical, captioned, platform-formatted clips. Opus Clip is reported
stronger for fast, high-volume output with good highlight-picking; Vizard for cleaner cut points
and fuller workflow control.

Workflow for this channel specifically:
- Feed the finished long-form episode in.
- Because this is a serialized drama, the "highlight" the AI flags algorithmically (loudest/most
  emotional-sounding moment) won't always be the moment that actually matters to the ongoing
  story — a siege breach or betrayal reveal that only lands if you already know the House rivalry.
  Austin should pre-flag the 2-4 moments per episode that are genuinely the dramatic peaks (this
  can literally reuse the beat-sheet from Stage 1) rather than trusting the tool's automatic
  selection blind.
- Let the tool handle the mechanical repurposing work: vertical reframe, auto-captions, clip
  trimming to Shorts length.
- Every Short's caption/on-screen text should point back to the full episode and the server IP,
  per the top-of-funnel role Shorts already have in `BUSINESS.md`'s format decision — that CTA
  line is a manual add, not something the clipping tool will do correctly by default.

---

## 8. Content repurposing — TikTok/Reels cross-posting from the same footage

Same clipped assets from Stage 7 extend directly to TikTok and Instagram Reels — both Opus
Clip/Vizard and CapCut's 2026 toolset explicitly target multi-platform export (TikTok, Reels,
YouTube Shorts) from one source cut.

Practical notes specific to this channel:
- Cross-posting is close to free extra reach once a Short exists — same file, different upload
  target, minor aspect-ratio/caption-length tweaks the tools already automate.
- Caption copy per platform should still be reviewed by Austin, not auto-pasted identically —
  TikTok/Reels audiences respond to different framing than YouTube (more meme-native, less
  "watch the full episode" formality) even when the clip itself is identical.
- Every cross-post should carry the server IP/Discord link in the caption/bio-link, since the
  entire point of this channel (per `BUSINESS.md`) is funneling viewers to the real server, not
  building isolated audiences on each platform.
- No auto-posting/scheduling tool is connected yet — per `BUSINESS.md`'s hard constraint, any new
  platform integration is something Austin connects himself; until then this stage produces
  ready-to-post files/captions in `inbox/`, not live posts.

---

## 9. Publishing & workflow management — weekly production pipeline

No YouTube upload/analytics connector exists yet (confirmed in `BUSINESS.md`), so "publishing" in
this workflow means: agent prepares a complete, ready-to-upload package in `inbox/`; Austin does
the actual upload and any account-level actions himself.

**Weekly pipeline** (assumes one episode/week cadence once the launch arc is airing):

| Day | Task | Who / AI role |
|-----|------|----------------|
| Mon | Log real server events from the past week (rivalries, sieges, builds, Discord drama) | Austin logs raw events; AI has no input yet |
| Mon | AI structures event log into 2-3 candidate episode beats | AI drafts, Austin picks the real story to tell |
| Tue | AI-assisted script outline from chosen beats; Austin rewrites VO copy in his own voice | AI drafts, Austin owns final copy |
| Wed | Record gameplay footage (OBS) + record narration (Austin's voice or ElevenLabs fallback) | Human capture, no AI substitute for performance |
| Thu | Edit in CapCut: auto-captions + auto silence/jump-cut pass first, then manual pacing/cliffhanger edit | AI handles mechanical cleanup, Austin owns the cut |
| Thu | Pull real keyword data (VidIQ/TubeBuddy); AI drafts description/tags from verified keywords | AI drafts, grounded in real tool data |
| Fri | AI generates 8-10 title variants + Canva generates thumbnail concepts; Austin picks finalists | AI generates options, Austin decides |
| Fri | Clip 2-4 Shorts from Austin-flagged dramatic peaks (Opus Clip/Vizard); cross-post versions for TikTok/Reels | AI does mechanical repurposing, Austin flagged which moments matter |
| Fri | Package everything (video file, title, description, tags, thumbnail, Shorts, cross-post captions) into `inbox/` | Agent assembles the package |
| Weekend | Austin uploads episode + Shorts + cross-posts himself; updates `content-calendar/` | Human-only step (no connector yet) |
| Following Mon | Review actual view/CTR/retention data (YouTube Studio + VidIQ/TubeBuddy) to inform next week's title/thumbnail choices | AI can summarize the data, Austin decides what changes |

**Where AI should never take the wheel, restated:** the narration performance, the judgment call
on which server moments are the real story, and the final creative decisions on the cut and the
thumbnail/title. Those are the channel's actual product — everything else in this document is
there to buy Austin more time to spend on exactly those three things.

---

## Sources consulted (July 2026 WebSearch)

- CapCut AI features/auto-cut/silence removal: nemovideo.com, fluxnote.io, blitzcutai.com,
  autocut.com
- AI thumbnail generators / Canva Magic Media: bityclips.com, ytzolo.com, canva.com, thumbmagic.co
- VidIQ/TubeBuddy SEO tooling: slobodskyi.com, tubebuddy.com, shuvoimtiaz.com, linodash.com
- Opus Clip / Vizard Shorts repurposing: vizard.ai, viral.day, ngram.com, techsy.io
- AI script-writing tools/Claude-ChatGPT for YouTube scripting: dupple.com,
  blockchain-council.org, overseeros.com, sureprompts.com, fluxnote.io
- YouTube title length/CTR best practices: veefly.com, teleprompter.com, ytzolo.com, fluxnote.io
