# Facebook Ads — Fiction Site Traffic Playbook

Load this reference when the user asks about Facebook advertising, ad copy, taglines for promotion, cover image requirements for ads, or campaign setup for fiction sites.

---

## Beginner's Wiki — Facebook Ads Concepts

Everything a first-time advertiser needs to know before running a single dollar. Read this section before anything else.

---

### Facebook Pixel — what it is and why it matters

**What it is:** A small piece of JavaScript code you paste into your website's `<head>`. Once installed, it sends an event to Facebook every time someone visits a page, clicks something, or takes an action (like reading a chapter).

**What it does for you:** Facebook uses this data to:
1. Know who visited your site — so it can find more people just like them (Lookalike Audiences)
2. Track whether someone who saw your ad actually came to your site (attribution)
3. Optimize delivery toward people who are most likely to do what you want (read, click, stay)

**Without a Pixel:** You are flying blind. Facebook shows your ad to whoever its guess says is right. With a Pixel, it learns from real visitor behavior and improves targeting automatically over time.

**In this project:** The Pixel ID is set in `fictions/CLAUDE.md` under `facebook_pixel`. All sites in this project share Pixel `1549585523220726`. The code is injected in `src/app/layout.tsx`. Two events fire automatically: `PageView` on every page load.

**One critical rule:** The Pixel must fire *before* any ad spend. Run at least 500–1,000 organic pageviews through the site first so the Pixel has baseline data. Cold Pixels (zero events) make the algorithm guess randomly.

---

### Campaign Structure — the three-level hierarchy

Every Facebook ad lives inside a three-level hierarchy. Confusing these levels is the most common beginner mistake.

```
Campaign
  └── Ad Set (one or more)
        └── Ad (one or more)
```

| Level | You control | Analogy |
|---|---|---|
| **Campaign** | Objective (what you want people to do) | The goal of the entire effort |
| **Ad Set** | Budget, audience, schedule, placement | Who sees it, when, for how much |
| **Ad** | The actual image + copy the user sees | The creative itself |

**Campaign objective for fiction sites:** Choose **Traffic** (sends people to your URL) or **Engagement** (optimizes for reactions and shares). Do not choose Conversions unless your Pixel is firing purchase events — which fiction sites don't have.

**One campaign, multiple ad sets:** Run 2–3 ad sets with different audiences under one campaign. Facebook will automatically shift budget toward the best-performing one if you use CBO (see below).

---

### Budget Types — CBO vs ABO

**ABO (Ad Set Budget Optimization):** You set a fixed daily budget on each ad set individually. If you have 3 ad sets at $10/day each, you spend $30/day total regardless of which one performs.

**CBO (Campaign Budget Optimization):** You set one budget at the campaign level. Facebook automatically shifts spend toward whichever ad set is performing best that day.

**For beginners: start with CBO.** It reduces the number of decisions you have to make and lets Facebook's algorithm do the optimization work. Set $20–50/day at the campaign level and let it run for at least 3–5 days before drawing conclusions.

---

### Audiences — the three types

**Core Audience (Interest Targeting):** You manually pick demographics, interests, and behaviors. Example: Women 25–45 in the US who follow "Kindle Unlimited" or "romance novels." This is where beginners start.

**Custom Audience:** Built from your own data — people who visited your site (via Pixel), people on your email list, or people who watched your video. Requires existing traffic. Not useful until you have at least 1,000 Pixel events.

**Lookalike Audience:** Facebook finds new people who look statistically similar to your Custom Audience. Example: "Find me 1 million people similar to the 500 who read more than 3 chapters on my site." This is the most powerful targeting type — but requires a Custom Audience as its source first.

**Practical order for fiction sites:**
1. Start with Core Audience (interest targeting: romance readers, Kindle, specific sub-genres)
2. After 2–4 weeks and 1,000+ Pixel events: create a Custom Audience of site visitors
3. After Custom Audience has 500+ people: create a 1% Lookalike Audience

---

### Key Metrics — what each number means

| Metric | What it means | What's "good" for fiction |
|---|---|---|
| **CPM** (Cost Per Mille) | Cost per 1,000 impressions — how much to show your ad 1,000 times | $8–20 for the US; lower = your creative is being favored |
| **CTR** (Click-Through Rate) | % of people who saw the ad and clicked | ≥ 1.5% is solid; ≥ 3% is excellent for fiction |
| **CPC** (Cost Per Click) | How much you pay each time someone clicks | < $0.50 is the target for arbitrage to work |
| **Frequency** | Average number of times one person saw your ad | Keep below 3 in the first week; above 5 = audience fatigue |
| **ROAS** | Return on Ad Spend — revenue / ad spend | Fiction arbitrage target: ROAS > 1.5× (AdSense revenue vs. ad cost) |
| **Landing Page Views** | People who actually loaded your site (vs. just clicked) | Should be 70–80% of Link Clicks; lower = slow page load hurting you |

**The metric that matters most for this business model:** CPC. Your profit equation is:

```
Profit per click = (avg pageviews per session × RPM / 1000) − CPC
```

If your RPM is $8 and users average 4 pageviews, you earn $0.032 per pageview, or ~$0.128 per session. You need CPC < $0.12 to break even. Target CPC < $0.08 to profit.

---

### The Learning Phase — why you must not touch the ad for 7 days

When you launch a new ad set, Facebook enters a **Learning Phase**. It needs to show your ad to ~50 people who take your desired action before it knows who to target efficiently. During this phase:

- Performance will be unstable and often bad
- CPM and CPC will be higher than normal
- The algorithm is still guessing

**The rule:** Do not change your budget, audience, or ad creative during the Learning Phase. Any significant change resets the learning and you start over. Wait a minimum of 7 days and 50 optimization events before judging performance or making changes.

**"Learning Limited" warning:** If Facebook shows this label, your budget is too low or your audience is too small to collect enough events. Fix: increase the daily budget or broaden the audience.

---

### Ad Account vs. Business Manager vs. Page

These three things are different and beginners constantly confuse them.

| Thing | What it is | You need it for |
|---|---|---|
| **Facebook Page** | Your public-facing Facebook presence | Required to run ads at all |
| **Ad Account** | The billing account where your ads live | Running ads, setting budgets, holding your credit card |
| **Business Manager (Meta Business Suite)** | The container that holds your Pages and Ad Accounts | Managing multiple ad accounts or giving team members access |

**Practical setup:** Create one Business Manager → add your Page → create an Ad Account inside it → add your credit card to the Ad Account. Never run ads directly from a personal profile.

---

### What Gets Your Ad Account Banned

Facebook reviews landing pages, not just creatives. Your account can be restricted or permanently banned for:

| Violation | Example |
|---|---|
| **Misleading claims** | "Doctors hate this trick", fake endorsements, before/after comparisons |
| **Explicit sexual content** | Nipples, genitals, sex acts in the ad image or on the landing page |
| **Cloaking** | Showing Facebook reviewers a different page than what ad clickers see |
| **Missing trust pages** | No Privacy Policy, no Terms of Service, no About page |
| **Prohibited content categories** | Tobacco, weapons, MLM, payday loans — doesn't apply to fiction |

**For fiction sites specifically:** Suggestive covers (bare shoulders, implied intimacy) are fine. Explicit/pornographic imagery is not. The distinction: allure and tension = fine; exposed genitals or sex acts = account ban. See `references/cover-allure-elements.md` §0 for the exact line.

**If your account gets restricted:** Do not create a new account immediately — Facebook links accounts by payment method, IP, and device. First file a review appeal through Meta's support portal. Creating a second account while restricted = permanent ban.

---

### Attribution Window — what the numbers actually count

When Facebook says "this campaign got 500 clicks," which 500? Attribution windows define how long after seeing your ad Facebook credits you a result.

**Default (recommended for fiction):** 7-day click, 1-day view
- "7-day click": if someone clicked your ad and visited your site within 7 days, it counts
- "1-day view": if someone only saw your ad (no click) and visited within 1 day, it also counts

**Why this matters:** If you compare Facebook's reported clicks to your Google Analytics sessions, they will never match. Facebook counts views; Analytics counts sessions with different cookies. Expect a 20–40% gap. Neither is wrong — they measure different things.

---

### Creative Fatigue — when to refresh your ads

**Creative fatigue** happens when the same people see your ad too many times and stop responding. Signs:
- CTR drops more than 30% from week 1 to week 2
- Frequency above 4 with no new audience expansion
- CPM rising week-over-week with stable targeting

**Fix:** Create 2–3 ad variations (different tagline, same image; or different image, same copy) and run them simultaneously. Facebook will automatically favor the one with better engagement.

**Rule of thumb for fiction:** Refresh creative every 3–4 weeks for ongoing campaigns. For a new site launch, prepare at least 3 image + copy variants before spending.

---

## What Makes Fiction Ads Work on Facebook

Fiction readers on Facebook are not searching — they are scrolling. The ad has 0.3 seconds to interrupt the feed. Everything below is built around that constraint.

**The two-asset model:** Every Facebook ad for a fiction site needs exactly two things working together:
1. **Tagline** — the copy that hooks in the first 8 words
2. **Cover image** — the visual that stops the scroll before the copy is read

Both must tell the same implied story. A shocking image with bland copy fails. Great copy with a stock-photo cover fails. They amplify each other.

---

## Tagline Standards (Facebook Copy)

### Core principle

The tagline is not a book description. It is the one sentence that makes someone think *"I need to know what happens next"* before they realize they've already tapped.

### Structure: Setup → Reversal → Unresolved tension

Every high-CTR fiction tagline has the same skeleton:

```
[Situation that seems normal or controlled]
[Reversal that flips who has power or what is true]
[One unresolved detail that forces a click]
```

Examples:
- "Fake marriage. Six-month contract. Clean business deal with an expiration date. He keeps showing up at 3am with printed spreadsheets when she's in crisis — and the contract ends in two weeks. He hasn't brought it up."
- "For six weeks she vented to a stranger about her nightmare boss. Then she found his business card in her car. The stranger WAS her boss — and he'd known for two weeks and said nothing."

### Writing rules

**Length:** 25–40 words. Mobile feeds show roughly 3 lines of body text before "See more." The hook must land inside those 3 lines.

**Opening 8 words:** Must contain either a curiosity gap OR an emotional punch. Never start with character names or scene-setting. Test: cover the rest of the tagline — do the first 8 words make someone want to read on?

| Weak opening | Strong opening |
|---|---|
| "Elena Vargas has been running for eighteen months..." | "She's been running for eighteen months — and the man protecting her was there that night." |
| "When Nora Blake's sister disappeared in Prague..." | "Her sister vanished. The only lead: a sealed vault with a man inside who hadn't aged in six centuries." |
| "In a world where your score determines everything..." | "In this city, your score is your life. One morning hers hit zero. No error. No appeal." |

**Sentence rhythm:** Short sentences hit harder. Vary length — one long setup, one short reversal, one short unresolved detail.

**The final line:** Always unresolved. Never conclude. The reader should feel *"and then what?"* as a physical pull.

| Weak final line | Strong final line |
|---|---|
| "...and they both fell in love." | "...and he hasn't brought it up." |
| "...but she couldn't resist him." | "...she cannot find the lie she needs." |
| "...everything changed between them." | "...she's still there. The debt stopped being the point somewhere in week two." |

**Power words that earn their place:** "already knew", "hasn't mentioned it", "stopped being the point", "said nothing", "recognized it", "hasn't filed the report" — words that imply someone has information the reader doesn't.

### Genre-specific angles

| Genre | Angle that works on Facebook |
|---|---|
| Billionaire / dark romance | Discovery of manipulation ("he built the job for her two years before she applied") |
| Paranormal / shifter | Involuntary recognition ("the alpha looked at her like something inside him just snapped") |
| Contract marriage / fake dating | Contract expiration ignored ("the end date passed. He hasn't brought it up.") |
| Enemies to lovers | Reluctant respect ("he was right. She hates that he was right.") |
| Second chance | Unavoidable proximity ("seven years of silence. Then he walked in as her new attending.") |
| Revenge romance | The plan disrupted by a human detail ("the plan couldn't survive the gentleness he showed a small boy") |
| Mystery / thriller | Evidence of cover-up ("the village called it an accident before the body was cold") |

### What to avoid

- Adjective-heavy prose ("brooding", "mysterious", "irresistible", "smoldering") — these are generic and invisible
- Telling the emotion instead of showing the situation ("their forbidden love burned bright")
- Ending on a resolution — always leave the thread hanging
- More than one question mark — one rhetorical question is a hook; two is a quiz

---

## Cover Image Standards (Facebook Creative)

See `references/story-cover.md` Step 1.7 for the full technical spec. Summary here for ad context:

### Five scroll-stop signals

| Signal | What it does |
|---|---|
| **Expression** | One unmistakable emotion on the female lead's face — shocked, longing, torn, furious. Never neutral. |
| **Depth composition** | Female lead large in foreground (65% of frame), male lead smaller in background. Creates "what happened between them?" instantly. |
| **Implied story** | Viewer constructs a 3-word premise in 0.3 seconds: "morning after scandal", "forbidden attraction exposed", "dangerous obsession discovered". |
| **World signal** | One background element identifies the story world without the title: city penthouse = billionaire; candlelit manor = Regency; neon rain = cyberpunk. |
| **Partial reveal** | Bare shoulders + clutched sheet > full exposure. Suggestion generates more CTR than explicit. Better Facebook delivery too. |

### High-performing composition template (billionaire / dark romance)

Extracted from a proven high-CTR Facebook creative:

```
photorealistic cinematic photograph, luxury penthouse bedroom,
floor-to-ceiling windows with city skyline at dawn, warm golden morning light,

female lead [ethnicity + hair], late 20s, bare shoulders,
clutching white bedsheet to chest, wide eyes looking off-camera with shocked expression,
lips slightly parted, positioned large in foreground filling 65% of frame height,

male lead [ethnicity + hair], late 20s–mid-30s, casual open-collar shirt,
seated on bed behind her, watching her with quiet intensity,
positioned smaller in mid-ground,

white linen bedding, warm amber morning light, soft bokeh depth of field,
cinematic depth of field, dark romance novel cover composition, photorealistic, 8k
```

### Image + copy pairing rule

The image and tagline must imply the same scene without repeating each other.

| If the image shows | The tagline should imply |
|---|---|
| Woman clutching sheet, man watching from bed | What she just discovered, not the morning itself |
| Two people in charged proximity | What neither of them is saying |
| Woman alone with a document / object | What that object reveals that changes everything |
| Man behind her, she doesn't see him yet | What he already knows that she doesn't |

---

## Campaign Setup Notes

### Audience targeting angles for romance fiction

Facebook algorithm reads the tagline + image together to find the audience. Writing for the reader, not for the algorithm, produces better auto-targeting.

**Primary audiences that convert for fiction sites:**
- Women 25–45 interested in romance novels, Kindle Unlimited, BookTok, Wattpad
- Lookalike audiences from email list (if available)
- Interest: specific romance sub-genres (paranormal romance, dark romance, historical romance)

**Do not target broadly by "reading" interest** — the creative (image + tagline) does the targeting. A dark romance cover with the right tagline will self-select the right audience more precisely than interest layers.

### Ad format recommendations

| Format | When to use |
|---|---|
| Single image | Fastest to test; use the book cover + tagline in the ad copy |
| Carousel | Multiple books from the same site; each card = one book cover + short tagline |
| Video (slideshow) | Animate the cover with Ken Burns effect + tagline appearing word by word — high engagement for romance |

### Copy structure for the full ad unit

```
[Tagline — 25–40 words, follows the rules above]

[CTA line — 1 sentence, tells them exactly what to click]
Example: "Read Chapter 1 free →" or "Start reading now — no sign-up required."

[URL — the book's chapter 1 or the site homepage]
```

Keep the copy above the "See more" fold. The tagline is the entire body — no additional paragraphs.

### High-performing composition template 2 — three-character power hierarchy (dark romance / mafia / cartel)

Extracted from a proven high-CTR Facebook creative. Outperforms two-character compositions because the viewer must decode three relationships simultaneously — that cognitive load keeps them on the image longer.

```
photorealistic cinematic photograph, underground parking garage,
concrete pillars, luxury black SUV in background,
dramatic low ambient lighting, dark moody atmosphere,

three-character power dynamic composition:

antagonist: [ethnicity + hair] woman, sleek hair pulled back tight,
wearing sharp [color] business suit,
pointing finger down aggressively at woman on the ground,
cold authoritative expression, standing tall, commanding,

protagonist: young woman, long [hair] disheveled,
wearing [color] casual clothing, kneeling on concrete floor,
looking up with frightened defeated expression, visibly distressed,

ally or rival: [ethnicity + hair] woman, wearing [color] fitted outfit,
kneeling beside protagonist in protective stance,
reaching toward her, expression of fierce concern,

cinematic thriller composition, three-way female power hierarchy,
dark mafia-romance atmosphere, photorealistic, 8k
```

**Why three-character compositions outperform on Facebook:**

| Three-character advantage | Why it works |
|---|---|
| Viewer must decode three relationships | Longer dwell time before the scroll continues |
| Physical height hierarchy (standing vs. kneeling) | Power dynamic is legible in under 0.1 seconds |
| Ambiguous third character | "Is she friend or enemy?" forces a click |
| No male characters required | Female power conflict hooks romance audiences directly |
| Accusation gesture (pointing finger) | Single most visceral confrontation signal — instantly raises "what did she do?" |

**3-word implied story:** "betrayal costs everything" / "she paid the price" / "two sides, one woman"

---

### What to A/B test first

1. **Tagline variant** (same image, two different taglines) — fastest signal on which hook wins
2. **Opening line** (same tagline structure, different first 8 words) — tests the scroll-stop moment
3. **Image composition** (same book, different scene: morning-after vs. discovery moment vs. confrontation)

Never test image AND copy simultaneously in early rounds — isolate the variable.

---

## Quick Reference: Tagline Checklist Before Publishing

- [ ] First 8 words contain a curiosity gap or emotional punch
- [ ] 25–40 words total
- [ ] One clear reversal of power or expectation
- [ ] Final line is unresolved — no conclusion
- [ ] No generic adjectives ("brooding", "forbidden", "irresistible" as standalone descriptors)
- [ ] Image and tagline imply the same scene without repeating each other
- [ ] Cover passes the 0.3-second test: viewer feels something before reading the copy
