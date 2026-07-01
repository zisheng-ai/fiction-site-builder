# Story Short Write

Load this reference when the user asks to write a short story or flash fiction.

## Niche Research Input

Before writing a new short story, check `outputs/{site-slug}/{book-slug}/niche-research.json`:

- **Exists** → read `differentiation_angle`, `selected_tropes`, and `adsense_policy.high_risk_notes`. Anchor the emotional hook and twist to these.
- **Does not exist + user gave explicit genre/premise** → proceed directly.
- **Does not exist + no explicit brief** → run `fiction-niche-researcher.md` first, then return here.

## Core Principles

1. **Emotion before story**: Lock the target reader emotion before plotting. All structure serves that emotion.
2. **One twist, total commitment**: Every line of setup exists for the twist. No sub-plots, no world-building.
3. **Every sentence earns its place**: If a sentence doesn't advance plot, build toward the twist, or raise emotion — cut it.
4. **Opening 3 sentences are everything**: Hook or lose the reader. Ending creates shareability.
5. **Default first-person**: First-person narration creates the strongest reader identification in web fiction.

## Emotion Targets

Pick one before starting. The entire story structure flows from this choice.

| Target emotion | Best for | Difficulty | Market heat |
| --- | --- | --- | --- |
| Lingering regret | Romance, missed connection | Medium | High |
| Twist shock | Suspense, identity reversal | Hard | High |
| Cathartic release | Face-slapping, reversal of fortune | Easy | Medium |
| Healing warmth | Growth, family, friendship | Medium | Medium |
| Creeping dread | Psychological, suspense | Hard | Low-Medium |
| Resonant emotion | Realist, workplace, marriage | Medium | High |

## Writing Process

### Step 1: Lock the emotion and framework

Answer before writing any prose:

```
Target emotion: {choose one from the table above}
One-line premise: {protagonist + predicament + reversal + emotional landing}
Core twist: {one sentence}
Opening hook: {first 3 sentences — must contain suspense or conflict}
Closing echo: {final sentence — must have resonance or impact}
```

Save as `content/short/{story-title}/setup.md` from the project root.

### Step 2: Beat outline

Write a beat-level outline with section markers. Target 6–12 beats for 8,000–20,000 characters.

```md
### 1. Hook — {action/conflict that hooks immediately}
### 2. Setup — {introduce character situation, raise stakes}
### 3. Misdirection 1 — {first misdirection or setup detail}
### 4. Misdirection 2 — {second misdirection, tighten tension}
### 5. False resolution — {appears to resolve, but raises new question}
### 6. Twist — {the twist, from a single unambiguous moment}
### 7. Resonance — {emotional landing, last image or line}
```

**For mystery / suspense short form**, use the investigation beat structure instead:

```md
### 1. Hook — {the crime, wrong, or anomaly — discovered in the first scene, not reported}
### 2. Position — {why she is the one who will solve it; her access, knowledge, or relationship to the victim}
### 3. Clue 1 — {first piece of evidence planted inside a normal scene action; not announced as a clue}
### 4. Red herring — {the obvious explanation and why it seems correct; the reader should believe it}
### 5. Clue 2 — {the impossible clue — one detail that doesn't fit; protagonist notices but can't yet use it}
### 6. Reveal — {the protagonist connects Clue 1 + Clue 2; the red herring collapses; truth visible}
### 7. Confrontation or consequence — {what happens next: confrontation with the culprit, or the cost of knowing}
```

The investigation beat structure replaces misdirection-based beats for whodunit and mystery short form. The key difference: clues are **found inside other scenes** (they piggyback on action the story already needed), not in dedicated "I search for clues" scenes.

Save as `content/short/{story-title}/beat-outline.md` from the project root.

### Step 3: Write prose

Write full prose section by section following the beat outline. Save all to `content/short/{story-title}/prose.md` from the project root.

Prose formatting:
- Adjacent paragraphs: single `\n` between them — no blank lines
- Dialogue: half-width double quotes `""`
- Section markers: `### 1.` / `### 2.` — consistent throughout
- No `……` or `——` — rewrite as action, short sentence, or line break

## Romance Heat Level (Short Form)

Apply when the genre is romance or the premise has a central pairing.

### Target Heat Level

**Default: steamy / closed-door at peak, non-graphic.** Matches `fiction-niche-researcher.md` AdSense safety policy. Build tension with sensation, breath, skin, pressure — fade at the peak intimate moment; stop before explicit sexual acts.

In short form, heat is almost always tension-only or tension-plus-first-kiss. Escalated intimacy scenes belong in long form (and fade at peak there too). In 8,000–20,000 characters, one well-written almost-kiss or first kiss is worth more than a full scene.

---

### Short-Form Tension Toolkit

**Slow the clock at the peak.** The story can move fast everywhere else. The one charged moment gets full real-time treatment — fragment sentences, micro-beats, every sensation named.

**Body-first, thought-second.** Show the physical symptom before naming the feeling.
> *Her pulse moved into her throat. She stepped back. He followed — one step, no more.*

**The interrupted moment as the story's payoff.** Short romance often resolves at the almost-kiss, not past it. The interruption IS the ending — the reader supplies the rest. This is structurally correct for short form.

**Escalate contact in sequence.** Even in 8,000 characters, track the physical ladder: eye contact → proximity → touch → held contact. Don't jump from eye contact to a kiss without the rungs between.

**Charged dialogue.** Words that mean one thing and signal another. Short form lives here.
> *"You should leave," she said.*
> *He didn't move. "I know."*

---

### Vocabulary

**Use:** `skin`, `heat`, `pulse`, `breath`, `jaw`, `throat`, `hands`, `lips`, `exhale`, `pressure`, `warmth`, `closer`, `the space between them`

**Avoid:** explicit anatomical terms (AdSense violation), `throbbing / heaving / moist / quivering` (cliché), `they made love` without any preceding sensation (too vague)

---

### Heat Positioning in Short Form

| Story section | Heat beat |
|--------------|-----------|
| Setup (first 20%) | Awareness. Character notices — something specific, not generic attractiveness. |
| Rising action (20–70%) | Proximity, accidental or forced contact. Charged dialogue. |
| Climax beat (70–85%) | The almost-kiss, first kiss, or the moment one character admits what they want. |
| Resolution (85–100%) | Emotional landing. The heat is acknowledged or deliberately not — both are valid. |

The heat climax should arrive before the story's emotional climax, not after. Let the physical moment open up the emotional resolution.

---

## Mystery & Suspense Short Form

Apply when the genre is mystery, cosy mystery, gothic, psychological suspense, or literary thriller. This section replaces "Romance Heat Level" for these genres — the structural parallel is dread escalation rather than physical tension escalation.

### The Short-Form Mystery Standard

Mystery short form lives or dies on **one well-planted clue** and **one genuine twist**. The twist must arise from information the reader was given — not from information withheld until the reveal. The reader should be able to re-read the story and see the answer was always there.

**The three-sentence test:** read the story's first three sentences. If the reader does not have a question they need answered, the story starts too late. Mystery opens in the middle of the wrong thing already happening — not in the setup to it.

---

### Short-Form Dread Toolkit

**Plant the clue inside action.** The clue should appear while the protagonist is doing something else — pouring tea, leaving a room, answering a question. The reader registers it; neither character makes it significant. This is the only kind of clue that works in short form: the one that looks like scene detail.

**One red herring, one redirect.** Short form can sustain one misdirection, not three. Plant the obvious explanation early (around the 20% mark), let the reader settle into it, then deploy the impossible clue at the 65–70% mark. The redirect is not a twist — it is a re-examination of what was already shown.

**Make the reveal physical.** The moment of deduction should arrive through a sensory trigger, not through narration. She picks up an object, reads a line twice, sees two things in the same frame. Explain nothing — let the protagonist's action show the connection. The reader should reach the conclusion one sentence before she names it.

**Dread is cumulative.** Even in short form, build dread by repeating one wrong detail in two different scenes. The second occurrence is when the reader's attention sharpens. The third is when the protagonist's does.

**The closing image.** Mystery short form ends on an image, not an explanation. The last sentence shows the consequence or the weight of knowing — it does not summarize what happened. The reader should feel the cost or the chill, not receive a verdict.

---

### Dread Positioning in Short Form

| Story section | Dread beat |
|--------------|-----------|
| Opening (first 15%) | The wrong thing, already in motion. The reader is dropped into the anomaly. |
| Rising action (15–65%) | Clue planted inside action. Red herring established. Protagonist pursues wrong theory. |
| Turn (65–75%) | The impossible clue. Cannot fit the current theory. The protagonist notices and can't dismiss it. |
| Reveal (75–90%) | The connection made. Physical trigger. The wrong theory collapses. |
| Closing (90–100%) | The cost or consequence of knowing. One image. No summary. |

---

### Vocabulary: Mystery Register

**Use freely:**
`shadow`, `wrong`, `silence`, `watch`, `still`, `cold`, `weight`, `careful`, `close`, `pattern`, `the thing she noticed`, `the thing she hadn't noticed until now`, `the explanation that fit`, `the detail that didn't`

**Use sparingly (once per story maximum):**
`fear`, `certain`, `understand` — these land hardest when used once, at the turn

**Avoid:**
`dark and stormy` clichés for atmosphere (earn the weather through character state, not as stage dressing), `suddenly` as a tension device (if the reader needs "suddenly," the scene didn't build correctly), any direct statement of the solution before the protagonist reaches it

---

### Cosy Mystery Tone Register

Cosy mystery is a distinct sub-register: **warmth + darkness in deliberate balance**. The village is charming; the poison is real. Write both with equal conviction — neither the warmth nor the death should be ironic.

**Cosy tone rules:**
- The protagonist is competent and readable — her intelligence is the reader's pleasure, not her suffering
- Community and routine are load-bearing; the crime is a violation of the domestic order the story values
- The culprit is someone the reader (and protagonist) liked — the betrayal is the genre's emotional core
- Resolution restores order; the final scene should feel like the village exhaling

**Cosy pacing:** the investigation is also the reader's excuse to spend time in a world they enjoy. Do not rush clues. Let a scene have two purposes: the clue AND the vicarage tea, the clue AND the market gossip. The second purpose is not padding — it is the genre's promise to the reader.

---

### Gothic Short Form

Gothic short form does not resolve — it **reveals the shape of the wrongness**. The reader does not need to know what happened; they need to understand, at the end, what the protagonist now understands. The revelation may be that the house is dangerous, that the other person is not what they seemed, that she has been deceived — but it need not name the mechanism. The feeling of understanding, without full explanation, is the gothic ending.

**Gothic short form checklist:**
- [ ] The setting is doing half the narrative work — not described, but active
- [ ] One ordinary object has been made uncanny
- [ ] The protagonist's certainty has been eroded by the end — she is less sure of something she was sure of at the start
- [ ] The final image is ambiguous enough to linger

---

## Short Story Quality Checks

- Hook (first 3 sentences): contains a question, conflict, or unusual detail?
- Twist: arrives from setup, not from nowhere?
- Ending: has one image or line that lingers?
- No consecutive 3+ sentences with identical syntactic structure.
- Total word count: 8,000–20,000 characters for a self-contained short story.

## After Story Completion → Cover Generation (automatic, no prompt)

When the story passes quality checks, **immediately load `story-cover.md` and generate the cover** — do not ask the user whether to proceed. This is always the next step.

## Reference Book Integration

If the user has a reference book to emulate:

1. Read `{story-title}/reference/{book-title}/teardown.md` and `techniques.md`.
2. Extract: twist positioning, pacing of misdirection, sentence-level technique.
3. Add a brief "Reference Summary" section at the bottom of `setup.md`.
4. During Step 3, pull 1–2 specific techniques per section from the summary — do not copy, emulate.

If no reference exists, use the genre emotion table to select a structural template before writing.

