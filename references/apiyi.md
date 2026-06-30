# APIyi Image Generation

Reference for `story-cover.md`. Covers authentication, model selection, request format, and response handling for cover generation via `api.apiyi.com`.

Docs: https://docs.apiyi.com/

## Authentication

```bash
Authorization: Bearer $APIYI_API_KEY
Content-Type: application/json
```

Base URL: `https://api.apiyi.com/v1` (backup: `https://vip.apiyi.com/v1`)

Rate limits: 3,000 RPM · 1M TPM · 100 concurrent requests. `429` → exponential backoff.

---

## Models

### gpt-image-2-all (primary — use this for all covers)

- **Price:** $0.03/image flat across all 30 sizes (4K does not cost extra)
- **Generation time:** 90–150s typical; configure `--max-time 300` minimum
- **Sizes:** 30 presets only (10 aspect ratios × 3 resolution tiers). Invalid sizes return an error.
- **Limitations:** no `quality` parameter, no `n` (single output per call), no inpainting

**Portrait cover sizes (2:3 ratio):**

| Tier | Size | Use |
|------|------|-----|
| 1K Fast | `848x1280` | Default — sufficient for all on-screen display sizes |
| 2K | `1360x2048` | Higher fidelity if budget allows |
| 4K | `2336x3520` | Print / retina only |

**Complete 30-size table:**

| Ratio | 1K | 2K | 4K |
|-------|----|----|-----|
| Square | 1280×1280 | 2048×2048 | 2880×2880 |
| Portrait 2:3 | 848×1280 | 1360×2048 | 2336×3520 |
| Landscape 3:2 | 1280×848 | 2048×1360 | 3520×2336 |
| Portrait 3:4 | 960×1280 | 1536×2048 | 2480×3312 |
| Landscape 4:3 | 1280×960 | 2048×1536 | 3312×2480 |
| Social 4:5 | 1024×1280 | 1632×2048 | 2560×3216 |
| Landscape 5:4 | 1280×1024 | 2048×1632 | 3216×2560 |
| Story 9:16 | 720×1280 | 1152×2048 | 2160×3840 |
| Wide 16:9 | 1280×720 | 2048×1152 | 3840×2160 |
| Cinema 21:9 | 1280×544 | 2048×864 | 3840×1632 |

**Request:**

```bash
curl "https://api.apiyi.com/v1/images/generations" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $APIYI_API_KEY" \
  --max-time 300 \
  -d '{
    "model": "gpt-image-2-all",
    "prompt": "...",
    "size": "848x1280"
  }'
```

**Response format:** `b64_json` field already includes the `data:image/png;base64,` prefix. Strip the prefix before writing to disk:

```python
import base64, json, sys
data = json.load(sys.stdin)
b64 = data["data"][0]["b64_json"]
# strip prefix if present
if b64.startswith("data:"):
    b64 = b64.split(",", 1)[1]
with open("cover_v1.png", "wb") as f:
    f.write(base64.b64decode(b64))
```

Or if the response returns a CDN `url` instead of `b64_json`, download it directly (valid ~24h).

**Content filter behavior:**
- 5xx response → no charge, retry with softened prompt
- 200 response containing refusal text → billed, do not retry the same prompt

---

### gpt-image-1 (alternative — more flexible sizes)

- **Price:** $0.005–$0.052/image (token-based, auto-selected cheapest billing)
- **Sizes:** `1024x1024`, `1536x1024`, `1024x1536`, or `auto`
- **Supports:** `quality` (low/medium/high/auto), `n` (1–10), `output_format` (png/jpeg/webp), `background` (transparent/opaque/auto)
- **Response:** `url` (default) or `b64_json` (raw base64, no prefix)

```bash
curl "https://api.apiyi.com/v1/images/generations" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $APIYI_API_KEY" \
  -d '{
    "model": "gpt-image-1",
    "prompt": "...",
    "size": "1024x1536",
    "quality": "medium"
  }'
```

Use gpt-image-1 only when a non-preset aspect ratio is needed. Default to gpt-image-2-all.

---

## Error handling

| Code | Meaning | Action |
|------|---------|--------|
| 429 | Rate limit | Exponential backoff, retry |
| 5xx | Content filter or server error | No charge; retry with softened prompt once |
| Timeout | Generation exceeded `--max-time` | Increase to 360s, retry once; then fall back to SVG |
