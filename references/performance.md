# Performance

## Core Web Vitals Targets

Slow page loads lose readers before the first chapter. Fiction reading sites have no tolerance for sluggish chapter transitions.

| Metric | Target | Notes |
| --- | --- | --- |
| LCP | < 2.5s | Largest contentful paint at the 75th percentile of real users (Google "good" threshold; > 4s is "poor"). On a fiction site the LCP element is usually the first cover image or the chapter's opening heading. |
| INP | < 200ms | Reader controls (theme switch, font size) must be instant |
| CLS | < 0.1 | Font loading and image loading must not cause visible layout shifts |
| TTFB | < 600ms | For server-rendered routes |

### Verification strategy

**Default (fast, unattended):**
- Build the site (`pnpm run build`).
- Check the build output for warnings about large JS bundles or unoptimized images.
- Run automated smoke tests with `curl` against the started server (see `qa-checklist.md`).
- Verify cover images are WebP (lossy q82) and comfortably under 300KB (q82 typically lands ~50–60KB).

**Deep audit (only when user explicitly asks):**
- Test on simulated mobile (Moto G4 equivalent) at Slow 3G in Chrome DevTools Lighthouse. Do not test only on fast desktop connections.

Do not block the pipeline on a full Lighthouse run by default.

## Images

Book covers are the heaviest assets on the home and detail pages.

- Target < 80KB per cover at display size (typically 160×240px on mobile).
- Always set `width` and `height` on `<img>` to prevent CLS during load.
- Use `loading="lazy"` for below-fold covers on the home page.
- Use `fetchpriority="high"` on the first visible cover image.
- Ship covers and illustrations as lossy WebP — no `<picture>`/JPEG fallback needed (WebP is supported by every modern browser).
- CSS cover placeholders are acceptable when no image is provided. They must use flat color or subtle texture, not heavy gradients or box shadows.

**Cover compression (B5 step):** AI-generated covers are PNG and typically 400–800 KB. Convert to lossy **WebP q82** — this consistently brings covers to ~50–60 KB with no visible loss at display size. Prefer `cwebp`, fall back to Pillow:

```bash
for f in public/covers/*/cover_v1.png; do
  slug="$(basename "$(dirname "$f")")"
  out="public/covers/${slug}.webp"
  if command -v cwebp &>/dev/null; then
    cwebp -quiet -q 82 "$f" -o "$out"
  else
    python3 -c "from PIL import Image; im=Image.open('$f'); im.save('$out','webp',quality=82,method=6)"
  fi
done
```

**Never use lossless WebP** — on photographic covers it is ~3× larger than the source PNG. After conversion, ensure all `cover` paths in `src/lib/books.ts` use `.webp` and rebuild.

## Fonts

- Prefer system font stacks for body text. Do not load a web font for body reading — system stacks render faster and are often better for CJK.
- On Next.js, load any display font (titles, logo) via `next/font` instead of a CDN `<link>`. `next/font` self-hosts Google Fonts as static assets served from your own deployment domain — the browser never requests Google at runtime, so no `preconnect` is needed and there is no third-party dependency or GDPR exposure. A failed font download fails the build rather than silently falling back to the Google CDN.
- `font-display: swap` alone does **not** prevent layout shift — the swap from fallback to web font still moves text and counts against CLS. To actually hold CLS near zero, use `next/font` (it applies a size-adjusted fallback metric automatically) or define a fallback with matching `size-adjust`/`ascent-override`. Do not claim swap "fixes" CLS.
- Subset any loaded font to the characters actually used (Latin, CJK range as appropriate). `next/font` with `subsets: ['latin']` handles this.
- Never load a CJK web font for body text on mobile. The system stack (Hiragino, Yu Mincho, Noto) is always faster and equally good.
- If a custom reader font is offered as a setting, load it lazily only when the reader selects it.

## Chapter Content Loading

- Never bundle all chapter text into the initial HTML or JS payload.
- For static builds: generate one HTML file or JSON file per chapter and navigate between them.
- For SPA/Next.js: lazy-load chapter content when entering the reader route. Do not prefetch every chapter at book-detail load time.
- Prefetch only the next chapter when the reader reaches 80% of the current chapter.
- Avoid loading the full book catalog on a chapter reader page.

### Next.js App Router prefetch behavior

Chapter navigation is the hot path; lean on the framework's native prefetching rather than rolling your own.

- **Statically rendered chapter routes** (the `generateStaticParams` + SSG path this skill recommends) are fully prefetched by `<Link>` when they enter the viewport, and cached client-side for ~5 minutes by default. This is what makes prev/next feel instant — no extra code needed.
- **Dynamically rendered chapter routes** are *not* prefetched at all unless a `loading.js` boundary exists, in which case only the shell up to that boundary is prefetched. If your reader must be dynamic, add a `loading.tsx` so the layout/skeleton still prefetches. Prefer SSG to avoid this entirely.
- **Sibling navigation** (chapter N → N+1) reuses the shared parent layout and only fetches the changed leaf segment. Keep the reader chrome (header, nav, settings) in a parent `layout.tsx` so it is not re-fetched on every page turn.
- Next.js maintains a prioritized prefetch queue: links in the viewport first, then links showing hover/touch intent, and links scrolled off-screen are discarded rather than queued forever. A book-detail page with hundreds of chapter links therefore will not thrash the network — but still avoid rendering a 1000-link catalog without virtualization.

## JavaScript Bundle

- Initial JS on the reader page must be below 200KB gzipped for a prototype.
- Defer any script that is not needed for first paint.
- Do not load analytics, chat widgets, cookie consent banners, or ad scripts on a prototype unless the user explicitly asks.
- Avoid heavy React bundle setups for simple prototypes. Vanilla JS or Preact can deliver the same reading experience at a fraction of the cost.
- If using Next.js, enable `swcMinify` and check the bundle analyzer before delivery.

## CSS

- Inline critical above-the-fold CSS (reader background, font size, body text color).
- Tailwind: configure `content` paths correctly to eliminate unused utility classes.
- Reader theme switching must use DaisyUI `data-theme` value updates, not class-swap-triggered reflows.
- Avoid layout-triggering animations (avoid animating `width`, `height`, `top`, `left`). Use `transform` and `opacity` only.

## Caching

For static builds:
- Recommend `Cache-Control: public, max-age=31536000, immutable` for hashed assets.
- Recommend `Cache-Control: public, max-age=3600` for HTML pages.

## Offline / PWA

Implement a Service Worker only if the user asks for PWA or offline reading support.

When implementing:
- Cache the site shell (HTML, CSS, core JS) on install.
- Cache visited chapters on fetch, using a cache-first strategy for chapter content.
- Cache the home page and last-visited book detail.
- Show an offline fallback page for uncached routes.
- Do not cache chapter content speculatively (pre-cache the whole book) unless the user asks — it wastes mobile data.

## Vercel Deployment Checklist

Five standards every fiction site deployed to Vercel must satisfy before going live.

### 1. sitemap.ts + robots.ts

Use Next.js App Router's native metadata route files — no third-party package needed.

Place both files directly under `src/app/`:

**`src/app/sitemap.ts`** — imports the books array, generates URLs for every book detail page and every chapter page. All URLs end with `/` (matches `trailingSlash: true` in next.config):

```ts
import { MetadataRoute } from 'next'
import { books } from '@/lib/books'

export default function sitemap(): MetadataRoute.Sitemap {
  const base = 'https://your-domain.com'
  const staticPages: MetadataRoute.Sitemap = [
    { url: base + '/', changeFrequency: 'weekly', priority: 1.0 },
    { url: base + '/about/', changeFrequency: 'yearly', priority: 0.3 },
    { url: base + '/privacy/', changeFrequency: 'yearly', priority: 0.2 },
    { url: base + '/terms/', changeFrequency: 'yearly', priority: 0.2 },
    { url: base + '/contact/', changeFrequency: 'yearly', priority: 0.2 },
  ]
  const bookPages: MetadataRoute.Sitemap = books.flatMap(book => [
    { url: `${base}/book/${book.slug}/`, changeFrequency: 'weekly' as const, priority: 0.8 },
    ...Array.from({ length: book.chapterCount }, (_, i) => ({
      url: `${base}/book/${book.slug}/chapter/${i + 1}/`,
      changeFrequency: 'monthly' as const,
      priority: 0.6,
    })),
  ])
  return [...staticPages, ...bookPages]
}
```

**`src/app/robots.ts`** — points search engines at `/sitemap.xml`:

```ts
import { MetadataRoute } from 'next'

export default function robots(): MetadataRoute.Robots {
  return {
    rules: { userAgent: '*', allow: '/' },
    sitemap: 'https://your-domain.com/sitemap.xml',
  }
}
```

Both files are automatically served at `/sitemap.xml` and `/robots.txt` by the framework — no `next.config` change required.

### 2. vercel.json Cache Headers + Security

**`vercel.json`** at the project root:

```json
{
  "headers": [
    {
      "source": "/(covers|illustrations)/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=31536000, immutable"
        }
      ]
    }
  ],
  "rewrites": [
    { "source": "/covers/:file.json", "destination": "/___blocked___" },
    { "source": "/illustrations/:book/:file.json", "destination": "/___blocked___" }
  ]
}
```

**Cache headers**: covers and illustrations are content-addressed and never change after upload — one combined pattern caches both at the CDN edge for one year, eliminating origin bandwidth on repeat visits.

**Rewrites (security)**: each image generation also produces a `.json` sidecar that contains the full AI prompt. Rewriting `.json` requests to a non-existent path causes Vercel to return a natural 404, blocking prompt exposure without affecting image delivery. The two patterns cover the flat cover structure (`/covers/{slug}.json`) and the nested illustration structure (`/illustrations/{book}/{file}.json`).

### 3. CookieBanner

Each site needs its own cookie-consent banner with a site-specific localStorage key so consent state is isolated per domain.

**`src/components/CookieBanner.tsx`**:

```tsx
'use client'
import { useEffect, useState } from 'react'

// Use a site-specific key, e.g. "vt-cookie-consent" for Velvet Throne,
// "mf-cookie-consent" for Midnight Fable, etc.
const CONSENT_KEY = 'vt-cookie-consent'

export default function CookieBanner() {
  const [visible, setVisible] = useState(false)

  useEffect(() => {
    if (!localStorage.getItem(CONSENT_KEY)) setVisible(true)
  }, [])

  if (!visible) return null

  const accept = () => {
    localStorage.setItem(CONSENT_KEY, '1')
    setVisible(false)
  }

  return (
    <div className="fixed bottom-0 left-0 right-0 z-50 bg-base-200 border-t border-base-300 p-4 flex flex-col sm:flex-row items-center gap-3 text-sm">
      <p className="flex-1 text-base-content/80">
        {/* Replace "Velvet Throne" with the actual site name */}
        Velvet Throne uses cookies to personalise content and ads.
      </p>
      <button onClick={accept} className="btn btn-primary btn-sm shrink-0">
        Accept
      </button>
    </div>
  )
}
```

Import and render `<CookieBanner />` at the end of the `<body>` in `src/app/layout.tsx`:

```tsx
import CookieBanner from '@/components/CookieBanner'
// ...
<body>
  {children}
  <CookieBanner />
</body>
```

Banner text template: `"{Site Name} uses cookies to personalise content and ads."`

### 4. OG Image

Three-layer requirement. Every layer must be covered before launch:

| Layer | Where | Image | URL form |
|---|---|---|---|
| **Homepage** | `layout.tsx` openGraph | `logo.png` (512×512) | Absolute (`https://`) |
| **Book detail** | `book/[slug]/page.tsx` generateMetadata | `book.cover` (848×1280) | Relative OK — resolved by `metadataBase` |
| **Chapter** | `book/[slug]/chapter/[n]/page.tsx` generateMetadata | `book.cover` (848×1280) | Relative OK — resolved by `metadataBase` |

**`metadataBase` is the key**: set it once in `layout.tsx` with the real domain, and all relative OG image URLs in child pages resolve to absolute automatically. No `siteUrl` env var needed.

**`src/app/layout.tsx`** — homepage fallback (logo, absolute URL):

```ts
export const metadata: Metadata = {
  metadataBase: new URL('https://your-domain.com'),  // hardcode real domain
  openGraph: {
    siteName: 'Your Site Name',
    type: 'website',
    images: [{ url: 'https://your-domain.com/logo.png', width: 512, height: 512, alt: 'Your Site Name' }],
  },
}
```

**`src/app/book/[slug]/page.tsx`** and **`src/app/book/[slug]/chapter/[n]/page.tsx`** — book cover (relative path resolved by metadataBase):

```ts
openGraph: {
  title: book.title,
  description: book.description,
  images: [{ url: book.cover, width: 848, height: 1280, alt: book.title }],
  type: 'book',  // or 'article' for chapter pages
  siteName: 'Your Site Name',
},
twitter: { card: 'summary_large_image' },
```

**Chapter page without explicit OG image** is acceptable — Next.js falls back to the root layout's `logo.png`. But setting `book.cover` on chapter pages is preferred for better FB/Twitter previews.

Rules:
- `logo.png` must exist at `public/logo.png`. Dimensions: 512×512 minimum, square is safe for all platforms.
- `book.cover` is `/covers/{slug}.webp` — a relative path. With `metadataBase` set, Next.js outputs an absolute URL in the built HTML. Verify by grepping `og:image` in `out/` after build.
- The book cover (portrait 2:3, 848×1280) doubles as the FB link preview for book and chapter pages — no separate OG image asset needed.

### 5. Speed Insights + Analytics

Vercel Speed Insights collects real-user Core Web Vitals (LCP, INP, CLS) and surfaces them in the Vercel dashboard. Vercel Analytics tracks page views and visitor trends. Both are GDPR-friendly (no cookies, no cross-site tracking) and complement GA4 rather than replace it.

**Install:**

```bash
pnpm add @vercel/speed-insights @vercel/analytics
```

**`src/app/layout.tsx`** — import and render both components inside `<body>`:

```tsx
import { SpeedInsights } from '@vercel/speed-insights/next'
import { Analytics } from '@vercel/analytics/react'
// ...
<body>
  {children}
  <CookieBanner />
  <SpeedInsights />
  <Analytics />
</body>
```

Both components inject a minimal script that runs after the page is interactive — they do not block first paint or affect LCP.

---

## Pitfall: Internal npm Registry in pnpm Lockfile

If the development machine has a corporate or internal npm registry set as the global pnpm registry (e.g. Alibaba's `registry.npm.alibaba-inc.com`), pnpm bakes the registry's tarball URLs into `pnpm-lock.yaml`. Vercel's CI cannot reach an internal network and the build fails with `ERR_SOCKET_TIMEOUT` when fetching packages.

**Symptom**: Vercel build log shows errors like:
```
WARN GET https://registry.anpm.alibaba-inc.com/@vercel/analytics/-/analytics-x.x.x.tgz
ERR_SOCKET_TIMEOUT ... Socket timeout
Error: Command "pnpm install" exited with 1
```

**Fix**: add a project-level `.npmrc` at the site root to override the global registry, then regenerate the lockfile:

```ini
# .npmrc
registry=https://registry.npmjs.org
```

```bash
rm pnpm-lock.yaml
pnpm install --registry https://registry.npmjs.org
```

The `--registry` flag is required because pnpm's own global config (`pnpm config set registry`) takes precedence over `.npmrc`; passing it on the CLI overrides everything. Commit both `.npmrc` and the regenerated `pnpm-lock.yaml`. The lockfile should contain only `integrity` hashes, not `tarball` URLs pointing to the internal host.
