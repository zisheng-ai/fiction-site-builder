# Story Cover

Load this reference when the user asks to generate a novel cover (/story-cover, cover generation), or when Phase 3 of the pipeline is entered.

**Execution principle: invoke tools directly. Never surface a "please run X" prompt to the user mid-phase. Call the image generation tool, write the file, log the result — then move on.**

## Phase 3 Entry Check

**MANDATORY — run this bash command before anything else. Do not skip it. Do not assume the result.**

```bash
[ -n "$APIYI_API_KEY" ] && echo "API_PATH=apiyi" || echo "API_PATH=skip"
```

**If the output is `API_PATH=apiyi` → you MUST use the apiyi curl path below.**

If the output is `API_PATH=skip` → print the warning below, then **skip cover generation for this book and continue the pipeline** (no SVG fallback — leave the cover to be filled in later):
```
\033[33m⚠ WARNING: APIYI_API_KEY is not set. Skipping cover generation (no SVG fallback).\033[0m
\033[33m  Covers require apiyi. Get an API key at:\033[0m
\033[33m  https://api.apiyi.com/register/?aff_code=ijv5\033[0m
\033[33m  Then set: export APIYI_API_KEY="your-key"\033[0m
```

The apiyi path produces a file at `{BOOK_DIR}/cover_v1.png`. When the key is missing, no file is produced — do not block the pipeline; the book launches without a cover and the slot is flagged for a later pass.

## Modes

| Mode | When to use | What it generates |
|---|---|---|
| **Batch** | Initial site launch — all books written, Pre-Build Gate pending | Covers for every book in `content/` |
| **Single-book** | Adding one new book to an existing site | Cover for one book only (logo/favicon already exist) |

**Default to Batch mode at initial launch.** The Pre-Launch Gate requires covers for all ≥5 books. Single-book mode is for incremental updates only.

---

## Batch Mode (initial launch)

### B1 — Discover all books

List every directory in `content/` that is NOT `content/short/` — short stories do not get standalone covers.

```bash
CONTENT_DIR="${CONTENT_DIR:-./content}"
BOOKS=()
for d in "$CONTENT_DIR"/*/; do
  [ -d "$d" ] && [ "$(basename "$d")" != "short" ] && BOOKS+=("$(basename "$d")")
done
printf 'Found %d books:\n' "${#BOOKS[@]}"
printf '  %s\n' "${BOOKS[@]}"
```

If fewer than 5 books are found, log a warning and continue with whatever books exist. Cover generation is not blocked by the book count — missing covers can be retried later.

### B2 — Resolve pen name (no prompt)

Read the pen name from project files in this order — do not ask the user:

1. Any `content/{book}/world/worldbuilding.md` → first "Author" line
2. Any `content/{book}/tracking/context.md` → first "Pen name" line
3. `src/lib/books.ts` → first book's `author` field (only exists after Phase 8 site build)

Note: `src/lib/books.ts` is generated during Phase 8 and will not exist when Phase 3 runs. Try it last, not first.

If the pen name cannot be found in any of these files, substitute `"The Author"` as a placeholder and log a warning. Never stop the batch to ask.

### B3 — Generate covers

**MANDATORY — generate all covers in parallel.** Never loop books sequentially. Launch one background process per book (`gen_cover_apiyi ... &`), then `wait` for all to finish. For each book:
1. Read `content/{book-title}/world/worldbuilding.md` to extract genre and tone.
2. Run genre detection (Step 1.5 below) to select cover style.
3. Roll the cover tier (T2 or T3, per the Female figure rule) and build the cover prompt (Step 2 below) substituting the book's title, genre, and characters.
4. Run Step 3 (apiyi cascade: gpt → doubao → nano).
5. Verify the output file exists.
6. Log: `✓ {book-title} — cover saved` or `⚠ {book-title} — cover skipped: {reason}`.

```bash
# parallel batch — one process per book, then wait
for BOOK in "${BOOKS[@]}"; do
  ( BOOK_DIR="public/covers/$BOOK"; build_and_generate_cover "$BOOK" ) > "/tmp/cover_$BOOK.log" 2>&1 &
done
wait
rm -f /tmp/cover_*.log
```

### Batch completion checklist

- [ ] Covers exist for as many books as possible.
- [ ] Any failed/skipped covers are logged with the book title and error reason.

Missing covers are not a hard blocker for site build — the site can use CSS placeholders during development. Re-run Phase 3 later if needed. Site logo and favicon are generated in Phase 6 (Design plan) — do not block on them here.

---

## Single-book mode

Use for adding one book to an already-launched site. Skip logo and favicon steps — they already exist.

## Generation Method

**apiyi path (preferred):** `curl` to `https://api.apiyi.com/v1/images/generations` with model `gpt-image-2-all`. Response `b64_json` already includes `data:image/png;base64,` prefix — strip it before decoding. See Step 3 and `references/apiyi.md` for full API reference.

**No SVG fallback.** When `APIYI_API_KEY` is not set, skip cover generation for the book (print the warning, continue the pipeline) — never write a styled SVG cover.

## Environment Variables

| Variable | Required | Notes |
|---|---|---|
| `APIYI_API_KEY` | No | API key for `api.apiyi.com`. If unset, cover generation is **skipped** (no SVG fallback) — the pipeline continues and the cover slot is filled later. Get one at https://api.apiyi.com/register/?aff_code=ijv5 |
| `BOOK_DIR` | Yes | Output directory, e.g. `./public/covers/{book-title}` |

## Step 1 — Resolve required info (no prompt)

Must have before proceeding: **book title**, **author pen name**, **BOOK_DIR**.

Derive all three from project files:
- **Book title**: directory name under `content/`
- **Pen name**: see B2 resolution order above (worldbuilding → context → books.ts → placeholder)
- **BOOK_DIR**: `public/covers/{book-title}/`

Do not ask the user. Do not fabricate values that cannot be derived.

Cover ratio: **2:3 portrait**. Generate at `848x1280` (1K Fast tier — sufficient for all UI display sizes, fastest generation). No resize step needed.

## Step 1.5 — Determine visual register and genre

**First: check the site-level visual register** (set during Phase 6 design plan, or derive from the site's dominant content type):
- If the site is drama/romance-dominant → **Cinematic Drama** register for all covers
- If the site is fantasy/sci-fi-dominant → **Dark Fantasy Illustration** register for all covers
- Record the register and apply it consistently across all books on this site

**Then: detect per-book genre** by scanning the book title (and synopsis if available) against the keyword table in `references/cover-styles.md`.
- One match → use it
- Multiple matches → priority order: Cultivation Fantasy > Dark Fantasy > Historical > Thriller > Contemporary Romance > Urban Drama > Sci-Fi > Horror > Isekai
- No match → default to the site's primary genre

The genre determines composition template, color palette, character design, and typography style. The visual register determines render quality language (photorealistic film-still vs. hyperrealistic 3D render).

**For romance/drama genres: allure elements are MANDATORY, not optional.** Load `references/cover-allure-elements.md` and apply the highest-intensity pose from the appropriate genre section. The target is maximum implication within gpt-image-2-all policy — bodies pressed together, visible skin, explicit physical contact (grip, hold, almost-kiss). A cover where two people are simply standing near each other fails this gate.

- **Romance / Drama genres:** use `references/cover-allure-elements.md` (Costume Elements, Poses, and English Romance Playbook). Pick the genre-specific prompt formula, select the highest-intensity pose that fits the book's synopsis, and follow the Escalation Strategy if the output looks tame.

## Step 2 — Build the prompt

All prompt text in English. Structure: text layer + style layer + visual layer.

```
[Genre style from cover-styles.md].
Title text '{book-title}' at top center in [title font style for genre].
Author name '{pen-name}' at bottom center in [author name style for genre].
[genre style tags]. [character description]. [background description].
[color palette]. [lighting].
Professional book cover, high detail digital painting, portrait [ratio] ratio,
keep title and author name inside the central safe area (inner ~85%), no watermark
```

**Character count rule — must follow before writing `[character description]`:**

| Genre | Characters in prompt |
|---|---|
| Urban Drama / Contemporary Romance / Historical Court Drama | TWO OR MORE characters — describe EACH explicitly: position, expression, clothing. At minimum male AND female. Single-character prompts produce single-character covers for these genres. |
| Dark Fantasy | TWO OR MORE characters — male in dark armored robes, female in dark dress with crown; side-by-side or pressed together. A third figure (rival, dark king, betrayer) is welcome where it sharpens the conflict. |
| Thriller / Horror | TWO OR MORE figures — protector + protected, or supernatural presence + ordinary person. May be partial silhouette. |
| Cultivation Fantasy / Sci-Fi / Historical War Epic | Single protagonist (Lone Hero template), but a confronting rival/antagonist may be added for stakes. |
| Isekai / Slice of Life | Single protagonist, duo, or small group — match the book's genre composition. |

**Multi-character rule:** two is the floor for romance/drama, not the ceiling. When the synopsis supports it — a love triangle, rival suitors, a betrayer, a pack/court arrayed behind the leads — render three or more figures. A third figure that introduces tension (a jealous third party, a looming antagonist, a rival pressing in) reads as more dramatic conflict than a clean two-person embrace and is encouraged. Keep one clear focal pairing so the composition still has a center; arrange extra figures to amplify the central power dynamic, not to crowd it out.

**Female figure rule — MANDATORY:** the female character must be visually magnetic — impossible to scroll past. **Exposure = randomly T2 (Bold) or T3 (Maximum), picked independently per cover** — for each cover, roll T2 or T3 and bake that tier's assembly block from the Exposure Tiers table (`references/cover-allure-elements.md`) directly into the prompt; do not rely on the model rolling a lucky exposed result. Across a batch of books, this produces a mix of T2 and T3 covers (do not make every cover the same tier). Required elements, every time:
- Figure: `voluptuous hourglass figure, slim toned waist dramatically cinched, large full bust dramatically prominent, E-cup figure, long shapely legs` — curves are dramatic but the figure is NOT heavy or overweight; the waist must read as narrow against the hips and bust; bust baseline is E cup or larger — "full generous" alone undershoots, use explicit size language. (At T3, drop explicit `E-cup` per the doubao T3-safe rule — use visual-effect phrasing only; see `cover-allure-elements.md`.)
- Clothing: maximally revealing for the assigned tier — T2 = two simultaneous revealing elements (deep neckline + bare back/midriff/high slit); T3 = garment failing in multiple places (torn, slipped, soaked, sheer). See `references/cover-allure-elements.md` Skin & Clothing Vocabulary
- Skin: as much bare skin as the assigned tier allows within the §0 floor — T2 = cleavage + one secondary zone; T3 = three or more zones (bare back, legs, midriff, shoulders, extreme neckline)
- Pose: use top-three **frontal** poses from `references/cover-allure-elements.md` Poses table; bodies must be in physical contact; from-behind poses (marked ▲) are accents, not defaults — at most 1 in 3 covers
- Framing: state the camera frame explicitly in every prompt — "full-body shot, both figures from feet to crown" or "medium shot from hip to crown". Never allow the model to default to a face-only crop.

A modest, fully-clothed, non-contact, or head-shot-only composition is a quality gate failure. Exposure is stochastic — a tame roll is RNG, not the spec; the fix is baking in higher-tier fragments, never accepting the weak roll. Hard floor: no nipples, no genitals, no sex acts (§0 in `cover-allure-elements.md`). Everything above that floor: push it.

**Drama rule — MANDATORY (see Drama Hook section in `cover-allure-elements.md`):** allure without drama is a fashion photo, not a book cover. Every prompt must include:
- A specific emotional expression from the Expression Rules table (never neutral/pleasant)
- A visible power dynamic between the central characters (and any added third figure)
- At least one environmental element that amplifies the emotional stakes
- The "one-second test": a viewer must feel something — not just notice someone attractive

Title font styles and author name styles are in `references/cover-styles.md` per genre.
Default composition: **full-body or medium shot** — both figures visible from hip to crown minimum. Close-up portrait (face and chest only) is a secondary variant, not the default. Pure scene (no figures) only for thriller/horror genres.

## Step 3 — Generate cover

Set `BOOK_DIR="public/covers/{book-title}"` and `OUTPUT_PATH="$BOOK_DIR/cover_v1.png"` before running.

### Model capability ranking (cascade order)

Three apiyi models are viable for covers, ranked by tested capability for this use case (portrait 2:3, clean title text, maximum allure + drama, no watermark). The generator tries them **in this order** and falls through to the next on any failure:

| Rank | Model | Size | Response | Notes |
|---|---|---|---|---|
| 1 (primary) | `gpt-image-2-all` | `848x1280` | `b64_json` (PNG) | True 2:3, cleanest title text, best brief adherence, no watermark. Most reliable — but the strictest content filter. |
| 2 (fallback) | `doubao-seedream-5-0-260128` | `1664x2496` | `url` (JPEG) | Highest visual quality + strongest allure, true 2:3, far more permissive filter. **Stamps an `AI生成` watermark in the bottom-right corner — must crop it (see post-process).** Needs ≥3.7M px, hence the large size. |
**nano-banana-pro is not used in production.** It silently downgrades any T3+ prompt to ~T1 output and emits square 1024×1024 (wrong aspect ratio). Nano is reserved for model testing only — never include it in a production cascade.

### apiyi path

```bash
mkdir -p "$BOOK_DIR"
PROMPT_JSON=$(printf '%s' "$PROMPT" | python3 -c 'import json,sys; print(json.dumps(sys.stdin.read().strip()))')

# Generic generator: handles both b64_json (PNG) and url (JPEG) responses.
# Returns 0 on success (file written), non-zero on any failure.
gen_cover_apiyi() {
  local model="$1" size="$2"
  curl -s --max-time 300 https://api.apiyi.com/v1/images/generations \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $APIYI_API_KEY" \
    -d "{\"model\":\"$model\",\"prompt\":$PROMPT_JSON,\"size\":\"$size\"}" \
  | OUTPUT_PATH="$OUTPUT_PATH" python3 -c "
import sys, json, base64, os, urllib.request
output_path = os.environ['OUTPUT_PATH']
raw = sys.stdin.read()
if not raw.strip():
    print('ERROR: empty response (timeout)'); sys.exit(1)
data = json.loads(raw)
if 'error' in data:
    msg = data['error']['message'] if isinstance(data['error'], dict) else str(data['error'])
    print('API_ERROR:' + msg); sys.exit(2)
if not data.get('data'):
    print('SOFT_REJECT: empty data array (model declined silently)'); sys.exit(2)
item = data['data'][0]
if item.get('b64_json'):
    b64 = item['b64_json']
    if ',' in b64: b64 = b64.split(',', 1)[1]
    with open(output_path, 'wb') as f: f.write(base64.b64decode(b64))
elif item.get('url'):
    urllib.request.urlretrieve(item['url'], output_path)
else:
    print('UNKNOWN_FORMAT:' + str(list(item.keys()))); sys.exit(3)
print('SAVED:' + str(os.path.getsize(output_path)))
"
}

# Capability cascade — try best model first, fall through on failure
# nano-banana-pro is NOT in the production cascade (model-test only)
if   gen_cover_apiyi "gpt-image-2-all"            "848x1280";  then MODEL_USED="gpt-image-2-all"
elif gen_cover_apiyi "doubao-seedream-5-0-260128" "1664x2496"; then MODEL_USED="doubao-seedream-5-0-260128"
elif gen_cover_apiyi "doubao-seedream-5-0-260128" "1664x2496"; then MODEL_USED="doubao-seedream-5-0-260128"  # retry once
else MODEL_USED=""; echo "ALL_MODELS_FAILED — skipping book"
fi
echo "MODEL_USED=$MODEL_USED"

# Save prompt alongside cover
printf '%s' "$PROMPT" > "$BOOK_DIR/cover_v1.prompt.txt"
```

**Post-process by model used:**
- `doubao-seedream-5-0-260128` → crop the bottom-right `AI生成` watermark. Trim a corner strip (the tag sits in the bottom ~6% / right ~22%); easiest is `sips`/ImageMagick to crop ~7% off the bottom, then the author-name band still clears it. Verify the watermark is gone before shipping.
- `gpt-image-2-all` → no post-process needed.

**If the whole cascade fails on content safety** (`API_ERROR` containing `invalid_prompt` / `safety` / `rejected` from the primary, and the fallbacks also reject): replace triggering terms in `$PROMPT` and re-run the cascade once:

| Replace | With |
|---|---|
| `bare back exposed` | `off-shoulder gown, collarbone catching the light` |
| `exposed breast`, `topless`, `naked`, `nude` | `off-shoulder`, `elegant neckline`, `décolletage` |
| `bodies pressed flush together` | `close proximity, charged tension` |
| `gripping her hip`, `hand on her bare hip` | `hand at her waist` |
| `wet transparent fabric`, `see-through wet` | `rain-soaked fabric, damp clothing` |
| `clinging to and outlining every curve` | `rain-soaked clothing pressed against her silhouette` |
| `lips pressed against` | `faces close, the moment before` |
| `erotic`, `sexual`, `explicit` | `alluring`, `intimate atmosphere`, `romantic tension` |

Re-run the full cascade once with the softened prompt. If every model (gpt → doubao → doubao retry) still fails, **skip the book and continue the batch** — no SVG fallback, no nano fallback.

On any other API error: log the response, skip this book, continue batch.

### Terminal fallback — skip (no nano, no SVG)

The production cascade ends at doubao (retry once). There is **no nano fallback and no SVG fallback**:
- If `APIYI_API_KEY` is not set → skip the cover (warning + continue).
- If gpt + doubao (×2) all fail → skip the book, log the reason, continue the batch.
- Never fall through to `nano-banana-pro` in production — nano is model-test only.
- Never write a styled `.svg` cover.

### B3 batch flow

**Generate all books in parallel** — one background process per book, then `wait`. Build the prompt inline per book — do not pre-build a map:

```bash
for bookSlug in "${BOOKS[@]}"; do
  (
    BOOK_DIR="public/covers/${bookSlug}"
    # Steps 1.5 + 2: detect genre, roll T2/T3 tier, build PROMPT string for this book
    PROMPT="$(build_cover_prompt "$bookSlug")"  # inline per Step 2 template
    # Step 3: apiyi cascade (gpt → doubao → nano); skip on no key / total failure
  ) > "/tmp/cover_${bookSlug}.log" 2>&1 &
done
wait
rm -f /tmp/cover_*.log
```

`build_cover_prompt` is not a real function — it represents executing Steps 1.5 and 2 inline for each book before the curl call.

## Step 3.5 — Compress the cover

Run immediately after Step 3, before quality check. Do not skip.

```bash
COVER_FILE="$BOOK_DIR/cover_v1.png"
if [ -f "$COVER_FILE" ]; then
  if ! command -v pngquant &>/dev/null; then
    if ! brew install pngquant -q; then
      echo "⚠ pngquant install failed — skipping compression for $COVER_FILE"
    fi
  fi
  if command -v pngquant &>/dev/null; then
    BEFORE=$(stat -f%z "$COVER_FILE" 2>/dev/null || stat -c%s "$COVER_FILE")
    pngquant --quality=80-90 --ext .png --force "$COVER_FILE"
    AFTER=$(stat -f%z "$COVER_FILE" 2>/dev/null || stat -c%s "$COVER_FILE")
    echo "✓ pngquant: ${BEFORE}B → ${AFTER}B (-$(( (BEFORE-AFTER)*100/BEFORE ))%)"
  fi
fi
```

For **batch mode**, run this loop after all covers are generated:

```bash
for bookSlug in "${BOOKS[@]}"; do
  COVER_FILE="public/covers/${bookSlug}/cover_v1.png"
  # same snippet as above with COVER_FILE set per book
done
```

---

## Step 4 — Quality check

| Check | Standard |
|---|---|
| Title legible | Clear, font matches genre |
| Genre match | Visual style matches book |
| Composition | Subject prominent, text not blocking key art |
| Ratio correct | 2:3 portrait |

**Automated pass criteria (unattended):** If `{BOOK_DIR}/cover_v1.png` exists and has portrait dimensions (height > width), mark as passed automatically. Do not regenerate unless the file is missing or obviously corrupt (0 bytes). If regeneration is needed, retry once with the same prompt; on second failure, skip and log the book as needing manual cover review.

## Output Location

```
public/covers/{book-title}/cover_v1.png        ← main cover, served as /covers/{book-title}/cover_v1.png
public/covers/{book-title}/cover_v1.prompt.txt ← prompt used
```

Served from `public/` — no CDN needed. The site builder reads `Book.cover` as `/covers/{book-title}/cover_v1.png`.

Site logo and favicon are **not** part of this phase. They are generated in Phase 6 (Design plan) via `references/design-system.md`.
