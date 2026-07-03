# Social Sharing — ShareBar Component & Platform Requirements

## Tagline Length Constraint

Taglines must be **≤ 180 characters**, single line (no `\n`).  
This ensures `${title} — ${tagline}` fits within X's 220-char text budget for all titles.  
Keep this limit when writing or regenerating taglines.

## ShareBar Platforms

| Platform | Share button | Image in card | Notes |
|----------|-------------|---------------|-------|
| **Pinterest** | ✅ | `&media=` URL param | Does NOT scrape OG; must pass `coverUrl` explicitly |
| **X (Twitter)** | ✅ | `twitter:card: summary_large_image` | Needs Twitter Card Validator crawl for new URLs |
| **Facebook** | ✅ | OG tags | Scrapes `og:image` automatically |
| **WhatsApp** | ✅ | OG tags | Scrapes `og:image` automatically |
| **Telegram** | ✅ | OG tags | Scrapes `og:image` automatically |
| **Messages (SMS/iMessage)** | ✅ | OG tags (iMessage) | SMS is plain text only |
| **Copy Link** | ✅ (copies text+url) | — | Copies `title\ntagline\nurl` to clipboard |
| **Discord** | No button needed | OG tags | User pastes URL; Discord scrapes OG automatically |

## X Character Limit

X total = 280 chars. URL auto-shortened to 23 chars (t.co). Text budget = **257 chars**.
Use `${title} — ${tagline}` directly — no truncation needed with taglines ≤ 180 chars.

## Share Card (Rich Preview) Per Platform

### Facebook, WhatsApp, iMessage, Telegram, Discord, LinkedIn
Scrape Open Graph tags from the shared URL. No extra parameters needed in the share URL.

Required OG tags (handled by Next.js `generateMetadata`):
```ts
openGraph: {
  title: book.title,
  description: book.tagline,
  images: [{ url: book.cover, width: 848, height: 1280, alt: book.title }],
  type: 'book',          // book detail pages
  // type: 'article',   // chapter pages
}
```

Image spec: 848×1280 (portrait covers) — platforms center-crop. Acceptable for all.

### X (Twitter)
Set in `generateMetadata`:
```ts
twitter: { card: 'summary_large_image' }
```
Next.js copies `openGraph.images` → `twitter:image` automatically.  
**New URLs**: use Twitter Card Validator (`cards.twitter.com/validator/`) to force a crawl.  
The compose dialog does not preview cards until Twitter has crawled the URL.

### Pinterest
Does NOT scrape OG. Requires `&media=` URL parameter in the share link:
```
https://pinterest.com/pin/create/button/
  ?url={enc(pageUrl)}
  &media={enc(coverUrl)}    ← absolute URL required
  &description={enc(text)}
```

### SMS / Messages
No card preview. Plain text: `title\npageUrl`.

## metadataBase Requirement

All OG/Twitter image URLs must be absolute. Set in `src/app/layout.tsx`:
```ts
export const metadata: Metadata = {
  metadataBase: new URL('https://your-domain.com'),
}
```
This resolves relative cover paths (`/covers/book.webp`) to absolute URLs in all meta tags.  
**Each site must have its own correct domain.** Verify before deploying.

## ShareBar Component

File: `src/components/ShareBar.tsx` — must be a client component (`'use client'`).

```tsx
'use client'
import { useState } from 'react'

interface ShareBarProps {
  title: string      // book title
  tagline: string    // single-line hook, ≤ 180 chars
  coverUrl: string   // absolute URL — required for Pinterest &media= param
  pageUrl: string    // absolute URL — always the book detail page, not a chapter
}

export default function ShareBar({ title, tagline, coverUrl, pageUrl }: ShareBarProps) {
  const [copied, setCopied] = useState(false)
  const enc = encodeURIComponent

  const platforms = [
    { key: 'pinterest', label: 'Pinterest', color: '#E60023', newTab: true,
      href: `https://pinterest.com/pin/create/button/?url=${enc(pageUrl)}&media=${enc(coverUrl)}&description=${enc(`${title} — ${tagline}`)}` },
    { key: 'x',         label: 'X',         color: '#000000', newTab: true,
      href: `https://twitter.com/intent/tweet?url=${enc(pageUrl)}&text=${enc(`${title} — ${tagline}`)}` },
    { key: 'facebook',  label: 'Facebook',  color: '#1877F2', newTab: true,
      href: `https://www.facebook.com/sharer/sharer.php?u=${enc(pageUrl)}` },
    { key: 'whatsapp',  label: 'WhatsApp',  color: '#25D366', newTab: true,
      href: `https://wa.me/?text=${enc(`${title}\n${tagline}\n${pageUrl}`)}` },
    { key: 'telegram',  label: 'Telegram',  color: '#229ED9', newTab: true,
      href: `https://t.me/share/url?url=${enc(pageUrl)}&text=${enc(`${title}\n${tagline}`)}` },
    { key: 'messages',  label: 'Messages',  color: '#34C759', newTab: false,
      href: `sms:?body=${enc(`${title}\n${pageUrl}`)}` },
  ]

  async function copyLink() {
    try {
      await navigator.clipboard.writeText(`${title}\n${tagline}\n${pageUrl}`)
      setCopied(true)
      setTimeout(() => setCopied(false), 2000)
    } catch { /* clipboard not available */ }
  }

  // Render: icon buttons with brand-color hover, plus Copy Link button
}
```

Icon SVGs: use inline SVGs (no icon library dependency). Copy from existing site's `ShareBar.tsx`.

## Placement

**Book detail page** (`/book/[slug]/page.tsx`):
```tsx
<p className="... italic">{book.tagline}</p>
<ShareBar title={book.title} tagline={book.tagline}
  coverUrl={`${BASE_URL}${book.cover}`} pageUrl={`${BASE_URL}/book/${slug}/`} />
<p className="...">{book.description}</p>    {/* description comes AFTER ShareBar */}
```

**Chapter page** (`/book/[slug]/chapter/[n]/page.tsx`) — after chapter content and bottom ad, before "Next chapter" CTA:
```tsx
{/* Share */}
<div className="my-8 py-6 border-t border-base-300 text-center">
  <p className="text-sm text-base-content/50 mb-3">
    {next ? <>Enjoying <em>{book.title}</em>?</> : <>Loved <em>{book.title}</em>?</>} Share it!
  </p>
  <div className="flex justify-center">
    <ShareBar title={book.title} tagline={book.tagline}
      coverUrl={`${BASE_URL}${book.cover}`} pageUrl={`${BASE_URL}/book/${slug}/`} />
  </div>
</div>
```

Spanish sites — use localised CTA: `¿Disfrutando <em>{book.title}</em>? ¡Compártelo!`

**Home page**: not needed — no single book to share.

## Always share the book detail page URL

Pass `pageUrl={`${BASE_URL}/book/${slug}/`}` everywhere — including from chapter pages.  
New readers should land at the book detail page to start from chapter 1.
