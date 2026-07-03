# AdSense / AdX Arbitrage Playbook (Facebook Traffic)

Load this reference whenever the site's purpose is **paid-traffic monetization** — i.e. buying traffic on Facebook (Meta) ads and monetizing reading sessions with AdSense + AdX. This is the default business model for every site built by this skill (see CLAUDE.md ad accounts). Apply it during Phase B1–B6 and at content/cover direction time.

> **One sentence:** the site is a machine that converts a Facebook click (cost) into multiple viewable ad impressions across a reading session (revenue). Everything below exists to widen that margin **without** getting the ad account or the AdSense account banned.

---

## 0. Profit model — what we are actually optimizing

```
Profit per visit = (viewable session RPM)  ×  (pageviews per session) / 1000  −  Facebook CPC  −  overhead
```

The build can move two of the three levers directly:

| Lever | Owner | Where this skill helps |
|---|---|---|
| Facebook CPC in | campaign / creative / targeting | keep landing page approvable (cheap, compliant) — see §1 |
| **Pageviews per session** | the site | chapter model, pagination, cliffhangers, prefetch — see §2 |
| **Viewable session RPM** | the site | ad layout, density, viewability, lazy-load, refresh — see §3 |

A site is only profitable when `session RPM × PV/session` clears the CPC. Two below-average levers kill the margin even if the third is great. Treat layout and pageview depth as **revenue engineering**, not decoration.

---

## 1. Account-survival guardrails (READ FIRST — non-negotiable)

A banned Facebook ad account or a disabled AdSense account ends the business. These rules **override every aesthetic, allure, or CTR suggestion anywhere else in this skill.**

### 1.1 Content safety (Facebook + AdSense both scan the landing page)

Facebook crawls the **destination URL**, not just the ad creative; AdSense scans the whole site. Suggestive / risqué covers and imagery — cleavage, curvy/busty figures, off-shoulder, low-cut, charged proximity — are **allowed and encouraged** for click appeal. The only hard line is outright explicit content:

- **Forbidden (hard ban):** actual nudity (exposed genitals/nipples), sex acts, graphic/pornographic imagery. This both trips the image generator's own filter and, on a live site, risks a **permanent Facebook ad-account ban** and **AdSense disable**.
- **No cloaking:** never serve FB's crawler a tame page and users a racier one — detected, and causes permanent account loss.
- **Allowed:** everything short of explicit — suggestive poses, deep cleavage, figure-forward bodies, wet/rain looks, bed-sheet morning scenes, almost-kiss tension. Push allure hard.

This is the governing register for `story-cover.md` and `cover-allure-elements.md` (§0). Use the safe-wording rules in `cover-allure-elements.md` to get maximum spice without tripping the `gpt-image-2-all` keyword filter.

### 1.2 No cloaking, no bridge/doorway pages

Showing FB's crawler one page and users another, or sending paid traffic to a thin redirect page, is detected and causes **permanent** account loss. The page the ad points to is the page users and crawlers both get.

### 1.3 Inventory-value rules (AdSense)

- Do **not** run more ad area than publisher content. Keep **ad pixels < 30% of content pixels** per screen.
- No low-value / replicated / auto-generated thin pages. **Every paginated screen must carry substantial original prose** (see §2.2) — pagination purely to multiply ad slots is a policy violation.
- Ads must not push content below the fold on mobile (FB low-quality + Google page-experience penalty).

### 1.4 No deceptive placement / no click encouragement

- Ads must never be styleable-mistakable for the "Next →" button, TOC, or nav. Keep a clear visual + spatial gap between any ad and the Next control.
- Never label, arrow, or arrange content to push ad clicks. No "click here", no images adjacent to ads that bait clicks.

### 1.5 Consent + trust pages (AdSense approval + FB quality)

- A Google-certified **CMP / cookie-consent** is required to serve personalized ads in EEA/UK; without it demand drops to non-personalized only.
- Site MUST have: **Privacy Policy, Terms, About, Contact** (and a Cookie notice). AdSense approval fails and FB flags "low quality" without them. Link them in the footer of every page.

---

## 2. Pageviews per session — the #1 arbitrage lever

The chapter model already multiplies pageviews. Push it harder (within §1.3):

### 2.1 Forward momentum (already core to this skill)

- Cliffhanger chapter endings (Zeigarnik effect) — see `story-long-write.md` pacing. The unresolved loop is what makes the next pageview involuntary.
- Forward-only nav (no Previous), vivid Next button — see `reader-ux.md`.
- **Full-page navigation on chapter change** (`window.location.href`, not SPA) so AdSense/AdX reinitialize and count a fresh pageview with fresh impressions — already required in `reader-ux.md`.
- Prefetch the next chapter at ~80% scroll so the next pageview feels instant.

### 2.2 In-chapter pagination (optional, high-impact — use only if it stays compliant)

Split a long chapter into sequential **pages of ~600–900 words each**, each a real route (`/book/{slug}/chapter/{n}/p/{k}`) with a full-reload "Continue reading →" control.

- Each page is a fresh pageview → fresh ad impressions, multiplying RPM-per-chapter.
- **Compliance gate (§1.3):** every page must hold substantial prose (≥ ~500 words of real content), keep ad-area < 30% of content, and never strand the reader on a near-empty page. Pagination that creates thin pages is a ban--worthy inventory-value violation — when in doubt, fewer/longer pages.
- Keep the same cliffhanger discipline at page breaks, not just chapter breaks.

### 2.3 End-of-content continuation

- End of chapter → prominent Next.
- End of book → "Continue with {next book}" / related-title cards to restart the loop instead of dead-ending.

**Target: ≥ 2.5–4 pageviews per session.** Below ~2 the arbitrage rarely clears CPC.

---

## 3. Ad layout, density & viewability — the RPM lever

Map the CLAUDE.md inventory (AdX `q1–q5` via `AdSlot`, AdSense slots 1–5 via `AdsenseSlot`) onto these positions. Layout structure matters more than raw ad count — moving a unit to a better slot can double its CPM; adding a 6th+ unit usually cannibalizes the others.

### 3.1 Placement map

| Position | Viewability | Notes |
|---|---|---|
| Pre-content (above all text, just below header) | **< 30%** | **Avoid.** Paid-traffic users start scrolling immediately — this unit exits the viewport before the 1-second viewability threshold. Moving this slot into content can double its Active View score. |
| After `contentParts[0]` (~20% into content) | 70–90% | **First slot.** Reader has invested ~2 min and is still engaged. Pass `priority` to `AdsenseSlot`; AdX uses normal `AdSlot` (singleRequest). |
| In-content, every N paragraphs after the first break | 65–85% | the workhorse — inside the natural reading path |
| End-of-chapter (before the inline Next CTA) | high | catches the "decide to continue" pause; keep clear gap from Next button (§1.4) |
| Mobile sticky **anchor** (bottom, `position: fixed`) | very high | **AdX only** (`StickyAnchorAd` / q4). AdSense policy prohibits fixed-position manual units — omit for AdSense sites. One anchor; reliably viewable & refreshable. |
| Desktop sticky **side-rail** | high | uses empty side space; never a static sidebar (low viewability) |

### 3.1.1 Per-page loading rule (AdSense only)

**Rule: first ad slot on every page gets `priority`; all others lazy-load by default.**

| Page | First slot (priority) | Remaining slots (lazy) |
|------|-----------------------|------------------------|
| Home / book list | first `<AdsenseSlot>` after the hero section | all others |
| Book detail | first `<AdsenseSlot>` above the chapter TOC | all others |
| Chapter reader | first `<AdsenseSlot>` **after `contentParts[0]`** (not above all content — pre-content viewability is < 30% on paid traffic) | all others |

```tsx
<AdsenseSlot slot="..." priority />   {/* immediate — no IntersectionObserver */}
<AdsenseSlot slot="..." />            {/* lazy — 150px rootMargin trigger */}
```

**AdX sites**: do NOT add lazy loading to `AdSlot`. GPT's `singleRequest` batches all slots in one HTTP call automatically; delaying `display()` breaks impression counting.

### 3.2 Density ceiling (compliance + diminishing returns)

- **≤ 3–4 ad units per 1,000 words** of chapter content.
- **Ad pixels < 30% of content pixels** per screen (FB + AdSense inventory-value).
- RPM typically peaks around 5 units; beyond that each added unit adds ~2–4% and erodes engagement + page-experience. Cutting the weakest slot often **raises** total RPM.
- **Recommended dynamic layout** (measure chapter word count before rendering ads):
  - All chapters: q1 (after part[0]) + q2 (after part[1]) + q5 (fluid, bottom) + q4 sticky anchor — **minimum 3 ads always**
  - > 2,000 words with ≥ 3 paragraphs: q1 + q2 + q3 + q5 (all in-content) + q4 sticky anchor
  - Avoid a fourth mid-content unit; it sits too close to q5 and adds clutter without meaningful RPM lift.

### 3.3 CLS protection (Core Web Vitals = cheaper FB traffic + SEO)

- Every ad slot wrapper reserves explicit `min-height` / `aspect-ratio` matching the largest expected creative **before** it loads. (CLAUDE.md `AdSlot` min sizes already do this for q1–q4; keep it.)
- A jumping layout when an ad loads tanks CLS, raises bounce, and raises effective CPC.

### 3.4 Viewability & refresh

- Target **viewability ≥ 70%** (advertisers bid markedly higher; 40%→70% ≈ +30% RPM). Don't chase 95% at the cost of fill rate.
- Refresh ads only when the unit is **in the viewport** and after **≥ 30s active dwell**. Sticky/anchor units are the safe place to refresh because they stay viewable.
- Never refresh on a hidden tab or an off-screen unit.

**Critical: first ad slot placement rule.**
The single biggest viewability lever on chapter pages is WHERE the first ad slot (q1 for AdX / slot 1 for AdSense) appears. Two failure modes:

1. **Pre-content placement (worst):** q1 above all prose → user starts scrolling immediately, ad exits viewport in < 1s. Active View score < 30%. This was the historical default; do not repeat it.
2. **Deep-content placement (bad):** first ad at 50%+ of chapter → only readers who finish more than half ever see it. Active View 30–50% on paid traffic.

Rule: place the **first** ad after `contentParts[0]` — the first ~20% of paragraphs (min 3, max 5 paragraphs). At this depth the reader has invested ~2 minutes and is still engaged — first-ad viewability should reach 70–90% vs < 30% pre-content.

AdX layout (2-part chapters): `part[0] → q1 → part[1] → q2 → q5(fluid)` + q4 sticky anchor always visible.
AdX layout (3-part chapters): `part[0] → q1 → part[1] → q2 → part[2] → q3 → q5(fluid)` + q4 sticky anchor.

AdSense layout (2-part): `part[0] → slot1(priority) → part[1] → slot2`.
AdSense layout (3-part): `part[0] → slot1(priority) → part[1] → slot2 → part[2]`.

Diagnostic signal: if AdX viewability is below 60% and match rate is ≥ 95%, the problem is almost always first-slot placement depth, not fill. Fix the slot position before investigating any other cause.

---

## 4. Facebook side — tracking & landing

### 4.1 Tracking

- **Meta Pixel + Conversions API (CAPI)**: Pixel alone loses signal to iOS/ad-blockers; CAPI (server-side) recovers it. Run both, deduplicated by event ID.
- Events to fire: `PageView`, `ViewContent` (chapter open), scroll-depth (e.g. 50/90%), `NextChapter` / page-advance, and a custom "engaged session" (≥ N pageviews or ≥ M seconds) as the optimization signal.
- Optimize the FB campaign toward the **engaged/value event**, not raw landing PageView — that is what trains delivery toward profitable readers.
- UTM-tag every campaign; keep `campaign → landing chapter` mapping for ROAS attribution.

### 4.2 Landing page choice

- Land on a **strong hook chapter** (often chapter 1, or the highest-tension opening) — not the home page. The faster a reader is inside prose, the more pageviews follow.
- Landing page must: LCP < 2.5s on mid-range Android/4G, have footer trust links (§1.5), no pre-content interstitial, no deceptive pop-ups (FB "disruptive" + Google Better-Ads). A bottom anchor ad is fine; a full-screen interstitial before content is not.

---

## 5. Required trust pages (build in B4)

Add these routes/pages to every monetized site — they are gating requirements, not optional:

- `/privacy` — Privacy Policy (mentions cookies, AdSense/Google & third-party vendors, Meta Pixel, data use)
- `/terms` — Terms of Use
- `/about` — About (a real description of the site/brand)
- `/contact` — Contact (a reachable address — either a dedicated email or a reference to the domain WHOIS contact for DMCA/content requests; a page must exist)
- Cookie-consent banner wired to a Google-certified CMP
- Footer on every page links all of the above.

Without these, AdSense approval fails and Facebook flags the domain as low quality.

---

## 6. KPIs & iteration

Track and optimize:

| Metric | Target / note |
|---|---|
| Session RPM (viewable) | the headline revenue number |
| Pageviews / session | ≥ 2.5–4 |
| Ad viewability | ≥ 70% |
| CLS / LCP | CLS < 0.1, LCP < 2.5s (cheaper FB delivery + SEO) |
| Facebook CPC | the cost side — drive down via creative/targeting |
| **ROAS** = ad revenue ÷ FB spend | must be > 1 with margin; the whole game |

- Change layout via **50/50 A/B** (AdSense Experiments or a feature flag), run **≥ 14–21 days** to cover weekly + seasonal cycles, roll out only if RPM lift > 5% **with no engagement degradation**.
- Re-test placements every 6–12 months — demand and behavior drift; set-and-forget loses 8–15% RPM over two years.

---

## 7. Build-time checklist (wire into B4–B6)

- [ ] Covers, hero images, titles, synopses contain no outright explicit/pornographic content (§1.1); suggestive allure is fine.
- [ ] Privacy / Terms / About / Contact pages exist and are footer-linked on every route (§5).
- [ ] Google-certified CMP / cookie consent wired (§1.5).
- [ ] Every ad slot reserves explicit size (no CLS) (§3.3).
- [ ] AdSense units lazy-load via `AdsenseSlot` with 150px `rootMargin`; above-fold AdSense unit passes `priority` to load immediately; every slot reserves explicit size (no CLS) (§3.3, §8.6).
- [ ] Ad components from §8.6 are used unchanged; never revert to mount-time `display()`/`push({})` for all slots.
- [ ] Ad density ≤ 3–4 / 1,000 words and ad-pixels < 30% of content (§1.3, §3.2).
- [ ] No ad is mistakable for the Next/TOC control; clear gap maintained (§1.4).
- [ ] Chapter change does a full reload so ads reinit and a fresh pageview counts (§2.1).
- [ ] (If used) in-chapter pagination keeps each page content-rich and compliant (§2.2).
- [ ] *(Optional — add when running FB campaigns)* Meta Pixel installed (§8.1).
- [ ] Landing chapter LCP < 2.5s, no interstitial before content (§4.2).
- [ ] `og:image` set on all chapter and book detail pages; `metadataBase` set in root layout (§4 impl).
- [ ] End-of-last-chapter shows cross-book recommendation grid, not a dead-end link (§2.3 impl).
- [ ] `<link rel="prefetch">` added for next chapter URL on every chapter page (§2.1 impl).

---

## 8. Implementation patterns (Next.js App Router + static export)

### 8.1 Meta Pixel — `layout.tsx` *(add when running FB campaigns)*

Fires `PageView` on every full-reload chapter navigation automatically. Only add this when you have a real Pixel ID — do not add placeholder env vars to the build.

Hardcode `metadataBase` with the real domain (no env var needed):

```tsx
export const metadata: Metadata = {
  metadataBase: new URL('https://yoursite.com'),  // hardcode — no env var
  // ...
}
```

Then add the Pixel script in `<head>` when the campaign goes live:

```tsx
<script
  dangerouslySetInnerHTML={{
    __html: `!function(f,b,e,v,n,t,s){if(f.fbq)return;n=f.fbq=function(){n.callMethod?n.callMethod.apply(n,arguments):n.queue.push(arguments)};if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';n.queue=[];t=b.createElement(e);t.async=!0;t.src=v;s=b.getElementsByTagName(e)[0];s.parentNode.insertBefore(t,s)}(window,document,'script','https://connect.facebook.net/en_US/fbevents.js');fbq('init','YOUR_PIXEL_ID');fbq('track','PageView');`,
  }}
/>

### 8.2 OG image — three layers required

Set `metadataBase` once in `layout.tsx` — all relative OG image paths in child pages resolve to absolute automatically. No `siteUrl` env var needed.

**Layer 1 — Homepage (`layout.tsx`):** logo as fallback for any page without a specific OG image:
```ts
metadataBase: new URL('https://yoursite.com'),
openGraph: {
  siteName: 'Your Site Name',
  type: 'website',
  images: [{ url: 'https://yoursite.com/logo.png', width: 512, height: 512, alt: 'Your Site Name' }],
},
```

**Layer 2 — Book detail page (`book/[slug]/page.tsx`):**
```ts
openGraph: {
  title: book.title,
  description: book.description,
  images: [{ url: book.cover, width: 848, height: 1280, alt: book.title }],  // relative path OK, metadataBase resolves it
  type: 'book',
  siteName: 'Your Site Name',
},
twitter: { card: 'summary_large_image' },
```

**Layer 3 — Chapter page (`book/[slug]/chapter/[n]/page.tsx`):**
```ts
openGraph: {
  title: `${chapter.title} — ${book.title}`,
  description: `Read Chapter ${n} of ${book.title} by ${book.author}.`,
  images: [{ url: book.cover, width: 848, height: 1280, alt: book.title }],  // same cover as book page
  type: 'article',
  siteName: 'Your Site Name',
},
twitter: { card: 'summary_large_image' },
```

The book cover (portrait 2:3, 848×1280) doubles as the FB link preview for book and chapter pages — no separate OG asset needed. Chapter page may omit `images` and fall back to the layout logo, but setting `book.cover` is preferred. See `references/performance.md` §4 for the full requirements table.

### 8.3 Next-chapter prefetch — chapter `page.tsx`

```tsx
return (
  <>
    {next && <link rel="prefetch" href={`/book/${slug}/chapter/${next.order}`} />}
    <div className="min-h-screen bg-base-100">
      ...
    </div>
  </>
)
```

Next.js App Router hoists `<link rel="prefetch">` from Server Components into `<head>` automatically.

### 8.4 Cross-book recommendation at end of book

Replace the dead-end "Back to book page" with a 3-book grid. Import `books` (already used in `generateStaticParams`) and filter out the current book:

```tsx
{!next && (
  <div className="my-10 border border-base-300 rounded-2xl px-6 py-10">
    <p className="text-base font-semibold text-base-content text-center mb-1">
      You&apos;ve finished <em>{book.title}</em>.
    </p>
    <p className="text-xs text-base-content/40 uppercase tracking-widest text-center mb-8">Keep reading</p>
    <div className="grid grid-cols-3 gap-4">
      {books.filter(b => b.slug !== slug).slice(0, 3).map(b => (
        <HardLink key={b.slug} href={`/book/${b.slug}/chapter/1`} className="flex flex-col items-center gap-2 group">
          <div className="w-full rounded-lg overflow-hidden shadow-md" style={{ aspectRatio: '2/3' }}>
            <img src={b.cover} alt={b.title} className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300" />
          </div>
          <span className="text-[11px] font-semibold text-center text-base-content group-hover:text-primary transition-colors line-clamp-2 leading-tight">
            {b.title}
          </span>
        </HardLink>
      ))}
    </div>
  </div>
)}
```

Link directly to chapter 1 of each book — not the book detail page — to minimize the click-to-reading funnel.

### 8.5 Trust pages — minimal viable set

Each trust page follows the same shell: site header `<Link href="/">← Site Name</Link>` + content + footer with trust nav links. Footer pattern:

```tsx
<footer className="border-t border-base-300 mt-16">
  <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col sm:flex-row items-center justify-between gap-3">
    <p className="text-[13px] text-base-content/40">&copy; {new Date().getFullYear()} Site Name</p>
    <nav className="flex gap-5">
      <Link href="/about" className="text-[13px] text-base-content/40 hover:text-base-content/70 transition-colors">About</Link>
      <Link href="/privacy" className="text-[13px] text-base-content/40 hover:text-base-content/70 transition-colors">Privacy</Link>
      <Link href="/terms" className="text-[13px] text-base-content/40 hover:text-base-content/70 transition-colors">Terms</Link>
      <Link href="/contact" className="text-[13px] text-base-content/40 hover:text-base-content/70 transition-colors">Contact</Link>
    </nav>
  </div>
</footer>
```

Privacy Policy must explicitly name: the ad network (Google AdSense or Google Ad Manager), cookies, and user rights. Add Meta Pixel mention only if Pixel is actually installed. Terms must state: fiction content, 18+ audience, no reproduction. Contact page must exist and be reachable — a dedicated email is fine, but for independently-operated sites a note directing DMCA requests to the domain WHOIS contact is acceptable.

### 8.6 Ad components

#### AdX / GAM — `AdSlot.tsx`

Mount immediately on render — no IntersectionObserver. GPT's `singleRequest` batches all requests in one call automatically.

```tsx
'use client'

import { useEffect } from 'react'

type Size = [number, number] | 'fluid'

type Props = {
  path: string
  id: string
  sizes: Size[]
  className?: string
}

declare global {
  interface Window {
    // eslint-disable-next-line @typescript-eslint/no-explicit-any
    googletag: any
  }
}

export default function AdSlot({ path, id, sizes, className = '' }: Props) {
  useEffect(() => {
    window.googletag = window.googletag || { cmd: [] }
    window.googletag.cmd.push(() => {
      const slot = window.googletag.defineSlot(path, sizes, id)
      if (!slot) return
      slot.addService(window.googletag.pubads())
      window.googletag.display(id)
    })
    return () => {
      window.googletag?.cmd.push(() => {
        const slot = window.googletag.pubads().getSlots()
          .find((s: { getSlotElementId: () => string }) => s.getSlotElementId() === id)
        if (slot) window.googletag.destroySlots([slot])
      })
    }
  }, [path, id]) // eslint-disable-line react-hooks/exhaustive-deps

  const isFluid = sizes.includes('fluid')
  return (
    <div className={`flex justify-center my-6 ${className}`}>
      <div id={id} style={isFluid ? undefined : { minWidth: 250, minHeight: 250 }} />
    </div>
  )
}
```

Placement mapping — always minimum 3 ads (q1 + q2 + q5), add q3 for long chapters:

```tsx
function wordCount(text: string): number {
  return text.split(/\s+/).filter(Boolean).length
}

// q2 break at ~20% of paragraphs (min 3, max 5) — not 33% or 50%.
// Rationale: Facebook readers often bounce within 2 minutes. Placing q2 after
// only 3–5 paragraphs (~300–400 words) keeps it in the high-engagement window
// where viewability is 70–90%. At 50%, q2 is only seen by readers who finish
// more than half the chapter — a minority of paid-traffic visitors.
// Validated: AU viewability went from 53% → target 70%+ after this change.
function splitContent(content: string): string[] {
  const paras = content.split(/\n{2,}/).filter(p => p.trim())
  const words = wordCount(content)
  // AdSense only: skip ad injection on very short pieces
  if (words < 1000) return [content]
  // Early break: first 20% of paragraphs, clamped to [3, 5]
  const earlyBreak = Math.min(5, Math.max(3, Math.ceil(paras.length * 0.2)))
  if (paras.length <= earlyBreak) return [content]
  if (words >= 2000 && paras.length >= earlyBreak + 4) {
    // 3-part: q2 early, q3 at ~60% of content
    const midBreak = Math.floor((earlyBreak + paras.length) / 2)
    return [
      paras.slice(0, earlyBreak).join('\n\n'),
      paras.slice(earlyBreak, midBreak).join('\n\n'),
      paras.slice(midBreak).join('\n\n'),
    ].filter(Boolean)
  }
  // 2-part: q2 early
  return [
    paras.slice(0, earlyBreak).join('\n\n'),
    paras.slice(earlyBreak).join('\n\n'),
  ]
}

// render — q1 goes AFTER part[0], not before all content
// q4 StickyAnchorAd is mounted at the page level (outside <main>), always visible
{contentParts.length >= 3 ? (
  <>
    <div className="prose-reader">{contentParts[0]}</div>
    <AdSlot path="/23294357175/q1" id="div-gpt-ad-1782711338284-0" sizes={[[250,250],[300,250],[336,280]]} />
    <div className="prose-reader">{contentParts[1]}</div>
    <AdSlot path="/23294357175/q2" id="div-gpt-ad-1782711428179-0" sizes={[[250,250],[336,280],[300,250]]} />
    <div className="prose-reader">{contentParts[2]}</div>
    <AdSlot path="/23294357175/q3" id="div-gpt-ad-1782711490041-0" sizes={[[250,250],[336,280],[300,250]]} />
  </>
) : (
  <>
    <div className="prose-reader">{contentParts[0]}</div>
    <AdSlot path="/23294357175/q1" id="div-gpt-ad-1782711338284-0" sizes={[[250,250],[300,250],[336,280]]} />
    <div className="prose-reader">{contentParts[1]}</div>
    <AdSlot path="/23294357175/q2" id="div-gpt-ad-1782711428179-0" sizes={[[250,250],[336,280],[300,250]]} />
  </>
)}

<AdSlot path="/23294357175/q5" id="div-gpt-ad-1782711618925-0" sizes={['fluid']} />

{/* StickyAnchorAd (q4) — mount outside <main> so it overlays the bottom viewport */}
{/* See StickyAnchorAd.tsx; chapter <main> must use className="pb-sticky-ad" */}
{/* (calc(280px + env(safe-area-inset-bottom))) to clear the ad */}
```

#### AdX sticky anchor — `StickyAnchorAd.tsx` (AdX sites only)

Mount outside `<main>` (sibling in the page return, before `<div className="min-h-screen">`). Uses q4 slot. Includes a dismiss button. `<main>` must use `className="pb-sticky-ad"` to prevent content being hidden behind it.

```tsx
'use client'

import { useEffect, useRef, useState } from 'react'

declare global {
  interface Window { googletag: any }
}

export default function StickyAnchorAd() {
  const [dismissed, setDismissed] = useState(false)
  const defined = useRef(false)

  useEffect(() => {
    if (defined.current) return
    defined.current = true
    window.googletag = window.googletag || { cmd: [] }
    window.googletag.cmd.push(() => {
      const slot = window.googletag.defineSlot(
        '/23294357175/q4',
        [[336, 280], [250, 250], [300, 250]],
        'div-gpt-ad-1782711562651-0'
      )
      if (!slot) return
      slot.addService(window.googletag.pubads())
      window.googletag.display('div-gpt-ad-1782711562651-0')
    })
    return () => {
      window.googletag?.cmd.push(() => {
        const slots = window.googletag.pubads().getSlots()
        const slot = slots.find(
          (s: { getSlotElementId: () => string }) =>
            s.getSlotElementId() === 'div-gpt-ad-1782711562651-0'
        )
        if (slot) window.googletag.destroySlots([slot])
      })
    }
  }, [])

  if (dismissed) return null

  return (
    <div
      className="fixed bottom-0 left-0 right-0 z-40 flex justify-center bg-base-100/95 backdrop-blur-sm border-t border-base-300"
      style={{ paddingBottom: 'env(safe-area-inset-bottom)' }}
    >
      <div className="relative py-2">
        <div id="div-gpt-ad-1782711562651-0" style={{ minWidth: 250, minHeight: 250 }} />
        <button
          onClick={() => setDismissed(true)}
          className="absolute -top-1 -right-1 w-5 h-5 rounded-full bg-base-200 text-base-content/60 text-xs flex items-center justify-center hover:bg-base-300 leading-none"
          aria-label="Close ad"
        >
          ×
        </button>
      </div>
    </div>
  )
}
```

**Do NOT add a similar fixed-position component for AdSense sites.** Google AdSense policy prohibits placing manual `<ins class="adsbygoogle">` units in fixed/sticky/floating containers. AdSense anchor ads must use Google's Auto Ads system, not manual slots.

#### AdSense — `AdsenseSlot.tsx`

```tsx
'use client'

import { useEffect, useRef, useState } from 'react'

declare global {
  interface Window {
    adsbygoogle: unknown[]
  }
}

type Props = {
  slot: string
  priority?: boolean
  className?: string
}

export default function AdsenseSlot({ slot, priority = false, className = '' }: Props) {
  const [shouldLoad, setShouldLoad] = useState(priority)
  const insRef = useRef<HTMLModElement>(null)

  // Load the ad when it comes within 150px of the viewport.
  useEffect(() => {
    if (shouldLoad) return
    const el = insRef.current
    if (!el || typeof IntersectionObserver === 'undefined') {
      setShouldLoad(true)
      return
    }
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          setShouldLoad(true)
          observer.disconnect()
        }
      },
      { rootMargin: '150px' }
    )
    observer.observe(el)
    return () => observer.disconnect()
  }, [])

  useEffect(() => {
    if (!shouldLoad) return
    try {
      window.adsbygoogle = window.adsbygoogle || []
      window.adsbygoogle.push({})
    } catch {
      // blocked by ad blocker
    }
  }, [shouldLoad, slot])

  return (
    <div className={`flex justify-center my-6 overflow-hidden ${className}`}>
      <ins
        ref={insRef}
        className="adsbygoogle"
        style={{ display: 'block' }}
        data-ad-client="ca-pub-5417273853283747"
        data-ad-slot={slot}
        data-ad-format="auto"
        data-full-width-responsive="true"
      />
    </div>
  )
}
```

### 8.7 Layout viewport and empty-div collapse

Export an explicit viewport in `app/layout.tsx` so mobile ad sizing and viewability measurement are correct:

```tsx
import type { Metadata, Viewport } from 'next'

export const viewport: Viewport = {
  width: 'device-width',
  initialScale: 1,
}
```

For AdX sites, use `setConfig` to collapse unfilled slots (no deprecated `pubads()` calls):

```tsx
<script
  dangerouslySetInnerHTML={{
    __html: `window.googletag=window.googletag||{cmd:[]};googletag.cmd.push(function(){googletag.setConfig({singleRequest:true,collapseDiv:true});googletag.enableServices();});`,
  }}
/>
```

### 8.8 Refresh rule (optional)

Only refresh ads when the unit is in the viewport and the tab has been active for ≥ 30 seconds. Sticky/anchor units are the safest refresh surface because they remain viewable. Do not refresh below-the-fold units.
