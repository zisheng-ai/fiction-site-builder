# Content Quality Standards

## Chapter Count (20–26 Chapters)

Target chapter count per book is **20–26**, determined by genre:

| Genre arc | Target | Notes |
|-----------|--------|-------|
| Psychological suspense / revenge arc | 20–21 | Tight pacing, hard twist every chapter |
| Paranormal / billionaire romance (slow burn) | 22–23 | |
| Space opera / fae epic / multi-POV dark fantasy | 24–26 | |

**Verification command (run before starting any new book):**

```bash
for d in content/*/chapters; do
  book=$(basename $(dirname "$d"))
  count=$(ls "$d"/*.md 2>/dev/null | wc -l | tr -d ' ')
  echo "$book: $count"
done
```

Rules:
- New books must fall within 20–26 chapters and must not duplicate an existing title.
- Existing books with fewer than 20 chapters must be extended to reach 20.

## Deslop Workflow

Run deslop (remove AI flavor) on all chapters periodically. Load `references/story-deslop.md` before executing.

**Execution order:**

1. **Triage pass (required first):** Quick scan of all chapters in the book. Output a severity table (clean / mild / moderate / severe). Skip clean chapters — saves 30–50% tokens.
2. **Process by severity group:**
   - Mild → Pass 1 (Gate A + C + D + G)
   - Moderate → Pass 1 + Pass 2 (+ Gate A literary + Gate B template patterns)
   - Severe → All 3 passes + targeted rewrite of flagged paragraphs
3. **Output a De-Slop Report after each chapter:** log which gates were applied, change rate, and any `[NEEDS REVIEW]` annotations.

**When to trigger:**
- After finishing all chapters of a new book (Write → Review → Deslop)
- During bulk maintenance of existing books

## Duplicate Chapter File Cleanup

When `content/{book}/chapters/` contains multiple files mapping to the same chapter number (e.g. two files both starting with `ch-005`):

**Resolution priority (highest first):**
1. Keep the file with more words; delete the shorter one.
2. If word counts are equal, keep the file whose frontmatter `chapter:` field matches the filename number (e.g. `chapter: 5` should not appear in `ch-003-xxx.md`).
3. If both are equal, keep the file with more complete content or a more descriptive title.

**Detection command:**

```bash
book="book-slug"
ls content/$book/chapters/ | sed 's/\(ch-[0-9]*\).*/\1/' | sort | uniq -d
```

For each duplicate pair, run `wc -w` on both files and delete the shorter version. No confirmation needed before deletion — the user reviews all changes via `git status` at wrap-up.
