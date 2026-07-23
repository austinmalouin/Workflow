# Houses of the Throne — Analytics Dashboard & Tracking System

**Status**: pre-launch, built ahead of the first upload so tracking starts from video #1.
**Owner**: Austin (manual — no YouTube Studio/analytics API connector exists yet, see
`BUSINESS.md`). Every number below is pulled by hand from YouTube Studio.
**Purpose**: this is the source of truth for "is this channel working," week over week, until
Austin has 1,000 subscribers and 4,000 watch hours (YouTube Partner Program eligibility) — and
then it keeps working as the revenue tracker on top.

---

## 0. The one thing to obsess over first: CTR at healthy retention

Before the tables — the single highest-priority metric while pre-monetization: **impressions
click-through rate (CTR), read together with average-percentage-viewed**. Reasoning:

- Pre-YPP, the channel has no revenue metric to chase, and subscriber count is a lagging effect
  of watch time, which is itself a lagging effect of two upstream levers: *does the thumbnail/title
  get clicked* (CTR) and *does the video hold the click once earned* (retention). Everything else
  in this doc (traffic sources, subs, engagement) is downstream of those two.
- CTR specifically is the one Austin can improve fastest and cheapest — a thumbnail/title swap
  is a five-minute edit with no reshoot, versus retention fixes which often require changing how
  future episodes are *cut*. Early on, with only a handful of videos, CTR experiments compound
  learning about what "Houses of the Throne" concept/imagery actually gets clicked, before Austin
  has sunk cost into a full season built on a premise nobody clicks on.
- CTR alone is a trap, though — a high CTR with a retention cliff in the first 30 seconds just
  means the thumbnail lied. So the real discipline is: **track CTR every single week from video
  1, and never read it without the 30-second and average-retention numbers next to it.** Section
  3's decision tree below is built around exactly this pairing.

---

## 1. Manual weekly tracking template

Two tables: a **per-video table** (filled in once, then re-checked at day 7 / day 28) and a
**channel-level weekly table** (filled in every week regardless of whether a video published that
week). Recommended as a Google Sheet with these as two tabs — the markdown structure below is the
exact column layout to build.

### Tab A — Per-Video Performance

Source: YouTube Studio → Content → click the video → **Analytics** tab (Overview, Reach,
Engagement, Audience sub-tabs). Fill in Day-7 numbers a week after publish, then Day-28 numbers a
month after, since early numbers move fast and settle.

| Column | Where in YouTube Studio | Notes |
|---|---|---|
| Video title / episode # | — | e.g. "Ep. 2 — House Ashvale's Founding" |
| Publish date | — | |
| Video length (min:sec) | Content list | needed to interpret AVD % |
| Impressions | Reach tab | thumbnail shown count |
| Impressions CTR (%) | Reach tab | clicks ÷ impressions |
| Views | Overview tab | |
| Average view duration (min:sec) | Overview/Engagement tab | absolute time |
| Average % viewed | Engagement tab | AVD ÷ video length |
| Retention at 30s (%) | Engagement tab retention curve, read manually | hook check |
| Retention at 50% mark (%) | Engagement tab retention curve | mid-video sag check |
| Retention curve shape (note) | Engagement tab, visual read | "steady decline" / "cliff at X" / "sawtooth (re-watches)" / "spike at end" |
| Returning viewers (%) | Audience tab | new vs. returning viewers split |
| Subscribers gained | Engagement tab (or Overview) | |
| Subscribers lost | Engagement tab | often hidden by default — toggle it on |
| Net subscriber change | = gained − lost | |
| Likes | Engagement tab | |
| Comments | Engagement tab | |
| Shares | Engagement tab | |
| Engagement rate (%) | = (likes+comments+shares) ÷ views | compute manually, Studio doesn't total this |
| Traffic: Browse features (%) | Reach tab → "How viewers find your videos" | homepage/home-feed |
| Traffic: Search (%) | Reach tab | YouTube search |
| Traffic: Suggested videos (%) | Reach tab | sidebar/end-screen algo |
| Traffic: External (%) | Reach tab | Discord, Reddit, server ads etc. |
| Traffic: Notifications (%) | Reach tab | subscriber bell |
| Traffic: Other (playlists/channel page/direct) (%) | Reach tab | catch-all |
| Top traffic source this video | — | the single largest % above |
| What changed vs. last video (title/thumbnail/hook/length/CTA) | — | free text — your own experiment log |
| One-line diagnosis | — | filled in during weekly review, see Section 2 |

### Tab B — Weekly Channel Snapshot

Filled in every Monday regardless of whether anything published, pulled from YouTube Studio →
**Analytics → Overview**, set to "Last 7 days."

| Column | Where in YouTube Studio | Notes |
|---|---|---|
| Week ending date | — | |
| Videos published this week | — | includes Shorts, tracked separately if volume warrants |
| Total views (7-day) | Overview tab | |
| Total watch hours (7-day) | Overview tab | this is the YPP-eligibility counter — track cumulative separately, see below |
| Cumulative watch hours (trailing 365 days) | Overview → Audience or Advanced mode | the actual YPP gate number |
| Subscribers gained (7-day) | Overview tab | |
| Subscribers lost (7-day) | Overview tab | |
| Net subscriber change (7-day) | = gained − lost | |
| Cumulative subscribers | Overview tab | the other YPP gate number |
| Channel-average CTR (7-day) | Reach tab | |
| Channel-average view duration (7-day) | Overview tab | |
| Returning viewers (%) | Audience tab | trend this over time — rising = format is building a real audience, not just one-off discovery |
| Top traffic source (channel-wide) | Reach tab | |
| Publishing consistency: on schedule? (Y/N) | — | compare actual publish date to `content-calendar/` plan |
| Days late/early vs. planned schedule | — | |
| Revenue metrics (fill in only after YPP acceptance) | Earn tab | see Section 4 — leave blank/N/A pre-monetization |
| Notes / one thing to try next week | — | ties to Section 3 decision tree |

---

## 2. Weekly review checklist — what to look at, in order

Do this every Monday, 15–20 minutes, before touching the next script. Order matters: each step
either resolves the question or tells you which of the later steps actually matters this week.

**Step 1 — Did anything publish on schedule?**
Check Tab B "publishing consistency." If Austin missed the planned date, note why (recording,
editing, server-event timing) before looking at any performance number — an erratic schedule
depresses subscriber notifications and returning-viewer trust independent of video quality, so
don't over-read a soft week that was really a "we published four days late" week.

**Step 2 — Impressions and CTR (did people even see it, and did they click?)**
Pull up the Reach tab for the newest video. Low impressions with decent CTR usually means the
suggested/browse algorithm isn't picking the video up yet (normal for early videos with no
watch-history signal) — not a thumbnail problem. Low CTR *despite* solid impressions is the
thumbnail/title's fault, full stop — that's the first lever to pull (see Section 3).

**Step 3 — Retention curve shape (did it hold the click?)**
Open the Engagement tab, look at the actual curve, not just the average-%-viewed number:
- A steep early drop (first 15–30 seconds) = hook problem — the cold open didn't earn the next 10
  seconds.
- A gradual, roughly linear decline = normal and healthy for narrative content; compare the
  average % viewed against YouTube's own relative-retention benchmark line if Studio shows one.
- A cliff at one specific timestamp = something in the video itself (a lull, a repeated setup, an
  ad break, a jump cut that breaks the story) — check what's happening in the footage at that
  second.
- A sawtooth pattern (repeated up-down spikes) = people are rewatching a specific moment (a
  siege, a reveal) — good news, means a shorts-cut opportunity, not a problem.
- A late spike near the very end = people skipping to a payoff (the throne/duel outcome) — signal
  the cold open is under-selling that payoff; move a teaser earlier.

**Step 4 — Cross-reference CTR against retention (the overpromise check)**
This is the diagnostic pair, not two separate checks:
- High CTR + low early retention → title/thumbnail overpromised something the video doesn't
  deliver in the first 30 seconds. Fix the cold open to deliver on the thumbnail's promise faster,
  or be more honest in the thumbnail next time.
- Low CTR + high retention (whoever clicks, stays) → the content is good but not getting chosen;
  thumbnail/title problem, not a content problem. Don't touch the format — touch the packaging.
- Low CTR + low retention → double problem, but fix packaging first since it's cheaper to test;
  if a re-thumbnail doesn't move it, the format/premise itself needs a rethink.
- High CTR + high retention → this is the pattern to reverse-engineer. Note exactly what title
  language, thumbnail composition, and cold-open structure this video used, and repeat it
  deliberately next episode.

**Step 5 — Traffic source mix**
If Browse/Suggested is near zero across several videos, the algorithm hasn't picked the channel
up yet — expected in the first handful of uploads, not yet a signal to change anything. If
External is unusually high, that's the server community (Discord, server forums) doing the work —
good sign for the funnel thesis in `BUSINESS.md`, worth reinforcing with more cross-posting. If
Search starts appearing, note what query brought people in (Studio sometimes surfaces this) — it
tells you which title keywords are actually searched for.

**Step 6 — Subscriber net change and returning viewers**
Only look at this after Steps 2–5, because it's a lagging output of them. A single video with a
subscriber spike usually traces back to strong retention + a clear subscribe CTA at the payoff
moment. A rising returning-viewer % over several weeks is the best available leading signal that
the *series* (not just individual videos) is working — this is the metric to graph over time,
not any single week's value.

**Step 7 — Engagement (likes/comments/shares rate)**
Lowest priority of the core metrics — it doesn't drive discovery the way CTR/retention/traffic do,
but comments are a free source of "what did people actually think," so skim them for recurring
complaints or requests even if the rate number itself is unremarkable.

**Step 8 — Log the diagnosis and one experiment**
Write the one-line diagnosis in Tab A and the single next experiment in Tab B. Never carry more
than one active experiment into the next video — changing title, thumbnail, and cold-open
structure simultaneously makes it impossible to tell which change did anything.

---

## 3. Highest-impact-improvement decision tree

Read top to bottom; stop at the first pattern that matches this video/week.

```
Is CTR below ~4% (healthy zone is roughly 4-6%, series average may run higher once branded)?
├─ YES → Is average % viewed also low (well below similar-length videos)?
│         ├─ YES → Double problem. Fix thumbnail/title FIRST (cheapest test).
│         │         If a re-thumbnail doesn't lift CTR within a week, the premise/topic
│         │         itself likely doesn't have pull — revisit the episode concept.
│         └─ NO  → Packaging-only problem. The content holds people who click, they're
│                   just not clicking. TEST: new thumbnail (bigger faces/expressions,
│                   higher contrast, one clear focal subject) and/or a punchier title
│                   naming a specific stake (a House, a name, a threat) instead of a
│                   vague episode label.
└─ NO (CTR healthy) → Is retention weak in the first 30 seconds specifically?
          ├─ YES → Hook problem. TEST: rewrite the cold open to open on the stakes/
          │         conflict/cliffhanger instead of setup — cut faster into the
          │         "why should I care" moment. Don't touch the thumbnail; it's working.
          └─ NO  → Is there a retention cliff at one identifiable mid-video timestamp?
                    ├─ YES → Pacing/edit problem at that specific point. TEST: tighten or
                    │         cut the section right before the drop (likely a lull,
                    │         repeated explanation, or slow build-up); consider moving a
                    │         teaser of the payoff earlier to bridge it.
                    └─ NO  → Retention curve is healthy and CTR is healthy.
                              → This is a "what's working" video, not a "what's broken"
                                one. Don't fix anything — instead, mine it: note the
                                title pattern, thumbnail composition, and cold-open
                                structure, and deliberately repeat them. Also check
                                Traffic Sources: if Suggested/Browse is climbing here
                                specifically, the algorithm has started trusting this
                                type of episode — lean into more of exactly this.

Separately, regardless of the above — is Returning Viewer % flat or falling across
the last 3-4 uploads even when individual-video metrics look fine?
└─ YES → Series-level problem, not a video-level one. Single episodes are fine on
          their own but the series isn't building a habit. TEST: strengthen
          episode-to-episode continuity cues (recaps, "previously on," explicit
          teases of the next episode at the end) and check publishing consistency
          (Section 2, Step 1) — irregular schedules erode the "come back" habit
          faster than any single content issue.
```

---

## 4. Revenue metrics — track only after YPP monetization

**Gate**: revenue metrics do not exist and should not be tracked as goals until the channel is
accepted into the YouTube Partner Program (YPP). As of 2026 the standard path is **1,000
subscribers + 4,000 public watch hours in the trailing 365 days** (there is also an alternate path
via Shorts views, and a newer reduced first-tier threshold YouTube has piloted in some regions —
Austin should re-check the exact numbers in YouTube Studio → **Earn** tab once the channel is
close, since program terms shift). Until then, Section 0-3 above (CTR, retention, traffic,
returning viewers) are the entire tracking system — they are the leading indicators that
determine whether the 4,000-watch-hour bar gets hit at all, so there is no revenue number to
distract from that work.

**Once accepted**, add this to the Weekly Channel Snapshot (Tab B), pulled from YouTube Studio →
**Earn → Revenue reports / Analytics → Revenue tab**:

| Column | Definition | Where in YouTube Studio |
|---|---|---|
| Estimated ad revenue (7-day, $) | Gross estimated earnings from ads on the channel's videos this week | Earn tab / Revenue analytics |
| CPM ($) | What advertisers pay per 1,000 *ad* impressions, before YouTube's cut — reflects how valuable the audience/content is to advertisers | Revenue analytics (Advanced mode) |
| RPM ($) | What the creator actually earns per 1,000 *views* (all monetized playback, after YouTube's ~45% revenue share and unmonetized views factored in) — always lower than CPM, the number that actually predicts payout | Revenue analytics (Advanced mode) |
| Monetized playbacks (%) | Share of views that served an ad at all | Revenue analytics |
| Ad types breakdown (skippable / non-skippable / mid-roll / bumper) | Which formats are running and their relative earnings | Revenue analytics |
| Non-ad revenue (memberships/Super Thanks/shopping, if enabled) | Any revenue outside straight ad serving | Earn tab |

Read CPM and RPM together, not RPM alone: a low RPM with a healthy CPM usually means low
monetized-playback rate (ad blockers, ineligible countries, or too few ad breaks) rather than a
content/advertiser-demand problem — check "monetized playbacks %" before concluding the content
itself is under-monetized.

---

## Sources consulted (2026)

- [Decoding CTR & impressions in your Analytics — YouTube Help](https://support.google.com/youtube/answer/16767369?hl=en)
- [Impressions & click-through-rate FAQs — YouTube Help](https://support.google.com/youtube/answer/7628154?hl=en)
- [Understand ad revenue analytics — YouTube Help](https://support.google.com/youtube/answer/9314357?hl=en)
- [Understand your YouTube content performance — YouTube Studio App Help](https://support.google.com/youtubecreatorstudio/answer/12220281?hl=en-GB&co=GENIE.Platform%3DAndroid)
- [YouTube Video Analytics: The 6 Most Important Metrics (2026 Guide) — vidiq](https://vidiq.com/blog/post/youtube-channel-analytics/)
- [YouTube Average View Duration: What Is a Good AVD? — vidiq](https://vidiq.com/blog/post/average-view-duration/)
- [YouTube Partner Program: Requirements and How to Join in 2026 — vidiq](https://vidiq.com/blog/post/youtube-partner-program-guide/)
- [YouTube Traffic Sources Explained: Browse Features, Search & More (2026) — humbleandbrag](https://humbleandbrag.com/blog/youtube-traffic-sources)
- [YouTube Audience Retention Benchmarks 2026 — humbleandbrag](https://humbleandbrag.com/blog/youtube-audience-retention-benchmarks)
- [YouTube CPM & RPM — A Guide to Understanding YouTube Ad Revenue Metrics — creator-hero](https://www.creator-hero.com/blog/youtube-cpm-rpm---a-guide-to-understanding-youtube-ad-revenue-metrics)
