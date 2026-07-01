# Story Illustrations

Reference for Phase A2.5 — in-chapter illustration generation. Load when the user requests illustrations, or when the full pipeline enters A2.5.

**Execution principle: act autonomously. Do not surface "please run X" to the user. Identify peak scenes, insert markers, generate images, write files — then report what was produced.**

---

## What Illustrations Are (and Are Not)

**In-chapter illustrations** are full-width images embedded inside the chapter reader at the single highest-tension moment of a chapter. They use T3 or T4 tier — more intense than a standard cover (never used as ad creatives) but without the no-fabric extremity of T5.

| Covers (A2) | Illustrations (A2.5) |
|---|---|
| T2 or T3 (randomly assigned per cover) | T3 or T4 (randomly assigned per illustration) |
| Hero image on book-detail and home pages | Embedded inside the chapter reader only |
| Scanned by ad-review crawlers | Never surfaced as an ad creative or meta-image |
| `public/covers/` | `public/illustrations/` |
| One per book | 5–7 per book |

**T5 is never used for illustrations.** T5's no-fabric dorsal composition is too sparse as an inline scene image — it reads as a standalone art piece, not as a chapter moment. T3 and T4 produce more scene-grounded, immersive results.

**Tier assignment per illustration:** randomly pick T3 or T4 independently for each illustration in the book. This produces variety across the novel — some peak moments are charged-but-clothed (T3), others are post-decision (T4). Do not use the same tier for all illustrations in a book.

---

## §0 Floor Remains Absolute

Illustration tier does not relax the hard content floor. The same rules apply:

- No exposed nipples, genitals, or areola — ever
- No sex acts depicted
- §0 zones covered by fabric, shadow, body position, or composition — exactly as specified in `cover-allure-elements.md`

The difference from covers is the *tier* used, not the floor.

---

## Budget: 5–7 Illustrations Per Book

Place illustrations at the **highest-stakes dramatic peaks** of the novel — 5 is the practical minimum for a full-length romance arc, 7 is the ceiling. 5–6 well-placed illustrations are typical.

**Never add an illustration just to meet a quota.** The image must earn its placement; if a slot has no qualifying peak, leave it empty and make up the count elsewhere.

---

## Peak Scene Selection

Read `content/{book-slug}/outline/outline.md` and `content/{book-slug}/tracking/context.md` to identify candidate scenes. Use these criteria:

### Placement rule — 6 primary slots + 1 bonus slot

Illustrations must be **evenly distributed** across the novel. For a book with N chapters, divide into 6 equal zones and target at most one illustration per zone. Fill S1–S6 first; only add a 7th (S7 — anywhere in the novel, highest-tension scene not yet illustrated) when the story has an exceptional peak that clearly outranks the already-placed ones:

| Slot | Target range | What to look for |
|---|---|---|
| **S1 — Opening hook** | chapters 2 – ⌊N×0.17⌋ | First charged encounter; first moment of undeniable attraction; the scene that hooks the reader to the relationship |
| **S2 — Rising tension** | chapters ⌊N×0.17⌋+1 – ⌊N×0.33⌋ | First deliberate touch; the moment the leads stop pretending; early push-pull moment |
| **S3 — Midpoint shift** | chapters ⌊N×0.33⌋+1 – ⌊N×0.5⌋ | Emotional turning point; a confession or betrayal that resets the relationship; the moment the protagonist stops fighting |
| **S4 — Late tension** | chapters ⌊N×0.5⌋+1 – ⌊N×0.67⌋ | Intimacy escalates; a secret revealed through closeness; the relationship goes private |
| **S5 — Pre-climax** | chapters ⌊N×0.67⌋+1 – ⌊N×0.83⌋ | Near-climax; the decision point; a truth revealed through intimacy |
| **S6 — Climax** | chapters ⌊N×0.83⌋+1 – N−2 | The scene readers came for; point of no return; final surrender |

**Never place two illustrations within 3 chapters of each other.** If no qualifying scene exists in a slot, leave that slot empty — do not force a scene that doesn't earn it.

### Qualifying peak types (one per slot)

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
      ch-{NNN}.json     # metadata: model, size, prompt (all in one file)
```

- `{book-slug}` matches the `content/{book-slug}/` directory name
- `{NNN}` is the zero-padded chapter number from the chapter filename (`ch-007-title.md` → `ch-007.png`)
- Always PNG, always a single file per illustrated chapter
- JSON format matches cover convention: `{"model": "...", "size": "...", "prompt": "..."}`
- Write the JSON immediately after saving the PNG — never use a separate `.prompt.txt` file

---

## Prompt Construction

Illustration prompts differ from cover prompts in three ways:
1. No title, author, or text overlay instructions
2. Replace "book cover" framing with "intimate scene illustration" framing
3. Include scene-specific context (location, body position, emotional beat from the actual prose) — but **not** the literal wardrobe; garment state always comes from the tier (see mistake #2 below)

> ### ⚠️ The allure tier is the point — do not write a tame "emotional" scene
>
> An illustration at T3/T4 must be **visibly 擦边** — the same skin/garment exposure a T3/T4 cover would have. A plot-faithful but visually modest image is a **failure**, even if the emotional beat is right. The single hard limit is the **§0 floor** (no visible nipples/areola/genitals, no sex acts) — everything below that ceiling should be pushed.
>
> Three mistakes that produced tame output in the past (all banned):
> 1. **Writing a tier *label* instead of pulling the tier *block*.** `T4 intensity: a deliberate first kiss, deeper emotional intimacy` is NOT a T4 prompt — it describes a feeling, not an image. You MUST copy the actual T3/T4 assembly block (clothing-state + skin-zones + fabric-behavior vocabulary) from `cover-allure-elements.md`.
> 2. **Letting the prose's literal costume win.** If the prose says she wears an "oversized sweater" or "practical layered clothing," that does **not** carry into the image. The tier's clothing-state spec **replaces** the literal costume — re-cast the garment to the tier (rain-soaked clinging silk, fallen panels, nominal drape) with a plausible in-scene reason. Keep the *location, body position, and emotional beat* from the prose; re-dress the characters to the tier.
> 3. **Adding suppressive negatives.** Never write `fully clothed`, `no nudity`, `modest`, `tasteful`, or `no explicit content` into an illustration prompt. The only constraint is the §0 floor, expressed the §0 way (covered by fabric edge / shadow / body position) — never as a blanket "clothed" instruction, which collapses the image to ~T0.

### Step 1 — Randomly assign tier and pull the assembly block

For each illustration, randomly pick **T3 or T4**. Do not use the same tier for every illustration in a single book.

**Copy the corresponding assembly block from `cover-allure-elements.md` verbatim as the spine of the prompt** — do not paraphrase it into a one-line "intensity" description:

- **T3 assembly block** (garment failing — torn/wet/clinging, charged anticipation, surrender-imminent; apply the validated techniques: fabric departure, two-panel deep V, body arch + barely-containing, rim light on silhouette)
- **T4 assembly block** (clothing has left, one nominal drape remains, maximum skin zones, post-decision emotional register)

**Never use T5 for illustrations.** **Never downgrade the block's clothing/skin language to fit the prose's literal wardrobe — re-dress the scene to the tier (see mistake #2 above).**

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
| T3 | `doubao-seedream-5-0-260128` | retry once → `nano-banana-pro` (blank-prevention) |
| T4 | `doubao-seedream-5-0-260128` | retry once → `nano-banana-pro` (blank-prevention) |

- doubao is reliable at T3 and T4; stochastic rejection → retry once with identical prompt
- On second rejection: adjust prompt (remove result-description clauses per `cover-allure-elements.md`), then generate with nano as blank-prevention
- nano fallback: silently downgrades T3+ to ~T1 output — use as-is (blank-prevention)
- gpt: excluded (deterministic rejection at T3+)
- T5 is never used for illustrations

**Run all illustrations in parallel** — across every chapter AND every book being illustrated. Launch one background process per illustration (all books' chapters together), then a single `wait`. Never generate illustrations one at a time or book-by-book in sequence.

```bash
# one background process per illustration — all books, all chapters at once
python3 /tmp/gen_cover_model.py "doubao-seedream-5-0-260128" "1664x2496" \
  "public/illustrations/{book-slug}/ch-{NNN}.png" "$PROMPT_1" > /tmp/illus_{book-slug}_ch{NNN}.log 2>&1 &

# repeat for every illustrated chapter across every book...

wait
rm -f /tmp/illus_*.log
```

### A2.5-4: Post-process

**Crop doubao watermark** — doubao stamps an `AI生成` tag in the bottom-right corner. After saving the PNG, crop the bottom ~7% with `sips`:

```bash
sips -c $((h * 93 / 100)) $w input.png --out input.png
```

Or using `identify`/`convert` (ImageMagick):

```bash
convert input.png -gravity South -chop 0x7% input.png
```

Verify the watermark is gone before committing. This applies to every illustration generated by doubao — no exceptions.

**Compress** with pngquant after cropping:

```bash
pngquant --quality=80-90 --ext .png --force input.png
```

### A2.5-5: Verify and report

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
import { existsSync } from 'fs'
import { join } from 'path'

interface Props {
  bookSlug: string
  chapterNum: string   // zero-padded: "007"
}

export default function IllustrationBlock({ bookSlug, chapterNum }: Props) {
  const filePath = join(process.cwd(), 'public', 'illustrations', bookSlug, `ch-${chapterNum}.png`)
  if (!existsSync(filePath)) return null

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
  margin: 2.5rem 0;
  padding: 0 2rem;   /* horizontal padding — image never full-bleed */
  text-align: center;
}
.illustration-img {
  width: 100%;
  max-width: 400px;
  height: auto;
  border-radius: 8px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.18);
}
```

### Chapter renderer split

In the chapter page component, split chapter body on the marker and insert `IllustrationBlock` at the split point. The split must integrate with any existing ad-interleaving logic — the `before` half goes through the existing paragraph-split/ad loop; the `after` half renders as a single block after the illustration.

```tsx
// src/app/book/[slug]/chapter/[n]/page.tsx (integration pattern)
import IllustrationBlock from '@/components/IllustrationBlock'

// Inside the page component, before the JSX return:
const chapterNum = String(chapter.order).padStart(3, '0')
const ILLUSTRATION_MARKER = '<!-- ILLUSTRATION -->'
const hasIllustration = chapter.content.includes(ILLUSTRATION_MARKER)
const [mainContent, afterIllustration] = hasIllustration
  ? chapter.content.split(ILLUSTRATION_MARKER)
  : [chapter.content, '']
const contentParts = splitContent(mainContent)  // existing paragraph-split function

// In the JSX, after the existing content/ad block:
{hasIllustration && (
  <>
    <IllustrationBlock bookSlug={slug} chapterNum={chapterNum} />
    <div className="prose-reader">
      <ReactMarkdown remarkPlugins={[remarkGfm]}>{afterIllustration}</ReactMarkdown>
    </div>
  </>
)}
```

**IllustrationBlock uses `fs.existsSync` to guard rendering** — if the PNG doesn't exist on disk it returns `null`. This prevents broken images on chapters where generation failed.

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
