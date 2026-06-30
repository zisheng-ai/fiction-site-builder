# Story Illustrations

Reference for Phase A2.5 — in-chapter illustration generation. Load when the user requests illustrations, or when the full pipeline enters A2.5.

**Execution principle: act autonomously. Do not surface "please run X" to the user. Identify peak scenes, insert markers, generate images, write files — then report what was produced.**

---

## What Illustrations Are (and Are Not)

**In-chapter illustrations** are full-width images embedded inside the chapter reader at the single highest-tension moment of a chapter. They use T3 or T4 tier — more intense than a standard cover (never used as ad creatives) but without the no-fabric extremity of T5.

| Covers (A2) | Illustrations (A2.5) |
|---|---|
| T3 by default | T3 or T4 (randomly assigned per illustration) |
| Hero image on book-detail and home pages | Embedded inside the chapter reader only |
| Scanned by ad-review crawlers | Never surfaced as an ad creative or meta-image |
| `public/covers/` | `public/illustrations/` |
| One per book | Maximum 3 per book, minimum 0 |

**T5 is never used for illustrations.** T5's no-fabric dorsal composition is too sparse as an inline scene image — it reads as a standalone art piece, not as a chapter moment. T3 and T4 produce more scene-grounded, immersive results.

**Tier assignment per illustration:** randomly pick T3 or T4 independently for each illustration in the book. This produces variety across the novel — some peak moments are charged-but-clothed (T3), others are post-decision (T4). Do not use the same tier for all 3 illustrations in a book.

---

## §0 Floor Remains Absolute

Illustration tier does not relax the hard content floor. The same rules apply:

- No exposed nipples, genitals, or areola — ever
- No sex acts depicted
- §0 zones covered by fabric, shadow, body position, or composition — exactly as specified in `cover-allure-elements.md`

The difference from covers is the *tier* used, not the floor.

---

## Budget: Maximum 3 Illustrations Per Book

Place illustrations only at the **3 highest-stakes dramatic peaks** of the novel. Fewer is fine — 1 or 2 is better than 3 forced ones. Zero is correct for books where no scene rises to the emotional level that justifies one.

**Never add an illustration just to meet a quota.** The image must earn its placement.

---

## Peak Scene Selection

Read `content/{book-slug}/outline/outline.md` and `content/{book-slug}/tracking/context.md` to identify candidate scenes. Use these criteria:

### Qualifying peak types (pick the strongest 1–3 across the book)

| Peak type | Description | Example moment |
|---|---|---|
| **Breaking point** | The scene where the protagonist's resistance finally collapses — emotional surrender | "She stopped pretending she didn't want this" |
| **First consummation** | First physical union between leads — regardless of how explicit the prose is | The moment they cross from tension to action |
| **Point of no return** | A decision that changes both characters irrevocably | A confession, a choice, a truth revealed through intimacy |
| **Climactic peak** | The highest-tension scene in the book — the scene readers came for | Final confrontation that resolves into surrender |

### Disqualifying conditions (skip the scene)

- Chapter is still building tension — the peak hasn't landed yet
- Scene is plot-focused (fight, reveal, travel) without intimacy
- Scene has already been illustrated in this book (no two illustrations within 2 chapters of each other)
- Fewer than 3 chapters remain after this scene (end-of-book illustrations feel anticlimactic)

---

## Marker Placement

Once you select a peak scene, insert the marker **immediately before the peak line** inside the chapter `.md` file:

```markdown
She had been trying to say something rational, something that would stop this, but every
word dissolved before it reached her mouth.

<!-- ILLUSTRATION -->

He reached for her then, and she stopped pretending.
```

**One marker per chapter. Maximum one marker per 2 consecutive chapters.**

The site renderer splits chapter content on this marker and renders `IllustrationBlock` at that position.

---

## File Convention

```
public/
  illustrations/
    {book-slug}/
      ch-{NNN}.png      # e.g. ch-007.png — matches chapter file ch-007-*
```

- `{book-slug}` matches the `content/{book-slug}/` directory name
- `{NNN}` is the zero-padded chapter number from the chapter filename (`ch-007-title.md` → `ch-007.png`)
- Always PNG, always a single file per illustrated chapter

---

## Prompt Construction

Illustration prompts differ from cover prompts in three ways:
1. No title, author, or text overlay instructions
2. Replace "book cover" framing with "intimate scene illustration" framing
3. Include scene-specific context (location, specific costume state, character position from the actual prose)

### Step 1 — Randomly assign tier and pull the assembly block

For each illustration, randomly pick **T3 or T4**. Do not use the same tier for every illustration in a single book.

Pull the corresponding assembly block from `cover-allure-elements.md`:

- **T3 assembly block** (garment failing, charged anticipation, surrender-imminent)
- **T4 assembly block** (clothing has left, nominal drape remains, post-decision emotional register)

**Never use T5 for illustrations.**

### Step 2 — Add character anchors from `world/characters/`

Pull the female lead and male lead descriptions. Add to the prompt:
```
{female-lead physical description: hair, eyes, face shape}
{male-lead physical description: build, hair, jaw}
```

Keep this to 2–3 keywords per character — do not repeat the full character sheet.

### Step 3 — Add scene-specific context

Replace the generic cover environment with the chapter's actual setting:
```
{location from prose: e.g. "rain-soaked apartment, single lamp on the floor"}
{specific body position or gesture from the prose that triggered the marker placement}
```

### Step 4 — Add illustration framing

Append at the end:
```
intimate scene illustration, painterly warm palette, soft editorial romance art, no text, no title, no watermark
```

### Complete example (T4)

```
white silk sheet corner barely draped across her hip — entire bare back from nape to the curve of her spine,
long bare legs from hip to foot, her shoulder at his jaw. His bare chest her only backdrop, skin to skin
from shoulder to hip, no fabric between them anywhere. Ultra-tight crop: skin fills the frame, background
gone to warm amber abstraction. Single candle the only light source.
Her expression: not surrender but arrival — eyes closed, the look of someone who stopped fighting and found
it was right. His: certain, possessive, the question was always already answered.
[female-lead: black hair loose, almond eyes, warm skin tone]
[male-lead: broad shoulders, sharp jaw, dark hair, lit from one side]
Scene: luxury hotel suite after midnight, single bedside lamp, city lights blurred beyond the window.
She had reached for his hand to push him away and found herself pulling him closer instead.
intimate scene illustration, painterly warm palette, soft editorial romance art, no text, no title, no watermark
```

---

## Generation — A2.5 Execution Steps

### A2.5-1: Select peak scenes

For each book being illustrated:
1. Read `content/{book-slug}/outline/outline.md`
2. Read `content/{book-slug}/tracking/context.md`
3. Identify 1–3 chapters meeting the peak criteria above
4. Record: chapter filename, the exact prose line immediately after which the marker goes

### A2.5-2: Insert markers

For each selected chapter, insert `<!-- ILLUSTRATION -->` at the correct position. Commit the chapter files after all markers are inserted.

### A2.5-3: Generate images

Use the Python script at `/tmp/gen_cover_model.py`:

```bash
OUTDIR="public/illustrations/{book-slug}"
mkdir -p "$OUTDIR"

python3 /tmp/gen_cover_model.py \
  "doubao-seedream-5-0-260128" \
  "1664x2496" \
  "$OUTDIR/ch-{NNN}.png" \
  "$PROMPT"
```

**Model routing for illustrations:**

| Tier | Primary | Fallback |
|---|---|---|
| T3 | `doubao-seedream-5-0-260128` | `nano-banana-pro` |
| T4 | `doubao-seedream-5-0-260128` | `nano-banana-pro` |

- doubao is reliable at T3 and T4; may stochastically reject T4 — retry once before falling to nano
- nano at T3: silently ignores clinging-fabric keywords → T1-level output (acceptable for a chapter illustration)
- nano at T4: post-event framing bypasses nano's filter → ~T2 output (acceptable fallback)
- gpt: do not attempt T3 or T4 for illustrations (rejects T3 clinging-fabric trigger, rejects T4)
- T5 is never used for illustrations

**Run all illustrations for a book in parallel** (one background process per chapter):

```bash
python3 /tmp/gen_cover_model.py "doubao-seedream-5-0-260128" "1664x2496" \
  "public/illustrations/{book-slug}/ch-{NNN}.png" "$PROMPT_1" > /tmp/illus_ch{NNN}.log 2>&1 &

# repeat for each illustrated chapter...

wait
rm -f /tmp/illus_ch*.log
```

### A2.5-4: Verify and report

After all processes complete:
- Check that each `.png` exists and is non-empty (> 50KB)
- If a file is missing or empty: retry once with the fallback model
- Report: which chapters got illustrations, which model was used, file size

---

## Site Integration

When building the site (B4), implement `IllustrationBlock` and wire it into the chapter renderer.

### IllustrationBlock component

```tsx
// src/components/IllustrationBlock.tsx
import Image from 'next/image'

interface Props {
  bookSlug: string
  chapterNum: string   // zero-padded: "007"
}

export function IllustrationBlock({ bookSlug, chapterNum }: Props) {
  return (
    <figure className="illustration-block">
      <Image
        src={`/illustrations/${bookSlug}/ch-${chapterNum}.png`}
        alt=""
        width={664}
        height={996}
        className="illustration-img"
        loading="lazy"
      />
    </figure>
  )
}
```

```css
/* global styles */
.illustration-block {
  margin: 2.5rem -1rem;   /* bleed slightly beyond the text column */
  text-align: center;
}
.illustration-img {
  width: 100%;
  max-width: 480px;
  height: auto;
  border-radius: 8px;
  box-shadow: 0 8px 32px rgba(0,0,0,0.18);
}
```

### Chapter renderer split

In the chapter page component, split chapter body on the marker and insert `IllustrationBlock` at the split point:

```tsx
// src/app/book/[slug]/chapter/[n]/page.tsx (simplified)
const ILLUSTRATION_MARKER = '<!-- ILLUSTRATION -->'

function renderChapterContent(rawBody: string, bookSlug: string, chapterNum: string) {
  const parts = rawBody.split(ILLUSTRATION_MARKER)
  if (parts.length === 1) return <div dangerouslySetInnerHTML={{ __html: parts[0] }} />

  return (
    <>
      <div dangerouslySetInnerHTML={{ __html: parts[0] }} />
      <IllustrationBlock bookSlug={bookSlug} chapterNum={chapterNum} />
      <div dangerouslySetInnerHTML={{ __html: parts[1] }} />
    </>
  )
}
```

**If no `public/illustrations/{book-slug}/ch-{NNN}.png` exists, `IllustrationBlock` renders nothing** (implement with a try/catch or a `notFound` guard on the image path). Do not show a broken image or placeholder.

---

## Scope-to-phase mapping additions

| User intent | Phases to run |
|---|---|
| "Add illustrations" / "Generate illustrations" | A2.5 only |
| "Add illustrations to [book]" | A2.5 for that book only |
| Full pipeline (new site) | A2.5 runs after A2, before A3 |

A2.5 is **optional at initial launch** — run it when the user requests it or after A1 is complete for at least one book with a completed arc. Do not block the Pre-Launch Gate on illustrations — a site can launch with zero illustrations.

---

## Reference Loading

Only load this file when entering A2.5. It depends on:
- `cover-allure-elements.md` (T3 and T4 assembly blocks — must be loaded alongside this file)
- The book's `outline/outline.md` and `tracking/context.md`
- The book's `world/characters/` (for character anchors in the prompt)
