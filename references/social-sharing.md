# Social Sharing — Platform Limits & Card Requirements

## Character Limits

X (Twitter) is the tightest constraint. Design sharing text to fit X first.

| Platform | Limit | Notes |
|----------|-------|-------|
| **X** | 280 chars total | URL auto-shortened to 23 chars (t.co); **text budget = 257**. Keep `text=` ≤ 220 to be safe. |
| SMS | 160 chars/segment | Multi-segment supported on modern phones. Body = title + "\n" + URL (~100 chars total) — fine as-is. |
| Pinterest | 500 chars (description) | Full tagline fits. |
| WhatsApp | ~65,000 chars | No practical limit. Include full tagline. |
| Facebook | No hard limit | Platform scrapes OG tags; URL-only share is sufficient. |
| Messages (iMessage) | No limit | OG-based link preview on Apple devices. |

## Sharing Text Strategy

X is the binding constraint. Use this approach in `ShareBar.tsx`:

```ts
// X: first tagline line only, capped at 220 chars
const xText = `${title} — ${tagline.split('\n')[0].trim()}`.slice(0, 220)

// WhatsApp / Pinterest: full tagline is fine
const fullText = `${title}\n${tagline}\n${pageUrl}`
```

For SMS, only title + URL (no tagline).

## Share Card (Rich Preview) Requirements Per Platform

### Facebook, WhatsApp, iMessage, Telegram, LinkedIn
Scrape Open Graph tags from the shared URL. No extra parameters needed.

Required OG tags (handled by Next.js `generateMetadata`):
```
og:title        → book.title
og:description  → book.tagline
og:image        → absolute URL to cover image (resolved via metadataBase)
og:type         → "book" (detail pages) | "article" (chapter pages)
```

Image spec: minimum 200×200. Recommended 1200×630 (landscape) for best display.
Our covers are 848×1280 (portrait) — platforms will center-crop. Acceptable.

### X (Twitter)
Uses Twitter Card meta tags. Set in `generateMetadata`:
```ts
twitter: { card: 'summary_large_image' }
```
Next.js automatically copies `openGraph.images` to `twitter:image` when `twitter.card` is set.
No additional code needed as long as `metadataBase` is configured in `layout.tsx`.

Twitter card types:
- `summary` — small square image, title, description
- `summary_large_image` — **use this** — large image above title

### Pinterest
Does NOT scrape OG tags for pinning. Requires the `&media=` URL parameter:
```
https://pinterest.com/pin/create/button/
  ?url={encoded page URL}
  &media={encoded absolute cover image URL}   ← required for image
  &description={encoded text}
```
`coverUrl` must be absolute (not a relative path).

### SMS / Messages
No card preview. Body is plain text only. Keep concise: `title\npageUrl`.

## metadataBase Requirement

All OG/Twitter image URLs must be absolute. In Next.js App Router, set `metadataBase` in `src/app/layout.tsx`:

```ts
export const metadata: Metadata = {
  metadataBase: new URL('https://your-domain.com'),
  // ...
}
```

This allows relative paths like `/covers/book.webp` to resolve correctly in meta tags.
**Each site must have its own domain in `metadataBase`.** Verify this before deploying.

## ShareBar Component Pattern

```tsx
// src/components/ShareBar.tsx — client component
'use client'
import { useState } from 'react'

// Props
interface ShareBarProps {
  title: string      // book title
  tagline: string    // 3-line hook (lines separated by \n)
  coverUrl: string   // absolute URL — required for Pinterest media param
  pageUrl: string    // absolute URL — the book detail page (not the current chapter)
}
```

**Always share the book detail page URL** (not the current chapter URL). New readers should
land at `/book/[slug]/` where they can start from chapter 1.

## Placement Guidelines

- **Book detail page** (`/book/[slug]/`): below tagline + description, above chapter count.
- **Chapter page** (`/book/[slug]/chapter/[n]/`): after chapter content (and bottom ad),
  before the "Next chapter" CTA. This is the highest-impulse moment.
- **Home page**: not needed — no single book to share.

## CTA Copy

English sites:
- Mid-book: *Enjoying [Book Title]? Share it!*
- Last chapter: *Loved [Book Title]? Share it!*

Spanish sites (fuego-eterno):
- All chapters: *¿Disfrutando [Book Title]? ¡Compártelo!*
