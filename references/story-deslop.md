# Story Deslop

Load this reference when the user asks to remove AI flavor from novel prose, or when prose review detects template patterns.

## Core Philosophy

AI flavor is not a grammar error — it is a style problem: over-polished, symmetrical, over-explained. The goal is to pull text from over-crafted back toward specific, natural, readable. Change the minimum amount to shift the character of the passage.

**Never delete entire paragraphs.** Plot function, foreshadow, character reveals, and tension hooks must survive. If a passage is bad, rewrite it — don't erase it.

## Detection: The 7 Gates

Run the applicable gates based on severity (see Severity Levels below).

| Gate | Problem | Signal |
| --- | --- | --- |
| A | Banned words / high-frequency clichés | "something flickered in his eyes" "he drew a deep breath" "the corner of his mouth curved" — all patterns apply equally with he/she/they/their variants |
| B | Template sentence patterns | negation-then-reversal setups, "with a ...", "his voice was low but ...", consecutive parallel structures ≥3 |
| C | Telling not showing (psychology) | "he felt" "she realized" "emotion surged inside her" without grounding action |
| D | Uniform rhythm / paragraph length | Every paragraph 4–6 sentences, identical beat |
| E | Flat dialogue tags | "said/asked/smiled" on nearly every line |
| F | Moral summary endings | Last paragraph summarizes or moralizes what just happened |
| G | Narrator intrusion / god-view | "What she didn't know was..." / "The reason he ... was because..." / evaluative aside that steps outside character POV |

## Severity Levels

| Level | Quantity signal | Gates to run |
| --- | --- | --- |
| Mild | ≤5 banned words/1,000 chars, no consecutive 3+ templates | A + B |
| Moderate | 6–15 banned words/1,000 chars, or 3+ consecutive templates | A + B + C + D + G |
| Severe | >15 banned words/1,000 chars, or 4+ of the 7 Gates flagged | All 7 Gates + targeted rewrites |

Deletion cap by severity: Mild ≤15%, Moderate ≤25%, Severe ≤35% of the passage. Mark anything borderline `[NEEDS REVIEW]` rather than deleting.

## Natural Writing Benchmarks

| Dimension | Natural web fiction | AI-flavored text |
| --- | --- | --- |
| Paragraph length | 1–3 sentences; occasional 1-sentence standalone | 4–6 sentences, uniform |
| Dialogue tags | 60%+ tagless, action-attributed | Nearly every line tagged |
| Emotion | Body action ("his hands shook") | Direct statement ("he was terrified") |
| Simile | Everyday ("like a dog guarding its bowl") | Literary ("like crystalline ice") |
| Filler words | Colloquial ("God", "damn", "ugh") | Almost none |
| Detail | Specific, concrete | Vague and thorough |
| Parallel structure | At most 1–2, never 3+ consecutive | 3–5 in a row is standard |
| Endings | Action or dialogue | Summary or uplift |

## Quick Replacement Reference

| AI-flavored phrase | Natural alternative |
| --- | --- |
| he drew a deep breath | his chest rose / delete |
| something flickered in his eyes | he looked away / narrowed his eyes |
| the corner of his mouth curved | he smiled — it didn't reach his eyes / he laughed |
| as if / as though / as though woven from | plain comparison or literal description |
| couldn't help but | direct action verb |
| slowly opened his mouth | just use dialogue / action-then-dialogue |

## Triage Pass (run before any rewriting — token-saving gate)

Before touching a single chapter, do a fast read-only scan of all chapters and output a severity table:

```
| Chapter | Banned words/1k | Consecutive templates | Gates triggered | Severity |
|---------|-----------------|----------------------|-----------------|---------|
| ch-001  | 4               | 1                    | A               | mild    |
| ch-002  | 11              | 3                    | A B C           | moderate|
...
```

Rules:
- Scan by reading each chapter once — do not rewrite anything yet.
- Assign severity (mild / moderate / severe) per the Detection table above.
- Chapters with **zero** banned words and no Gate triggers: mark `clean` — **skip entirely**, do not process.
- Group results: clean (skip) → mild (Pass 1 only) → moderate (Pass 1+2) → severe (all 3 passes).

This triage pass typically saves 30–50% of total tokens on a full book by skipping clean chapters and limiting mild chapters to one pass.

## Three-Pass Method

- **Pass 1 — Deabstract**: Gates A, C (abstract emotion), D (uniform rhythm), G (narrator intrusion)
- **Pass 2 — Deliteralize**: Gates A (literary register), B (sentence templates)
- **Pass 3 — Restore natural voice**: Gates D (short/long rhythm mix), E (dialogue differentiation), F (ending de-moralization), add sensory detail

- Clean: skip — no passes
- Mild: Pass 1 only
- Moderate: Pass 1 + Pass 2
- Severe: All 3 passes + targeted rewrites of worst paragraphs

## Whitelist

If the project root contains `.deslop-whitelist`, skip flagging any phrase that appears there. Format: one entry per line, `#` for comments. Use for world-building terms, character nicknames, or intentional stylistic choices that happen to match banned patterns.

## Deslop Report Format

```
## De-Slop Report

AI flavor level: {mild / moderate / severe}
Gates applied: {A B C ...}
Deletion rate: {X%}

### Change Log
| Location | Gate | Original | Revised | Note |
|----------|------|----------|---------|------|

### [NEEDS REVIEW]
{Any passages marked for human review rather than auto-rewrite}
```
