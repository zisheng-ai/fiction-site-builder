# UI And Visual Quality (Mobile-First Responsive)

**Mobile-first means responsive — not mobile-only.** Write styles for mobile first, then layer in `min-width` breakpoints to enhance the layout for tablet and desktop. Every component spec in this file covers all three breakpoints. Desktop must have a distinct, purposeful layout — not a stretched phone screen.

## Aesthetic Direction

Default to refined editorial reading product. This is the quality floor. `design-system.md` defines the brief-specific point of view on top of this floor.

Non-negotiable aesthetic defaults:
- Calm, low-saturation palette.
- Strong text hierarchy with at least 3 visible levels.
- Crisp surfaces with small, consistent border radii (6–8px).
- Subtle `1px` borders over heavy box shadows.
- Book covers clear enough to read title and art at thumbnail size.
- Sparse but useful metadata: genre tag, status, word count or chapter count, update date.
- **Font:** System sans-serif stack site-wide. No external webfont required. `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Hiragino Sans", "Yu Gothic UI", "Malgun Gothic", sans-serif`. For Japanese or Korean content use the language-specific stacks in `references/internationalization.md`. Loads zero extra bytes.

## What To Avoid

Any of these is a quality gate failure:

- Loud purple/red/orange gradients as the primary identity.
- Decorative glassmorphism or frosted glass panels.
- Large glowing orbs, blurred blobs, or SaaS hero graphic patterns.
- Dense ad-card layouts with 4+ metadata lines per row.
- Body text below 18px on mobile or below 19px on desktop.
- Metadata text below 12px.
- Body fonts that are playful, handwritten, or display-only.
- A full-screen marketing hero section before the actual book list.
- Pure black or pure white as any default background.

## Component Specifications

### Top / Navigation Bar
- Height: 48–56px on mobile.
- Content: logo (left), optional action (right). Never more than one action icon.
- **Logo spec (site-wide):** `<img src="/logo.png" className="block h-8 w-auto rounded-sm" />`; on home page use `next/image` (`width={28} height={28} className="rounded-sm"`) for consistent rendering.
- Home: logo + site name text + ThemeToggle
- Book detail: logo (links to `/`) + ThemeToggle
- Chapter: logo (links to `/`) + centered book/chapter name + TOC icon + ThemeToggle
- On scroll down: may compress or hide (if implementing immersive mode).

### Bottom Bar (Mobile Reader)
- Height: 60–64px + `env(safe-area-inset-bottom)`. Large tap targets are non-negotiable — this is the primary interaction on the page.
- Content: "Table of contents" (left) + "Next →" (right, hidden on last chapter).
- Must not cover body text. Use `padding-bottom` on the content area to prevent overlap.
- See `reader-ux.md` **Navigation Button Size** for full button spec.

**Bottom bar TOC button behavior:** navigates to the book detail page and scrolls to the chapter list anchor — does not open a drawer. The book detail chapter list container must have `id="toc"`.

Column ratio `minmax(96px, 0.75fr) minmax(136px, 1.12fr)`. TOC button font-size uses `!text-[12px]` to override btnBase default. Text may wrap on very narrow viewports — do not add `whitespace-nowrap`.

```tsx
// bottom bar grid
// ⚠️ all nav links must use window.location.href — <a href> gets intercepted by Next.js router after hydration
<div style={{
  display: 'grid',
  gap: '12px',
  gridTemplateColumns: nextChapter !== null ? 'minmax(96px, 0.75fr) minmax(136px, 1.12fr)' : '1fr',
}}>
  <a
    href={`/book/${bookSlug}#toc`}
    onClick={(e) => { e.preventDefault(); window.location.href = `/book/${bookSlug}#toc` }}
    className={`${btnBase} !text-[12px]`}
  >
    Table of contents
  </a>
  {nextChapter !== null && (
    <a
      href={`/book/${bookSlug}/chapter/${nextChapter}`}
      onClick={(e) => { e.preventDefault(); window.location.href = `/book/${bookSlug}/chapter/${nextChapter}` }}
      className={`${btnBase} bg-primary text-white`}
    >
      Next →
    </a>
  )}
</div>

// book detail page — BelowFold component
<section id="toc">
  {/* chapter list */}
</section>
```

This allows readers on any chapter to return to the detail page and see the full chapter list in one tap.

### Book Card (Cover-First Responsive Grid)

The book list uses a responsive grid. The card is the page's primary visual unit; get it right.

**Grid columns:**
- Mobile (< 640px): 1 column
- Tablet (≥ 640px): 2 columns
- Desktop (≥ 1024px): 3 columns, or `repeat(auto-fill, minmax(280px, 1fr))`
- Column gap: 20–24px; row gap: 24–32px

**Cover:**
- Aspect ratio: `3/4` (portrait book cover). Do not use landscape or square.
- Fills full card width. Top corners match card radius (16px). Bottom of image: no radius — the text area sits flush below.
- Genre badge: absolute-positioned at top-right of the cover, `background: rgba(0,0,0,0.55)`, `backdrop-filter: blur(4px)`, white text, `border-radius: 6px`, `font-size: 11px`, `font-weight: 700`, `padding: 3px 9px`. Shows the genre name only (e.g. "Romance", "Thriller").

**Card container:**
- `background: var(--surface)` (white or near-white)
- `border-radius: 16px`
- `box-shadow: 0 2px 16px rgba(0,0,0,0.07)`
- Card gap in the feed: `16px`

**Text area below the cover:**
- Padding: `14px 16px 18px`
- Title: `font-size: 18–20px`, `font-weight: 700`, `line-height: 1.28`, 2-line clamp, `letter-spacing: -0.01em`
- Metadata (second line): `font-size: 13px`, `--muted` color. Shows chapter count + status — e.g., "24 Chapters · Ongoing". **Never show the raw domain URL** as metadata.
- Tap area: entire card.

**Quality bar:** A finished book card should look like it belongs in a native app — not a WordPress blog post list. The genre badge and proper metadata line are non-negotiable.

### Book Row (Text-First List)
- Row height: auto, minimum 72px.
- Left: small cover thumbnail (48×72px) or genre accent strip (8px wide).
- Right: title, author, 1-line synopsis or latest chapter name, metadata.
- Divider: `1px` `--muted` border between rows, or `8px` gap without border.

### Home Page Hero

The home page hero sets the site's identity before the reader sees a single book. Choose one style and apply it consistently — same logic as the book detail hero.

**Choose by site tone (same decision as book detail):**

| Site tone | Home hero style |
|---|---|
| Dark romance / thriller / vampire / paranormal | **cinematic** — Featured Book Full-Bleed |
| Fantasy / contemporary romance / colorful multi-genre | **gradient** — Brand Gradient Tagline |
| Literary fiction / clean romance / prose-first / short story | **editorial** — Text-Only Editorial |

The home page hero is a site-level decision — every site uses one style. The book detail hero is per-book — each book sets its own `heroStyle` independently.

---

#### cinematic — Featured Book Full-Bleed

One designated featured book's cover fills the top of the home page, full viewport width. Site tagline and a "Start reading" CTA are overlaid at the bottom. Book grid follows below the fold.

```
┌─────────────────────────────────────────────┐  ← full viewport width
│                                             │
│    [featured book cover, object-cover]      │  min-h-[55vh]
│                                             │
│▓▓▓▓ gradient from-base-100 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓│
│  Site tagline                               │
│  [Read now →]  [Browse all ↓]              │
└─────────────────────────────────────────────┘
  Book grid (all books including featured)
```

Implementation:
```tsx
// books.ts — mark one book as featured
{ slug: 'blood-and-velvet', featured: true, ... }

// page.tsx
const featured = books.find(b => b.featured) ?? books[0]

<div className="relative min-h-[55vh] flex items-end">
  <Image src={featured.cover} alt={featured.title} fill className="object-cover object-center" priority />
  <div className="absolute inset-x-0 top-0 h-20 bg-gradient-to-b from-black/40 to-transparent pointer-events-none" />
  <div className="absolute inset-0 bg-gradient-to-t from-base-100 via-base-100/60 to-transparent pointer-events-none" />
  <div className="relative z-10 w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pb-10">
    <p className="text-xs font-semibold uppercase tracking-widest text-primary mb-2">Featured</p>
    <h1 className="text-3xl sm:text-4xl font-extrabold text-base-content leading-tight tracking-tight mb-1">
      {featured.title}
    </h1>
    <p className="text-sm text-base-content/60 mb-5">by {featured.author}</p>
    <HardLink href={`/book/${featured.slug}/chapter/1`} className="inline-flex items-center justify-center px-7 h-11 rounded-[12px] bg-primary text-white font-bold text-sm tracking-tight hover:-translate-y-px transition-transform">
      Read now
    </HardLink>
  </div>
</div>

{/* Book grid — all books */}
<section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
  <div className="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-x-4 gap-y-8">
    {books.map(book => <BookCard key={book.slug} {...book} />)}
  </div>
</section>
```

Notes:
- Nav: same transparent floating pattern as book detail `cinematic` — `text-white/80` back link, top scrim
- Featured book also appears in the grid below — do not hide it
- Add `featured?: boolean` to the `Book` type in `books.ts`

---

#### gradient — Brand Gradient Tagline

No cover image. Site's brand color fills the hero as a gradient. Site name, genre descriptor, and tagline sit on the gradient. Book grid below.

```
┌─────────────────────────────────────────────┐
│  ░░░░░ brand gradient (accent → base-100) ░░│
│                                             │
│         Site Name                           │
│         Genre descriptor                   │
│         Tagline                             │
│                                             │
└─────────────────────────────────────────────┘
  Book grid
```

Implementation:
```tsx
<section
  className="pt-24 pb-16 px-4 text-center"
  style={{ background: 'linear-gradient(160deg, oklch(from var(--p) l c h / 0.15) 0%, transparent 70%)' }}
>
  <h1 className="text-4xl sm:text-5xl font-extrabold text-base-content leading-tight tracking-tight mb-3">
    {siteTitle}
  </h1>
  <p className="text-base text-base-content/60 max-w-sm mx-auto">{tagline}</p>
</section>
```

Notes:
- Background: subtle accent tint, not a loud solid — `oklch` with low alpha keeps it readable in both light and dark themes
- Nav: standard opaque `bg-base-100/95 backdrop-blur-sm` header

---

#### editorial — Text-Only Editorial

Plain page background. Big typographic headline + subtitle. No image, no gradient in the hero. Book grid starts immediately below.

```
  Site Name (in nav)
  ─────────────────────────────────────────
  Big headline line 1
  Big headline line 2 (accent color)
  Subtitle
  ─────────────────────────────────────────
  Book grid
```

Implementation (current velvet-throne pattern):
```tsx
<header className="border-b border-base-300">
  <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-14 flex items-center justify-between">
    <Link href="/" className="flex items-center gap-2.5">
      <Image src="/logo.png" alt={siteTitle} width={28} height={28} className="rounded-sm" priority />
      <span className="text-lg font-bold text-base-content tracking-tight">{siteTitle}</span>
    </Link>
    <ThemeToggle />
  </div>
</header>

<section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-12 pb-8 text-center">
  <h1 className="text-4xl sm:text-5xl lg:text-6xl font-extrabold text-base-content leading-[1.1] tracking-tight pb-1">
    {headlineLine1}<br />
    <span className="text-primary">{headlineLine2}</span>
  </h1>
  <p className="mt-4 text-base text-base-content/60 max-w-md mx-auto">{subtitle}</p>
</section>

<section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pb-16">
  <div className="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-x-4 gap-y-8">
    {books.map(book => <BookCard key={book.slug} {...book} />)}
  </div>
</section>
```

Notes:
- Nav: standard opaque header with logo + site name + ThemeToggle
- Headline is 2 lines split at a natural break — first line neutral, second line in accent color
- No CTA in hero — the book grid *is* the CTA
- Best for sites where the catalog speaks for itself

---

### Book Detail Hero

Each book declares its hero style via the `heroStyle` field in `books.ts`. All three styles can coexist on the same site; `page.tsx` dispatches rendering by this field.

**Decision table (choose by book tone and cover quality):**

| Book tone | `heroStyle` |
|---|---|
| Dark romance / thriller / vampire / paranormal | `'cinematic'` |
| Fantasy / contemporary romance / vivid colorful cover | `'gradient'` |
| Literary fiction / clean romance / prose-first | `'atmospheric'` |

When the cover lacks enough visual tension to fill the full screen, default to `'atmospheric'`.

**Top nav bar — transparent with scroll-aware backdrop (per-heroStyle):**

The header starts **fully transparent** so the hero image/gradient shows through. It gains a frosted-glass backdrop only after the reader scrolls past 80 px. Icon treatment differs by background type:

| `heroStyle` | Logo filter | ThemeToggle wrapper |
|---|---|---|
| `cinematic` | `drop-shadow(0 1px 4px rgba(0,0,0,0.6))` | `<div className="bg-white/15 backdrop-blur-sm rounded-full p-1.5 text-white">` |
| `atmospheric` | `drop-shadow(0 1px 4px rgba(0,0,0,0.6))` | `<div className="bg-white/15 backdrop-blur-sm rounded-full p-1.5 text-white">` |
| `gradient` | `drop-shadow(0 1px 3px rgba(0,0,0,0.4))` | `<div className="bg-base-100/60 backdrop-blur-sm rounded-full p-1.5">` |

Implementation — add a `<style>` block and inline scroll script at the top of the hero component, and set `id="book-header"` on the `<header>`:

```tsx
// Inside each HeroXxx function, before <header>:
<style dangerouslySetInnerHTML={{ __html: `
  #book-header { transition: background .2s, backdrop-filter .2s, border-color .2s; }
  #book-header.bh-scrolled {
    background: color-mix(in oklch, var(--color-base-100) 80%, transparent);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid color-mix(in oklch, var(--color-base-300) 40%, transparent);
  }
` }} />
<script dangerouslySetInnerHTML={{ __html: `(function(){
  var h = document.getElementById('book-header');
  if (!h) return;
  function u() { h.classList.toggle('bh-scrolled', window.scrollY > 80); }
  window.addEventListener('scroll', u, { passive: true }); u();
})();` }} />

<header id="book-header" className="fixed top-0 left-0 right-0 z-30 h-14">
  <div className="max-w-7xl mx-auto px-4 h-full flex items-center justify-between">
    <Link href="/" aria-label="Home">
      <img src="/logo.png" alt={SITE_NAME} className="block h-8 w-auto rounded-sm"
        style={{ filter: 'drop-shadow(0 1px 4px rgba(0,0,0,0.6))' }} />
    </Link>
    <div className="bg-white/15 backdrop-blur-sm rounded-full p-1.5 text-white">
      <ThemeToggle />
    </div>
  </div>
</header>
```

For `gradient` heroStyle, swap the ThemeToggle wrapper and logo filter:
```tsx
style={{ filter: 'drop-shadow(0 1px 3px rgba(0,0,0,0.4))' }}
// ThemeToggle wrapper:
<div className="bg-base-100/60 backdrop-blur-sm rounded-full p-1.5">
```

> **DaisyUI v5 note:** `color-mix(in oklch, var(--color-base-100) 80%, transparent)` is the correct syntax. Do NOT use `oklch(var(--color-base-100)/0.8)` — DaisyUI v5 custom properties are already full `oklch(...)` strings, not bare channel tuples.

---

**`books.ts` type definitions:**

```ts
export type HeroStyle = 'cinematic' | 'gradient' | 'editorial'

export type Book = {
  slug: string
  title: string
  author: string
  tagline: string
  description: string
  genres: string[]
  cover: string
  status: BookStatus
  chapterCount: number
  heroStyle: HeroStyle  // required, no default
  heroColor?: string    // required when heroStyle === 'gradient', e.g. '#1a0a1e'
}
```

---

**`src/components/HardLink.tsx` (must create — server component replacement for `<a>` and `<Link>`):**

```tsx
'use client'
import type { CSSProperties, ReactNode } from 'react'
export default function HardLink({ href, className, style, children }: {
  href: string; className?: string; style?: CSSProperties; children: ReactNode
}) {
  return (
    <a href={href} className={className} style={style}
      onClick={(e) => { e.preventDefault(); window.location.href = href }}>
      {children}
    </a>
  )
}
```

---

**Full `app/book/[slug]/page.tsx` (all three hero styles in one component):**

```tsx
import type { Metadata } from 'next'
import Image from 'next/image'
import Link from 'next/link'
import { notFound } from 'next/navigation'
import { allChapters } from 'content-collections'
import { books, getBook, type Book } from '@/lib/books'
import ThemeToggle from '@/components/ThemeToggle'
import ResumeReading from '@/components/ResumeReading'
import HardLink from '@/components/HardLink'

type Props = { params: { slug: string } }

export function generateStaticParams() {
  return books.map(b => ({ slug: b.slug }))
}

export function generateMetadata({ params }: Props): Metadata {
  const book = getBook(params.slug)
  if (!book) return {}
  return {
    title: book.title,
    description: book.description,
    openGraph: {
      title: book.title,
      description: book.description,
      images: [{ url: book.cover, width: 800, height: 1200, alt: book.title }],
      type: 'book',
      siteName: 'SITE_NAME',
    },
    twitter: { card: 'summary_large_image' },
  }
}

// ── shared: synopsis + chapter list ─────────────────────────────────────────

function BelowFold({ book, chapters, slug }: { book: Book; chapters: { order: number; title: string }[]; slug: string }) {
  return (
    <div className="max-w-2xl mx-auto px-6 pt-6 pb-16">
      <p className="text-base text-base-content/75 leading-relaxed mb-2">{book.description}</p>
      <p className="text-sm text-base-content/40 mt-3 mb-10">
        {chapters.length} {chapters.length === 1 ? 'chapter' : 'chapters'} available
      </p>
      {chapters.length > 0 && (
        <section id="toc">
          <h2 className="text-[11px] font-semibold uppercase tracking-widest text-base-content/40 mb-4" style={{ letterSpacing: '0.12em' }}>
            Chapters
          </h2>
          <div className="divide-y divide-base-300">
            {chapters.map(ch => (
              <HardLink
                key={ch.order}
                href={`/book/${slug}/chapter/${ch.order}`}
                className="flex items-center gap-4 py-3.5 group hover:bg-base-200 -mx-3 px-3 rounded transition-colors"
              >
                <span className="text-sm text-base-content/30 w-6 text-right tabular-nums shrink-0">{ch.order}</span>
                <span className="flex-1 text-sm text-base-content group-hover:text-primary transition-colors">{ch.title}</span>
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className="text-base-content/30 group-hover:text-primary transition-colors shrink-0" aria-hidden="true">
                  <polyline points="9 18 15 12 9 6" />
                </svg>
              </HardLink>
            ))}
          </div>
        </section>
      )}
    </div>
  )
}

// ── shared: CTA button group ─────────────────────────────────────────────────

// ⚠️ CTABlock is a server component — cannot use onClick, must use HardLink
// HardLink uses window.location.href internally to trigger the browser progress bar and re-init ads
function CTABlock({ book, slug, chapters }: { book: Book; slug: string; chapters: unknown[] }) {
  return (
    <div className="flex flex-col sm:flex-row gap-3">
      {chapters.length > 0 ? (
        <HardLink
          href={`/book/${slug}/chapter/1`}
          className="inline-flex items-center justify-center px-8 h-12 rounded-[14px] bg-primary text-white font-extrabold text-[15px] tracking-tight transition-all duration-150 hover:-translate-y-px active:translate-y-0"
          style={{ boxShadow: '0 8px 18px rgba(236,75,155,.25)' }}
        >
          Start reading
        </HardLink>
      ) : (
        <span className="inline-flex items-center justify-center px-8 h-12 rounded-[14px] bg-base-300 text-base-content/40 font-extrabold text-[15px] tracking-tight cursor-not-allowed">
          Coming soon
        </span>
      )}
      <ResumeReading bookSlug={slug} totalChapters={book.chapterCount} />
    </div>
  )
}

// ── cinematic: full-bleed cover with bottom gradient overlay ─────────────────
// Cover fills the viewport edge-to-edge (no blur); dark gradient overlaid at bottom; title and CTA sit directly on the image.
// Best for: dark romance / thriller / paranormal

function HeroCinematic({ book, chapters, slug }: { book: Book; chapters: { order: number; title: string }[]; slug: string }) {
  return (
    <>
      <style dangerouslySetInnerHTML={{ __html: `#book-header{transition:background .2s,backdrop-filter .2s,border-color .2s;}#book-header.bh-scrolled{background:color-mix(in oklch,var(--color-base-100) 80%,transparent);backdrop-filter:blur(12px);border-bottom:1px solid color-mix(in oklch,var(--color-base-300) 40%,transparent);}` }} />
      <script dangerouslySetInnerHTML={{ __html: `(function(){var h=document.getElementById('book-header');if(!h)return;function u(){h.classList.toggle('bh-scrolled',window.scrollY>80);}window.addEventListener('scroll',u,{passive:true});u();})();` }} />
      <header id="book-header" className="fixed top-0 left-0 right-0 z-30 h-14">
        <div className="max-w-7xl mx-auto px-4 h-full flex items-center justify-between">
          <Link href="/" className="shrink-0 opacity-90 hover:opacity-100 transition-opacity duration-150" aria-label="Home">
            <img src="/logo.png" alt={SITE_NAME} className="block h-8 w-auto rounded-sm" style={{ filter: 'drop-shadow(0 1px 4px rgba(0,0,0,0.6))' }} />
          </Link>
          <div className="bg-white/15 backdrop-blur-sm rounded-full p-1.5 text-white">
            <ThemeToggle />
          </div>
        </div>
      </header>

      <div className="relative min-h-[75vh] flex items-end">
        <Image src={book.cover} alt={book.title} fill className="object-cover object-center" priority />
        <div className="absolute inset-x-0 top-0 h-28 bg-gradient-to-b from-black/50 to-transparent pointer-events-none" />
        <div className="absolute inset-0 bg-gradient-to-t from-base-100 via-base-100/70 to-transparent pointer-events-none" />
        <div className="relative z-10 w-full max-w-2xl mx-auto px-6 pb-8">
          <div className="flex flex-wrap gap-2 mb-3">
            {book.genres.map(g => (
              <span key={g} className="inline-block rounded-full bg-primary/20 border border-primary/40 px-3 py-0.5 text-xs text-primary font-semibold backdrop-blur-sm">{g}</span>
            ))}
          </div>
          <h1 className="text-4xl sm:text-5xl font-extrabold text-base-content leading-tight tracking-tight mb-1">{book.title}</h1>
          <p className="text-sm text-base-content/60 mb-6">by {book.author}</p>
          <CTABlock book={book} slug={slug} chapters={chapters} />
        </div>
      </div>

      <BelowFold book={book} chapters={chapters} slug={slug} />
    </>
  )
}

// ── gradient: cover displayed in full over a color-extracted gradient background ──
// Primary color from the cover (heroColor field) used as the gradient source; cover shown in full, centered.
// Best for: fantasy / contemporary romance / vivid colorful covers

function HeroGradient({ book, chapters, slug }: { book: Book; chapters: { order: number; title: string }[]; slug: string }) {
  const bg = book.heroColor ?? 'var(--p)'
  return (
    <>
      <style dangerouslySetInnerHTML={{ __html: `#book-header{transition:background .2s,backdrop-filter .2s,border-color .2s;}#book-header.bh-scrolled{background:color-mix(in oklch,var(--color-base-100) 80%,transparent);backdrop-filter:blur(12px);border-bottom:1px solid color-mix(in oklch,var(--color-base-300) 40%,transparent);}` }} />
      <script dangerouslySetInnerHTML={{ __html: `(function(){var h=document.getElementById('book-header');if(!h)return;function u(){h.classList.toggle('bh-scrolled',window.scrollY>80);}window.addEventListener('scroll',u,{passive:true});u();})();` }} />
      <header id="book-header" className="fixed top-0 left-0 right-0 z-30 h-14">
        <div className="max-w-7xl mx-auto px-4 h-full flex items-center justify-between">
          <Link href="/" className="shrink-0 opacity-90 hover:opacity-100 transition-opacity duration-150" aria-label="Home">
            <img src="/logo.png" alt={SITE_NAME} className="block h-8 w-auto rounded-sm" style={{ filter: 'drop-shadow(0 1px 3px rgba(0,0,0,0.4))' }} />
          </Link>
          <div className="bg-base-100/60 backdrop-blur-sm rounded-full p-1.5">
            <ThemeToggle />
          </div>
        </div>
      </header>

      <div className="pt-14">
        <div
          className="py-14 flex flex-col items-center text-center"
          style={{ background: `linear-gradient(160deg, ${bg}33 0%, transparent 70%)` }}
        >
          <div className="relative w-40 sm:w-52 aspect-[2/3] rounded-xl overflow-hidden shadow-2xl mb-8">
            <Image src={book.cover} alt={book.title} fill className="object-cover" priority />
          </div>
          <div className="flex flex-wrap justify-center gap-2 mb-4">
            {book.genres.map(g => (
              <span key={g} className="inline-block rounded-full bg-primary/10 border border-primary/30 px-3 py-0.5 text-xs text-primary font-semibold">{g}</span>
            ))}
          </div>
          <h1 className="text-3xl sm:text-4xl font-extrabold text-base-content leading-tight tracking-tight mb-1 px-6">{book.title}</h1>
          <p className="text-sm text-base-content/50 mb-6">by {book.author}</p>
          <div className="px-6">
            <CTABlock book={book} slug={slug} chapters={chapters} />
          </div>
        </div>
        <BelowFold book={book} chapters={chapters} slug={slug} />
      </div>
    </>
  )
}

// ── atmospheric: blurred cover bg with sharp cover card centered ─────────────
// Blurred, darkened, saturated cover fills the zone behind a crisp floating cover card.
// Best for: literary fiction / clean romance / prose-forward

function HeroAtmospheric({ book, chapters, slug }: { book: Book; chapters: { order: number; title: string }[]; slug: string }) {
  return (
    <>
      <style dangerouslySetInnerHTML={{ __html: `#book-header{transition:background .2s,backdrop-filter .2s,border-color .2s;}#book-header.bh-scrolled{background:color-mix(in oklch,var(--color-base-100) 80%,transparent);backdrop-filter:blur(12px);border-bottom:1px solid color-mix(in oklch,var(--color-base-300) 40%,transparent);}` }} />
      <script dangerouslySetInnerHTML={{ __html: `(function(){var h=document.getElementById('book-header');if(!h)return;function u(){h.classList.toggle('bh-scrolled',window.scrollY>80);}window.addEventListener('scroll',u,{passive:true});u();})();` }} />
      <header id="book-header" className="fixed top-0 left-0 right-0 z-30 h-14">
        <div className="max-w-7xl mx-auto px-4 h-full flex items-center justify-between">
          <Link href="/" className="shrink-0 opacity-90 hover:opacity-100 transition-opacity duration-150" aria-label="Home">
            <img src="/logo.png" alt={SITE_NAME} className="block h-8 w-auto rounded-sm" style={{ filter: 'drop-shadow(0 1px 4px rgba(0,0,0,0.6))' }} />
          </Link>
          <div className="bg-white/15 backdrop-blur-sm rounded-full p-1.5 text-white">
            <ThemeToggle />
          </div>
        </div>
      </header>

      <div className="pt-14">
        <div className="relative overflow-hidden pb-7">
          <img
            src={book.cover} alt="" aria-hidden="true"
            className="absolute pointer-events-none select-none"
            style={{ inset: '-5%', width: '110%', height: '110%', objectFit: 'cover', filter: 'blur(40px) brightness(0.45) saturate(1.4)' }}
          />
          <div className="relative z-10 flex justify-center pt-10">
            <div className="relative w-[200px] rounded-[18px] overflow-hidden" style={{ aspectRatio: '2/3', boxShadow: '0 24px 64px rgba(0,0,0,0.55)' }}>
              <Image src={book.cover} alt={book.title} fill className="object-cover" priority />
            </div>
          </div>
        </div>
        <div className="max-w-2xl mx-auto px-6 pt-6">
          <div className="flex flex-wrap gap-2 mb-4">
            {book.genres.map(g => (
              <span key={g} className="inline-block rounded-full bg-primary/10 border border-primary/30 px-3 py-0.5 text-xs text-primary font-semibold">{g}</span>
            ))}
          </div>
          <h1 className="text-3xl sm:text-4xl font-extrabold text-base-content leading-tight tracking-tight mb-1">{book.title}</h1>
          <p className="text-sm text-base-content/50 mt-1 mb-6">by {book.author}</p>
          <CTABlock book={book} slug={slug} chapters={chapters} />
        </div>
        <BelowFold book={book} chapters={chapters} slug={slug} />
      </div>
    </>
  )
}

// ── page entry: dispatch by heroStyle ────────────────────────────────────────

export default function BookDetailPage({ params }: Props) {
  const book = getBook(params.slug)
  if (!book) notFound()

  const chapters = allChapters
    .filter(ch => ch.bookSlug === params.slug && ch.status === 'published')
    .sort((a, b) => a.order - b.order)
    .map(ch => ({ order: ch.order, title: ch.title }))

  return (
    <div className="min-h-screen bg-base-100">
      {book.heroStyle === 'cinematic'   && <HeroCinematic   book={book} chapters={chapters} slug={params.slug} />}
      {book.heroStyle === 'gradient'    && <HeroGradient    book={book} chapters={chapters} slug={params.slug} />}
      {book.heroStyle === 'atmospheric' && <HeroAtmospheric book={book} chapters={chapters} slug={params.slug} />}
    </div>
  )
}
```

**Notes:**
- `cinematic`: transparent header + top scrim gradient ensures logo legibility over dark cover
- `gradient`: append `33` to `heroColor` (20% alpha hex) as the gradient start; adaptive (not white) icon pill
- `atmospheric`: same header treatment as cinematic; blurred bg = always dark enough for white icons

**Typography hierarchy (shared across all three BelowFold styles):**
- Genre pill: `bg-primary/10 border border-primary/30 text-primary text-xs font-semibold rounded-full px-3 py-0.5`
- Title: `text-3xl sm:text-4xl font-extrabold text-base-content leading-tight tracking-tight` (cinematic uses `text-4xl sm:text-5xl`)
- Author: `text-sm text-base-content/50` (cinematic uses `/60`)
- Synopsis: `text-base text-base-content/75 leading-relaxed`
- CTA: `bg-primary text-white font-extrabold text-[15px] h-12 px-8 rounded-[14px]`
- Chapter count: `text-sm text-base-content/40`

### Chapter List Row
- Height: auto, minimum 48px.
- Content: chapter number, title, optional publish date or word count (right-aligned).
- Volume/arc grouping: sticky or bold section header between groups. `--text-sm`, uppercase, `--muted`.
- Locked chapters (if requested): lock icon, grayed text. Do not show paywall UI by default.

### Chapter Reader — Cover on Chapter 1

When rendering chapter 1 (first chapter of a book), display the book cover at the top of the article, before the chapter title. Subsequent chapters show no cover.

```tsx
{/* chapter 1 only */}
{idx === 0 && (
  <div className="mb-10 flex flex-col items-center gap-4">
    <img
      src={book.cover}
      alt={`${book.title} cover`}
      width={220}
      height={330}
      className="rounded-lg shadow-2xl"
      style={{ aspectRatio: '2/3', objectFit: 'cover' }}
    />
    <div className="text-center">
      <p className="font-display text-2xl italic text-base-content">{book.title}</p>
      <p className="text-sm text-base-content/50 mt-1">{book.author}</p>
    </div>
  </div>
)}
```

`idx` is the zero-based index of the current chapter in the sorted published chapter list. Insert this block inside `<article>`, before the `<header>` that contains the chapter title.

### Reader Settings Sheet

Add only when the brief explicitly asks for font size, line height, or font family controls.

- Trigger: settings icon in reader navigation.
- Delivery: bottom sheet on mobile (slides up from bottom, `max-height: 60vh`), side drawer or inline panel on desktop.
- Content order: theme picker, font size stepper, line height picker, optional font family picker.
- Theme picker: clearly labeled swatches (Light / Dark by default; Light / Sepia / Dark if sepia is enabled). Not just color dots — include a label.
- Font size: stepper with A− / A+ buttons and current size label. Not a slider.
- Dismiss: tap outside, swipe down, or explicit close button.

### Progress Indicator

Add only when the brief explicitly asks for it.

- Style: thin rail at the top or bottom of the reader viewport. 2–3px height. `--accent` color or `--muted`.
- Update: on scroll, tied to scroll percentage within the chapter.
- No numeric percentage label by default — the rail position is sufficient for reading.

## Spacing

- Mobile page padding: 14–18px horizontal for discovery pages.
- Reader horizontal padding: 18–22px (see `reader-ux.md`).
- Card gap: 12–16px in a grid, 0 or 1px divider in a list.
- Card radius: 6–8px. Consistent across the site.
- No nested cards. A card inside a card creates visual noise.
- Book grids: 1 column on mobile (< 640px), 2 columns on tablet (≥ 640px), 3 columns on desktop (≥ 1024px). Text-first list layouts use single column at all breakpoints.

## Imagery

- Use real or plausible cover-like imagery when available.
- If no cover image is provided, generate a CSS placeholder: flat background using `--accent` or a genre-specific swatch, with the book title and author in white text. No complex gradients.
- Do not use abstract hero graphics or AI-generated illustrations as the primary book visual unless the brief explicitly asks.
- Always constrain image display with explicit width/height to prevent layout shift.

## Dark Mode

- Implement via DaisyUI `data-theme` on `<html>` (see `reader-ux.md`).
- Check that all enabled themes pass WCAG AA contrast for body text AND metadata text.
- Cover images should render clearly on both light and dark backgrounds — add a `1px` border or subtle shadow to covers on dark theme if the cover has a white or light edge.

## Animation and Transition

- Use `transition: opacity 150ms, transform 150ms` for chrome show/hide only.
- Do not animate content or cards on scroll-into-view.
- Theme switching: instant, no crossfade.
- Font size change: instant.
- Chapter navigation: a brief `opacity` fade (100–150ms) between chapters is acceptable.
- No `transition` on `color` or `background-color` during theme switch — it creates a slow burn that feels like a bug.

## Safe Area and Notch Handling

```css
.reader-content {
  padding-bottom: calc(56px + env(safe-area-inset-bottom));
}
.bottom-bar {
  padding-bottom: env(safe-area-inset-bottom);
}
```

Always account for iPhone notch and home-indicator clearance on iOS. Test at 390×844 (iPhone 14) and 393×852 (iPhone 15).

## Desktop Adaptation

Desktop must feel like a different layout, not a stretched phone:

- Discovery pages: 3-column responsive grid (`repeat(auto-fill, minmax(280px, 1fr))`), `max-width: 1200px`, centered.
- Book detail: 2-column layout (cover + metadata left, catalog right) at ≥ 768px.
- Reader: centered text column, `max-width: 680px` for Latin prose, `max-width: 620px` for Japanese/Korean. Optional left chapter catalog sidebar at ≥ 1024px.
- Navigation: horizontal nav bar replaces mobile bottom bar. Side panel for settings instead of bottom sheet.
- Mouse hover states must exist on all interactive elements.
- Cursor: `pointer` on all clickable elements.
