# Reader UX

## Reading First Principles

The reader is the product. Optimize for long sessions, low fatigue, and fast return to the current chapter. Every interaction in the reader must serve the reading act or stay out of the way.

**Ease of reading over visual precision.** If a choice makes prose harder to track, it is wrong regardless of how it looks in a screenshot. The chapter page must feel as effortless to read as a well-formatted paperback — generous body size, ample line-height, neutral background, no chrome competing for attention.

## Required Reader Controls

The default reader ships with a focused set of controls. Add font size, density, or reading progress indicator only when the brief explicitly asks for them. Table of contents is always required.

| Control | Requirement | Notes |
| --- | --- | --- |
| Next chapter | Required | Inline CTA in the content flow at the end of chapter text (see **End-of-Chapter Navigation** below). Also accessible via the top header's TOC drawer. No Previous button — TOC handles backward navigation. |
| Table of contents | Required | List icon (≡) in the top header right slot — opens a bottom-sheet drawer with the chapter list. |
| Book cover header | Required | Small cover thumbnail in the reader header above the chapter title; omit if no cover image exists |
| End-of-chapter prompt | Required | Inline "Next chapter →" CTA at the very bottom of chapter text. Use **`my-10`** (symmetric 40px) margin — never asymmetric `mt-16 mb-6`. |
| Keyboard prev/next | Required on desktop | `←` / `→` arrow keys |
| Error / empty states | Required | See Error States section |
| Dark mode toggle | Required | DaisyUI `data-theme` swap; persists in `localStorage` |
| Resume last chapter | Required | Store last visited chapter slug in `localStorage`; restore on home/detail page |
| Tap zones (mobile) | Recommended | Left/right 15% tap zones for prev/next |

## Top Reader Header

Always fixed (`position: fixed; top: 0`), `height: 56px`, `bg-base-100/95 backdrop-blur-sm`, `border-b border-base-300`.

**Layout — left: site logo | center: book + chapter title | right: TOC icon + theme toggle**

```
[ site logo ]   [ Book Title (xs, muted)    ]   [ ≡ ]  [ ☽ ]
                [ Ch. 1 - Chapter Title (sm)]
```

- **Left slot — site logo** (`h-8 w-auto`, links to `/`): the site logo links to the home page. Never a back arrow (`<`), never the book cover thumbnail. The logo anchors the reader in the site brand across all chapters.
- **Center slot** — two-line text block: book title in `11px` muted, chapter title in `13px` medium. Truncate both.
- **Right slot** — two icon buttons (TOC list-icon, dark mode toggle). Use `btn btn-ghost btn-sm btn-circle`.

No back arrow (`<`) anywhere in the header. The site logo IS the back link to home (`/`).

Add `padding-top: 56px` (or `pt-14`) to the chapter content wrapper so it clears the fixed header.

---

## End-of-Chapter Navigation

**No fixed bottom navigation bar.** The bottom viewport is reserved for the sticky anchor ad (AdX sites use `StickyAnchorAd` / q4; AdSense sites leave the bottom clear per policy). Navigation lives in two places:

1. **Top header** — right slot has the TOC list icon (≡) that opens the chapter-list drawer. This is the primary TOC entry point.
2. **Content flow** — inline "Next chapter →" CTA and cross-book recommendation grid appear at the end of chapter text, in the natural scroll path.

```tsx
{/* Inline next-chapter CTA — at bottom of prose */}
{next && (
  <div className="my-10 border border-base-300 rounded-2xl text-center px-8 py-10">
    <p className="text-xs text-base-content/40 uppercase tracking-widest mb-5">Continue reading</p>
    <HardLink
      href={`/book/${slug}/chapter/${next.order}`}
      className="inline-flex items-center gap-2 text-xl font-bold text-primary hover:text-primary/80 transition-colors"
    >
      Next chapter →
    </HardLink>
  </div>
)}
```

No "Previous" button anywhere. Fiction reading is a forward-only experience — the TOC handles backward navigation.

**Bottom padding — account for sticky anchor ad (AdX only):**

AdX chapter pages must add enough bottom padding so the last content line is not hidden behind the sticky q4 ad (min 250px height):

```css
/* AdX sites */
.pb-sticky-ad {
  padding-bottom: calc(280px + env(safe-area-inset-bottom));
}

/* AdSense sites — no sticky ad, just safe-area clearance */
.pb-safe-reader {
  padding-bottom: calc(24px + env(safe-area-inset-bottom));
}
```

**Next button — psychology-driven design:**

The "Next chapter →" inline CTA must trigger an almost involuntary desire to tap. Use a vivid, saturated warm color — hot pink (`#E91E8C` range), coral, or electric magenta when rendered as a full button. Never use the site's calm brand color here; this button needs contrast-driven urgency.

Why this works: bright saturated warm colors activate dopamine anticipation. Combined with the unresolved story tension (Zeigarnik effect — the reader's brain cannot rest on an open narrative loop), the button becomes the path of least resistance. The reader taps before consciously deciding to.

**TOC panel — DaisyUI 5 modal bottom sheet:**

Bottom sheet is the right choice for mobile fiction reading: thumb-friendly, native feel, fast in/out. Right-side drawer is not suitable — requires reaching the screen edge and covers more reading context.

Use `<dialog>` with `className="modal modal-bottom"` (DaisyUI 5). Open with `dialogRef.current.showModal()`, close with `dialogRef.current.close()`. Inside: `modal-box rounded-t-3xl rounded-b-none`, max-height `72vh`. Current chapter: `border-l-2 border-primary text-primary bg-primary/5 font-semibold`. Non-current: `border-l-2 border-transparent text-base-content/65`. Auto-scroll to current chapter on open (`scrollIntoView` with 50ms delay). Close on backdrop click (`e.target === dialogRef.current`).

**Quality gate failure if not met:**

- Next button uses a muted, dark, or low-saturation color.
- Next button is same width or narrower than TOC.
- "Previous" button appears anywhere in the reader nav.
- On mobile ≤ 640px: maintain 60px height minimum.

## Cross-Book Recommendation Grid

Show a 3-book recommendation grid on **every chapter** — the moment a reader finishes any chapter is the highest-intent moment for cross-promotion. Render it after the next-chapter nav on mid-book chapters, and after the "You've finished" message on the last chapter.

**Mid-book chapters** (`next` exists) — insert after the next-chapter nav block:

```tsx
{/* Cross-book recommendations */}
{next && (
  <div className="mt-10 pt-8 border-t border-base-300">
    <p className="text-xs text-base-content/40 uppercase tracking-widest text-center mb-6">You might also like</p>
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

**Last chapter** (`!next`) — use a more conclusive heading:

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

Rules:
- Links go to `/book/${b.slug}/chapter/1` so the reader starts immediately; arbitrage flows convert better when the next click lands in the reader, not on a detail page.
- Filter out the current book (`b.slug !== slug`). Take first 3 from remaining.
- **Use `HardLink` for cross-book grid links.** The chapter reader carries in-content ad slots; a client-side `<Link>` transition would skip ad reinitialization and reduce impressions. Only pages that carry no ad slots may use `next/link` for internal navigation.
- For Spanish sites, use "También te puede gustar" instead of "You might also like".

## Optional Enhancements

Add only when explicitly requested:

| Control | Notes |
| --- | --- |
| Font size | ≥ 4 steps (e.g. 14/16/18/20px) |
| Line height / density | ≥ 2 options: "Compact" and "Comfortable" |
| Theme | Light / Sepia / Dark via DaisyUI themes |
| Reading progress | Visible but not distracting |
| Resume scroll position | Per-chapter scroll restoration |
| Immersive mode | Chrome-hidden reading mode |

## Never Add Without Explicit Request

These features add UI complexity and distract from reading. Omit by default:

- Favorites / bookmarks
- Social sharing buttons
- Comment sections
- User accounts / login
- Bookshelf or reading list management
- Search
- Ranking or recommendation widgets
- Payment or chapter-lock UI

## Default Typography

Use conservative defaults. Readers should not need to adjust settings to find a comfortable starting point.

- **Font:** system sans-serif stack only. Set `--font-reader` in `:root` to `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif`. Do not use `Georgia`/serif stacks for prose — they add perceived reading friction for social traffic audiences. Do not load web fonts from any external source. `next/font/google` requires network access to Google Fonts at build time and will fail on mainland China developer machines; it also degrades performance for users in regions where Google is blocked. If a custom display font is essential, self-host it via `@fontsource` — never depend on Google Fonts CDN at build or runtime.
- **Prose size:** `19px` mobile → `20px` sm+.
- **Line height:** `1.8` mobile → `1.85` sm+.
- **Paragraph spacing:** `margin-bottom: 1.1em`.

```css
.prose-reader { font-size: 19px; line-height: 1.8; }
@media (min-width: 640px) { .prose-reader { font-size: 20px; line-height: 1.85; } }
```
- Latin line-height: 1.8–1.85 (compact but trackable — optimised for social traffic landing pages).
- Japanese/Korean line-height: 1.75–1.9.
- Paragraph spacing: `1em` top margin between paragraphs. Enough to separate beats without the double-spaced blog-style gap.
- Max line length: 32–38em for Latin prose; narrower for CJK (28–34em) to avoid very long line scanning.

## Layout

- Mobile horizontal padding: 18–22px.
- The sticky anchor ad (AdX only, `position: fixed; bottom: 0`) must not cover body text — use `.pb-sticky-ad` on the `<main>` wrapper. AdSense sites use `.pb-safe-reader`.
- Chapter title: visible at the top but not oversized. `--text-xl` or smaller.
- Reader background: off-white, paper tone, or deep neutral dark. Never pure `#fff` or `#000` in any theme.
- Do not use full-bleed background images behind prose.

## Immersive Mode

If implementing an immersive (chrome-hidden) reading mode:
- Trigger: tap the center of the screen, or scroll past a threshold.
- On hide: animate the top bar and bottom bar out smoothly (200ms, `transform: translateY`).
- On show: single tap or scroll-up restores chrome.
- Progress indicator may remain visible in immersive mode as a thin rail, not a full bar.
- Never hide previous/next controls entirely in immersive mode — they must be accessible with a single tap.

## Theme Implementation

Use DaisyUI's `data-theme` attribute on `<html>` to switch themes. The default reader provides **light and dark**. Add **sepia** only when the brief explicitly asks for it.

```js
// tailwind.config.js
plugins: [require('daisyui')],
daisyui: {
  themes: [
    {
      light: {
        'base-100': '#f9f6f1',
        'base-content': '#1a1814',
      },
    },
    {
      dark: {
        'base-100': '#141210',
        'base-content': '#e8e4de',
      },
    },
  ],
}
```

- Theme change must be instant — no transition delay that makes the UI feel unresponsive.
- Theme preference must persist in `localStorage`.
- Respect `prefers-color-scheme: dark` as the initial default if no saved preference exists.

## Font Size Implementation

Use only when the brief explicitly asks for font size control.

```js
const SIZES = [14, 16, 18, 20, 22]; // px
let current = 2; // default index

function applySize(index) {
  document.documentElement.style.setProperty('--reader-size', SIZES[index] + 'px');
  localStorage.setItem('reader-font-size', index);
}
```

- Font size changes must reflow gracefully without layout breakage.
- Line height should scale proportionally with font size.
- Save preference per reader (not per book).

## Scroll and Navigation

- Default: vertical scroll for H5. Horizontal paging is an optional mode, not the default.
- End-of-chapter: show a clear "Next chapter" prompt at the bottom of content — do not rely on navigation bars alone.
- Resume: on entering a chapter, restore scroll position from `localStorage` if available.
- Chapter transitions: force a full browser reload so AdSense reinitializes and the browser shows its native loading progress bar. Do NOT use `<Link>` from `next/link` or `router.push()` — Next.js App Router intercepts same-origin clicks after hydration and performs SPA navigation even on plain `<a>` tags. The only reliable override is `e.preventDefault()` + `window.location.href`:

  ```tsx
  <a
    href={`/book/${bookSlug}/chapter/${nextChapter}`}
    onClick={(e) => {
      e.preventDefault()
      window.location.href = `/book/${bookSlug}/chapter/${nextChapter}`
    }}
  >
    Next →
  </a>
  ```

  A plain `<a href>` without the `onClick` override is NOT sufficient in Next.js App Router — the framework hydration intercepts it for SPA routing.

  **When to use `HardLink` vs. `next/link`:**
  - **Any navigation that leaves an ad-bearing page** (home with ad slots, book detail, chapter reader): use `HardLink` / `window.location.href` so ad slots reinitialize and each destination counts as a fresh pageview.
  - **Chapter reader navigation** (Next →, prev/next tap zones, keyboard shortcuts): force a full reload with `window.location.href` so ad slots reinitialize.
  - **Ad-free pages only** (about, contact, privacy, terms, cookie policy, /dashboard): `next/link` with prefetch is acceptable for internal navigation because there are no ad slots to reinitialize.

## Gestures and Tap Zones (Mobile)

- Left-edge tap (15% width): previous chapter.
- Right-edge tap (15% width): next chapter.
- Center tap: toggle chrome visibility (if implementing immersive mode).
- These zones must not conflict with text selection.
- Swipe left/right for chapter navigation is acceptable as an enhancement, not a requirement.

## Keyboard Shortcuts (Desktop)

- `ArrowLeft` / `ArrowRight` or `←` / `→`: previous / next chapter.
- `F` or `Esc`: toggle immersive mode.
- These shortcuts must not conflict with browser defaults.
- Include a one-time tooltip hint for first-time desktop visitors.

## Interaction Rules

- All settings changes (theme, font size, density) apply instantly with no delay when those controls are present.
- Preserve reader preferences in `localStorage` for prototypes; in a server-side user account for real products.
- Preserve reading position in `localStorage` for prototypes; durable backend for real products.
- Reader controls must be reachable with one thumb on mobile.
- Do not require login before basic reading unless the user explicitly asks for a gated product.
- Display ads are expected on monetized sites (the default arbitrage model — see `references/adsense-arbitrage.md`): place the first AdSense/AdX slot **after** `contentParts[0]` (not before all content — pre-content ads have near-zero viewability on paid traffic), then interleave remaining slots within the reading flow. AdX sites add a `StickyAnchorAd` (q4, `position: fixed; bottom: 0`) for high-viewability anchor impressions. AdSense sites omit the sticky anchor (Google AdSense policy prohibits fixed-position manual units). Keep each slot's size reserved (no CLS), never let an ad be mistakable for navigation, and never push chapter content below the fold. Pop-ups and pre-content interstitials remain forbidden.

## Accessibility

- Use `<button>` for all interactive controls, not clickable `<div>` or `<span>`.
- Maintain WCAG AA contrast (4.5:1) for body text and controls in all enabled themes.
- Ensure visible `:focus` states on all keyboard-navigable controls.
- Do not disable browser pinch-to-zoom (`user-scalable=no` is forbidden).
- Avoid motion or animations on the reading surface itself. Restrict motion to chrome transitions.
- Use `aria-label` on icon-only controls (prev/next arrows, settings gear).
- Chapter content should be wrapped in `<article>` with an appropriate `aria-label`.

## Empty and Error States

- Chapter not found: "This chapter isn't available yet." with a link back to the catalog.
- Load failure: "Couldn't load this chapter. Try refreshing or check your connection."
- End of book: "You've finished [Book Title]." with a link to the book detail page.
- No chapters yet: "No chapters published yet. Check back soon."

Never show a raw error object or stack trace to the reader.
