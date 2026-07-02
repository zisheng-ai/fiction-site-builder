# Operations Dashboard

Some fiction sites ship a non-reader `/dashboard` route used for operations: site status, deployment targets, ad account mapping, and a timeline of major changes. This page is **not part of the reader product** and must be excluded from search engine indexing.

## When to use

- Add a dashboard only when the parent `fictions/CLAUDE.md` explicitly requires it (e.g., `midnight-fable/dashboard`).
- Do not add it to new sites by default — it is an operational convenience, not a reader feature.

## Data contract

Keep site metadata and change history in `src/lib/docs-data.ts` so the dashboard can render them without parsing Markdown.

```ts
export type SiteStatus = 'live' | 'tbd'
export type AdType = 'AdX' | 'AdSense' | 'TBD'

export interface SiteInfo {
  id: string
  name: string
  domain: string
  url: string
  status: SiteStatus
  lang: string
  langLabel: string
  flag: string
  adType: AdType
  adAccount: string
  tone: string
  slogan: string
}

export type TimelineScope =
  | '全站'
  | 'skill'
  | 'velvet-throne'
  | 'midnight-fable'
  | 'wildfire-reads'
  | 'fuego-eterno'
  | 'london-pages'

export type TimelineRisk = 'high' | 'medium' | 'low'

export interface TimelineEntry {
  date: string
  title: string
  description: string
  tags: ('google-ads' | 'facebook' | 'perf' | 'seo' | 'geo' | 'ui' | 'content')[]
  scope: TimelineScope
  risk: TimelineRisk
  commit?: string
  commitUrl?: string
}

export const sites: SiteInfo[] = [
  {
    id: 'velvet-throne',
    name: 'velvet-throne',
    domain: 'velvet.nablepart.com',
    url: 'https://velvet.nablepart.com',
    status: 'live',
    lang: 'en',
    langLabel: '英语（美式）',
    flag: '🇺🇸',
    adType: 'AdX',
    adAccount: 'nablepart',
    tone: '暗黑浪漫小说，侧重权力、欲望与禁忌关系。',
    slogan: 'Dark desires. Unforgettable stories.',
  },
  // ... one entry per site in fictions/CLAUDE.md site table
]

export const timeline: TimelineEntry[] = [
  {
    date: '2026-07-02T22:06:31+08:00',
    title: 'Update midnight-fable submodule — fix dashboard CSS import',
    description: 'Update midnight-fable submodule — fix dashboard CSS import.',
    tags: ['ui'],
    scope: 'midnight-fable',
    risk: 'medium',
    commit: '40a786157c6b2cfa90d37f4e6ac9ccdc583d6622',
    commitUrl: 'https://github.com/zisheng-ai/fictions/commit/40a786157c6b2cfa90d37f4e6ac9ccdc583d6622',
  },
  // ... one entry per major operational change
]
```

### Field guidelines

- `scope`: operational scope of the change. Use `全站` for project-wide changes, `skill` for `fiction-site-builder` skill changes, or the specific site slug for single-site changes.
- `risk`: business/technical risk level. Use `high` for ad, pixel, consent, or revenue-impacting changes; `medium` for perf/seo/ui changes; `low` for content/docs-only changes.
- `tags`: classify the change so the dashboard can group/filter by dimension. Supported tags: `google-ads`, `facebook`, `perf`, `seo`, `geo`, `ui`, `content`.
- `commit` / `commitUrl`: optional but recommended for traceability.

## Sync rule

Whenever the site table or any major operational change in `fictions/CLAUDE.md` is updated, mirror the change in `src/lib/docs-data.ts`. The dashboard at `/dashboard` reads this file directly.

Also sync recent git commits back into `timeline` regularly so the history stays up to date.

## Route and robots

Place the route under `src/app/dashboard/page.tsx`. It does not need to be SSG-friendly; it can be a regular page component.

Block it from crawlers in both `src/app/robots.ts` and page metadata:

```ts
// src/app/robots.ts
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

```ts
// src/app/dashboard/page.tsx
import type { Metadata } from 'next'

export const metadata: Metadata = {
  title: 'Dashboard',
  description: 'Fiction site overview and change history.',
  robots: { index: false, follow: false },
}
```

## Dashboard UX patterns

The current `midnight-fable` dashboard uses the following patterns. Apply them to new dashboards when appropriate:

- **Top-level tabs**: switch between "站点总览" (site overview) and "改动历史" (change history). Remember the active tab in `localStorage`.
- **History dimension tabs**: group timeline events by tag (`google-ads`, `facebook`, `perf`, `seo`, `geo`, `ui`, `content`). Remember the active dimension in `localStorage`.
- **Filter chips**: allow filtering history by `scope` (change scope) and by additional tags.
- **Liquid-style cards**: display each event as a card with a subtle gradient glow, showing dimension icon, title, risk badge, commit hash, description, scope tag, and tags.
- **Risk badge**: render `high` / `medium` / `low` with red / amber / green colors.
- **Commit diff**: clicking the commit hash opens a side panel. Because the project uses static export (`output: 'export'`), embed the GitHub commit page in an iframe or link out to GitHub as a fallback. Do not rely on a local API route unless the deployment target supports serverless functions.
- **Language**: use the operational language required by `fictions/CLAUDE.md` (e.g., Chinese for `midnight-fable`). Timeline titles and descriptions should be localized.

## Implementation notes

- Keep the dashboard utilitarian: tables, filters, and plain text.
- Do not import reader components, ad slots, or analytics into the dashboard.
- Link back to the live site and to the parent repo when useful.
- Do not add the dashboard to the sitemap.
