# SEO Reference

Load this reference during Phase B4/B5 and before any site goes live. It consolidates everything search engines and social platforms need to crawl, index, and preview the site correctly.

## Required Files

Create all of these in every site. They are not optional.

| File | Location | Purpose |
|---|---|---|
| `sitemap.ts` | `src/app/sitemap.ts` | Generates `/sitemap.xml` for all static, book, and chapter URLs |
| `robots.ts` | `src/app/robots.ts` | Generates `/robots.txt` allowing all crawlers and pointing to the sitemap |
| `metadata` export | `src/app/layout.tsx` | Site-wide title template, description, `metadataBase`, OG fallback |
| `openGraph` + `twitter` | `book/[slug]/page.tsx` and `book/[slug]/chapter/[n]/page.tsx` | Per-book / per-chapter social previews |
| JSON-LD | `src/app/layout.tsx` (home), optionally book/chapter pages | Structured data: `WebSite`, `Book`, `WebPage` |

## 1. Sitemap

Use Next.js App Router's built-in metadata route. No third-party package.

```ts
// src/app/sitemap.ts
import { MetadataRoute } from 'next'
import { books } from '@/lib/books'

export default function sitemap(): MetadataRoute.Sitemap {
  const base = 'https://your-domain.com'

  const staticPages: MetadataRoute.Sitemap = [
    { url: base + '/', changeFrequency: 'weekly', priority: 1.0 },
    { url: base + '/about/', changeFrequency: 'yearly', priority: 0.3 },
    { url: base + '/contact/', changeFrequency: 'yearly', priority: 0.3 },
    { url: base + '/privacy/', changeFrequency: 'yearly', priority: 0.2 },
    { url: base + '/terms/', changeFrequency: 'yearly', priority: 0.2 },
  ]

  const bookPages: MetadataRoute.Sitemap = books.flatMap(book => [
    {
      url: `${base}/book/${book.slug}/`,
      changeFrequency: 'weekly',
      priority: 0.8,
    },
    ...Array.from({ length: book.chapterCount }, (_, i) => ({
      url: `${base}/book/${book.slug}/chapter/${i + 1}/`,
      changeFrequency: 'monthly',
      priority: 0.6,
    })),
  ])

  return [...staticPages, ...bookPages]
}
```

Rules:
- All URLs must end with `/` if the site uses `trailingSlash: true` in `next.config.js`.
- `book.chapterCount` must match the actual number of chapter files. Derive from the filesystem if possible.
- Run `pnpm build` and verify `/out/sitemap.xml` contains every expected URL.

## 2. Robots

```ts
// src/app/robots.ts
import { MetadataRoute } from 'next'

export default function robots(): MetadataRoute.Robots {
  return {
    rules: { userAgent: '*', allow: '/' },
    sitemap: 'https://your-domain.com/sitemap.xml',
  }
}
```

## 3. Root Metadata

```ts
// src/app/layout.tsx
import type { Metadata } from 'next'

export const metadata: Metadata = {
  metadataBase: new URL('https://your-domain.com'),
  title: {
    default: 'Your Site Name',
    template: '%s | Your Site Name',
  },
  description: 'Short, keyword-rich description of the site.',
  openGraph: {
    siteName: 'Your Site Name',
    type: 'website',
    locale: 'en_US',
    images: [
      {
        url: '/logo.png',
        width: 512,
        height: 512,
        alt: 'Your Site Name',
      },
    ],
  },
  twitter: {
    card: 'summary_large_image',
  },
  alternates: {
    canonical: './',
  },
}
```

Notes:
- `metadataBase` must be the real, live domain.
- `alternates.canonical: './'` makes every page self-canonicalize to its own path.
- Set `locale` to the site's actual language (`en_US`, `es_ES`, `ja_JP`, etc.).

## 4. Book and Chapter Metadata

```ts
// src/app/book/[slug]/page.tsx
import type { Metadata } from 'next'
import { getBook } from '@/lib/books'

export async function generateMetadata({ params }: { params: { slug: string } }): Promise<Metadata> {
  const book = getBook(params.slug)
  if (!book) return {}

  return {
    title: book.title,
    description: book.description.slice(0, 160),
    openGraph: {
      title: book.title,
      description: book.description.slice(0, 160),
      type: 'book',
      images: [{ url: book.cover, width: 848, height: 1280, alt: book.title }],
    },
    twitter: { card: 'summary_large_image' },
    alternates: { canonical: `./` },
  }
}
```

```ts
// src/app/book/[slug]/chapter/[n]/page.tsx
export async function generateMetadata({ params }: { params: { slug: string; n: string } }): Promise<Metadata> {
  const book = getBook(params.slug)
  const chapterNum = parseInt(params.n, 10)
  const chapter = getChapter(book?.slug, chapterNum)
  if (!book || !chapter) return {}

  return {
    title: `${chapter.title} — ${book.title}`,
    description: book.description.slice(0, 160),
    openGraph: {
      title: `${chapter.title} — ${book.title}`,
      description: book.description.slice(0, 160),
      type: 'article',
      images: [{ url: book.cover, width: 848, height: 1280, alt: book.title }],
    },
    twitter: { card: 'summary_large_image' },
    alternates: { canonical: `./` },
  }
}
```

## 5. JSON-LD Structured Data

Add a `WebSite` and `Organization` script on the home page, and a `Book` object on each book detail page.

### Home / Layout

```tsx
<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{
    __html: JSON.stringify({
      '@context': 'https://schema.org',
      '@type': 'WebSite',
      name: 'Your Site Name',
      url: 'https://your-domain.com',
      potentialAction: {
        '@type': 'SearchAction',
        target: 'https://your-domain.com/?q={search_term_string}',
        'query-input': 'required name=search_term_string',
      },
    }),
  }}
/>
```

### Book detail

```tsx
<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{
    __html: JSON.stringify({
      '@context': 'https://schema.org',
      '@type': 'Book',
      name: book.title,
      author: { '@type': 'Person', name: book.author },
      description: book.description,
      image: `https://your-domain.com${book.cover}`,
      url: `https://your-domain.com/book/${book.slug}/`,
      genre: book.genres.join(', '),
    }),
  }}
/>
```

## 6. Post-Launch Checklist

- [ ] Submit `/sitemap.xml` to Google Search Console.
- [ ] Verify `/robots.txt` returns 200 and references the correct sitemap URL.
- [ ] Inspect a book page with the [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/) and the [Twitter Card Validator](https://cards-dev.twitter.com/validator).
- [ ] Search the built `out/` folder for `og:image` and confirm every absolute URL is well-formed.
- [ ] Confirm the canonical URL on every route matches the route itself (no unexpected trailing index).

## 7. Common Mistakes

- **Forgetting `metadataBase`:** relative OG image URLs will not resolve to absolute URLs in production.
- **Serving the prompt JSON:** block `/covers/*.json` and `/illustrations/*/*.json` in `vercel.json` rewrites so prompts are not public.
- **Wrong chapter count:** `sitemap.ts` and `chapterCount` in `books.ts` must stay in sync with the actual file count.
- **No trailing slash mismatch:** if `next.config.js` uses `trailingSlash: true`, every URL in `sitemap.ts` must end with `/`.
