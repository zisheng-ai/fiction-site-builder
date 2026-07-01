# Fiction Niche Researcher

## When to Run This

Run this reference **once per book**, not once per site. A site can have multiple books, each with its own niche research.

**Multi-book sites:** When generating multiple books for the same site, run this independently for each book. Selecting the same genre cluster as another book on the site is acceptable — genre repetition is allowed and expected. Optimize each book for demand independently; do not coordinate genres or try to maximize variety across the site.

Load and run whenever:
- Starting a new book (first book on a new site, or adding a book to an existing site)
- `outputs/{site-slug}/{book-slug}/niche-research.json` does not exist
- The user has NOT already stated the genre, tropes, and story premise explicitly

Skip (read the existing JSON instead) when:
- `outputs/{site-slug}/{book-slug}/niche-research.json` already exists for this book
- The user has stated the genre and premise — document them in `tracking/context.md` directly and proceed

---

Use this reference to pick a genre × trope combination with real reader demand, a differentiated story angle, and a clear path to social traffic and AdSense approval.

## The Opportunity Formula

**Fiction opportunity = reader demand × trope freshness × producibility × monetization safety × distribution fit**

All five factors multiply — a zero in any one factor kills the opportunity. Do not start with "what should I write?" Start with: **which reader has a craving that existing stories aren't fully satisfying? What trope combination gives them that hit? Can you write it well? Will the traffic convert to ad revenue?**

---

## Platform & Language Targeting

Fiction traffic is platform-driven, not search-driven. Pick your distribution channel before evaluating any genre — the same story can succeed on TikTok BookTok and fail on Wattpad because the format expectations differ.

### Platform tiers by expected traffic profile

| Platform | Dominant audience | Content format | Traffic type |
| --- | --- | --- | --- |
| **TikTok BookTok (EN)** | F 18–34, US/UK/AU | Short clips, quotes, trope tags | Viral, spiky, social |
| **Pinterest (EN)** | F 25–44, US | Aesthetic boards, cover art, quote cards | Evergreen, steady |
| **Reddit r/RomanceBooks, r/Fantasy, r/horrorlit, r/mysterybooks, r/scifibooks** | Varies by genre | Community recs, discussion threads | Referral, high intent |
| **Wattpad** | F 13–25, global | Long serialized reads | Organic, loyal |
| **Webnovel / Fizzo** | M+F 18–30, SEA/CN | Fast-paced chapters, power fantasy | In-app only, hard to funnel externally |
| **Facebook Groups (romance, horror, mystery, dark fantasy)** | F 30–50, US | Group posts, share-fests | Referral, high-volume |

Default target: **English, US-dominant**. Platform selection depends on genre — romance/drama leans TikTok BookTok + Pinterest + Facebook groups; mystery/thriller leans Reddit + Goodreads; horror/fantasy leans Reddit + Discord community + Pinterest. Pick the platform where your genre's readers already gather; highest ad RPM comes from matching audience intent to advertiser vertical.

### What platform choice affects downstream

- **Cover design:** BookTok favors cinematic two-person drama covers. Pinterest favors aesthetic/mood boards. Wattpad favors illustrated character art.
- **Chapter length:** TikTok funnel → short punchy chapters (1 500–2 500 words). Wattpad organic → longer chapters (3 000–5 000 words).
- **Update cadence:** Serialized platforms (Wattpad, Webnovel) reward frequent updates. H5 sites for social traffic can launch complete.
- **Content tone:** BookTok skews toward dramatic, emotionally intense tropes with a strong "hook sentence." Reddit skews toward well-crafted prose and originality signals.

Record `primary_platform` in `niche-research.json`.

---

## Step 1: Find Genre × Trope Candidates

Generate at least 3× more candidates than you need before scoring any.

### Where to find demand signals

**Social platforms (highest signal for fiction):**
- TikTok: search `#[genre/trope]` — check total views and recency of top videos. Views >50M on a genre tag = proven demand. Examples: `#darkromance`, `#mysterythriller`, `#horrorreads`, `#epicfantasy`, `#dystopianfiction`.
- Pinterest: search the genre or trope as a phrase — pin volume and board freshness signal sustained interest.
- Reddit: `r/RomanceBooks`, `r/fantasyromance`, `r/horrorlit`, `r/scifi`, `r/Fantasy`, `r/ifyoulikeblank` — search the trope and read what readers say they can't find enough of. "Does anyone know more books like X?" is a gap signal.
- Facebook groups: search your genre keywords — group size and post frequency indicate audience depth. Examples: "dark romance books," "horror fiction fans," "fantasy book club."

**Fiction platforms:**
- Wattpad trending list by genre — what's rising this week vs. last month.
- Webnovel/GoodNovel hot list — fast-rising titles signal demand.
- Amazon Kindle Unlimited bestsellers by genre — the commercial market lags social trends by 3–6 months; use as confirmation, not discovery.

**Community signals:**
- Reddit AMA threads and "what tropes do you want MORE of" posts.
- GoodReads "Readers Also Enjoyed" chains on a trending title — adjacent tropes.
- BookTok comment sections: "PLEASE write more of this" = unmet demand.

### Candidate types to prefer

Each genre has its own community, demand signals, and trope language. Pick the genre that fits the **target site's tone** (see `CLAUDE.md` site table) first, then find the best trope angle within that genre.

| Genre | Hot trope / angle combinations | Primary platform signal |
| --- | --- | --- |
| **Romance — Dark / Mafia** | Enemies to lovers + forced proximity + possessive hero; morally grey captor | `#darkromance` 15B+ TikTok views |
| **Romance — Paranormal** | Alpha werewolf + fated mates + rejected mate arc | `#wolfromance` `#materomance` |
| **Romance — Contemporary** | Cold CEO + contract marriage; rivals to lovers; small-town second chance | `#ceoromance` `#sportsromance` |
| **Mystery / Cosy Mystery** | Amateur detective + closed setting + cast of suspects; cold case revival | `#mysterythriller` Reddit `r/cozynoir` |
| **Thriller / Suspense** | Unreliable narrator + hidden identity + ticking clock | `#psychologicalthriller` `#thrillerbooks` |
| **Horror** | Haunted location + unreliable senses + isolation; folk horror + outsider | `#horrorreads` `#horrorbooks` Reddit `r/horrorlit` |
| **Epic / Dark Fantasy** | Chosen burden + political intrigue + magic cost; fae court + mortal bargain | `#epicfantasy` `#darkfantasy` Reddit `r/Fantasy` |
| **Sci-Fi / Dystopian** | Resistance cell + surveillance state + one person who sees the truth; first contact | `#dystopian` `#scifi` Reddit `r/scifi` |

Prefer combinations where:
- At least two tropes or tension angles overlap (readers search the intersection, not just one)
- There is a visible reader community around the combination (subreddit, hashtag, Facebook group)
- There is a clear escalating arc you can structure as chapter-ending hooks

Avoid:
- Single-angle stories with no combination (low differentiation)
- Sub-genres where the top titles have 100M+ Wattpad reads (too saturated to break through organically)
- Stories that require deep proprietary world-building before the first hook — if you can't open in medias res in chapter 1, reconsider scope

---

## Step 2: Validate Reader Demand

Before scoring, confirm the genre × trope combo has real reader demand.

### Three-signal demand check

All three must pass:

1. **Social proof** — at least one TikTok hashtag related to this trope has >10M total views, OR a Reddit thread about this trope has >200 upvotes in the last 6 months.
2. **Existing successful titles** — you can name at least 3 titles (any platform) in this exact trope combo with confirmed readership (Wattpad reads >500K, KU bestseller, or BookTok viral). This proves the market exists and readers return to the sub-genre.
3. **Reader appetite gap** — community evidence (Reddit comments, BookTok comments, Facebook posts) that readers want MORE of this trope. Absence of complaints about oversaturation.

Reject candidates that fail any of these three checks.

### Demand dimensions

| Dimension | What to measure | Where to check |
| --- | --- | --- |
| **Trope tag views** | Total TikTok views on primary trope hashtag | TikTok hashtag search |
| **Community depth** | Active subreddit or Facebook group dedicated to this sub-genre | Reddit, Facebook Groups |
| **Title density** | How many existing titles in this exact combo? Sparse (<20 active titles) = gap; saturated (>500) = harder entry | Wattpad search, Amazon KU filter |
| **Recency** | Is demand rising, flat, or falling? | Google Trends (trope as phrase), TikTok video recency |
| **Emotional hook strength** | Can the premise be stated in one sentence that triggers a strong emotional reaction? | Gut check + test against 5 similar titles |

### Competitive landscape check

For the top 3–5 existing titles in your target genre × trope combo:

| Signal | What to look for |
| --- | --- |
| Chapter count and update frequency | Serialized? Complete? Cliffhanger density? |
| Reader comments | What are readers praising? What are they asking for that the story doesn't give them? |
| Cover and title conventions | What visual/naming patterns does this sub-genre use? You need to fit in before you can stand out. |
| Prose style | Is the market's standard first-person present or third-person past? How short are the chapters? |
| Weakness to exploit | Thin world-building, weak protagonist agency, slow pacing, abrupt ending, unresolved tension — pick one weakness to beat |

Record one `differentiation_angle` per candidate: the specific thing your story does that the top titles don't. This feeds the story brief in A1.

---

## Step 3: Content Producibility Assessment

A niche you can't write well at speed is not viable regardless of demand.

| Factor | Assessment question |
| --- | --- |
| **Genre fluency** | Have you read (or is Claude trained on) enough titles in this sub-genre to replicate the emotional beats, pacing, and dialogue register? |
| **World complexity** | How much world-building is required before the first chapter? Contemporary = zero. Paranormal = light. Epic fantasy = heavy. |
| **Chapter structure** | Does this genre follow recognizable chapter patterns? Romance: meeting → tension → almost-moment → cliffhanger. Mystery: discovery → investigation → red herring → revelation. Horror: normalcy → unease → escalation → confrontation. Predictable genre structure = easier to produce at volume. |
| **Content intensity** | Romance: steamy / closed-door at peak = AdSense-safe default; explicit = policy risk. Horror: graphic violence → AdSense-safe if not gratuitous. All genres: no explicit sex, no graphic content sexualizing minors. See Step 4 for full policy rules. |
| **Target chapter count** | Can the story be told in 15–20 chapters at 1 500–2 000 words each? If yes, it's producible in one session. If it needs 50+ chapters, plan for serialized delivery. |

Score producibility 1–5. Below 3 = reject unless you have a specific reason to proceed.

---

## Step 4: AdSense Policy Safety Assessment

Fiction sites can be approved for AdSense. Most genre fiction qualifies. A small set of content types does not.

### Disqualified content (hard rejection)

| Content type | Why disqualified |
| --- | --- |
| Sexually explicit / pornographic prose | AdSense explicit content policy — regardless of whether it's labeled "fiction" |
| Content sexualizing minors (even implied) | Hard banned, no exceptions |
| Graphic torture / gore as primary content | Violent content policy |
| Real-person fiction in defamatory or sexual framing | Legal and policy risk |
| Content that glorifies violence against real groups | Hate content policy |

### High-risk (proceed with care)

| Content type | Risk | Safer angle |
| --- | --- | --- |
| Dark romance with non-consent elements | Can trigger content flags | Frame as "morally complex," keep explicit force off-page; focus on emotional complexity |
| Mafia / crime fiction with detailed criminal methods | Can read as instructional | Keep methods vague; focus on emotional/relational stakes |
| Vampire / supernatural with graphic blood scenes | Borderline violence | Keep blood atmospheric, not gratuitous |
| Reverse harem / polyamory | Generally fine for AdSense; some ad networks flag | Proceed; just avoid explicit scenes |

**For romance genres:** Default to steamy but not explicit — sexual tension, implied scenes, fade-to-black or closed-door at the peak intimate moment. Readers understand; AdSense approves.

**For non-romance genres (mystery, horror, fantasy, sci-fi):** Sexual content is not the primary risk. Watch for graphic violence, torture, or body horror as the primary content — atmospheric tension is fine, sustained gore is not.

### Advertiser demand by fiction genre

| Genre | Expected AdSense RPM | Reason |
| --- | --- | --- |
| Romance (all sub-genres) | Moderate–High | Female 18–45 audience; beauty, fashion, relationship product advertisers |
| Paranormal / Fantasy Romance | Moderate | Broad demographic; entertainment product advertisers |
| Dark Romance / Mafia | Moderate | Some advertiser exclusions due to content tone; partially offset by high session time |
| Cosy Mystery / Thriller | Moderate | Book, streaming, and home product advertisers |
| Horror | Low–Moderate | Niche audience; some advertiser avoidance of dark content |
| Fantasy / Sci-Fi | Low–Moderate | Narrower audience; entertainment and tech advertiser crossover |
| Literary Fiction | Low | Small audience; low commercial advertiser interest |

---

## Step 5: Score Candidates

Score each candidate 1–5 on all five dimensions. Select only candidates averaging ≥ 3.5 with no dimension below 2.

| Dimension | Meaning |
| --- | --- |
| `reader_demand` | Active community, growing hashtag views, confirmed existing readership |
| `trope_freshness` | The specific combination feels distinctive within the sub-genre |
| `producibility` | Can be written well at target chapter count within a single session |
| `differentiation` | Clear one-line angle that beats the top 3 incumbents on at least one axis |
| `adsense_safety` | Content is policy-safe; no explicit material; advertiser-friendly audience |

`adsense_safety` is a hard gate: any candidate scoring below 3 is rejected regardless of other scores.

---

## Output

Write `outputs/{site-slug}/{book-slug}/niche-research.json`.

**Romance example:**

```json
{
  "site_slug": "velvet-throne",
  "primary_platform": "tiktok-booktok | pinterest | facebook-groups",
  "target_language": "en",
  "target_market": "en-us",
  "selected_genre": "Dark Romance",
  "selected_tropes": ["CEO / billionaire", "enemies to lovers", "forced proximity"],
  "demand_validation": {
    "social_signal": "TikTok #darkromance 15B+ views",
    "existing_titles_confirmed": ["Title A", "Title B", "Title C"],
    "community_gap_evidence": "Reddit r/RomanceBooks: 'Why is there no dark CEO romance where the female lead actually has leverage?'"
  },
  "competitive_brief": [
    {
      "title": "His Obsession",
      "platform": "Wattpad",
      "reads": "12M",
      "weakness": "FMC is passive; plot resolves via the hero rescuing her in every arc",
      "beat_action": "FMC holds real power in at least 2 out of 3 major turning points"
    }
  ],
  "differentiation_angle": "FMC is the CEO's legal adversary — she can destroy his company; he can't let her go",
  "producibility": {
    "genre_fluency": 5,
    "world_complexity": "contemporary — zero setup",
    "chapter_structure": "meeting → power struggle → almost-moment → cliffhanger",
    "intensity_level": "steamy / closed-door at explicit moments",
    "target_chapters": 18,
    "words_per_chapter": 1700
  },
  "adsense_policy": {
    "explicit_content": false,
    "high_risk_notes": "Dark romance framing — keep force off-page, focus on tension and emotional stakes",
    "advertiser_demand_tier": "moderate"
  },
  "score": {
    "reader_demand": 5,
    "trope_freshness": 4,
    "producibility": 5,
    "differentiation": 4,
    "adsense_safety": 4
  },
  "decision": "select"
}
```

**Cosy Mystery example:**

```json
{
  "site_slug": "london-pages",
  "primary_platform": "pinterest | reddit | facebook-groups",
  "target_language": "en-GB",
  "target_market": "en-gb",
  "selected_genre": "Cosy Mystery",
  "selected_tropes": ["amateur sleuth", "small village", "found family", "recurring cast"],
  "demand_validation": {
    "social_signal": "TikTok #cozymystery 500M+ views; Reddit r/mysterybooks active community",
    "existing_titles_confirmed": ["The Thursday Murder Club", "Richard Osman village series", "A Flicker in the Dark"],
    "community_gap_evidence": "Reddit r/mysterybooks: 'Need more cosy mysteries with a quirky protagonist who isn't a professional detective'"
  },
  "competitive_brief": [
    {
      "title": "The Thursday Murder Club",
      "platform": "Amazon KU + Reddit",
      "reads": "Bestseller",
      "weakness": "Large ensemble cast is hard to track for new readers",
      "beat_action": "Tight 2-person duo as core sleuths — easier reader attachment"
    }
  ],
  "differentiation_angle": "A retired archivist discovers murder patterns hidden inside historical documents — each crime unlocks a secret from the village's past",
  "producibility": {
    "genre_fluency": 4,
    "world_complexity": "small English village — minimal setup, recurring locations",
    "chapter_structure": "discovery → investigation → red herring → clue reveal → confrontation",
    "intensity_level": "low — no explicit content, minimal on-page violence",
    "target_chapters": 20,
    "words_per_chapter": 1800
  },
  "adsense_policy": {
    "explicit_content": false,
    "high_risk_notes": "None — cosy mystery is the most AdSense-safe fiction genre",
    "advertiser_demand_tier": "moderate"
  },
  "score": {
    "reader_demand": 4,
    "trope_freshness": 4,
    "producibility": 4,
    "differentiation": 5,
    "adsense_safety": 5
  },
  "decision": "select"
}
```

The `decision` field accepts: `"select" | "reject" | "needs research"`

---

## Completion Gate

Before advancing to A1, verify all of the following:

- [ ] `outputs/{site-slug}/{book-slug}/niche-research.json` is written and valid JSON.
- [ ] `decision` is `"select"`.
- [ ] All three demand signals confirmed: social proof, existing titles, reader gap evidence.
- [ ] `differentiation_angle` is one specific sentence — not a vague claim like "better writing."
- [ ] `adsense_safety` score ≥ 3. No explicit content, no minors, no banned categories.
- [ ] Average score ≥ 3.5, no single dimension below 2.
- [ ] `competitive_brief` has at least one entry with a concrete `beat_action` that feeds the A1 story brief.
- [ ] `producibility.target_chapters` and `words_per_chapter` are set — A1 uses these as the writing target.
