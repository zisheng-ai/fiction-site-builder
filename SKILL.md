---
name: fiction-site-builder
description: write fiction and build the reading site end-to-end. use when the user asks to write a novel or short story (long-form novel, short-form story, write chapters, continue writing, story setup, import a manuscript, review prose, remove AI flavor), or asks for a mobile-first fiction reading site, web novel H5, work list/detail/catalog/reader pages, markdown chapters, multilingual reading sites in english/spanish/japanese/korean, or a simple fiction site for social traffic campaigns. do not use for creator dashboards, ranking systems, bookshelf platforms, or reader community features unless the user explicitly asks for those.
---

# Fiction H5 Builder

## Three Core Goals

This skill exists to run a **Facebook paid-traffic → AdSense/AdX display-ad arbitrage** business. Every decision — what to write, how to build the site, what image to generate — is ultimately a revenue decision. The three goals below are the levers:

**Goal 0 — Maximize pageviews per session (content lever).**
Each chapter = one pageview = one set of ad impressions. A reader who clicks through 6 chapters generates 6× the ad revenue of a reader who clicks through 1. Everything that keeps a reader reading — prose quality, cliffhanger endings, chapter length, hook copy — is revenue engineering. Quality fiction is not an aesthetic goal; it is the mechanism by which pageviews happen.

**Goal 1 — Maximize viewable RPM (layout lever).**
The site must load fast, render correctly on mobile, and place ads where they are actually seen. An ad that exits the viewport in under 1 second earns 30% of the revenue of an ad that is held in view for 3+ seconds. LCP < 2.5s, first ad after the first 20% of content, full-page reload on chapter navigation so AdSense/AdX reinitialize — these are revenue numbers, not UX preferences.

**Goal 2 — Maximize Facebook CTR while keeping accounts alive (creative + compliance lever).**
The cover image is the Facebook ad creative. Its scroll-stop power determines CPC. Suggestive covers (bare shoulders, implied intimacy, allure) increase CTR and are explicitly allowed; explicit/pornographic imagery and missing trust pages get the ad account banned. Account survival is a hard constraint — a banned account ends the business. Allure is optimized to the maximum safe level, never beyond it.

## Business Model — Paid-Traffic Arbitrage

Every site built by this skill is, by default, a **Facebook-traffic + AdSense/AdX arbitrage** property: buy a click on Meta ads, monetize a multi-pageview reading session with display ads, profit on the spread. This reframes two things:

- **Profit = (viewable session RPM × pageviews per session) − Facebook CPC.** The build directly controls pageview depth (chapter model, cliffhangers, pagination, prefetch) and viewable RPM (ad layout, density, viewability, lazy-load). Treat these as revenue engineering — see `references/adsense-arbitrage.md`.
- **Account survival is a top constraint.** Both Facebook and AdSense scan the landing page. Suggestive covers are fine and encouraged for CTR; only outright explicit/pornographic imagery, cloaking, missing trust pages, or runaway ad density get the Facebook ad account banned or AdSense restricted/disabled. See `references/adsense-arbitrage.md` §1 and `references/cover-allure-elements.md` §0.

Load `references/adsense-arbitrage.md` whenever building, laying out ads, directing covers, or wiring Facebook tracking.

## Operating Principles

- **Every chapter must end on a cliffhanger.** This is not a style preference — it is the mechanism that makes the next pageview happen. A chapter that resolves cleanly is a chapter that ends the session. See `story-long-write.md` hook-out techniques.
- **The cover is a Facebook ad creative first, a book cover second.** Design and generate it to stop the scroll in 0.3 seconds. Allure, composition, and implied story are CTR levers. See `cover-allure-elements.md` and `facebook-ads.md`.
- **Landing page = Chapter 1, not the homepage.** Facebook ads link directly to ch1. The homepage is for readers who already know the site. The ch1 hook is the first pageview; if it doesn't grab, the session ends at 1.
- The chapter page is the product. Every other page is a path to it.
- Mobile first — not mobile only. Design and code for mobile first, then enhance for tablet and desktop with `min-width` breakpoints. Social traffic is 90% mobile so 390px must work perfectly; desktop must still get a purposeful layout.
- Prefer the simplest tech choice that meets the brief. Complexity needs a reason.
- Fixed good typography beats user-adjustable bad typography.
- Content language determines layout, font, and line-flow decisions.
- Realistic content only. Never ship placeholder text to readers.
- Load only the references needed for the current task phase.

## Content-to-Site Promise

This skill delivers a Next.js-blog-style experience:

1. Novel files live in `content/` inside the Next.js project root.
2. `next dev` / `next build` picks them up automatically — no scripts, no JSON generation.
3. Adding a new book = create `content/{book-title}/chapters/` and write chapters. Rebuild. Done.

All writing phase outputs MUST be saved to the correct path under `content/` from the project root. `@content-collections` reads `content/` at build time and generates typed collections automatically.

## Build Pipeline

All work starts with Phase 0. After that, Track A (content) and Track B (site) run in parallel.

### Phase 0 — Setup

Reference: `references/story-setup.md`
Output: directory structure, naming conventions, GitHub private repo, submodule registration. Skip if the project directory already exists.

**`.npmrc` — MANDATORY first file (create before anything else):**

The development machine uses an internal npm registry (Alibaba `registry.anpm.alibaba-inc.com`). If `.npmrc` is not present at the site root, `pnpm install` bakes internal tarball URLs into `pnpm-lock.yaml` and Vercel's CI cannot reach them — **the build fails with `ERR_SOCKET_TIMEOUT`**. This has caused production outages.

```bash
echo "registry=https://registry.npmjs.org" > .npmrc
```

Create this file **before running `pnpm install` or `pnpm add` for the first time**. If the site already exists and the lockfile contains `registry.anpm.alibaba-inc.com` URLs, fix it:

```bash
echo "registry=https://registry.npmjs.org" > .npmrc
rm pnpm-lock.yaml
pnpm install --registry https://registry.npmjs.org
# Verify: grep "registry.anpm" pnpm-lock.yaml | wc -l  # must be 0
```

If `pnpm install` still bakes in internal URLs (cached resolution), replace them in-place:
```bash
sed -i '' 's|https://registry.anpm.alibaba-inc.com/|https://registry.npmjs.org/|g' pnpm-lock.yaml
```

Commit both `.npmrc` and the updated `pnpm-lock.yaml`.

**GitHub + Submodule setup (run once per new site):**

```bash
# 1. Initial commit inside the new site directory
git add -A && git commit -m "feat: initial commit"

# 2. Create private GitHub repo and push (account: zisheng-ai)
gh repo create zisheng-ai/{site-name} --private --source=. --remote=origin --push

# 3. Register as submodule in the fictions parent repo
git -C /Users/zisheng/github/fictions submodule add --force \
  https://github.com/zisheng-ai/{site-name}.git {site-name}

# 4. Commit the submodule entry in the parent repo
git -C /Users/zisheng/github/fictions add .gitmodules {site-name}
git -C /Users/zisheng/github/fictions commit -m "feat: add {site-name} as submodule"
git -C /Users/zisheng/github/fictions push
```

Replace `{site-name}` with the actual project directory name (kebab-case). Skip this block if the site already has a remote configured.

### Track A — Content

Starts after Phase 0. Runs in parallel with Track B.

| Phase | Name | Reference | Output |
| --- | --- | --- | --- |
| A0 | Niche Research | `fiction-niche-researcher.md` | `outputs/{site-slug}/{book-slug}/niche-research.json` |
| A1 | Write | see modes below + `facebook-ads.md` (taglines & hook copy) | chapters, outline, world, tracking |
| A2 | Cover | `story-cover.md` + `cover-styles.md` + `facebook-ads.md` | `public/covers/{book-title}.webp` + `public/covers/{book-title}.json` per book (flat, no subfolders) |
| A2.5 | Illustrations | `story-illustrations.md` + `cover-allure-elements.md` | `public/illustrations/{book-slug}/ch-{NNN}.webp` (exactly 5 per book) |
| A3 | Quality Pass | `story-review.md` + `story-deslop.md` | review report, AI flavor removed |

**Arbitrage role of each content phase:**
- **A0** — identifies high-demand genres and tropes with proven Facebook CTR. The `differentiation_angle` directly affects ad creative relevance and CPC.
- **A1** — each chapter = one pageview. Chapter length (1,200–1,600 words) and mandatory cliffhanger endings are the primary pageview/session multiplier. Taglines from `facebook-ads.md` are the ad copy.
- **A2** — cover = Facebook ad image. CTR determines CPC. Everything else in the profit equation is downstream of whether the cover stops the scroll.
- **A2.5** — illustrations increase scroll depth and ad viewability within a chapter page. Deeper scroll = longer time-in-view = higher Active View score = higher CPM bids from advertisers.
- **A3** — AI-flavored prose increases bounce rate. Deslopped prose keeps readers reading past chapter 1, which is the difference between a 1-pageview session and a 4-pageview session.

A0 runs once per book (not once per site). Required for each new book unless the user has explicitly stated the genre, tropes, and premise. A0's `differentiation_angle` and `competitive_brief` feed directly into A1's story brief.

**A1 modes — pick exactly one per session:**

- **Long-form:** `references/story-long-write.md` → `chapters/ch-NNN-{title}.md` + `tracking/`
- **Short-form:** `references/story-short-write.md` → `prose.md`, `setup.md`, `beat-outline.md`
- **Import:** `references/story-import.md` → split chapters, reconstructed `world/`, `outline/`, `tracking/`

**A2.5 rules:**
- **Runs by default on a full pipeline run** — once a book has its cover (A2) and ≥ 10 chapters, generate its illustrations automatically. Do **not** wait for the user to ask, and do **not** prompt. Skip only for short-form stories, or if the user has explicitly opted out of illustrations.
- As a standalone step, runs when the user requests illustrations ("Add illustrations" / "Generate illustrations").
- Never on short-form stories (no chapter files to illustrate).
- Illustrations use T3 or T4, randomly assigned per illustration. Never T1, T2, or T5.
- Exactly 5 illustrations per book, placed at the highest-stakes peaks (see `story-illustrations.md` for slot distribution). Never exceed 5 — cost constraint. A book may fall below 5 only when not enough scenes earn one — never skip the phase itself.
- Does not block the Pre-Launch Gate — but a full pipeline run is expected to produce illustrations for its long-form books.

A3 runs automatically after A1 completes for every long-form book. Do not skip or prompt — deslop is a required quality pass, not optional. Skip only for short-form stories or on explicit user opt-out.

### Track B — Site

Starts after Phase 0. Runs in parallel with Track A.

**Before starting B1, read the reference site that matches this site's ad network:**

| Ad network | Reference site | Path |
|---|---|---|
| nablepart AdX | velvet-throne | `/Users/zisheng/github/fictions/velvet-throne/` |
| varygames AdSense | midnight-fable | `/Users/zisheng/github/fictions/midnight-fable/` |
| none / unknown | velvet-throne | `/Users/zisheng/github/fictions/velvet-throne/` |

Read at minimum: `next.config.ts`, `vercel.json`, `src/app/layout.tsx` (non-ad parts). Copy config structure and patterns verbatim — this avoids stale config and Next.js export drift. **Dependency versions should always be the latest** — do not copy pinned versions from `package.json`; run `pnpm add` with no version pin to get the newest release. Ad components (`AdSlot` / `AdsenseSlot`) are defined in `references/adsense-arbitrage.md` and should not be copied from the reference site.

| Phase | Name | Reference | Output |
| --- | --- | --- | --- |
| B1 | Stack | `tech-stack.md` | chosen stack with one-line rationale |
| B2 | Design | `design-system.md` | tone, palette, type system, `public/logo.png`, `public/favicon-32x32.png` |
| B3 | Data | `data-contract.md` | content-collections schema |
| B4 | Build | `references/ui-components.md` + `reader-ux.md` + `adsense-arbitrage.md` + `seo.md` + `meta-ads-landing-requirements.md` + `social-sharing.md` | working site with all required pages, trust pages, sitemap, robots.txt, `llms.txt`, metadata, and ShareBar on book detail + chapter pages; ad slots and tracking only if configured |
| B5 | Performance | `performance.md` + `adsense-arbitrage.md` | Core Web Vitals targets met, images optimized, ad CLS/lazy-load tuned |
| B6 | QA | `qa-checklist.md` + `references/lighthouse-qa.md` | automated QA pass; Lighthouse median scores meet thresholds; ad-layout + policy-compliance checks; screenshots on failure only |

B1 → B2 → B3 → B4 are sequential. B5 and B6 run in parallel against the same build — run `pnpm run build` once, then check both.

**B4 gate:** at least one book with ≥ 10 chapters must exist before starting B4. B1–B3 may run while writing is still in progress.

### B4 — Domain (optional)

During B4, check the parent project `fictions/CLAUDE.md` site table for the domain assigned to this site.

- **If domain is specified**: use it in `metadataBase`, `sitemap.ts`, and `src/lib/site.ts`.
- **If no domain is specified**: set `metadataBase: new URL('https://PLACEHOLDER.example.com')` and record a TODO:
  ```
  - [ ] 配置正式域名（当前 metadataBase 为占位地址，需在 layout.tsx / src/lib/site.ts / sitemap.ts 同步更新）
  ```

### B4 — Google Ads (optional)

During B4, check the parent project `fictions/CLAUDE.md` site table for the ad account assigned to this site (either nablepart AdX or varygames AdSense).

- **If an ad account is specified**: wire up the full ad stack — GPT/AdSense script in `<head>`, `AdSlot` / `AdsenseSlot` components in pages, and follow `references/adsense-arbitrage.md` for slot placement and density rules.
- **If no ad account is specified**: skip all ad code entirely — no GPT script, no AdSense script, no slot components. Record a TODO:
  ```
  - [ ] 配置广告账号（当前无广告代码，待确定账号类型后接入 AdX 或 AdSense）
  ```

Do not add placeholder ad markup or commented-out ad code — leave the pages clean.

### B4 — Facebook Pixel (optional)

During B4, check the parent project `fictions/CLAUDE.md` for a `facebook_pixel.id` configuration. This step is **optional** — if the parent project does not specify a Pixel ID, skip the code change and only record it in `TODO.md`.

- **If configured**: add the Facebook Pixel base code to `src/app/layout.tsx` `<head>` using an inline `<script dangerouslySetInnerHTML>` tag. Use the exact Pixel ID from `fictions/CLAUDE.md`. Include both the script block and the `<noscript>` fallback `<img>`.
- **If not configured**: do not add any Pixel code. Instead, add a pending item to the site's `TODO.md` under `分析与广告`:
  ```
  - [ ] 配置 Facebook Pixel（项目 CLAUDE.md 未指定 Pixel ID）
  ```

This Pixel setup is **project-level** and must not be hardcoded into the skill template.

Optional phases (load only when the brief requires):
- `references/internationalization.md` — when target language is not the build default
- `references/product-surface.md` — when IA or URL structure needs formal documentation

### Parallel-safe pairs

| What | Notes |
| --- | --- |
| Track A + Track B | Both start after Phase 0; fully independent |
| Multiple books in A1 | All books run concurrently |
| Chapters within a book (A1) | Expand outline first → parallel chapters → continuity pass |
| Covers across books (A2) | Batch all books in one round, not one-at-a-time |
| Illustrations across books (A2.5) | All books in parallel — one Agent call per book |
| Illustrations within a book (A2.5) | All peak chapters (up to 5) in parallel — background processes |
| B2 + B3 | Design tokens and data schema are independent |
| B5 + B6 | Share one `pnpm run build` — do not run two concurrent builds |

### Post-Build Deliverables (required after B6)

After B6 passes, generate two files before closing the session:

**`README.md`** — site reference card for this repo, written in **Chinese (中文)**:
- 域名、语言、调性、广告账号等头部信息
- 书目表：slug、书名、章节数、插图数
- 技术栈一句话
- 开发命令（`pnpm dev`、`pnpm build`）

**`TODO.md`** — outstanding work for this site, written in **Chinese (中文)**:
- 部署状态（未部署 / 已上线 + 域名）
- 每本书的章节缺口：列出少于目标长度（20–26 章）的书及缺多少章
- 缺少插图的书
- `books.ts` 里的 `chapterCount` 与实际文件数不一致的地方
- 广告和分析工具中尚未完成的项

Both files must be written in **Chinese**. If the site is a new build, start with the expected state (all chapters to write, not yet deployed). If the site is updated, reflect the current delta.

### Per-Site `AGENTS.md`

If a site directory contains an `AGENTS.md` file, read it before starting site work. It may contain project-specific conventions that override this skill's defaults (e.g., a non-standard Next.js version or local build rules). Treat its instructions as site-specific addenda to `SKILL.md`.

### Pre-Launch Gate

All of the following must be true before go-live (after B6 passes):

| Check | Required location |
| --- | --- |
| ≥ 5 book directories | `content/{book-title}/` |
| Each book has **20–26 chapters** (randomized per book; optimized for Facebook session depth) | `content/{book-title}/chapters/` |
| Each chapter meets its type target (see Pacing Guidelines in `story-long-write.md`); word counts must vary naturally across chapters — never identical | A1 output |
| `outline/outline.md` exists and non-empty | A1 output |
| `world/worldbuilding.md` exists and non-empty | A1 output |
| `tracking/context.md` exists | A1 output |
| Cover image for every book | `public/covers/{book-title}.webp` |

If any book is missing a cover at launch time, run A2 immediately — do not prompt the user.

If a full pipeline run reaches launch with no illustrations generated for its long-form books, run A2.5 before go-live — do not prompt the user. (Illustrations are not a hard gate, but a full run should not silently skip them.)

### Scope-to-phase mapping

| User intent | Phases to run |
| --- | --- |
| "Write a novel" / "Continue writing" / `/story-long-write` | 0 (skip if exists), A1 long-form, **A3 (automatic)** |
| "Write a short story" / `/story-short-write` | 0 (skip if exists), A1 short-form (A3 skipped for short-form) |
| "Add one book to existing site" | A1 long-form (single book), A2 (single book) |
| "Generate covers" / `/story-cover` | A2 only |
| "Add illustrations" / "Generate illustrations" | A2.5 only |
| "Import manuscript" / `/story-import` | A1 import only |
| "Review prose" / `/story-review` | A3 only |
| "Build the site" / full pipeline | 0 → Track A + Track B in parallel; **A2.5 runs automatically after A2 for every long-form book** (skip only on explicit opt-out) |

**Book count cap — 5 per session, always.** Whether building a new site from scratch or adding books to an existing site, generate exactly **5 books** per session. Never exceed 5 in a single run regardless of user phrasing ("add some books", "fill the site", etc.). If the user explicitly specifies a different count, honor it; otherwise default to 5 and do not ask. For new sites: run A0 for all 5 in parallel, then A1 for all 5 in parallel. Genre and topic are selected independently per book by random sampling from the high-demand genre pool — repetition across books is allowed and expected. Do not attempt to maximize genre variety; just pick whatever has strong demand for each book independently.

For review and redesign tasks, start at the relevant phase and load only the references covering the failing areas.

## Environment Prerequisites

This skill requires Claude Code. Before doing anything else, verify the Bash tool is available:

```bash
echo "claude-code-ok"
```

If the Bash tool is unavailable (not a Claude Code session), stop immediately and output:
```
ERROR: fiction-site-builder requires Claude Code. Re-invoke from a Claude Code session.
```

**Cover image generation (A2):** Calls `https://api.apiyi.com/v1/images/generations` via curl through the cascade `doubao-seedream-5-0-260128` → `doubao-seedream-5-0-260128` (retry) → `gpt-image-2-all` → `nano-banana-pro`. Requires `APIYI_API_KEY` in the environment. **No SVG fallback** — if the key is not set, cover generation is skipped (warning + continue), and the slot is filled in a later pass. All covers in a batch are generated **in parallel**.

```bash
[ -n "$APIYI_API_KEY" ] && echo "apiyi path" || echo "skip (no SVG fallback)"
```

**Logo and favicon (B2):** Same `APIYI_API_KEY` check as A2. If set, generates PNG assets via `doubao-seedream-5-0-260128` → `gpt-image-2-all` fallback; if not set, yellow warning + **skip** (no SVG fallback). Do **not** use `nano-banana-pro` for logo/favicon.

Generate **three assets in parallel**:
- `public/logo-light.png` — square icon (no text, no wordmark) for light backgrounds (colored/dark elements on white), generate at 1920×1920 then resize to 512×512
- `public/logo-dark.png` — square icon (no text, no wordmark) for dark backgrounds (light/white elements on black), generate at 1920×1920 then resize to 512×512
- `public/favicon-32x32.png` — same icon style, works on any background, generate at 1024×1024 then resize to 256×256

**After generation, compress all three with pngquant** (quality 80–95, speed 1):
```bash
sips -z 512 512 public/logo-light.png --out public/logo-light.png
sips -z 512 512 public/logo-dark.png  --out public/logo-dark.png
sips -z 256 256 public/favicon-32x32.png --out public/favicon-32x32.png
pngquant --force --quality=80-95 --speed 1 --output public/logo-light.png public/logo-light.png
pngquant --force --quality=80-95 --speed 1 --output public/logo-dark.png  public/logo-dark.png
pngquant --force --quality=80-95 --speed 1 --output public/favicon-32x32.png public/favicon-32x32.png
```

Target sizes after compression: logo ≤ 100 KB, favicon ≤ 25 KB. Sites use static export (`output: 'export'`) so `next/image` optimization is unavailable — pre-compression is mandatory.

After generating the assets, add the following CSS to `src/app/globals.css` (theme switching, no JS required):
```css
/* Logo theme switching */
.logo-dark { display: none; }
[data-theme$="-dark"] .logo-light { display: none; }
[data-theme$="-dark"] .logo-dark { display: block; }
```

Create `src/components/SiteLogo.tsx`:
```tsx
export function SiteLogo({ className, alt }: { className?: string; alt?: string }) {
  const a = alt ?? 'SITE_NAME'
  return (
    <>
      <img src="/logo-light.png" alt={a} className={`logo-light${className ? ' ' + className : ''}`} />
      <img src="/logo-dark.png" alt={a} className={`logo-dark${className ? ' ' + className : ''}`} />
    </>
  )
}
```

Replace all `<img src="/logo.png" ...>` (and `<Image src="/logo.png" ...>`) in the codebase with `<SiteLogo className="..." />`. The OG image in `layout.tsx` metadata stays as `logo.png` (used for social sharing, not rendered in the page). Remove any `filter: brightness(0) invert(1)` or similar filter hacks that were compensating for a single-logo approach.

## Phase Execution Protocol

Execute phases one at a time. Track progress with the best mechanism available in the current environment:

**If `TaskCreate` / `TaskUpdate` are available** (Claude Code): use them. Create tasks only for the phases that will actually run in this session. Do not create tasks for phases outside the current scope. Flip a task to `in_progress` when entering that phase and `completed` when done. Use `TaskGet` on re-entry to restore state.

**Phase naming convention:**
- Full pipeline: use phase IDs in task titles, e.g. "A2: Cover", "B4: Build".
- Single-function triggers (`/story-cover`, `/story-import`, `/story-review`, etc.): use descriptive titles — "Cover Generation", "Manuscript Import", "Prose Review".

**If those tools are not available** (other agents / API): print a compact text progress block only when a phase runs. For `/story-cover`, output something like:

```
[ Fiction H5 Builder — Cover Generation ]
▶ Cover
```

**Orchestration — use `Agent` for all delegation:**

Use the `Agent` tool for every delegation task, whether single or parallel. To run tasks concurrently, send multiple `Agent` tool calls in a single response — the runtime executes them in parallel automatically. Do not use `Workflow`.

| Situation | Use |
| --- | --- |
| Single chapter rewrite, single cover retry | One `Agent` call |
| A1 — multiple books in parallel | Multiple `Agent` calls in one response, one per book |
| A1 — chapters within a book | Expand outline first → multiple `Agent` calls in one response (one per chapter) → continuity pass |
| A2 — cover batch across all books | Multiple `Agent` calls in one response, one per book |
| A2.5 — illustrations across all books | Multiple `Agent` calls in one response, one per book |
| Track A + Track B launched together | Two `Agent` calls in one response |
| B5 + B6 against the same build | Two `Agent` calls in one response |

**Model selection:**

**If the `Agent` tool is available** (Claude Code — guaranteed by the prerequisite check above): delegate all chapter. Never write fiction content directly in the main context. Never prompt the user to switch models manually.

**If the `Agent` tool is not available**: write chapters sequentially in the main context. Skip parallel multi-book and multi-chapter spawning; write one chapter at a time following the Single Chapter Writing Process in `story-long-write.md`. Note: this is a degraded mode — quality and speed are both reduced.

Track B phases carry no model override and inherit the session model regardless.

**Rules (apply in both modes):**
- **Within a phase: act autonomously.** Invoke all required tools (image generation, file writes, bash commands) without asking the user. Never surface a "please run X" prompt mid-phase — just do it.
- **Between phases: summarize and continue.** At each phase boundary, print a one-line summary of what was produced and move to the next phase. Do not wait for user confirmation unless the user explicitly says to pause.
- Parallel-safe phases may be executed in the same turn — announce both at the start and summarize both at the end.
- Sequential phases run back-to-back without pausing for confirmation.
- Load each phase's reference file only when entering that phase.
- If a phase is skipped, mark it done with a note explaining why, then continue.
- On re-entry, restore or reprint current state before proceeding.

## Quality Gates

Do not deliver a build if any of these are true.

**Reading product:**
- Chapter content contains lorem ipsum or generic placeholder text.
- Reader background is pure white (`#fff`) or pure black (`#000`), or a tinted hue that makes the page feel pink / rosy / flashy.
- Next chapter button is missing, broken, or below 60px height.
- Next button uses a muted or dark color instead of a vivid warm fill (hot pink / magenta / coral).
- A "Previous" button appears in the reader nav.
- Table of contents button is missing from the reader nav.
- Chapter content fails to load or shows a blank page.

**Visual quality:**
- Loud gradients, fake glass panels, glowing orbs, or heavy drop shadows on any surface.
- Light theme `--color-base-100/200/300` tinted pink, rosy, or any vivid hue — use warm neutral tones only (ivory, linen, parchment: e.g. `#F9F7F3` / `#F0EBE3` / `#E4DDD4`).
- Body font is decorative, handwritten, or a novelty display face.
- Body text is below 17px on mobile or below 17px on desktop.
- Body text fails WCAG AA contrast (4.5:1) against the page background.
- Desktop is a stretched phone layout with no layout adaptation.

**Content and language:**
- `<html lang>` is missing or set to the wrong locale.
- Font stack does not include appropriate language fallbacks for the target language.
- Any reader-visible copy mentions AI, Markdown, parser, prompt, skill, or generation.

**Content completeness:**
- Site launches with fewer than 5 books.
- Any book has fewer than 20 chapters or more than 26 chapters.
- Any chapter falls below its type's minimum (see Pacing Guidelines in `story-long-write.md`).
- All chapters in a book have the same word count — natural variation is required.
- `outline/outline.md` is missing or empty for any published book.
- `world/worldbuilding.md` is missing or empty for any published book.
- Cover image is missing for any book in the reader at launch time. (Development preview may use CSS placeholders; final launch requires real covers.)
- `public/logo-light.png` or `public/logo-dark.png` is missing at launch time. Both are required (apiyi). No SVG fallback — if generation was skipped, flag for a later pass.
- Favicon is missing or is the default Next.js favicon at launch time. Required: `public/favicon-32x32.png` (apiyi). No SVG fallback — if generation was skipped, flag for a later pass.
- `SiteLogo` component is missing or any `<img src="/logo.png">` reference remains (except OG metadata in layout.tsx).

**Technical:**
- Build errors or console errors exist on page load.
- Routes do not work or data does not load.
- Any required page (home, book detail, reader) is missing.
- Initial JS bundle exceeds 200KB for a prototype.
- Cover images are not optimized (`next/image` or equivalent).
- `chapterCount` in `books.ts` does not equal the actual number of `.md` files in `content/{slug}/chapters/`. Always derive the count from the filesystem at build time or keep in sync manually — a stale value breaks chapter progress indicators and reader UX.

**Monetization & ad-policy (paid-traffic arbitrage — see `references/adsense-arbitrage.md`):**
- Any cover, hero image, or imagery is outright explicit / pornographic — exposed genitals or nipples, sex acts, graphic nudity (suggestive allure is fine; only hardcore content gets the ad account banned and AdSense disabled).
- Privacy Policy, Terms, About, or Contact page is missing or not footer-linked (AdSense approval + FB quality requirement).
- No cookie-consent / Google-certified CMP wired.
- An ad slot has no reserved size (causes CLS), or the above-the-fold ad is lazy-loaded (kills viewability).
- Ad density exceeds ~3–4 units / 1,000 words, or ad area exceeds ~30% of content area on any screen.
- An ad is visually/spatially mistakable for the Next/TOC control, or any layout encourages ad clicks.
- Chapter navigation is SPA (does not full-reload), so ads do not reinitialize and pageviews/impressions are undercounted.

## Non-Negotiables

- Writing internals (`outline/`, `world/`, `tracking/`, `reference/`, `resources/`, `teardowns/`) are never exposed in reader routes, reader-facing URLs, or site navigation. Build the site as if those directories do not exist.
- Reader-facing only by default: no AI labels, writing workflow panels, or "generated by" branding.
- Mobile is the primary target. Desktop must have its own layout logic — not a stretched phone screen.
- Required pages: home / book list, book detail with chapter list, chapter reader.
- Required reader controls: fixed bottom bar with TOC (ghost) + Next → (vivid warm fill, min 60px height); no Previous button; dark mode toggle (DaisyUI `data-theme`); resume-last-chapter via localStorage.
- Add font size control or reading progress indicator only when the brief explicitly asks for them.
- ShareBar (social sharing) is a standard feature — always include it. See `references/social-sharing.md`.
- Do not add ranking, bookshelf, favorites/bookmarks, search, payment, comments, or account modules unless explicitly requested.
- Respect content language: set `lang`, use language-appropriate font stacks, handle CJK line flow.
- One deliberate visual signature per build — connected to reading, books, chapters, or genre.
- Monetized FB-traffic sites (the default): ship Privacy / Terms / About / Contact pages + cookie consent, and reserve size on every ad slot. Suggestive covers are allowed; avoid only outright explicit/pornographic imagery (see `references/cover-allure-elements.md` §0). Trust pages, ad-layout, and no-cloaking compliance still apply everywhere.

## Performance Baseline

Fast loading is a product requirement for social traffic.

- SSG (`generateStaticParams`) for all chapter and book routes. No runtime filesystem reads.
- Cover images: `next/image` with `priority` on above-the-fold images when covers exist; CSS placeholder when they don't.
- Chapter content: loaded per route, never bundled all-at-once.
- Prefetch next chapter at 80% scroll depth (simple `router.prefetch()` call).
- Initial JS bundle under 200KB.
- LCP target: under 2.5s on a mid-range Android device on 4G.

## Reference Loading

Load references only when entering that phase. Do not preload all references at the start.

**Writing references (load only for content authoring tasks):**
- `story-setup.md` — project directory initialization and naming conventions.
- `story-long-write.md` — long-form chapter writing pipeline, context handoff.
- `story-short-write.md` — short-form story pipeline, emotion-first structure.
- `story-import.md` — import and split an existing manuscript into project structure.
- `story-review.md` — multi-perspective structural and prose review.
- `story-deslop.md` — AI-flavor detection and removal (7 gates).
- `story-cover.md` + `cover-styles.md` — cover generation via apiyi cascade (doubao → doubao-retry → gpt → nano); romance/drama covers roll T2/T3; other genres T1–T2 or T1 per genre table in story-cover.md; no SVG fallback (skip if no API key); all covers generated in parallel.
- `cover-allure-elements.md` — visual-appeal vocabulary for covers and illustrations; §0 is a lightweight monetization risk note (avoid only outright explicit content).
- `story-illustrations.md` + `cover-allure-elements.md` — in-chapter illustration generation (A2.5); T3/T4 tier (never T5); peak scene selection; IllustrationBlock component pattern.
- `facebook-ads.md` — load during A1 for all tagline and hook copy writing (ensures taglines follow FB ad standards: punchy 8-word opener, setup→reversal→unresolved tension structure, 25–40 words, final line always unresolved); also load during A2 cover generation. Do not load for pure chapter prose writing.
- `seo.md` — load during A0 (niche research) for keyword demand validation; and during A1 when writing book synopses (self-contained descriptions that double as meta descriptions).
- `geo.md` — load during A0 and A1: book synopses must be written as self-contained relational sentences (not promotional copy) per GEO evidence; author pen-name entity strategy informs A0 differentiation.

**Site build references (load for publishing tasks):**
- `tech-stack.md` — choose the implementation stack before writing any code.
- `design-system.md` — plan design identity before building any UI.
- `data-contract.md` — define data models and @content-collections setup.
- `references/ui-components.md` — visual and component quality floor during build.
- `reader-ux.md` — chapter page UX requirements during build.
- `performance.md` — Core Web Vitals, loading strategy, image optimization.
- `qa-checklist.md` — final automated QA and screenshot verification (failures only).
- `lighthouse-qa.md` — Lighthouse performance/accessibility/best-practices/SEO thresholds and runbook.
- `adsense-arbitrage.md` — Facebook-traffic + AdSense/AdX arbitrage playbook: profit model, account-survival compliance, pageview-depth and ad-layout/viewability tactics, FB tracking, trust pages. Load whenever building, laying out ads, directing covers, or wiring tracking.
- `meta-ads-landing-requirements.md` — Meta/Facebook ad traffic landing page policy, account-survival rules, cloaking, trust pages, Pixel+CAPI architecture, B4 compliance checklist. Load during B4.
- `geo.md` — `llms.txt` generation, structured data for entity disambiguation, robots.ts for AI crawlers. Load during B4.
- `vercel-operations.md` — Vercel project setup, custom domains, cache headers, deploy hooks, `output: export` pitfalls. Load when deploying or configuring hosting.
- `product-surface.md` — IA and URL structure (optional, load when needed).
- `internationalization.md` — language and font decisions (optional, load when needed).

## Output Contract

```
<project>/
  README.md                     # site reference card (generated after B6)
  TODO.md                       # outstanding work (generated after B6)
  public/
    llms.txt                    # AI crawler manifest (generated during B4, see geo.md §9)
  content/                      # all writing outputs live here
    {book-title}/
      chapters/                 # ch-001-{title}.md, ch-002-{title}.md, ...
      world/                    # worldbuilding.md, characters/, map.md
      outline/                  # outline.md
      tracking/                 # context.md, threads.md, timeline.md
  src/app/
    page.tsx                    # home: book list
    book/[slug]/
      page.tsx                  # book detail: synopsis + chapter list
      chapter/[n]/
        page.tsx                # chapter reader: content + prev/next
  content-collections.ts        # collection schema definitions
  src/lib/
  src/components/
    BookCard.tsx
    ChapterNav.tsx
    ThemeToggle.tsx             # DaisyUI data-theme switcher
    IllustrationBlock.tsx       # inline chapter illustration (A2.5, optional)
  public/
    covers/                     # cover images (A2) — flat: {slug}.webp per book (lossy WebP q82)
    illustrations/              # in-chapter illustrations (A2.5, optional)
      {book-slug}/
        ch-{NNN}.webp           # 0–5 per book, at peak dramatic moments (lossy WebP q78)
    logo-light.png              # logo for light mode — PNG via apiyi (B2); no SVG fallback
    logo-dark.png               # logo for dark mode — PNG via apiyi (B2); no SVG fallback
    favicon-32x32.png           # favicon (single, no light/dark) — PNG via apiyi (B2); no SVG fallback
```

Cover images (`public/covers/{slug}.webp` — flat, one file per book, lossy WebP q82) are generated in A2 via the apiyi cascade (gpt → doubao → nano), all books in parallel. Logo and favicon follow the same pattern in B2 — PNG via apiyi (doubao → gpt-image-2-all), all three generated in parallel (`logo-light.png`, `logo-dark.png`, `favicon-32x32.png`). **No SVG fallback** anywhere: if `APIYI_API_KEY` is unset or the cascade fails, the asset is skipped (warning + continue) and flagged for a later pass. During development only, CSS placeholders are acceptable — never ship a launch without real assets.

For a review or redesign task, the output is a findings report and patch set, not a full scaffold.

## Collaboration With Other Skills

The skills listed in **Merged Skills** below are already integrated — no separate installation needed. Use their capabilities directly.

This skill's reader-comfort requirements and QA gates take priority over any visual suggestion. Accept aesthetic feedback only when it does not reduce reading comfort, reduce contrast, or add visual noise to the chapter surface.

## Merged Skills

Skills that have been absorbed into this skill. When a source skill releases an update, review the diff against the corresponding reference files listed here and sync any improvements.

| Skill | Source | Merged into | Notes |
| --- | --- | --- | --- |
| frontend-design | `frontend-design@claude-plugins-official` | `references/ui-components.md`, `references/design-system.md` | Visual component specs, typography system, responsive layout patterns, dark mode implementation |
| taste-skill | `taste-skill@claude-plugins-official` | `references/design-system.md`, `references/ui-components.md` | Aesthetic judgment, genre-specific visual direction, signature element discipline, anti-default design discipline |
| oh-story-claudecode | `https://github.com/worldwonderer/oh-story-claudecode` | `references/story-setup.md`, `references/story-long-write.md`, `references/story-short-write.md`, `references/story-import.md`, `references/story-review.md`, `references/story-deslop.md`, `references/story-cover.md` | Fiction writing pipeline: trend scan, deconstruct/analyze, write (long-form + short-form), project setup, AI-flavor removal, manuscript import, prose review, cover generation. Site build, UI components, and reader UX are fiction-site-builder's own additions not present in the source. **Source is in Chinese** — sync is not a strict diff; requires reading the upstream changes, translating, and adapting into the English reference files. Local adaptations and additions have been made on top of the source; do not overwrite them unless there is a compelling upstream reason. When in doubt, preserve the local version. |
