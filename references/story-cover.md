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

- **Romance / Drama genres:** use `references/cover-allure-elements.md` (Costume Elements, Poses, and English Romance Playbook). Pick the genre-specific prompt formula, select the pose assigned in Step 1.6, and follow the Escalation Strategy if the output looks tame.

## Step 1.6 — Batch Diversity Plan (batch mode only)

**Before generating any covers, assign each book a unique slot in a diversity grid.** Two covers on the same site must not share the same composition type AND pose. Log the plan before running the batch.

### Composition types — assign one per book, rotate across the batch

| Type | When to use | Character count |
|------|-------------|-----------------|
| **Solo** | Strong single-POV heroine; atmospheric/thriller; no prominent male lead in synopsis | 1 (female lead only) |
| **Duo** | Standard romance/drama — male + female leads in scene | 2 |
| **Trio** | Love triangle, rival over shoulder, court/pack dynamic with 3+ key figures | 3+ |
| **Environmental** | Thriller, mystery, horror — figure(s) small against a dramatic landscape/setting | 1–2, environment dominant |

- Across any batch of ≥3 books: at least **one Solo or Trio** cover must appear.
- Do not assign the same type to more than 2 consecutive books.

### Camera framing — rotate across the batch

| Frame | Prompt fragment | Cap per site |
|-------|----------------|-------------|
| Full body (feet to crown) | `full-body shot, both figures visible head to toe` | No cap |
| Medium (hip to crown) | `medium shot, from hip to crown` | No cap |
| Close-up / intimate crop | `tight crop on faces and upper chest` | ≤2 per site |
| Side-profile body + face forward | `pure side-profile body, face turned toward viewer` | ≤2 per site |

- No more than 2 covers per site may use the same framing.

### Pose — rotate through the full Poses table

- Assign each book a pose from `cover-allure-elements.md` Poses table.
- **No pose may repeat for 2 consecutive books** in the same batch.
- From-behind poses (marked ▲) cap at **2 per site** (not "1 in 3" — the cap is a count, not a ratio).
- Solo covers: pick any solo-friendly pose: Solo power pose, Solo atmospheric, Downcast gaze, Billowing skirt, Rain-soaked.

### Color palette / environment — vary across the batch

No two books on the same site should share the same dominant palette. Assign from:
`warm amber candlelight` · `cold silver moonlight` · `neon rain street` · `golden morning light` · `dark dramatic penthouse` · `moody gothic stone` · `coastal golden-hour` · `stark high-contrast black-and-white accent`

Log the diversity plan like this before generating:
```
Book 1 (alpha-claimed): Solo | full-body | Rain-soaked pose | neon rain street
Book 2 (blood-and-velvet): Duo | medium | Frontal chest press | warm amber candlelight
Book 3 (convenient-husband): Duo | close-up | Chin tilt almost-collision | golden morning light
Book 4 (crimson-court): Trio | full-body | Standing confrontation | cold silver moonlight
...
```

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

**Character count — use the composition type assigned in Step 1.6:**

| Composition type | Characters | Notes |
|---|---|---|
| **Solo** | 1 (female lead) | Powerful solo poses: dramatic expression, environment-forward, no male required. Valid for any genre when the heroine's arc stands alone. |
| **Duo** | 2 (female + male) | Standard romance/drama. Describe both explicitly. |
| **Trio** | 3+ | Love triangle, rival figure, pack/court arrayed behind the leads. Keep a clear focal pairing; extra figures amplify tension. |
| **Environmental** | 1–2, small against scene | Figure(s) partially subsumed by the dramatic environment. Best for thriller/mystery/gothic. |

**Genre defaults when Step 1.6 has not been run (single-book mode):**

| Genre | Default count |
|---|---|
| Urban Drama / Contemporary Romance / Historical Court Drama | Duo (2), or Trio when synopsis has a rival/triangle |
| Dark Fantasy / Paranormal | Duo or Trio — a third figure (antagonist, rival) is welcome |
| Thriller / Horror | Solo or Environmental — protector + protected optional |
| Cultivation Fantasy / Sci-Fi / War Epic | Solo protagonist; rival/antagonist may be added |
| Isekai / Slice of Life | Solo, Duo, or small group — match the synopsis |

**A third figure adds more tension than a clean two-person embrace** when the synopsis offers it. Keep one clear focal pairing; place the third figure to threaten or intrude (watching from behind, reaching between them, turned away in betrayal).

**Female figure rule — MANDATORY:** the female character must be visually magnetic — impossible to scroll past. **Exposure = randomly T2 (Bold) or T3 (Maximum), picked independently per cover** — for each cover, roll T2 or T3 and bake that tier's assembly block from the Exposure Tiers table (`references/cover-allure-elements.md`) directly into the prompt; do not rely on the model rolling a lucky exposed result. Across a batch of books, this produces a mix of T2 and T3 covers (do not make every cover the same tier). Required elements, every time:
- Figure: `voluptuous hourglass figure, slim toned waist dramatically cinched, large full bust dramatically prominent, E-cup figure, long shapely legs` — curves are dramatic but the figure is NOT heavy or overweight; the waist must read as narrow against the hips and bust; bust baseline is E cup or larger — "full generous" alone undershoots, use explicit size language. (At T3, drop explicit `E-cup` per the doubao T3-safe rule — use visual-effect phrasing only; see `cover-allure-elements.md`.)
- Clothing: maximally revealing for the assigned tier — T2 = two simultaneous revealing elements (deep neckline + bare back/midriff/high slit); T3 = garment failing in multiple places (torn, slipped, soaked, sheer). See `references/cover-allure-elements.md` Skin & Clothing Vocabulary
- Skin: as much bare skin as the assigned tier allows within the §0 floor — T2 = cleavage + one secondary zone; T3 = three or more zones (bare back, legs, midriff, shoulders, extreme neckline)
- Pose: use the pose assigned in Step 1.6 (batch) or pick freely from the full Poses table in `references/cover-allure-elements.md` (single-book). No pose is a fixed default — rotate through the table. From-behind poses (marked ▲) cap at 2 per site.
- Framing: use the camera frame assigned in Step 1.6 (batch) or pick per-book (single-book). State it explicitly in every prompt. Never allow the model to default to a face-only crop.

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
**nano-banana-pro — terminal blank-prevention fallback:**
- Silently downgrades T3+ prompts to ~T1 output; square 1024×1024 (wrong aspect ratio for covers — reframe to 2:3 after generation).
- Use only when gpt and doubao (×2) both fail.

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
if not data.get('data'): print('SOFT_REJECT: empty data array (model declined silently)'); sys.exit(2)
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
if   gen_cover_apiyi "gpt-image-2-all"            "848x1280";  then MODEL_USED="gpt-image-2-all"
elif gen_cover_apiyi "doubao-seedream-5-0-260128" "1664x2496"; then MODEL_USED="doubao-seedream-5-0-260128"
elif gen_cover_apiyi "doubao-seedream-5-0-260128" "1664x2496"; then MODEL_USED="doubao-seedream-5-0-260128"  # retry once
elif gen_cover_apiyi "nano-banana-pro"            "1024x1024"; then MODEL_USED="nano-banana-pro"  # blank-prevention — ~T1 square output, reframe to 2:3
else MODEL_USED=""; echo "ALL_MODELS_FAILED — skipping book"
fi
echo "MODEL_USED=$MODEL_USED"

# Save metadata JSON alongside cover
printf '{"model":"%s","size":"%s","prompt":%s}\n' \
  "$MODEL_USED" "$SIZE" \
  "$(printf '%s' "$PROMPT" | python3 -c 'import json,sys; print(json.dumps(sys.stdin.read().strip()))')" \
  > "${BOOK_DIR}.json"
```

**Post-process by model used (final target: ~848×1280 true 2:3 portrait, ≤ 300 KB):**
- `gpt-image-2-all` → already 848×1280 PNG; convert to JPEG quality 85 or run `pngquant --quality=75-85 --force`.
- `doubao-seedream-5-0-260128` → crop the bottom-right `AI生成` watermark, then resize to 848 px wide (maintaining 2:3):
  ```bash
  sips -c 2321 1664 "$OUTPUT"                 # crop ~7% from bottom to clear watermark, output stays ~1664x2321
  sips -z 1280 848 "$OUTPUT"                  # resize to 848x1280 (2:3)
  ```
- `nano-banana-pro` → output is square 1024×1024; center-crop width to get 2:3, then resize up to 848×1280:
  ```bash
  sips -c 1024 683 "$OUTPUT"                  # crops to 683x1024 (2:3), centered
  sips -z 1280 848 "$OUTPUT"                  # resize to 848x1280
  ```
  Note: nano silently downgrades T3+ to ~T1 allure.

**Final compression / format choice:**
- Prefer JPEG: `sips -s format jpeg -s formatOptions 85 "$OUTPUT" --out "${OUTPUT%.png}.jpg"`, then rename books.ts cover path to `/covers/{slug}.jpg`.
- If the site must keep `.png` extensions, run `pngquant --quality=75-85 --force "$OUTPUT"`.
- Either way, every shipped cover must be ≤ 300 KB on disk. If still larger, lower JPEG quality to 80 or resize to 683×1024.

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

Re-run the full cascade once with the softened prompt. If every model (gpt → doubao ×2 → nano) still fails, **skip the book and continue the batch** — no SVG fallback.

On any other API error: log the response, skip this book, continue batch.

### Terminal fallback — nano (no SVG)

The cascade ends at `nano-banana-pro`. There is **no SVG fallback**:
- If `APIYI_API_KEY` is not set → skip the cover (warning + continue).
- If nano also fails → skip the book, log the reason, continue the batch.
- A nano result is usable as-is — reframe to 2:3 after generation.
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
public/covers/{book-slug}.png   ← cover image, served as /covers/{book-slug}.png
public/covers/{book-slug}.json  ← metadata: model, size, prompt (all in one file)
```

JSON format:
```json
{ "model": "gpt-image-2-all", "size": "848x1280", "prompt": "..." }
```

Served from `public/` — no CDN needed. The site builder reads `Book.cover` as `/covers/{book-slug}.png`.

After generation, write the JSON alongside the image:
```bash
printf '{"model":"%s","size":"%s","prompt":%s}' \
  "$MODEL_USED" "$SIZE" \
  "$(printf '%s' "$PROMPT" | python3 -c 'import json,sys; print(json.dumps(sys.stdin.read().strip()))')" \
  > "$BOOK_DIR/${BOOK_SLUG}.json"
```

Note: the old `cover_v1.prompt.txt` file is no longer used — prompt is stored in the JSON.

Site logo and favicon are **not** part of this phase. They are generated in Phase 6 (Design plan) via `references/design-system.md`.
