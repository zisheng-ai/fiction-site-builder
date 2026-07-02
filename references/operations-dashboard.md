# Operations Dashboard

Some fiction sites ship a non-reader `/dashboard` route used for operations: site status, deployment targets, ad account mapping, and a timeline of major changes. This page is **not part of the reader product** and must be excluded from search engine indexing.

## When to use

- Add a dashboard only when the parent `fictions/CLAUDE.md` explicitly requires it (e.g., `midnight-fable/dashboard`).
- Do not add it to new sites by default — it is an operational convenience, not a reader feature.

## Data contract

Keep site metadata and change history in `src/lib/docs-data.ts` so the dashboard can render them without parsing Markdown.

```ts
export type SiteInfo = {
  name: string
  slug: string
  domain: string
  ads: string
  language: string
  tone: string
  status: 'live' | 'pending' | 'draft'
}

export type TimelineEntry = {
  date: string
  sites: string[]
  change: string
}

export const sites: SiteInfo[] = [
  {
    name: 'Velvet Throne',
    slug: 'velvet-throne',
    domain: 'velvet.nablepart.com',
    ads: 'nablepart AdX',
    language: 'en',
    tone: 'dark romance / paranormal / billionaire / sci-fi',
    status: 'live',
  },
  // ... one entry per site in fictions/CLAUDE.md site table
]

export const timeline: TimelineEntry[] = [
  { date: '2026-07-02', sites: ['midnight-fable'], change: 'Dashboard layout fix' },
  // ... one entry per major operational change
]
```

## Sync rule

Whenever the site table or any major operational change in `fictions/CLAUDE.md` is updated, mirror the change in `src/lib/docs-data.ts`. The dashboard at `/dashboard` reads this file directly.

## Route and robots

Place the route under `src/app/dashboard/page.tsx`. It does not need to be SSG-friendly; it can be a regular page component.

Block it from crawlers in `src/app/robots.ts`:

```ts
import { MetadataRoute } from 'next'

export default function robots(): MetadataRoute.Robots {
  return {
    rules: {
      userAgent: '*',
      allow: '/',
      disallow: '/dashboard/',
    },
    sitemap: 'https://your-domain.com/sitemap.xml',
  }
}
```

Also add a `<meta name="robots" content="noindex" />` tag inside the dashboard page itself as a safety net.

## UX notes

- Keep the dashboard utilitarian: tables, filters, and plain text.
- Do not import reader components, ad slots, or analytics into the dashboard.
- Link back to the live site and to the parent repo when useful.
- Use the same language as the site's operational docs (usually English or Chinese, not the reader-facing site language).
