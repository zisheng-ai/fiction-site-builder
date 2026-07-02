# Reader UX

## Reading First Principles

The reader is the product. Optimize for long sessions, low fatigue, and fast return to the current chapter. Every interaction in the reader must serve the reading act or stay out of the way.

**Ease of reading over visual precision.** If a choice makes prose harder to track, it is wrong regardless of how it looks in a screenshot. The chapter page must feel as effortless to read as a well-formatted paperback — generous body size, ample line-height, neutral background, no chrome competing for attention.

## Required Reader Controls

The default reader ships with a focused set of controls. Add font size, density, or reading progress indicator only when the brief explicitly asks for them. Table of contents is always required.

| Control | Requirement | Notes |
| --- | --- | --- |
| Next chapter | Required | Always visible via fixed bottom bar; see **Bottom Navigation Bar** below. No Previous button — Table of contents handles backward navigation |
| Table of contents | Required | "Table of contents" button in reader nav; links to or opens the chapter catalog |
| Book cover header | Required | Small cover thumbnail in the reader header above the chapter title; omit if no cover image exists |
| End-of-chapter prompt | Required | Repeat "Next chapter →" as inline CTA at the very bottom of chapter text, above the sticky bar. Use **`my-10`** (symmetric 40px) margin — never asymmetric `mt-16 mb-6`. |
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

## Bottom Navigation Bar

The bottom navigation bar is **always fixed** (`position: fixed; bottom: 0`) throughout the entire chapter reading experience — not just at the end of chapter content. It must remain visible while the reader scrolls. This is the primary navigation surface on mobile.

Apply `padding-bottom: env(safe-area-inset-bottom)` to handle iPhone notch/home bar.

**Layout — always two buttons, no Previous:**

```
[ Table of contents ]          [ Next → ]
  (ghost / outlined, ~36%)     (vivid fill, ~60%)
```

No "Previous" button. Ever. Fiction reading is a forward-only experience — the previous chapter is already read; showing a back button dilutes the forward momentum. If the reader wants to go back, the Table of contents handles that.

On the last chapter, the Next slot is an empty flex spacer — TOC button stays on the left. No "The End" label; nobody taps it.

**Always fixed — no transition:**

The nav bar is `position: fixed; bottom: 0` at all times. Never switch to inline mode. Add `padding-bottom` to the chapter content equal to the nav bar height (+ `env(safe-area-inset-bottom)`) so the last line of text is never hidden behind the bar.

```css
.chapter-content {
  padding-bottom: calc(80px + env(safe-area-inset-bottom));
}
.chapter-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  padding-bottom: env(safe-area-inset-bottom);
}
```

**Next button — psychology-driven design:**

The Next button must trigger an almost involuntary desire to tap. Use a vivid, saturated warm color — hot pink (`#E91E8C` range), coral, or electric magenta. Never use the site's calm brand color here; this button needs contrast-driven urgency.

Why this works: bright saturated warm colors activate dopamine anticipation. Combined with the unresolved story tension (Zeigarnik effect — the reader's brain cannot rest on an open narrative loop), the button becomes the path of least resistance. The reader taps before consciously deciding to.

- **Color:** vivid warm fill — hot pink / magenta / coral. Do NOT use dark navy, muted tones, or the site's neutral palette.
- **Label:** `Next →` — the arrow reinforces forward motion. Never "Next Chapter" (too wordy) or just "Next" without arrow.
- **Width:** ~60% of the nav bar. Significantly wider than TOC.
- **Height:** minimum 60px mobile, 64px desktop.
- **Font size:** 18–20px, weight 700–800, white text.
- **Border radius:** 14–18px (pill-ish, approachable).

**Button styling — no DaisyUI component classes:**

Do not use `.btn`, `.btn-primary`, `.btn-outline`, or any DaisyUI component class on nav buttons. Use plain Tailwind utilities only.

Both buttons must carry an explicit `style={{ fontFamily: '...' }}` with the full system stack — do NOT rely on body font inheritance, as DaisyUI resets can interfere:

```tsx
const btnFont = '-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif'
// apply as: style={{ fontFamily: btnFont }}
```

Shared base: `flex items-center justify-center font-extrabold tracking-tight select-none transition-all duration-150 hover:-translate-y-px active:translate-y-0 cursor-pointer`

Heights and radius (responsive):
- Mobile: `min-h-12` (48px), `rounded-[14px]`, `text-[15px]`
- Desktop sm+: `sm:min-h-[54px]`, `sm:rounded-2xl`, `sm:text-[17px]`

**TOC button:**

- `bg-base-100 border-2 border-base-300 text-base-content`
- Hover: `hover:border-primary hover:text-primary`
- Label: `Table of contents` — full text, no abbreviation.
- Width: ~40% of nav bar (grid `minmax(96px, 0.72fr)`)

**Next button:**

- `bg-primary text-white`
- `style={{ boxShadow: '0 8px 18px rgba(236,75,155,.18)' }}`
- Label: `Next →` (Unicode arrow, not SVG icon)
- Width: ~60% of nav bar (grid `minmax(136px, 1.12fr)`)
- Do not add glow wrappers (Aura component creates white padding artifacts)

**Nav bar grid layout:**

```jsx
<div style={{ display: 'grid', gap: '12px', gridTemplateColumns: 'minmax(96px, 0.72fr) minmax(136px, 1.12fr)' }}>
```

On the last chapter (no next), use `gridTemplateColumns: '1fr'` — TOC takes full width.

**TOC panel — DaisyUI 5 modal bottom sheet:**

Bottom sheet is the right choice for mobile fiction reading: thumb-friendly, native feel, fast in/out. Right-side drawer is not suitable — requires reaching the screen edge and covers more reading context.

Use `<dialog>` with `className="modal modal-bottom"` (DaisyUI 5). Open with `dialogRef.current.showModal()`, close with `dialogRef.current.close()`. Inside: `modal-box rounded-t-3xl rounded-b-none`, max-height `72vh`. Current chapter: `border-l-2 border-primary text-primary bg-primary/5 font-semibold`. Non-current: `border-l-2 border-transparent text-base-content/65`. Auto-scroll to current chapter on open (`scrollIntoView` with 50ms delay). Close on backdrop click (`e.target === dialogRef.current`).

**Quality gate failure if not met:**

- Next button uses a muted, dark, or low-saturation color.
- Next button is same width or narrower than TOC.
- "Previous" button appears anywhere in the reader nav.
- On mobile ≤ 640px: maintain 60px height minimum.

## Cross-Book Recommendation Grid

At the end of the **last chapter** (when `next` is null), render a 3-book recommendation grid below the chapter nav to retain readers who just finished a book.

```tsx
{!next && (
  <div className="my-10 border border-base-300 rounded-2xl px-6 py-10">
    <p className="text-base font-semibold text-base-content text-center mb-1">
      You&apos;ve finished <em>{book.title}</em>.
    </p>
    <p className="text-xs text-base-content/40 uppercase tracking-widest text-center mb-8">Keep reading</p>
    <div className="grid grid-cols-3 gap-4">
      {books.filter(b => b.slug !== slug).slice(0, 3).map(b => (
        <HardLink key={b.slug} href={`/book/${b.slug}/`} className="flex flex-col items-center gap-2 group">
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
- Links go to `/book/${b.slug}/` (book detail), not `/book/${b.slug}/chapter/1` — let the reader decide where to start.
- Filter out the current book (`b.slug !== slug`). Take first 3 from remaining.
- Use whatever link component the site uses (`HardLink`, `<a>`, or Next.js `<Link>`).
- Last chapter only — do not add to mid-book chapters.

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

- **Font:** system stack only — see `tech-stack.md` Fonts section. No webfonts.
- **Prose size:** `18px` mobile → `19px` sm+.
- **Line height:** `1.95` mobile → `2.05` sm+.
- **Paragraph spacing:** `margin-bottom: 1.3em`.

```css
.prose-reader { font-size: 18px; line-height: 1.95; }
@media (min-width: 640px) { .prose-reader { font-size: 19px; line-height: 2.05; } }
```
- Latin line-height: 1.9–2.1 (generous — easier to track across the line).
- Japanese/Korean line-height: 1.85–2.0.
- Paragraph spacing: `1em` top margin between paragraphs. Enough to separate beats without the double-spaced blog-style gap.
- Max line length: 32–38em for Latin prose; narrower for CJK (28–34em) to avoid very long line scanning.

## Layout

- Mobile horizontal padding: 18–22px.
- Sticky controls must not cover body text. Use a compact bottom bar with safe-area insets (`env(safe-area-inset-bottom)`).
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
- Display ads are expected on monetized sites (the default arbitrage model — see `references/adsense-arbitrage.md`): place AdSense/AdX slots below the header, in-content within the reading flow, end-of-chapter, and as a mobile sticky anchor. Keep each slot's size reserved (no CLS), keep a clear gap from the Next/TOC controls, never let an ad be mistakable for navigation, and never let ads push chapter content below the fold. Pop-ups and pre-content interstitials remain forbidden.

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
