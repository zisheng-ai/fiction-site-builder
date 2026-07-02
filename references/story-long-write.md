# Story Long Write

Load this reference when the user asks to write, continue, or revise long-form novel chapters.

**Before writing:** load the relevant genre file alongside this reference — `genre-romance.md`, `genre-mystery.md`, `genre-horror.md`, `genre-fantasy.md`, `genre-scifi.md`, or `genre-drama.md`. Genre-specific named emotional states, scene techniques, escalation registers, and synopsis formulas are there, not here.

## Niche Research Input

Before writing the first chapter of a new book, check `outputs/{site-slug}/{book-slug}/niche-research.json`:

- **Exists** → read `differentiation_angle`, `selected_tropes`, `competitive_brief[].beat_action`, and `producibility` (target chapters, words per chapter, intensity_level). These constrain the story brief.
- **Does not exist + user gave explicit genre/tropes/premise** → proceed directly; document them in `tracking/context.md`.
- **Does not exist + no explicit brief** → run `fiction-niche-researcher.md` first, then return here.

Continuing an existing book (adding chapters): skip this gate.

## Core Principles

1. **Emotion-first**: Every chapter has one primary emotional goal. Name it before writing a word.
2. **Validated patterns**: If a reference book exists in `reference/`, extract its technique before inventing new structure.
3. **Modular assembly**: Each chapter = hook + escalation + turn + hook-out. Each beat has a proven formula.
4. **Load only what's needed**: Before writing, read only the files relevant to this chapter's conflict and characters. Never load the full book.

## Scene-Level Drama — The Click Standard

Every scene must pass the same test as the cover image: **tension + question + desire, all three present**. Every scene must deliver at least two of the three simultaneously. Which two (or three) depends on the genre — see the relevant genre file for the genre-specific Click Standard.

### The One-Paragraph Test

Read the opening paragraph of every scene. Ask: *does the reader feel something in the first three sentences?* If the answer is only "I understand where we are" — the scene starts too early. Cut to the moment tension is already present.

---

### Named Emotion Requirement

**Banned:** generic emotional states — "she felt nervous", "he was angry", "she was confused", "he seemed interested". These communicate the emotion's name, not the experience of it.

**Required:** emotions with internal contradiction — the character feels one thing and does or says or wants something else. Name the specific state before writing the scene.

**Genre-specific named states are in the relevant genre file.** Load `genre-romance.md`, `genre-mystery.md`, `genre-horror.md`, `genre-fantasy.md`, or `genre-scifi.md` for the complete table for your genre.

Universal examples (apply to any genre):

| Named state | Internal contradiction | How it reads on the page |
|-------------|----------------------|--------------------------|
| **Shock recognition** | She understands something that changes the frame; the understanding is complete before she can speak | Goes still; what she was about to do or say dies before it happens; one physical detail only |
| **Performed calm** | She is not calm; she is performing calm for a specific person in the room | Voice measured; choices deliberate; the reader sees the effort the other character doesn't |
| **Deferred grief** | Something has been lost; she knows; she cannot stop moving long enough to feel it | Acts with unusual efficiency; the grief leaks through one small wrong detail in her behavior |

Use the named state as the scene's emotional throughline. Every action, beat of dialogue, and internal observation should be filtered through it.

---

### Environmental Drama — Setting Amplifies Emotion

The setting is not backdrop. It is a second character that pushes the primary emotion forward. Before writing any scene, ask: *does this location make the stakes harder or easier?*

**Genre-specific environment types are in the relevant genre file.** Load the genre file for environments mapped to your genre's emotional beats.

Universal principle: if the setting could be swapped with any other location without changing the scene — change the setting.

| Emotional beat | Universal environment choice | What it adds |
|---------------|------------------------------|--------------|
| Forced proximity | Enclosed space with no easy exit (elevator, car, small room) | No escape; whatever is between them must be dealt with here |
| Power imbalance | The antagonist's space, not the protagonist's | She is on his territory; the power imbalance is architectural |
| Aftermath | Her familiar space, now contaminated by what happened | The ordinary world is no longer neutral |

---

### Contrast — The Scene's Composition

High-contrast moments are read more slowly and remembered longer. Build at least two of these into any pivotal scene:

- **Control vs. chaos** — one character's composure against the other's fracture
- **Public face / private reality** — what they show the room vs. what the reader knows
- **What is said / what is meant** — dialogue that runs parallel to the subtext, not identical to it
- **The ordinary detail / the extraordinary stakes** — mundane action (pouring a drink, adjusting a cuff) against the weight of what is actually happening
- **Speed: slow body / fast mind** — physical movement slows to micro-beats while internal monologue accelerates

---

**Genre-specific scene techniques** are in the relevant genre file. Load `genre-romance.md` for regression/villainess/creature-fixation techniques; `genre-mystery.md` for clue architecture, investigation pacing, gothic atmosphere, and Regency social constraint; `genre-horror.md` for reveal architecture, monster problem, and terror pacing; `genre-fantasy.md` for council scenes, battle chapters, cost scenes, and world-building economy; `genre-scifi.md` for inciting violation, compliance scenes, scale reveals, and resistance cell dynamics.

---

## Chapter Hook-Out Framework — The Next Button

The hook-out is the most commercially important sentence in any chapter. It is the only sentence the reader evaluates before deciding whether to stay. Every chapter must end on forward pull, never on resolution.

**Core rule:** end mid-tension, not mid-resolution. The reader should feel like the chapter ended one beat too early — which means they must click Next to get the beat they were promised.

**Forbidden endings (rewrite flag — any of these = the chapter fails the hook-out gate):**
- Summary sentences: "It had been a long day." / "She had a lot to think about."
- Emotional generalization: "She felt hopeful for the first time in months." / "He finally felt at peace."
- Scene-closing clichés: "She closed her eyes and let herself breathe." / "She fell into a dreamless sleep."
- Perfect resolution: "Everything was going to be fine." / "She let it go."
- Going to sleep / waking up as the chapter's final beat
- Any sentence that begins with "She/He finally…" and then resolves

---

### The 10 Hook-Out Techniques

Pick the one technique per chapter that fits the emotional beat. Do not use the same technique twice in a row.

#### 1. Mid-Motion Cut
Cut inside an action, not at its completion. The reader's own momentum carries them to the next chapter.

**When:** Any chapter where something physical is about to happen. Best for early-arc chapters.

**Formula:** Describe the action beginning. Cut before it completes. Never write what happens next.
> *She reached for the door handle. Her hand closed around cold metal.*

---

#### 2. Withheld Reaction
Something significant happens. The chapter ends before the protagonist reacts. The reader must know.

**When:** Revelation moments, confrontations, admissions. The event is the beat; the reaction is the next chapter's opening.

**Formula:** [The event / the thing said.] [One physical stillness detail.] END.
> *He said it. All of it. She stood very still.*

---

#### 3. Planted Bomb
The chapter appears to resolve. The final sentence retroactively recolors everything the reader just experienced.

**When:** Best at chapter midpoints in the arc — when the reader thinks they understand the situation and the narrative needs to destabilize.

**Formula:** [Resolution paragraph — the reader thinks it's over.] [Final 1-2 sentences that shatter the premise.]
> *She locked the apartment and didn't look back. Three floors below, someone had been watching her window for two hours.*

---

#### 4. Ticking Clock
A deadline that didn't exist in the opening paragraph appears in the final paragraph.

**When:** Any chapter where the stakes need to escalate. Especially effective after quiet intimacy chapters — the contrast between the warmth of the scene and the sudden time pressure is the hook.

**Formula:** [Closing action.] [New deadline, stated specifically — not vague.] [Character acknowledges she doesn't have enough time.]
> *The deal was done. Her phone buzzed once. Forty-eight hours, the message said. She understood, for the first time, that she had miscounted.*

---

#### 5. Decision at the Threshold
The character stands at the choice. The chapter ends before the decision is made.

**When:** Any chapter whose arc is a character being pushed toward a decision. End at the maximum pressure point, not after.

**Formula:** [Forces converge on the character.] [She knows what she has to do / what she's about to do.] [END before she does it — she does not move.]
> *She had the evidence. She had the exit. She had, finally, after seven months, the window. She did not move.*

---

#### 6. The Unanswered Line
The other character's dialogue or action is the chapter's final note. Their words are still in the air when the chapter ends. The protagonist does not get to respond.

**When:** Any chapter-ending exchange between two characters. Works in any genre — romance (the love interest's charged admission), mystery (the suspect's ambiguous denial), horror (the antagonist's threat), thriller (the ally's revelation). The reader is left holding the words, with no release.

**Formula:** [Exchange builds.] [Their final line — specific, charged, or ambiguous.] [Protagonist's response reduced to one physical detail only — no interior, no speech.]
> *"I'll be here when you decide," he said. She heard the door close. She did not look.*
> *"We both know what you found," the inspector said. The room went very quiet.*

---

#### 7. Overheard / Discovered Truth
The character learns something they weren't supposed to know. The chapter ends before they process it or act.

**When:** Mystery reveals, accidental discoveries, eavesdropped conversations. The discovery is the beat; the response is the hook.

**Formula:** [Discovery moment.] [The fact stated in one sentence, flat.] [Physical stillness — the body receiving what the mind hasn't processed yet.] END.
> *The file was open on his desk. Her name was in it — not as a contact, not as a reference. As the target.*

---

#### 8. False Resolution + Detonation
Appear to fully close the chapter's tension in the penultimate paragraph. Destroy it in the final two sentences.

**When:** Late-arc chapters, chapters after a major emotional win. Let the reader exhale — then pull the floor.

**Formula:** [Full resolution paragraph — sell it.] [Line break.] [Final 1-2 sentences that erase the resolution entirely.]
> *She'd handled it. She told herself that on the walk home, in the elevator, standing at the bathroom mirror.*
>
> *Her phone rang with a number she hadn't seen in two years.*

---

#### 9. Body's Unfinished Business
The physical tension between the pairing is at maximum. The chapter cuts on held breath, not on exhale.

**When:** Any chapter ending in unresolved physical proximity — romance (near-kiss, held breath), horror (hunter and hunted inches apart), thriller (confrontation that hasn't broken yet). The reader is physiologically pulled forward.

**Formula:** [Maximum proximity established.] [One precise physical detail: his hand, her breath, the distance between them.] [Neither moves.] [One environmental detail that underlines the silence.] END.
> *His hand was still at her jaw. She had not stepped back. Outside, the city was doing what cities do at 2 AM — making noise to cover everything that wasn't being said.*

---

#### 10. The Unanswered Question
One sharp, specific question — not rhetorical — that the reader cannot answer without clicking Next.

**When:** Chapters that end on character insight or partial revelation. The insight opens the question; the chapter ends with the question open.

**Formula:** [Chapter beat resolves.] [The question emerges from the resolution — voiced or as internal monologue.] [No answer. The chapter ends on the question itself.]
> *She got in the car. She put the key in the ignition. She sat there for a long time with one thought she couldn't dismiss: if he'd known all along, why had he said nothing?*

---

### Technique Selection by Chapter Position

| Position | Recommended techniques | Avoid |
|----------|----------------------|-------|
| Ch 1–4 (early) | Mid-Motion Cut, Ticking Clock, Overheard Truth, Planted Bomb | False Resolution (reader not invested enough), Body's Unfinished Business (too early for physical tension) |
| Ch 5–(N-3) (mid) | Withheld Reaction, Decision at Threshold, The Unanswered Line, Body's Unfinished Business, Unanswered Question | Mid-Motion Cut (loses impact when overused) |
| Last 3 chapters | False Resolution + Detonation, Planted Bomb, Decision at Threshold | Ticking Clock (too mechanical at the end), Unanswered Question if it's the final chapter |
| Final chapter | Allowed to resolve — but the last paragraph must still earn the close | Any forbidden ending from the list above |

---

### Hook-Out Rewrite Protocol (if an existing chapter fails the gate)

1. Read the chapter's final 3 paragraphs.
2. Identify the chapter's primary emotional turn (what changed from opening to close).
3. Ask: *what does the reader most want to know right now that this chapter hasn't answered?*
4. Select the technique that withholds exactly that answer.
5. Rewrite the final 1–3 paragraphs only. Do not touch the rest of the chapter.
6. Verify: the new ending must end the chapter one beat before the reader expected it to end.

---

## What to Read Before Each Chapter

```
Required:
  tracking/context.md                   — previous chapter ending + open threads
  outline/outline.md                    — this chapter's role in the arc (find by chapter number)

Load only if needed:
  world/characters/{character-name}.md  — only characters appearing in this chapter
  tracking/threads.md                   — only if this chapter resolves or plants a foreshadow
  reference/{book-title}/techniques.md  — only if a reference technique is needed
```

## World & Cast Setup (required before any chapter writing)

Before expanding the outline or writing chapters, the world document must have a **Supporting Cast** section. A story with only two named characters produces flat scenes and limits cover composition to Duo.

**Minimum cast requirements for `world/worldbuilding.md`:**

```markdown
## Supporting Cast

### [Name] — [Role archetype]
- Relationship to protagonist: [see genre table below]
- Function in story: [what tension or information do they generate?]
- Distinct voice marker: [1 sentence — how they speak or behave differently from the leads]

### [Name] — [Role archetype]
...
```

**Required archetypes — pick at least 3 from your genre's table of 10:**

### Romance / Contemporary Drama
1. **Confidant** — best friend or sibling who receives the protagonist's confessions; absorbs exposition naturally; their reactions calibrate reader sympathy
2. **Romantic antagonist** — ex, rival suitor, or jealous third party who actively obstructs the central relationship
3. **Love triangle point** — a credible alternative romantic option; must be genuinely appealing, not obviously wrong
4. **Controlling authority figure** — parent, boss, or family member whose approval the protagonist needs or fears
5. **Matchmaker / orchestrator** — person who engineers proximity between the leads, knowingly or not
6. **Loyal ally with their own subplot** — friend or sibling with a romantic or personal arc running parallel; reinforces themes through contrast
7. **The messenger / witness** — someone who sees something they shouldn't, or delivers news that changes the stakes
8. **The work / world context character** — colleague, client, or professional contact who forces the leads into the same space on neutral ground
9. **Comic relief / grounding voice** — breaks tension without undercutting it; keeps the tone from becoming relentlessly serious
10. **The past made present** — someone from one lead's history who reveals a secret, complication, or wound the protagonist has kept hidden

### Fantasy / Paranormal
1. **Mentor / elder** — wizard, oracle, ancient being, or dying sovereign who holds knowledge the protagonist must earn; their power should be declining or limited
2. **Loyal companion / sidekick** — follows the hero without sharing their gift; reflects the arc back; can be killed to raise stakes
3. **Dark rival** — antagonist with mirrored power, opposing philosophy, or a claim on the same destiny
4. **Trickster / ambiguous ally** — helps and harms; true allegiance unclear until late; not evil, but not safe
5. **Council / court figure** — political power broker who forces the protagonist to navigate institutional constraint alongside magical threat
6. **The believer who is wrong** — someone whose faith in the old order or a false prophecy makes them dangerous despite good intentions
7. **The outsider / mundane anchor** — someone without magic or status who grounds the story in ordinary stakes and asks the questions the reader asks
8. **The defector from the other side** — an enemy who crosses over; brings secrets and distrust; may be a double agent
9. **The cost-bearer** — someone who pays the price of the protagonist's choices; their suffering personalizes the moral weight of power
10. **The keeper of the secret history** — archivist, scholar, or exile who knows what the official record erased; their knowledge arrives at exactly the wrong or right moment

### Mystery / Cosy Mystery / Gothic Thriller / Literary Thriller
1. **Red-herring suspect** — appears most guilty in the middle third; reader should genuinely believe them; their innocence must be earned, not announced
2. **Victim's inner circle** — friend, colleague, or lover who knew the victim best and reveals hidden motive by trying to protect someone or something
3. **Obstructive authority** — police, inspector, or institution that slows the protagonist; not incompetent — just working within different constraints
4. **The culprit** — must have a distinct voice, established presence, and at least one sympathetic trait before the reveal; their guilt must feel inevitable in retrospect
5. **The confidant / sounding board** — person the protagonist thinks through evidence with; voices the reader's doubts and pushes back on wild theories
6. **The informant / reluctant witness** — knows something but has a reason to stay silent; their silence is itself a clue
7. **The false ally** — appears to help; is concealing something (not necessarily guilt; could be shame, fear, or a separate secret)
8. **The prior victim** — someone who encountered the threat before the protagonist did and survived, escaped, or was silenced; their experience frames the protagonist's danger
9. **The community voice** — village gossip, pub regular, or local historian who holds the texture of a place and its grudges; provides colour and misdirection
10. **The character who changes the case** — late-arrival figure whose testimony, death, or disappearance forces the protagonist to restart from a new angle

### Horror
1. **Skeptic** — refuses to believe until forced to; their conversion is a structural beat; their disbelief makes the early dread feel earned
2. **First victim / cautionary figure** — establishes the threat's rules and reach before the protagonist is directly endangered
3. **Local expert / keeper** — historian, priest, old resident, or folkloric authority who holds the lore; their knowledge is partial and costs something to access
4. **Compromised ally** — possessed, coerced, mentally fracturing, or hiding their own infection; the protagonist cannot fully trust them
5. **The survivor from a prior cycle** — someone who lived through this before; traumatised, credible, and possibly unreliable
6. **The true believer / cultist** — someone who has chosen or been conditioned to serve the threat; their perspective makes the horror comprehensible without excusing it
7. **The protector who fails** — authority figure (parent, police, doctor) whose normal-world power is useless here; their failure marks the point of no return
8. **The innocent in danger** — child, dependent, or someone the protagonist is responsible for; their presence raises the cost of every decision
9. **The rationaliser** — insists on explaining everything away; useful for misdirection; must eventually be confronted with the inexplicable
10. **The one who knows and stays silent** — a character who understood the threat early and chose not to warn others; their silence is its own horror

### Sci-Fi / Dystopian
1. **Resistance cell member** — comrade with a distinct ideological angle, not just loyal; should disagree with the protagonist on method or priority
2. **True believer in the system** — enforcer or idealist who sees the protagonist as the villain; their logic should be coherent, not cartoonish
3. **Defector from the other side** — crossing over with secrets and earned distrust; their loyalty is perpetually in question
4. **Scientist / archivist with forbidden knowledge** — holds what the system erased; their knowledge creates the ethical dilemma at the story's core
5. **The compliant majority** — ordinary person who has accepted the system; their comfort makes the protagonist's resistance look irrational; their awakening (if it happens) is a turning point
6. **The handler / watcher** — regime figure assigned to monitor the protagonist; knows more than they reveal; may be an unlikely source of help
7. **The child of the system** — someone born after the change who has never known anything else; their innocence is both asset and vulnerability
8. **The black marketeer / information broker** — operates in the cracks between systems; helps for price, not principle; cannot be fully trusted
9. **The tech or protocol expert** — knows how the surveillance, the AI, or the infrastructure actually works; their knowledge is the protagonist's operational edge
10. **The ghost of the before** — someone who remembers the old world (or was shaped by it); their nostalgia is either wisdom or blindness, and the protagonist must determine which

### Historical / Regency
1. **Social gatekeeper** — hostess, matriarch, or gossip who controls reputation access; their approval or disapproval changes what is possible for the protagonist
2. **Rival or jealous peer** — same-class competitor with a different motive from the main antagonist; creates horizontal social pressure
3. **Confidant-servant or companion** — hears secrets by virtue of lower rank; sees the same events from a different vantage and provides corrective irony
4. **The reformer or outsider** — tradesman, foreigner, colonial subject, or political radical whose presence disrupts period social assumptions and forces the protagonist to examine their own position
5. **The family obligation** — sibling, ward, or dependent whose welfare the protagonist is responsible for; their needs constrain choices and create moral conflict
6. **The old scandal** — a person connected to a secret in the protagonist's or love interest's past; their reappearance destabilises the present
7. **The match-maker with an agenda** — parent, aunt, or sponsor engineering a marriage for reasons that may not align with the protagonist's interests
8. **The sympathetic enemy** — someone whose opposition is rooted in legitimate grievance, not malice; their conflict with the protagonist is the most interesting in the book
9. **The witness to the private self** — a character who has seen the protagonist outside their public role and holds that knowledge, whether as ally, threat, or complication
10. **The institution made human** — a character who embodies the period's dominant institution (the church, the law, the military, the court) and whose personal humanity complicates the protagonist's relationship to that power

Secondary characters must appear in **at least 2 chapters each**. They exist to create scenes beyond "just the two leads talking" — every secondary character unlocks a scene type that is impossible without them.

---

## Parallel Writing (default for new books)

Use this flow whenever writing ≥ 2 chapters from scratch. Single-chapter incremental additions use the sequential process below.

### Step 1 — Expand outline beats

Before spawning any agents, expand `outline/outline.md` so every chapter has a concrete beat entry:

```
Ch-NNN: [primary emotion] | hook: {1-sentence} | turn: {what changes} | hook-out: {open question}
```

All chapters must have this before any parallel writing starts. The beat entries replace `tracking/context.md` as the coordination signal during parallel writing.

### Step 2 — Spawn one Agent per chapter

Spawn all chapter agents concurrently. To avoid redundant file reads, read shared context once in the main context and pass it into each agent's prompt:

- **Read once, share with every agent:**
  - `world/worldbuilding.md`
  - Full expanded `outline/outline.md` (with beat entries for all chapters)
- **Read once, shard per agent:**
  - `world/characters/{character-name}.md` — only for characters appearing in that chapter
- **Coordination signal:** each agent receives the previous chapter's hook-out line from the outline beat.

Each agent writes to `content/{book-title}/chapters/ch-NNN-{title}.md` and returns its own hook-out line.

Use a **single batch Agent call** when the environment supports it (e.g. one Agent invocation carrying the whole chapter list), otherwise spawn individual Agents per chapter. Either way, all chapters must be produced in parallel, not sequentially.

### Step 3 — Lightweight continuity pass

After all chapter agents complete, do a single sequential pass:
1. Read chapters in order; verify hook-out of chapter N matches the opening of chapter N+1.
2. Fix only continuity breaks — do not rewrite prose for style.
3. Write `tracking/context.md` from the final chapter's ending.
4. Update `tracking/threads.md`, `tracking/timeline.md`, `tracking/character-status.md`.

Keep this pass minimal. Do not run a full quality rewrite here; that is Phase 4.

### Multiple books in parallel

Spawn one top-level Agent per book. Pass only that book's `world/`, `outline/`, and character files so each agent starts with a minimal context. Books share no state and can complete in any order.

## Single Chapter Writing Process

Use this for adding one chapter to an existing book (incremental update only).

1. Read `tracking/context.md` — know the exact last beat.
2. Read the chapter's outline entry in `outline/outline.md`.
3. Name the chapter's **primary emotion** (tension / release / shock / ache / warmth).
4. Name the chapter's **turn**: what changes from start to end?
5. Write the **hook** (≤3 sentences): drop into motion, not setup.
6. Write the **escalation**: raise stakes through action/dialogue. No passive reflection blocks.
7. Write the **turn**: the moment that changes something — reveal, decision, or loss.
8. Write the **hook-out**: end mid-motion or on an open question. Never summarize.
9. Save to `content/{book-title}/chapters/ch-NNN-{title}.md` from the project root, with correct zero-padded number.
10. Update `tracking/context.md`: last beat + open threads + any foreshadow planted.
11. Update `tracking/threads.md` if foreshadow added or resolved.
12. Update `tracking/character-status.md` for any character changes.

## Chapter File Format

```md
---
title: "Chapter One: Night Crossing"
chapter: 1
---

Prose starts here — no leading blank line.
```

Frontmatter is optional but recommended. The site loader falls back to filename if `title` is absent.

Prose formatting rules:
- Adjacent paragraphs: blank line between them (`\n\n`). Within a paragraph, do not hard-wrap lines. (CommonMark renders a single `\n` as a space, collapsing all paragraphs into one block.)
- Dialogue quotes: half-width double quotes `""`
- No `……` or `——` in the prose product — rewrite as action, short sentence, or line break
- No chapter summaries or author notes inline

## Title Craft — Book & Chapter Titles

Titles are clickable surface area. A reader sees the book title before the cover loads, and scans the chapter list before committing to read. Both must do work, not just label.

### Book Titles

The book title appears on the home grid, the book detail hero, browser tabs, and every share card. It is the single most-repeated piece of text for the book. It must promise a specific emotional experience — not describe the plot.

**The bar:** a strong book title creates a question or a tension the reader wants resolved. "Convenient Husband" works because *convenient* and *husband* are in productive conflict. "The Garden" does not work as a book title — it describes a location, promises nothing.

| Pattern | Mechanism | Examples |
|---------|-----------|----------|
| **Possessive + charged noun** | Ownership implies a power dynamic | *The CEO's Obsession*, *The Devil's Debt* |
| **Oxymoron / productive conflict** | Two words that shouldn't sit together | *Convenient Husband*, *Borrowed Time*, *Cartel Prince* |
| **Loaded object as metaphor** | A concrete object that carries the whole theme | *Mark of the Moon*, *Iron Veil*, *Blood and Velvet* |
| **Stakes-in-two-words** | Names the irreversible thing | *Protocol Zero*, *Dead Frequency*, *The Last Crown* |
| **Threat/promise verb phrase** | Implies action already in motion | *Alpha Claimed*, *Dragon in Debt* |

**Banned book titles:**
- Pure location or object with no charge: *The Garden*, *The House*, *The Library*
- Character name alone (unless the name itself is iconic to the premise)
- Generic genre words: *Desire*, *Passion*, *Forbidden*, *Temptation* — these signal "every romance" and rank for nothing
- Abstract emotion nouns: *Longing*, *Yearning*, *Hope*

**Test:** say the title aloud, then ask "a story about what?" If the answer is fully contained in the title with no tension left, the title is flat. The title should make someone *ask* the question, not answer it.

### Chapter Titles

Chapter titles appear in the book detail chapter list — the reader scans them to gauge momentum before committing. A list of flat nouns ("The Arrival", "Names", "The Garden") reads as low-energy and kills scroll-through. A list of charged titles makes the reader want to read just to find out what each one means.

**Core rule:** a chapter title should be a small hook — it raises a question the chapter answers, or names a turn without giving it away. It must never spoil the chapter's turn.

| Technique | What it does | Examples |
|-----------|-------------|----------|
| **The loaded fragment** | A phrase pulled from the chapter's most charged line | *The Real Reason*, *What Stays*, *Speaking for Herself* |
| **The countdown / number** | A specific number that implies a clock or stakes | *Seven Days*, *Forty-Seven Steps*, *Twelve Marks* |
| **The withheld noun** | Names a thing without explaining it | *The Hackney Claim*, *Pack Recognition*, *The List* |
| **The quiet menace** | Innocuous words made ominous by the genre | *Documented*, *Something Permanent*, *Below Again* |
| **The line of dialogue** | A short charged quote from the chapter | *"I Know About the Mark"*, *"You Knew"* |

**Banned chapter titles:**
- Bare setting labels: *The Garden*, *The Hall*, *The Arrival*, *Night* — a place is not a hook
- Generic beats: *The Meeting*, *The Talk*, *The Decision* — names the function, not the tension
- Single flat nouns with no charge: *Names*, *Morning*, *Home*
- Titles that spoil the turn: if the chapter's twist is that he betrays her, do not title it *The Betrayal*

**Pattern across the chapter list:** vary the techniques down the list — don't title every chapter with a number, or every chapter with a fragment. The list itself should have rhythm. Escalate menace as the arc climbs: early chapters can be quieter, late-arc titles should feel heavier.

**Test:** read the full chapter list top to bottom as if it were a table of contents on the book detail page. Does it build? Does each title make you mildly curious? If three consecutive titles are flat nouns, rewrite them.

## Chapter Count Planning

When writing a new book, decide the total chapter count before expanding the outline. Pick a number in the 10–20 range that fits the story's scope. **Never pick the same number as another book in the same site.** Treat the count as a story decision, not a quota:

- A tight revenge arc might need 11 chapters.
- A slow-burn romance with multiple subplots might need 17.
- A high-stakes thriller with many POVs might run to 20.

Document the chosen count in `outline/outline.md` header before writing any beat entries.

## Pacing Guidelines

Word counts are targets, not uniform quotas. Let each chapter breathe according to its dramatic weight — a chapter that needs 4,200 words should not be trimmed to hit a round number, and a lean 1,800-word chapter is fine if it lands the turn cleanly. Vary lengths across the book so readers feel the rhythm shift.

| Chapter type | Word count range | Dialogue ratio | Action beats |
| --- | --- | --- | --- |
| Opening chapter | 1,800–2,500 | 20–30% | 3+ |
| Escalation chapter | 1,500–2,200 | 30–50% | 2–4 |
| Climax chapter | 1,400–2,000 | 15–25% | 4–6 |
| Resolution chapter | 1,200–1,800 | 20–40% | 1–2 |

## Context Handoff (`tracking/context.md` template)

```md
## Last Chapter Ending
{Final action or dialogue — 1–3 sentences}

## Next Chapter Start
{Which action or scene to continue from}

## Open Threads
- {foreshadow/suspense 1}
- {foreshadow/suspense 2}

## Target Emotion for Next Chapter
{tension / release / shock / lingering regret / warmth}
```

Always overwrite `context.md` after each chapter. Do not append history — the file is a rolling handoff.

## Quality Check Before Saving

- Hook: does it drop into motion? No weather, backstory, or setup.
- Turn: does something change? A chapter where nothing changes is a filler chapter.
- Hook-out: does it create forward pull? Reader must want the next chapter.
- No consecutive paragraphs with identical rhythm or length.
- No three consecutive sentences starting with the same subject.
- **Hook-out gate:** does the final sentence / final paragraph use one of the 10 named techniques from §"Chapter Hook-Out Framework"? Any forbidden ending (summary, emotional generalization, going to sleep, "finally…resolved") is a mandatory rewrite — do not ship the chapter until this passes.
- **One-paragraph test:** does the opening paragraph make the reader feel something in the first three sentences? If it only establishes setting or backstory, cut to the tension.
- **Named emotion check:** does every pivotal scene have a specific named emotional state (from the genre file's Named Emotion table)? Generic emotions ("nervous", "angry", "interested") are a rewrite flag.
- **Dynamic check:** is it clear who holds the power in this scene and who is off-balance? If all characters feel equally matched, the scene has no subtext.
- **Setting check:** does the location amplify the emotional stakes, or could it be any room? If it's interchangeable, change it.
- If AI flavor is detected, flag the chapter for the Phase 4 deslop pass — do not run `/story-deslop` inline here. Phase 4 (`references/story-deslop.md`) is loaded separately and runs after all chapters are written.

## Book Description & Tagline (Required — write before cover generation)

After chapters are complete, write the `tagline` and `description` fields for `src/lib/books.ts`. These appear on the book detail page and are the primary click trigger for every reader who arrives at the site. Apply the same hook standards as the cover: tension + question + desire, all three.

### Tagline (1–3 short sentences)

One sentence is ideal. Two is the maximum. It must reveal the core irony of the situation — what she came for vs. what she got, what was supposed to be simple vs. what it became.

**Banned:** genre labels ("enemies-to-lovers", "fated mates", "dark romance"), passive descriptions ("a story about"), vague emotional promises ("a journey of self-discovery").

**Patterns — pick the one that fits:**

| Pattern | Formula | Example |
|---------|---------|---------|
| **Action → consequence** | [what she did] → [the thing that happened because of it] | "She mapped his world. He had no defense against that." |
| **Intent + ironic reversal** | [what she came to do]. [what he did instead]. | "She came to end him. He made her the only person he trusted." |
| **Three escalating beats** | One [setup]. One [complication]. One [the real problem]. | "One qualifying spot. One fake relationship. One very real problem." |
| **Plan + role + failure** | [His plan]. [Her assigned role]. [Why the role failed]. | "He had a plan. She was supposed to be a variable. She was not a variable." |
| **She/He didn't expect** | [What she went in to do]. [What she didn't expect]. | "She crossed the Veil to complete a survey. She didn't expect to be claimed before she could cross back." |
| **Title-as-peak-state (fantasy / progression)** | Name the protagonist's achievement state or core power mechanic, not a thematic abstraction. | "Hundredfold Dominion", "The Last Cartographer of the Shattered Court", "Iron Sovereign" |

### Description (4–6 sentences)

Back-cover copy, not a plot summary. Each sentence has a job:

| Sentence | Job | What it must do |
|----------|-----|----------------|
| **1 — Protagonist state** | Who she is + why she's there | Names the character + the specific ordinary-world goal. Not "a woman who" — a person doing a specific thing. |
| **2 — The collision** | What went wrong when he entered | The inciting event in one sentence. What changed. "She didn't expect X." "X happened instead." |
| **3 — The exchange** | What each needs from the other | "[Character A] needs [X]. [Character B] needs [Y]." The transactional logic of the forced proximity or central conflict. |
| **4 — The third variable** | What neither planned for | This is the actual story. The thing the arrangement didn't account for. Must be specific, not vague. |
| **5 — Stakes (optional)** | What happens if they fail or succeed | Only include if it sharpens the hook. Cut if it reads like a plot outline. |
| **6 — The feeling (optional)** | The emotional impossibility in one image | One sentence that makes the reader feel the situation rather than understand it. |

**Genre-specific synopsis formulas** are in the relevant genre file. Load `genre-romance.md` for Formulas G/H/I (regression, villainess, monster romance); `genre-mystery.md` for Formula J; `genre-fantasy.md` for Formula K; `genre-scifi.md` for the sci-fi/dystopian formula; `genre-horror.md` for the horror formula.

---

### Self-Aware Genre Declaration (Fantasy / Sci-Fi / Progression — closing sentence only)

After 3–4 sentences of plot hook, close the synopsis for fantasy, sci-fi, or progression titles with one sentence that names the emotional register and genre promise explicitly. This sentence is for the recommendation algorithm and the reader's genre filter — it is not literary, it is pitch:

**Formula:** `This is a [genre adjective] [genre noun] about [emotional core 1], [emotional core 2], and [protagonist's transformation or peak state].`

**Example:** "This is a cinematic sci-fi progression saga about strategy, bloodline, and the birth of a monarch in ruins."

**Rule:** use ONLY as the final sentence, never as the opening. Do NOT use for romance titles — the hook sentence performs this function through emotional identification instead.

---

### Suspense Layer — The Information Gap (Required)

The description must **withhold** at least one piece of critical information. The reader should finish reading and immediately need to click — not because the story sounds good, but because there is a specific thing they don't know yet and cannot tolerate not knowing.

**The technique:** reveal that something exists, without revealing what it is or why it matters. The gap between "this thing exists" and "what this thing means" is the click trigger.

**Withheld-detail patterns:**

| Type | Formula | Example |
|------|---------|---------|
| **The counter-intuitive fact** | State a fact that demands explanation | "He fired her three times. She came back each time. On the fourth, he stopped trying." |
| **The incomplete revelation** | Something happened — the description doesn't say what | "She found the letter. Everything after that is his fault." |
| **The already-happened twist** | A consequence is named, not the cause | "By the time she understood what she'd agreed to, she was already in his city, in his life." |
| **The double secret** | Both characters are hiding the same category of thing | "She's been lying to him for six weeks. He's known for five." |
| **The unanswered question (explicit)** | End with a direct question the reader must click to answer | "The question she can't answer: which one of them is more dangerous?" |
| **The counter-expectation** | The setup happens, then one sentence undercuts it | "The wedding happens. That's not the problem." |
| **The withheld identity** | One character knows something about the other that the reader knows they know | "The man who bought her contract doesn't know she's the person who destroyed his company five years ago. She's counting on that." |

**Suspense check:** after writing the description, ask — *what specific thing does the reader not know that they now need to know?* If the answer is "nothing, it's all there" — add a withheld detail. If the answer is "the whole plot" (too vague) — make it specific. The withheld detail must be one sentence away from being revealed; the reader should feel they are *this close* to the answer.

**New tagline pattern — The Withheld Fact:**

| Pattern | Formula | Example |
|---------|---------|---------|
| **The withheld fact** | [Something happened]. [What it means is not said]. | "She found what he'd been hiding. She didn't tell him what she planned to do about it." |

---

**Quality check — one-second test:** if someone reads only the tagline and the first sentence of description, do they feel something and want to know more? If the answer is only "this sounds like a romance novel" — rewrite. The goal is "I need to know how this ends."

**Banned patterns:**
- Trope labels in reader-facing copy: `enemies-to-lovers`, `fake dating`, `fated mates`, `alpha male`
- Passive construction: "a story is told of...", "discover the world of..."
- Vague stakes: "everything they know will be tested", "nothing will ever be the same"
- Suspense that is too vague to be specific: "dark secrets", "hidden truth", "nothing is as it seems" — name the specific thing that is hidden, or don't mention it
- Placeholder description: do not ship a `description: ""` or `description: "Coming soon."`

### GEO Layer — AI-Citability (apply to Sentence 1 of every description)

The first sentence of `description` is used verbatim in `llms.txt` and as the page `<meta description>`. AI retrieval engines (Perplexity, ChatGPT, Claude web) cite the first sentence of structured content most frequently. Write Sentence 1 as a **self-contained relational triple** — Subject → Relationship → Object — that remains fully intelligible with no surrounding context:

**Formula:** `[Character A] [relationship dynamic] [Character B] — [the irreversible consequence].`

| Bad (context-dependent) | Good (self-contained) |
|-------------------------|----------------------|
| "She didn't expect this." | "A contract lawyer discovers her new client is the man who destroyed her firm — and he doesn't recognize her." |
| "Everything changed that night." | "A cartel bride fakes her own death to escape her arranged marriage; the cartel's enforcer is sent to retrieve her." |
| "Their worlds collide." | "A billionaire CEO hires his legal adversary as his temporary wife — she's the only one who can destroy him, and she knows it." |

This requirement does **not** change the hook writing standards above — the full description is still written for emotional impact. Only Sentence 1 must additionally satisfy the self-contained test.

---

## After All Chapters Written → Cover Generation (automatic, no prompt)

After the `tagline` and `description` are written and added to `src/lib/books.ts`, **immediately load `story-cover.md` and generate the cover** — do not ask whether to proceed. This is always the next step after the final chapter is saved.
