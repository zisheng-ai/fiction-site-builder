# Story Long Write

Load this reference when the user asks to write, continue, or revise long-form novel chapters.

## Niche Research Input

Before writing the first chapter of a new book, check `outputs/{site-slug}/{book-slug}/niche-research.json`:

- **Exists** → read `differentiation_angle`, `selected_tropes`, `competitive_brief[].beat_action`, and `producibility` (target chapters, words per chapter, heat level). These constrain the story brief.
- **Does not exist + user gave explicit genre/tropes/premise** → proceed directly; document them in `tracking/context.md`.
- **Does not exist + no explicit brief** → run `fiction-niche-researcher.md` first, then return here.

Continuing an existing book (adding chapters): skip this gate.

## Core Principles

1. **Emotion-first**: Every chapter has one primary emotional goal. Name it before writing a word.
2. **Validated patterns**: If a reference book exists in `reference/`, extract its technique before inventing new structure.
3. **Modular assembly**: Each chapter = hook + escalation + turn + hook-out. Each beat has a proven formula.
4. **Load only what's needed**: Before writing, read only the files relevant to this chapter's conflict and characters. Never load the full book.

## Scene-Level Drama — The Click Standard

Every scene must pass the same test as the cover image: **tension + question + desire, all three present**. A scene with only desire is erotica. A scene with only tension is thriller. A scene with only question is mystery. Romance requires all three simultaneously.

### The One-Paragraph Test

Read the opening paragraph of every scene. Ask: *does the reader feel something in the first three sentences?* If the answer is only "I understand where we are" — the scene starts too early. Cut to the moment tension is already present.

---

### Named Emotion Requirement

**Banned:** generic emotional states — "she felt nervous", "he was angry", "she was confused", "he seemed interested". These communicate the emotion's name, not the experience of it.

**Required:** emotions with internal contradiction — the character feels one thing and does or says or wants something else. Name the specific state before writing the scene.

| Named state | Internal contradiction | How it reads on the page |
|-------------|----------------------|--------------------------|
| **Barely-controlled want** | He desires; his body is fighting it | Jaw tight, deliberate distance, too-controlled voice, won't look at her directly |
| **Surrender under protest** | She's giving in; her mind still argues | She moves closer while cataloguing every reason not to, stops herself, moves again |
| **Defiance + desire** | She refuses to admit she wants this | Chin up, eye contact held too long, contempt in her voice that doesn't match her pulse |
| **Raw vulnerability** | He's exposed; he hasn't decided if he'll survive it | Short sentences, no deflection, the absence of his usual armor |
| **Cold possession** | He's certain; she hasn't been asked | Calm, unhurried, his attention on her like she's already decided |
| **Overwhelmed surrender** | She stopped fighting; she knows it | Head back, stops explaining herself, asks for nothing, takes instead |
| **Shocked recognition** | He understands something he can't undo | Goes still, the thing he was about to say dies before it leaves his mouth |

Use the named state as the scene's emotional throughline. Every action, beat of dialogue, and internal observation should be filtered through it.

---

### Power Dynamic — Make It Visible

The gap between characters is the subtext readers are buying. It must be legible without being stated.

- **Who moves, who stays still** — movement is agency; stillness is reaction or restraint
- **Who speaks, who goes quiet** — silence is not neutral; it means something specific in the scene
- **Who is certain, who is conflicted** — asymmetric emotional states are magnetic; symmetry is flat
- **Who is watching, who is being watched** — the one who looks has the power until the one being looked at notices

**Prose formula:**
- ❌ `He stood behind her.`
- ✅ `He stood behind her. She felt him there before she heard him — the shift in the air, the particular quality of attention that made the back of her neck go warm. He didn't speak. He didn't have to.`

Show the dynamic through the body's involuntary response, not through description of the other person.

---

### Environmental Drama — Setting Amplifies Emotion

The setting is not backdrop. It is a second character that pushes the primary emotion forward. Before writing any scene, ask: *does this location make the stakes harder or easier?*

| Emotional beat | Environment choice | What it adds |
|---------------|-------------------|--------------|
| Forbidden / dangerous | Enclosed space (elevator, car, his office after hours) | No exit; the proximity is inescapable |
| Wealth / power gap | His space, her rules broken | She is on his territory; the power imbalance is architectural |
| Aftermath / intimacy | Her familiar space, suddenly strange | The ordinary world is now contaminated with him |
| Forced vulnerability | Public place, private crisis | She cannot hide and cannot leave |
| Supernatural stakes | A boundary space (threshold, forest edge, between worlds) | The rules of the normal world do not apply here |

If the setting could be swapped with any other location without changing the scene — change the setting.

---

### Contrast — The Scene's Composition

High-contrast moments are read more slowly and remembered longer. Build at least two of these into any pivotal scene:

- **His control / her chaos** (or reversed) — one character's composure against the other's fracture
- **Public face / private reality** — what they show the room vs. what the reader knows
- **What is said / what is meant** — dialogue that runs parallel to the subtext, not identical to it
- **The ordinary detail / the extraordinary stakes** — mundane action (pouring a drink, adjusting a cuff) against the weight of what is actually happening
- **Speed: slow body / fast mind** — physical movement slows to micro-beats while internal monologue accelerates

---

## What to Read Before Each Chapter

```
Required:
  tracking/context.md                   — previous chapter ending + open threads
  outline/outline.md                    — this chapter's role in the arc (find by chapter number)

Load only if needed:
  world/characters/{character-name}.md  — only characters appearing in this chapter
  tracking/threads.md                   — only if this chapter resolves or plants a foreshadow
  reference/{book-title}/techniques.md  — only if a reference technique is needed
```

## Parallel Writing (default for new books)

Use this flow whenever writing ≥ 2 chapters from scratch. Single-chapter incremental additions use the sequential process below.

### Step 1 — Expand outline beats

Before spawning any agents, expand `outline/outline.md` so every chapter has a concrete beat entry:

```
Ch-NNN: [primary emotion] | hook: {1-sentence} | turn: {what changes} | hook-out: {open question}
```

All chapters must have this before any parallel writing starts. The beat entries replace `tracking/context.md` as the coordination signal during parallel writing.

### Step 2 — Spawn one Agent per chapter

Spawn all chapter agents concurrently. To avoid redundant file reads, read shared context once in the main context and pass it into each agent's prompt:

- **Read once, share with every agent:**
  - `world/worldbuilding.md`
  - Full expanded `outline/outline.md` (with beat entries for all chapters)
- **Read once, shard per agent:**
  - `world/characters/{character-name}.md` — only for characters appearing in that chapter
- **Coordination signal:** each agent receives the previous chapter's hook-out line from the outline beat.

Each agent writes to `content/{book-title}/chapters/ch-NNN-{title}.md` and returns its own hook-out line.

Use a **single batch Agent call** when the environment supports it (e.g. one Agent invocation carrying the whole chapter list), otherwise spawn individual Agents per chapter. Either way, all chapters must be produced in parallel, not sequentially.

### Step 3 — Lightweight continuity pass

After all chapter agents complete, do a single sequential pass:
1. Read chapters in order; verify hook-out of chapter N matches the opening of chapter N+1.
2. Fix only continuity breaks — do not rewrite prose for style.
3. Write `tracking/context.md` from the final chapter's ending.
4. Update `tracking/threads.md`, `tracking/timeline.md`, `tracking/character-status.md`.

Keep this pass minimal. Do not run a full quality rewrite here; that is Phase 4.

### Multiple books in parallel

Spawn one top-level Agent per book. Pass only that book's `world/`, `outline/`, and character files so each agent starts with a minimal context. Books share no state and can complete in any order.

## Single Chapter Writing Process

Use this for adding one chapter to an existing book (incremental update only).

1. Read `tracking/context.md` — know the exact last beat.
2. Read the chapter's outline entry in `outline/outline.md`.
3. Name the chapter's **primary emotion** (tension / release / shock / ache / warmth).
4. Name the chapter's **turn**: what changes from start to end?
5. Write the **hook** (≤3 sentences): drop into motion, not setup.
6. Write the **escalation**: raise stakes through action/dialogue. No passive reflection blocks.
7. Write the **turn**: the moment that changes something — reveal, decision, or loss.
8. Write the **hook-out**: end mid-motion or on an open question. Never summarize.
9. Save to `content/{book-title}/chapters/ch-NNN-{title}.md` from the project root, with correct zero-padded number.
10. Update `tracking/context.md`: last beat + open threads + any foreshadow planted.
11. Update `tracking/threads.md` if foreshadow added or resolved.
12. Update `tracking/character-status.md` for any character changes.

## Chapter File Format

```md
---
title: "Chapter One: Night Crossing"
chapter: 1
---

Prose starts here — no leading blank line.
```

Frontmatter is optional but recommended. The site loader falls back to filename if `title` is absent.

Prose formatting rules:
- Adjacent paragraphs: blank line between them (`\n\n`). Within a paragraph, do not hard-wrap lines. (CommonMark renders a single `\n` as a space, collapsing all paragraphs into one block.)
- Dialogue quotes: half-width double quotes `""`
- No `……` or `——` in the prose product — rewrite as action, short sentence, or line break
- No chapter summaries or author notes inline

## Chapter Count Planning

When writing a new book, decide the total chapter count before expanding the outline. Pick a number in the 10–20 range that fits the story's scope. **Never pick the same number as another book in the same site.** Treat the count as a story decision, not a quota:

- A tight revenge arc might need 11 chapters.
- A slow-burn romance with multiple subplots might need 17.
- A high-stakes thriller with many POVs might run to 20.

Document the chosen count in `outline/outline.md` header before writing any beat entries.

## Pacing Guidelines

Word counts are targets, not uniform quotas. Let each chapter breathe according to its dramatic weight — a chapter that needs 4,200 words should not be trimmed to hit a round number, and a lean 1,800-word chapter is fine if it lands the turn cleanly. Vary lengths across the book so readers feel the rhythm shift.

| Chapter type | Word count range | Dialogue ratio | Action beats |
| --- | --- | --- | --- |
| Opening chapter | 1,800–2,500 | 20–30% | 3+ |
| Escalation chapter | 1,500–2,200 | 30–50% | 2–4 |
| Climax chapter | 1,400–2,000 | 15–25% | 4–6 |
| Resolution chapter | 1,200–1,800 | 20–40% | 1–2 |

## Context Handoff (`tracking/context.md` template)

```md
## Last Chapter Ending
{Final action or dialogue — 1–3 sentences}

## Next Chapter Start
{Which action or scene to continue from}

## Open Threads
- {foreshadow/suspense 1}
- {foreshadow/suspense 2}

## Target Emotion for Next Chapter
{tension / release / shock / lingering regret / warmth}
```

Always overwrite `context.md` after each chapter. Do not append history — the file is a rolling handoff.

## Romance Heat Level

Apply this section whenever the genre is romance or contains a romantic sub-plot (Dark Romance, Billionaire, Paranormal, Shifter, Vampire, Fantasy Romance, Mafia, Sports, Contemporary, or any genre with a central pairing).

### Target Heat Level

**Default: steamy / closed-door at peak, non-graphic.** Matches `fiction-niche-researcher.md` AdSense safety policy.

| Level | Definition | Policy |
|-------|-----------|--------|
| Sweet / closed-door | Tension only; intimacy implied off-page | Always safe |
| **Steamy / closed-door at peak** | **Build tension with sensation, breath, skin, pressure through proximity, touch, and kisses; fade-to-black or closed-door at the peak moment of intimacy — stop before explicit sexual acts** | **Default — use this** |
| Explicit | Describes sex acts in anatomical detail | AdSense violation — never use |

"Closed-door at peak" means: the reader feels the heat building — pulse, breath, contact, charged dialogue — but the camera cuts away at the peak intimate moment. They know what happened; they were not in the room for it. First kisses and make-out buildup are written through; escalated intimacy fades at the threshold.

---

### The 5 Tension Techniques

**1. Slow the clock**
Intimate moments run at 10× the normal time. Break actions into micro-beats. Sentence fragments are correct here — they signal the body overriding the mind.

> *He reached out. Stopped. His fingertips hovered one centimeter from her jaw.*
> *She didn't breathe.*
> *He touched her anyway.*

**2. Body-first, thought-second**
Physical sensation comes before emotional interpretation. Never name the emotion first; let the body report it.

> Wrong: *She felt desire rising in her chest.*
> Right: *Her pulse beat in her throat. She pressed her palm flat to the wall to keep from stepping closer.*

**3. The charged gap**
What isn't said or done carries as much weight as what is. Silence, held breath, and a character's decision NOT to move are tension. Use them.

> *He could have kissed her. They both knew it. He didn't.*

**4. Escalating contact**
Each physical touch must be a step up from the last. Track the progression across the scene and across the chapter arc: eye contact → accidental touch → intentional touch → held contact → skin → breath → lips. Don't skip rungs. Don't repeat rungs.

**5. Internal resistance**
The character wants what they will not admit — to themselves or to the reader. Both the want and the resistance must be legible on the page simultaneously.

> *She told herself it was the wine. It was not the wine. She knew it was not the wine.*

---

### Scene Types and How to Write Them

#### Pre-contact tension (most common — use in every chapter with the pairing present)

Write the charged air before anything happens. Proximity, awareness of the other person's body, involuntary physical response, and the effort to hide it.

Key beats:
- Character notices the other's specific detail (jaw, hands, the way they move) — not generic attractiveness
- Physical symptom: pulse, heat, the urge to close distance or increase it
- Dialogue that says one thing and means another
- One character nearly acts — then doesn't

#### First significant touch

This is a chapter-level event. Give it space. Slow the clock entirely.

- Name every sensation: temperature, pressure, texture, involuntary response
- Show the moment before (held breath, decision) and the moment after (stillness, recalibration)
- Keep internal monologue to short fragments — the body is louder than the mind here

#### Almost-kiss / interrupted moment

The most commercially effective beat in romance. Withhold the payoff.

Structure:
1. Close the distance in increments (half a step, leaning in, the breath mingling)
2. Write the threshold — the millisecond before contact
3. Interrupt (external: phone, knock, third party; or internal: one character pulls back)
4. Show the aftermath — the air after the interruption is charged differently than before

Never interrupt and immediately resolve. The tension from an interrupted moment must carry forward.

#### First kiss

Write through it fully. A first kiss is not a fade point — stay in the scene through contact, response, and separation.

Beats:
- The initiation (who moves first, how)
- The first contact: pressure, heat, the precise physical detail
- The second beat: one person's response — deeper, still, pulling back slightly then returning
- The internal recognition: the character understands something has changed
- The end of the kiss: how they separate, what the air between them feels like now

Keep it under 400 words. Longer is not more intense — it dilutes.

#### Escalated physical scene (make-out, pre-intimacy)

Build the escalation of contact — clothing, hands, skin — with sensory specificity (temperature, texture, pressure). **Fade-to-black or closed-door at the peak moment.** Do not write through the threshold; cut to aftermath or use a warm fade line. This is the AdSense-safe ceiling.

**Fade technique:**
> *His hand found the edge of her dress. She exhaled — barely sound, barely breath.*
> *— and then there was nothing but heat, and his voice saying her name.*

**Cut-to-aftermath technique:**
> *Later, she would not remember who had moved first. She would remember only the window light falling across his collarbone, and how she had not looked away.*

Both are correct. The fade is warmer; the cut is more literary. Match to the chapter's emotional register.

---

### Vocabulary: Use / Avoid

**Use freely:**
`skin`, `heat`, `pulse`, `breath`, `jaw`, `throat`, `collarbone`, `waist`, `hip`, `back`, `hands`, `fingers`, `lips`, `mouth`, `exhale`, `shiver`, `pressure`, `weight`, `warmth`, `close`, `closer`, `the space between them`, `his hands on her`, `her fingers in his shirt / against his chest`

**Use sparingly (once per scene maximum):**
`desire`, `want`, `need`, `ache` — these name the emotion directly; they're most powerful when used once, at the scene's peak

**Avoid (AI cliché or explicitly sexual):**
`throbbing`, `heaving`, `moist`, `quivering`, `manhood`, `womanhood`, `grinding`, `explicit anatomical terms` — any of these kills the scene's credibility or crosses the AdSense line

**Avoid (too vague / closed-door register):**
`they made love` (without any preceding sensation), `one thing led to another`, `the night passed between them` — these are soft fade-outs that feel evasive rather than deliberate

---

### Heat Pacing Across a Full Novel

Romance readers track the heat arc the same way they track plot. Structure it:

| Chapter range | Expected heat beats |
|--------------|---------------------|
| Ch 1–4 | Awareness only. Character notices the other; no physical contact yet. |
| Ch 5–8 | First accidental touch or forced proximity. One interrupted moment. |
| Ch 9–13 | Escalating contact. First significant touch. Almost-kiss or interrupted kiss. |
| Ch 14–16 | First kiss (if not earlier). Scene with real physical escalation. Emotional crisis interrupts. |
| Final 2–3 chapters | Resolution of both emotional and physical tension. Closed-door fade at peak if the arc supports it. |

In an 18-chapter book, the first kiss should land no later than chapter 14. Readers who reach chapter 16 without it begin to feel cheated.

---

### Applying to Parallel Writing

When spawning agents for parallel chapter writing, pass each agent its position in the heat arc:

```
Heat arc position: Ch-{N} of {total}
Expected heat beat this chapter: {awareness only / first touch / almost-kiss / first kiss / escalated contact / aftermath}
Previous heat beat (from tracking/context.md): {last physical beat that happened}
Next expected beat (from outline): {what the reader is waiting for}
```

Agents without this context will default to closed-door or will skip heat beats entirely. Always provide it.

---

## Quality Check Before Saving

- Hook: does it drop into motion? No weather, backstory, or setup.
- Turn: does something change? A chapter where nothing changes is a filler chapter.
- Hook-out: does it create forward pull? Reader must want the next chapter.
- No consecutive paragraphs with identical rhythm or length.
- No three consecutive sentences starting with the same subject.
- **One-paragraph test:** does the opening paragraph make the reader feel something in the first three sentences? If it only establishes setting or backstory, cut to the tension.
- **Named emotion check:** does every scene with the central pairing have a specific named emotional state (from the Named Emotion table in §"Scene-Level Drama")? Generic emotions ("nervous", "angry", "interested") are a rewrite flag.
- **Power dynamic check:** is it clear who is certain and who is conflicted? If both characters feel equally balanced, the scene has no subtext.
- **Setting check:** does the location amplify the emotional stakes, or could it be any room? If it's interchangeable, change it.
- If AI flavor is detected, flag the chapter for the Phase 4 deslop pass — do not run `/story-deslop` inline here. Phase 4 (`references/story-deslop.md`) is loaded separately and runs after all chapters are written.

## Book Description & Tagline (Required — write before cover generation)

After chapters are complete, write the `tagline` and `description` fields for `src/lib/books.ts`. These appear on the book detail page and are the primary click trigger for every reader who arrives at the site. Apply the same hook standards as the cover: tension + question + desire, all three.

### Tagline (1–3 short sentences)

One sentence is ideal. Two is the maximum. It must reveal the core irony of the situation — what she came for vs. what she got, what was supposed to be simple vs. what it became.

**Banned:** genre labels ("enemies-to-lovers", "fated mates", "dark romance"), passive descriptions ("a story about"), vague emotional promises ("a journey of self-discovery").

**Patterns — pick the one that fits:**

| Pattern | Formula | Example |
|---------|---------|---------|
| **Action → consequence** | [what she did] → [the thing that happened because of it] | "She mapped his world. He had no defense against that." |
| **Intent + ironic reversal** | [what she came to do]. [what he did instead]. | "She came to end him. He made her the only person he trusted." |
| **Three escalating beats** | One [setup]. One [complication]. One [the real problem]. | "One qualifying spot. One fake relationship. One very real problem." |
| **Plan + role + failure** | [His plan]. [Her assigned role]. [Why the role failed]. | "He had a plan. She was supposed to be a variable. She was not a variable." |
| **She/He didn't expect** | [What she went in to do]. [What she didn't expect]. | "She crossed the Veil to complete a survey. She didn't expect to be claimed before she could cross back." |

### Description (4–6 sentences)

Back-cover copy, not a plot summary. Each sentence has a job:

| Sentence | Job | What it must do |
|----------|-----|----------------|
| **1 — Protagonist state** | Who she is + why she's there | Names the character + the specific ordinary-world goal. Not "a woman who" — a person doing a specific thing. |
| **2 — The collision** | What went wrong when he entered | The inciting event in one sentence. What changed. "She didn't expect X." "X happened instead." |
| **3 — The exchange** | What each needs from the other | "He needs [X]. She needs [Y]." The transactional logic of the forced proximity. |
| **4 — The third variable** | What neither planned for | This is the actual story. The thing the arrangement didn't account for. Must be specific, not vague. |
| **5 — Stakes (optional)** | What happens if they fail or succeed | Only include if it sharpens the hook. Cut if it reads like a plot outline. |
| **6 — The feeling (optional)** | The emotional impossibility in one image | One sentence that makes the reader feel the situation rather than understand it. |

### Suspense Layer — The Information Gap (Required)

The description must **withhold** at least one piece of critical information. The reader should finish reading and immediately need to click — not because the story sounds good, but because there is a specific thing they don't know yet and cannot tolerate not knowing.

**The technique:** reveal that something exists, without revealing what it is or why it matters. The gap between "this thing exists" and "what this thing means" is the click trigger.

**Withheld-detail patterns:**

| Type | Formula | Example |
|------|---------|---------|
| **The counter-intuitive fact** | State a fact that demands explanation | "He fired her three times. She came back each time. On the fourth, he stopped trying." |
| **The incomplete revelation** | Something happened — the description doesn't say what | "She found the letter. Everything after that is his fault." |
| **The already-happened twist** | A consequence is named, not the cause | "By the time she understood what she'd agreed to, she was already in his city, in his life." |
| **The double secret** | Both characters are hiding the same category of thing | "She's been lying to him for six weeks. He's known for five." |
| **The unanswered question (explicit)** | End with a direct question the reader must click to answer | "The question she can't answer: which one of them is more dangerous?" |
| **The counter-expectation** | The setup happens, then one sentence undercuts it | "The wedding happens. That's not the problem." |
| **The withheld identity** | One character knows something about the other that the reader knows they know | "The man who bought her contract doesn't know she's the person who destroyed his company five years ago. She's counting on that." |

**Suspense check:** after writing the description, ask — *what specific thing does the reader not know that they now need to know?* If the answer is "nothing, it's all there" — add a withheld detail. If the answer is "the whole plot" (too vague) — make it specific. The withheld detail must be one sentence away from being revealed; the reader should feel they are *this close* to the answer.

**New tagline pattern — The Withheld Fact:**

| Pattern | Formula | Example |
|---------|---------|---------|
| **The withheld fact** | [Something happened]. [What it means is not said]. | "She found what he'd been hiding. She didn't tell him what she planned to do about it." |

---

**Quality check — one-second test:** if someone reads only the tagline and the first sentence of description, do they feel something and want to know more? If the answer is only "this sounds like a romance novel" — rewrite. The goal is "I need to know how this ends."

**Banned patterns:**
- Trope labels in reader-facing copy: `enemies-to-lovers`, `fake dating`, `fated mates`, `alpha male`
- Passive construction: "a story is told of...", "discover the world of..."
- Vague stakes: "everything they know will be tested", "nothing will ever be the same"
- Suspense that is too vague to be specific: "dark secrets", "hidden truth", "nothing is as it seems" — name the specific thing that is hidden, or don't mention it
- Placeholder description: do not ship a `description: ""` or `description: "Coming soon."`

---

## After All Chapters Written → Cover Generation (automatic, no prompt)

After the `tagline` and `description` are written and added to `src/lib/books.ts`, **immediately load `story-cover.md` and generate the cover** — do not ask whether to proceed. This is always the next step after the final chapter is saved.
