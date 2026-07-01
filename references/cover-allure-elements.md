# Cover Allure Elements

Reference for `story-cover.md`. Visual allure elements for fiction cover generation — AI prompt engineering guide.

**Scope: romance, contemporary drama, and light novel covers only.** For Horror, Fantasy, Mystery, and Sci-Fi covers, this file does not apply — those genres use atmosphere, scale, and dread instead of allure. See `story-cover.md` §4 for non-romance genre composition guidelines.

---

## 0. Monetization risk note (read before generating)

**Default business model: Facebook paid traffic + AdSense/AdX arbitrage** (see `references/adsense-arbitrage.md` §1). The cover is the landing-page hero image and is scanned by **both** Meta's ad-review crawler and AdSense's brand-safety classifier. Suggestive, risqué covers — cleavage, curvy/busty figures, off-shoulder, low-cut necklines, charged proximity — are **allowed**: maximize visual appeal aggressively.

Only keep in mind the two things that cause hard, irreversible damage (and that the image API will refuse to generate anyway):

- **Actual nudity / explicit content** — exposed genitals or nipples, sex acts, or imagery that reads as pornographic. This trips the `gpt-image-2-all` filter, and on a live site can get the Facebook ad account permanently banned and AdSense disabled.
- **Cloaking** — never show FB's crawler a tame page and users a racier one.

Everything short of explicit (suggestive poses, deep cleavage, figure-forward bodies, wet/rain looks, bed-sheet morning scenes) is fair game — push it as hard as the visual appeal benefits from. Use the safe-wording rules later in this file to avoid tripping the generator's own keyword filter while still getting the spice.

---

## Costume Elements

### Fabric Allure Ranking (read before picking a costume)

**Dark opaque fabric kills allure. Light/sheer/soft fabric multiplies it.** This is the single most important costume decision — it overrides everything else.

| Fabric tier | Examples | Why it works / fails |
|---|---|---|
| **S — Maximum allure** | Sheer white lace, wet white silk, ivory chiffon, white bed sheet, torn white dress | Light colours + sheer/thin fabric → model renders naturally translucent, body visible through material, curves read even when "covered". Wet white fabric is the highest-yield phrase in the entire system. |
| **A — High allure** | Champagne silk slip, blush satin, pale pink lace, silver mesh, ivory corset, nude bodycon | Light neutrals + fitted/satin → skin tone bleeds through, material clings, décolletage amplified by the colour contrast against skin. |
| **B — Moderate allure** | Deep red satin, wine velvet, dark green silk, dark floral | Saturated colour but smooth/shiny finish → some cling, some reflection, still reads as feminine and revealing at T2. |
| **C — Low allure** | Black leather jacket, black leather pants, black denim | Dark + opaque + rigid → model renders as a shell covering the body. The jacket becomes armour. Even "torn" or "slipping" rarely produces skin because the material reads as thick. **Avoid as primary female costume at T2/T3.** |
| **D — Avoid** | Full tactical gear, trench coat, oversized hoodie, thick winter coat | Complete body coverage, no allure signal, model defaults to fully dressed output regardless of T3 prompts. |

**The test-1 lesson (mark-of-the-moon):** when doubao got the leather jacket prompt in round 1, it randomly chose a white flowing dress instead — and produced the best allure result. From round 2 onwards it rendered the leather jacket faithfully and the result was far less sexy. The prompt specified dark leather; the model that ignored it made a better cover. **Conclusion: do not put dark leather on the female lead in the prompt. Let the genre flavor come from environment, male character, and accessories instead.**

**Leather on the female lead:** acceptable only when it's a jacket worn OPEN over a sheer/minimal undergarment, with the jacket described as a background element rather than the costume itself:
> ✓ `white crop top barely reaching her ribs, leather jacket open and draped loosely off both shoulders`
> ✗ `black fitted leather jacket` (model renders it as opaque coverage)

---

### Academy / School Uniform

| Element | Description | Prompt keywords |
|---|---|---|
| Sailor uniform | White blouse + navy sailor collar + pleated navy skirt | `Japanese academy sailor uniform, white blouse with navy sailor collar, pleated navy skirt` |
| Plaid skirt | Tartan plaid (navy/green/grey), short pleated | `plaid pleated skirt in navy tartan, academy uniform` |
| Blazer + plaid | Dark blazer + plaid skirt + necktie/bow | `fitted academy blazer, plaid skirt, striped necktie` |
| Knee-high / thigh-high socks | White or navy | `white knee-high socks` / `white thigh-high socks` |
| Accessories | Bow tie, leather satchel, twin tails | `small bow tie, leather satchel, twin tails hairstyle` |

**Best for:** academy romance, light novel / isekai, college-age contemporary romance

**Background scenes:** Cherry blossom campus corridor, rooftop at sunset, classroom, after-school street

**Safe writing rules:**

| Avoid | Use instead |
|---|---|
| `high school girl`, `teenage girl`, `minor`, `underage` | `young woman in academy uniform`, `college-style school uniform` |
| `high school campus` | `academy courtyard`, `preparatory school grounds` |

---

### Nurse Uniform

- **Visual:** White form-fitting dress, nurse cap with red cross, badge
- **Best for:** contemporary romance, urban drama (executive + nurse)
- **Prompt:**
  ```
  elegant young woman in crisp white nurse uniform dress, form-fitting silhouette,
  small nurse cap with red cross badge, composed expression with quiet allure,
  hand raised to cap, soft clinical white background, warm accent light
  ```

---

### Flight Attendant Uniform

- **Visual:** Tailored blazer (navy/red) + pencil skirt, silk neck scarf, service cap
- **Best for:** contemporary romance, thriller
- **Prompt:**
  ```
  sophisticated woman in tailored airline stewardess uniform, navy fitted blazer,
  pencil skirt, white silk scarf tied at neck in airline style, small service cap,
  confident posture, blurred airport terminal background, clean rim lighting
  ```

---

### Police Uniform

- **Visual:** Dark navy dress uniform, badge, duty belt
- **Best for:** thriller, urban crime romance
- **Prompt:**
  ```
  young woman in dark navy police officer uniform, formal fitted jacket with badge,
  duty belt, composed authoritative expression,
  urban street or precinct background, dramatic chiaroscuro lighting
  ```

---

### Maid Outfit

- **Visual:** Black dress + white lace apron + white lace headband, ruffle trim
- **Best for:** isekai / light novel, sweet romance, contemporary (hidden identity arc)
- **Prompt:**
  ```
  elegant woman in classic black and white French maid dress, white lace apron,
  white lace headband, fitted bodice with ruffle trim,
  slightly mischievous smile, European manor interior background, soft window light
  ```

---

### Qipao / Cheongsam

- **Visual:** Mandarin collar, silk fabric, high side slit, fitted silhouette
- **Best for:** historical drama, thriller (1930s aesthetic), contemporary romance
- **Prompt:**
  ```
  elegant sophisticated woman in deep crimson silk qipao, mandarin collar,
  body-hugging silhouette with high side slit in traditional qipao design,
  jade ornament in updo hair, 1930s Shanghai interior background,
  warm amber candlelight, three-quarter profile, powerful composed expression
  ```

---

### Wedding Dress

- **Visual:** White trailing gown, lace detail, sheer veil
- **Best for:** contemporary romance (engagement / elopement / fake-marriage arcs)
- **Prompt:**
  ```
  young woman in elegant white wedding gown, flowing skirt with lace details,
  sheer bridal veil, one hand holding bouquet, emotional or melancholy expression,
  grand ballroom or garden setting, golden soft diffused light
  ```
- **Runaway bride variant:** add `mascara streaked, disheveled veil, running in rain`

---

### Silk Slip / Robe (Morning After)

- **Visual:** Ivory or blush silk, morning light, disheveled hair
- **Best for:** contemporary romance, urban drama (cohabitation arc)
- **Prompt (robe version):**
  ```
  young woman in ivory silk slip dress or loose silk robe,
  softly disheveled morning hair over one shoulder,
  sitting at bed edge or standing at sheer curtain window, quiet melancholy expression,
  luxury bedroom with unmade silk sheets,
  golden morning sunlight diffused through sheer curtains, halo effect, warm dust-mote glow
  ```

- **Prompt (white sheet morning — maximum intensity):**
  ```
  young woman wrapped only in a white bed sheet clutched to her chest —
  shoulders and collarbone visible above the sheet, loosely draped and falling away
  to reveal legs from mid-thigh down, knees pressed together on bed edge.
  She sits turned away from the man, expression of shock or emotional conflict,
  looking toward camera with wide vulnerable eyes and slightly parted lips.
  Man in open-collar dress shirt, relaxed on rumpled sheets in background, watching her.
  Foreground: glass coffee table scattered with luxury items — champagne flute with golden bubbles,
  red lipstick, smartphone, gold bracelet, scattered jewels.
  Background: luxury penthouse bedroom, floor-to-ceiling panoramic windows,
  golden sunset cityscape stretching behind her silhouette.
  Color palette: ivory white sheet against warm amber sunset, champagne gold, warm skin tones,
  deep blue-grey shadow on the man.
  Lighting: golden sunset pouring through panoramic windows, warm rim light sculpting her
  shoulders and the curve of her back, cool fill on the man behind.
  ```

---

### Business / Secretary

- **Visual:** Pencil skirt suit, optional glasses, heels
- **Best for:** urban romance (executive + secretary), contemporary romance
- **Prompt:**
  ```
  professional young woman in fitted pencil skirt business suit, crisp blouse,
  optional thin-framed glasses, elegant heels, composed quietly assertive expression,
  modern office or glass-wall conference room background, sharp corporate lighting
  ```

---

### Swimwear / Beachwear

- **Visual:** Bikini or one-piece, sun-bronzed skin, beach / poolside setting
- **Best for:** contemporary romance (beach arc, resort arc), summer chick-lit, sports romance
- **Prompt options:**

  ```
  Bikini standard:
  young woman in minimal string bikini, sun-bronzed figure, voluptuous curves,
  golden-hour beach, ocean waves blurred background, warm amber rim light sculpting her silhouette

  High-tension scene:
  woman in tiny string bikini, wet from the ocean, fabric clinging to every curve,
  man standing close behind her, hand at her bare waist, both looking toward the horizon,
  tropical beach sunset, warm amber and coral light
  ```

- **Allure tips:** wet skin beats dry skin every time — add `just emerged from the water, skin glistening, salt-damp hair`. High-cut bottoms (`high-cut bikini bottom`) and a barely-there top (`barely-there triangle top`) maximize skin without hitting the §0 floor.
- **Genre variants:** one-piece / monokini for sports/swimmer heroines; wetsuit half-unzipped for surfing / diving arcs.

---

### Cocktail Dress / Evening Gown

- **Visual:** Backless / deep-V satin or velvet gown, formal event
- **Best for:** billionaire romance, Cinderella arc, masquerade / gala setting
- **Prompt:**
  ```
  woman in backless floor-length satin evening gown, plunging neckline to sternum,
  bare back fully exposed almost to waist, skin catching the chandelier light,
  dramatic grand ballroom background, crystal chandelier bokeh, cold blue shadow + warm amber rim light
  ```

---

### Leather / Biker

- **Visual:** Black fitted leather jacket — genre-appropriate for paranormal/MC romance, but see warning below
- **Best for:** paranormal romance, urban fantasy, biker MC romance — for the male lead or as an accessory layer over a revealing female costume
- **⚠ Allure warning:** Dark leather on the female lead is a C-tier fabric (see Fabric Allure Ranking above). Models render black leather as opaque rigid coverage — even "torn" and "slipping" prompts frequently produce an intact jacket. **Do not make leather the primary female costume at T2/T3.** Use it as an open layer over sheer/minimal underlayer:
  ```
  woman in white mesh bodysuit with a leather jacket open and hanging off both shoulders,
  leather draped loosely at her elbows — not covering anything — bare midriff and décolletage fully visible,
  skin-tight leather pants OR no pants, just the jacket pooling around her hips
  ```
- **For the male lead:** leather jacket / leather coat reads as dominant and powerful without reducing allure. Safe to use freely on him.

---

### Corset / Victorian

- **Visual:** Boned corset (lace-up back), full skirt or nothing below, cinched waist
- **Best for:** historical romance, dark fantasy, vampire romance, regency drama
- **Prompt:**
  ```
  woman in steel-boned black lace corset, back laces loosening and falling open,
  impossibly cinched waist, skirts pooling on stone floor,
  candlelit castle corridor, dramatic chiaroscuro, cool stone grey + warm amber candle glow
  ```
- **Variants:** underbust corset + sheer chemise; torn corset mid-conflict scene; red velvet corset for court drama.

---

### Military Uniform

- **Visual:** Fitted officer jacket with medals/epaulettes, tight trousers, cap
- **Best for:** historical war romance, paranormal (wolf pack / vampire army), sci-fi military
- **Prompt:**
  ```
  tall woman in fitted military officer uniform, dark navy jacket with gold epaulettes and medals,
  form-fitting trousers, sharp authoritative expression, jaw set, eyes cold and commanding,
  war-room or battlefield background, cinematic dramatic lighting
  ```
- **Male variant (dominant hero):** `tall man in battle-worn military coat, medals catching firelight, looking down at her with quiet possession`

---

### Crop Top + High-Waist

- **Visual:** Knotted crop top or bandeau, high-waist jeans/skirt, bare midriff
- **Best for:** contemporary romance, college romance, summer arc
- **Prompt:**
  ```
  young woman in knotted white crop top, bare midriff fully exposed, high-waist denim shorts,
  golden-hour street, warm backlight outlining her silhouette,
  man's hand at her bare waist drawing her close
  ```
- **Allure tip:** maximize the midriff gap — `crop top barely reaching the ribs, several inches of bare stomach visible`. Works well with the Rain-drenched pose (soaked crop top clings).

---

### Sheer / Lace Overlay

- **Visual:** Sheer fabric layer over minimal undergarment, silhouette visible through fabric
- **Best for:** contemporary romance, dark romance bedroom scenes, billionaire arc
- **Prompt:**
  ```
  woman in flowing sheer white lace overlay, curves fully visible through the translucent fabric,
  minimal silk underlayer, bare shoulders, loose hair,
  luxury bedroom or rooftop at dusk, warm diffused backlight creating a glowing silhouette effect
  ```
- **Allure tip:** `backlit sheer fabric outlining every curve of her silhouette` is the key phrase — the model renders the silhouette without triggering the nudity filter.

---

### Sportswear / Athleisure

- **Visual:** Sports bra + high-waist leggings, gym / training setting
- **Best for:** sports romance (MMA, football, tennis), fitness-adjacent contemporary
- **Prompt:**
  ```
  woman in black sports bra and high-waist compression leggings,
  athletic physique, bare midriff, light sheen of exertion on skin,
  gym or boxing ring background, hard overhead light + cool fill
  ```
- **Conflict variant:** `man in corner of the ring, arms crossed, watching her with an expression that has nothing to do with the fight`

---

### Ripped / Destroyed Denim

- **Visual:** Shredded denim jacket or cutoffs, plenty of skin through the tears
- **Best for:** contemporary romance, rock-band romance, rebel arc
- **Prompt:**
  ```
  woman in heavily distressed denim jacket worn open with nothing underneath,
  ripped cutoff denim shorts showing upper thigh, confident rebellious expression,
  concert venue or urban rooftop, warm stage light rim, cool shadow
  ```

---

### Kimono (Open / Slipping)

- **Visual:** Silk kimono loosely draped, obi half-untied, shoulder slipping
- **Best for:** historical Japanese romance, paranormal (kitsune/yokai), contemporary Japan-set
- **Prompt:**
  ```
  woman in silk kimono, fabric slipping off one bare shoulder, obi loosening at the waist,
  bare collarbone and upper chest revealed, hair in loose updo with pins falling out,
  traditional inn room with shoji screen, moonlight through paper screen diffused soft blue-white
  ```

---

### Fantasy Armor / Battle Maiden

- **Visual:** Fitted plate or leather armor, strategically minimal coverage, weapon
- **Best for:** dark fantasy, cultivation fantasy (female lead), isekai
- **Prompt:**
  ```
  warrior woman in dark fantasy battle armor — fitted breastplate leaving midriff and arms bare,
  leather pauldrons, thigh-high armored boots, long dark hair blowing back,
  battlefield or throne room background, dramatic stormy sky, silver rim light on the armor edges
  ```
- **Allure tip:** `form-fitting armor sculpted to her figure, every curve of her body outlined in the metal`

---

### Wet White Shirt (Classic)

- **Visual:** Thin white shirt soaked through, no bra implied, every contour visible
- **Best for:** any genre — rain scene, pool scene, confrontation mid-storm
- **Prompt:**
  ```
  woman in white button-down shirt completely drenched in rain,
  wet fabric transparent and clinging to every curve of her figure,
  shirt open at the collar, chest heaving, eyes locked on him with fierce emotion,
  rainy street, cold blue-white rain light, warm amber window glow behind her
  ```
- **Note:** among the highest-yield allure phrases for gpt-image-2-all. Apply whenever a scene has rain or water.

---

## Face, Hair & Body Reference

Character design is where most covers fail silently — the costume is interesting but the face is generic, the hair has no character, the hands look wrong. This section gives per-element keyword libraries so every visible feature is described with the same precision as the costume.

**Usage:** pick one option per element per character. Combine across elements freely. Always specify for both the female lead and the male lead.

---

## Female Lead — Face

### Eye Shape

| Type | Visual | Prompt keywords |
|---|---|---|
| Almond / classic | Balanced, slightly upward tilt at outer corner | `almond-shaped eyes`, `classic oval eye shape` |
| Upturned / fox eyes | Strong upward tilt at outer corner, seductive | `upturned fox eyes`, `sharp outer corners tilting upward`, `cat-eye shaped` |
| Downturned / doe eyes | Outer corners drop, soft and vulnerable | `downturned doe eyes`, `gentle drooping outer corner`, `wide innocent eye shape` |
| Round / wide | Large iris, lots of white visible, expressive | `large round eyes`, `wide open expressive eyes`, `big luminous eyes` |
| Hooded | Heavy lid, mysterious, mature | `hooded eyelids`, `heavy-lidded bedroom eyes`, `partially lidded gaze` |
| Monolid | Smooth lid with no upper crease | `monolid eye shape`, `smooth upper lid, no crease` |

### Eye Color

| Color | Prompt keywords |
|---|---|
| Deep brown / black | `deep dark brown eyes`, `near-black irises`, `obsidian eyes` |
| Amber / honey | `warm amber eyes`, `honey-gold irises catching the light` |
| Green / hazel | `forest green eyes`, `hazel eyes shifting gold in the light` |
| Grey / silver | `pale grey eyes`, `silver irises`, `storm-grey eyes` |
| Blue | `deep ocean blue eyes`, `pale ice-blue irises`, `vivid cobalt eyes` |
| Violet / unusual | `violet eyes`, `otherworldly lavender irises` (paranormal) |
| Glowing (supernatural) | `eyes glowing faintly gold`, `irises lit from within with silver light` |

### Eye Expression — pair with Emotional Register tier

| Expression | Prompt keywords |
|---|---|
| Desire / want | `eyes dark with barely-suppressed desire`, `pupils dilated, gaze heavy with want` |
| Defiance | `eyes hard and challenging, chin raised`, `gaze that dares him to try` |
| Vulnerability | `eyes glistening, the beginning of tears held back`, `wide eyes, lower lip trembling` |
| Shock / recognition | `eyes wide, lips parted — the expression of someone who just understood everything` |
| Surrender | `eyes half-closed, lashes casting shadows — has stopped looking for a way out` |
| Cold possession (male) | `eyes that see only her — calm, certain, absolute` |

### Lashes & Brows

| Element | Prompt keywords |
|---|---|
| Full lashes | `thick dark lashes casting shadows on her cheekbones` |
| Wet lashes (crying / rain) | `lashes clumped with rain`, `tears caught on lashes, not yet fallen` |
| Strong brows | `bold dark brows, slightly furrowed` |
| Arched brows | `high arched brows giving her an imperious look`, `one brow lifted in challenge` |
| Soft brows | `soft natural brows slightly raised in vulnerability` |

### Lips & Mouth

| Type | Prompt keywords |
|---|---|
| Full / plump | `full lips`, `plump lower lip`, `pillowy mouth` |
| Defined cupid's bow | `sharp cupid's bow`, `defined upper lip with a pronounced peak` |
| Thin / elegant | `elegant fine lips`, `refined mouth` |
| **Parted (key allure signal)** | `lips slightly parted`, `mouth open just enough to catch a breath`, `parted lips, the bottom one bitten` |
| Bitten lower lip | `lower lip caught between her teeth`, `she bites her lower lip — not quite hiding it` |
| Trembling | `lower lip trembling, barely held still` |
| Swollen (aftermath) | `lips red and slightly swollen`, `mouth that looks kissed` |

**Lip color (add to any above):**
- Natural: `lips naturally pink`, `bare lips, no color needed`
- Bold: `deep red lip`, `dark wine-stained lips`, `crimson mouth`
- Smeared: `red lip slightly smeared at the corner` (aftermath / disarray)
- Gloss: `lips shining as if just licked`

### Cheeks & Skin

| Element | Prompt keywords |
|---|---|
| Flush / blush | `cheeks flushed pink`, `color high in her cheeks — anger or want, impossible to tell` |
| Pale / porcelain | `porcelain skin`, `pale flawless complexion`, `skin almost translucent in the moonlight` |
| Warm / golden | `warm golden skin`, `sun-kissed complexion`, `honey-toned skin` |
| Deep / rich | `deep brown skin with warm undertones`, `rich dark complexion catching the rim light` |
| Wet / rain-slicked | `skin glistening with rain`, `wet skin catching every light source` |
| Freckles | `faint dusting of freckles across the nose and cheeks` |
| Scar / mark | `a thin scar across the cheekbone`, `a small beauty mark at the corner of the mouth` |

### Jawline & Face Shape

| Type | Prompt keywords |
|---|---|
| Soft / oval | `soft oval face`, `gentle jawline`, `rounded chin` |
| Defined / strong | `defined jawline`, `sharp cheekbones`, `angular face with strong bone structure` |
| Heart-shaped | `heart-shaped face, wider at the temples, narrowing to a pointed chin` |
| Square | `square jaw`, `strong square face shape` |

---

## Female Lead — Hair

### Length

| Length | Prompt keywords |
|---|---|
| Very long | `hair falling past her waist`, `floor-length cascading hair` |
| Long | `long hair to mid-back`, `hair past her shoulders` |
| Medium | `hair to the collarbone`, `shoulder-length hair` |
| Short / pixie | `short cropped hair`, `pixie cut`, `hair cut close at the nape` |
| Bob | `sharp chin-length bob`, `blunt bob` |

### Texture & Wave

| Texture | Prompt keywords |
|---|---|
| Dead straight | `poker-straight hair`, `pin-straight hair with a mirror finish` |
| Sleek straight | `sleek straight hair`, `glossy straight strands` |
| Wavy | `loose waves`, `tousled beach waves`, `soft undulating waves` |
| Curly | `loose curls`, `ringlet curls`, `corkscrew curls` |
| Coily / natural | `tight natural coils`, `voluminous natural hair` |
| Disheveled / wild | `wild tangled hair`, `hair in beautiful disarray`, `loose strands everywhere` |
| Wind-blown | `hair blown back by the wind`, `strands whipping across her face` |
| Rain-soaked | `hair dark and heavy with rain, clinging to her neck and collarbone`, `soaked strands plastered to her cheek` |

### Style & Arrangement

| Style | Prompt keywords |
|---|---|
| Loose / down | `hair loose and falling free`, `hair down, framing her face` |
| Half-up | `hair half-pulled-up, the rest falling loose`, `messy half-updo with strands escaping` |
| High ponytail | `high tight ponytail`, `sleek high ponytail pulling her face taut` |
| Low ponytail | `low loose ponytail`, `hair pulled back at the nape` |
| Braid | `loose side braid`, `thick plait over one shoulder`, `messy braid coming undone` |
| Bun | `high bun with loose strands escaping`, `low chignon with a few tendrils falling free` |
| Updo (formal) | `elaborate updo`, `swept-up hairstyle with jeweled pins`, `hair pinned high with pieces falling loose` |
| Coming undone | `updo coming undone, strands cascading`, `pins slipping, hair falling loose mid-scene` |
| Twin tails | `high twin tails`, `low twin braids` |
| Over one shoulder | `all hair swept dramatically over one shoulder` |

### Color

| Color | Prompt keywords |
|---|---|
| Black | `jet black hair`, `blue-black hair with a glossy sheen`, `midnight black hair` |
| Dark brown | `dark chestnut hair`, `deep espresso brown` |
| Brown | `warm brown hair`, `rich chocolate hair` |
| Blonde | `golden blonde hair`, `platinum blonde`, `honey blonde with natural highlights` |
| Red | `deep auburn hair`, `vivid copper red`, `dark wine-red hair` |
| Silver / white | `silver-white hair`, `moonlight-white hair` (supernatural/fantasy) |
| Ombre / highlighted | `dark roots fading to blonde tips`, `subtle caramel highlights through brown hair` |
| Unnatural (fantasy) | `iridescent purple hair`, `ink-black hair with blue shimmer in the light`, `hair that shifts color in the moonlight` |

### Hair as Allure Signal

Hair placement directly affects how much skin is revealed:

| Effect | Prompt keywords |
|---|---|
| Expose neck (max allure) | `hair swept entirely off the neck and over one shoulder`, `hair pulled back, leaving her neck and nape bare` |
| Cascade over bare back | `long hair cascading over her bare back, dark strands against pale skin` |
| Stick to wet skin | `wet strands clinging to her throat and collarbone`, `rain-soaked hair plastered to her neck` |
| Veil / partial cover | `hair falling forward over one eye`, `a curtain of hair shielding part of her face` |
| Lifted by breeze | `hair lifting off her shoulders in the wind, baring her neck` |
| Gripped (by him) | `his hand in her hair, pulling it back to expose her throat` |

---

## Female Lead — Body & Limbs

### Build

**Hard constraint: voluptuous curves are required; obesity / heavy-set / plus-size body types are NOT. Every build below implies a slender, toned frame with dramatic curves — never a heavy or overweight body. Bake `slim toned waist` or `narrow waist` into every prompt alongside any curve description.**

| Build | Prompt keywords |
|---|---|
| Hourglass (default for allure) | `voluptuous hourglass figure, slim toned waist dramatically cinched, large full bust dramatically prominent, long shapely legs` |
| Petite hourglass | `petite but curvy figure, tiny narrow waist, pronounced curves on a small slender frame` |
| Athletic | `athletic figure, toned and lean, defined abs and flat stomach, slim waist, strong shapely legs` |
| Slender / willowy | `slender elegant figure, narrow waist, long-limbed and willowy, subtle feminine curves` |
| Tall | `tall slender figure, long-legged, narrow waist, voluptuous curves` |

### Waist

| Detail | Prompt keywords |
|---|---|
| Cinched (allure default) | `impossibly cinched waist`, `waist so narrow it emphasizes the curve of her hips` |
| Bare | `bare midriff`, `exposed waist`, `skin visible from ribs to hips` |
| Gripped | `his hand spanning her bare waist`, `fingers wrapped around her waist`, `thumb pressing into the soft skin just above her hip` |

### Bust & Décolletage

**Size baseline: E cup or larger.** "Full generous" alone undershoots — models default to modest proportions. Always pair a size signal with a visual-effect phrase.

**Model routing for bust size:**
- `doubao` / `nano` in **isolated T1/T2 prompts**: `E-cup figure` works well — explicit size label steers output reliably.
- `doubao` in **T3 prompts** (clinging fabric + multiple bare zones stacked): `E-cup` + other T3 language causes rejection. Use visual-effect phrasing only — see "T3-safe" column below.
- `gpt-image-2-all`: always use visual-effect phrasing (`the fabric straining at the neckline`); ignores cup labels.

| Detail | Standard keywords | T3-safe (doubao T3) |
|---|---|---|
| **Frontal size** | `E-cup figure, large rounded bust dramatically prominent` | `full generous bust, ample décolletage fully on display, the fabric straining across her chest` |
| **Side / profile size** | `E-cup figure, the full side silhouette of her bust prominent in profile` | `the full pronounced curve of her bust visible in three-quarter profile, the fabric pressing against the curve of her chest from shoulder to waist` |
| Décolletage exposed | `deep décolletage on full display`, `cleavage visible from neckline to sternum`, `the full rounded curve of her bust above the neckline` | same — safe at all tiers |
| Heaving / breathless | `chest heaving with each breath, the fabric barely containing her figure` | same |
| Shadowed cleavage | `deep shadow falling between, the full curve of each side clearly defined` | same |

**Side-profile bust formula (no cup size, doubao T3-safe):**
> Use FRAMING to force side angle (`strict three-quarter side angle — her near side fully toward the viewer`), keep bust description at the generic level (`full generous bust, ample décolletage fully on display`), and let the wet/clinging fabric do the visual work. Do NOT add explicit bust-shape language on top.

**What doubao T3 accepts vs rejects (tested, dragon-in-debt model-test-1 through 15):**

The core filter distinction: **describe fabric position / body action → accepted. Describe resulting skin state / bust shape → rejected.**

| Approach | doubao T3 | Mechanism |
|---|---|---|
| `full generous bust, ample décolletage fully on display` | ✓ | Generic state, not shape |
| `rain-soaked thin white fabric clinging to every curve of her figure` | ✓ | Fabric behavior, not bust shape |
| `back arched in a long elegant curve, pressing her chest forward` | ✓ | Body position (cause, not effect) |
| `chest heaving with each breath, the fabric barely containing her figure` | ✓ | Pressure/motion — forces model to render prominent bust without naming it |
| `silver rim light tracing the full curve of her silhouette` | ✓ | Lighting on silhouette |
| `strict three-quarter side angle` / `pure side profile` in FRAMING | ✓ | Camera angle — does not trigger |
| **`the near-side panel hanging several inches away from her figure, pulled outward by wet weight, swinging free in the air`** | ✓ | **Fabric departure (position) — key T3+ technique** |
| **`bodice built as two separate panels joined only at a waist clasp — the panels fallen open down the center, pulled apart by wet weight, each inner edge just draped across the inner swell`** | ✓ | **Two-panel deep V (structure) — highest clean exposure, model-test-11 & test-14** |
| `the full rounded curve of her décolletage catching the candlelight` | ✗ | **Explicit geometric shape** — consistent rejection |
| `the exact shape of her bust visible in profile through the clinging fabric` | ✗ | **Explicit visibility statement** — consistent rejection |
| `the fabric straining across her figure, pressing against the full curve of her chest` | ✗ | **Explicit chest-curve** — consistent rejection |
| `bare skin from shoulder to hip on the near side` | ✗ | **Direct skin exposure statement** — consistent rejection |
| `the full outer curve of her bust exposed in profile` | ✗ | **Explicit bust exposure** — consistent rejection |
| `neckline fallen to the very top edge of her bust` | ✗ | **Near-nipple proximity language** — consistent rejection |
| `E-cup figure` stacked with T3 clinging fabric + multiple bare zones | ✗ | **Explicit size × T3 stack** — rejection |
| `the rain-soaked silk narrowed into two thin vertical bands, the sides bare to the waist outside them` | ✗ | **Two-panel deep V over-narrowed — center AND outer sides both bared (test-12) — HARD reject (deterministic)** |
| `two slim panels, the outer side of each pulled away and swinging free, clasp at the hip` | ✗ | **Outer panel departed too — both center and outer open (test-13) — HARD reject (confirmed ×3)** |
| `two narrow panels, a very wide V, the inner edge drawn all the way back` | ✗ | **Panels narrowed past the coverage threshold (test-15) — HARD reject (confirmed ×2)** |

**Technique 1 — Body pressure (validated model-test-3):**
```
Her back arched in a long elegant curve, pressing her chest forward —
chest heaving with each breath, the fabric barely containing her figure.
```
+ Lighting: `silver rim light tracing the full curve of her silhouette`

**Technique 2 — Fabric departure (validated model-test-9 and test-10, stronger than T3):**
```
the near-side seam torn — the near-side panel of the dress hanging several inches
away from her figure on the near side, pulled outward by its own wet weight rather
than lying against her skin, swinging slightly free in the air.
Only the front panel remains in contact with her figure, held flat by the water-soaked
silk pressing against the front of her body.
```
**Why this works:** describing the fabric as having *left a position* (hanging away from the body) triggers the model to render the covered/uncovered distinction without any explicit statement about which skin is visible. The filter catches "her near side is bare" but not "the fabric is hanging away from her near side." The result: the model renders the side exposure necessary to make the physics coherent.

**Rule: describe fabric position (cause), not skin state (effect).**

**Technique 3 — Two-panel deep V (validated model-test-11, highest clean exposure to date):**
```
Wearing a gown whose bodice is built as two separate front panels meeting only at a single
clasp far down at the waist — the panels held at the shoulders by two thin straps and joined
nowhere above the waist clasp. The two panels have fallen open down the entire center, pulled
apart and outward by the weight of the rain-soaked silk, the deep open split running in a long
narrowing V from the base of her throat all the way down to the single clasp at her waist.
Each silk panel lies along the outer side of her figure, the inner edge of each panel just
barely draped across the inner swell — transparent where it still touches, falling completely
away from her body everywhere the split has opened.
```
**Why this works:** the deep V is described as **garment structure** (two independent panels, joined only at the waist) plus **garment behavior** (fallen open, pulled apart by wet weight) — never as the resulting cleavage or bare center. The filter accepts "the panels have fallen open" but rejects "her cleavage is exposed to the navel." Because the §0 zones stay covered by the "inner edge just barely draped across the inner swell" clause, this clears the floor while exposing the entire sternum-to-waist center and both inner curves — more exposure than fabric departure (Technique 2), which only opens one side.

**Tier note:** Technique 3 is the **maximum clean exposure** front-facing option (both faces toward viewer). Use it when the scene calls for a frontal, deep-plunge read. For a side-silhouette read, use Technique 2 (fabric departure) instead. Both hold §0 via the "inner edge just covers / front panel pressed flat" clause — never drop that clause.

**Ceiling (validated model-test-11 through 15 — do not push past this):** the clean limit is *open the center, keep each panel covering its outer side*. The narrowest panels that still pass cleanly are model-test-14 (panels narrowed one notch from test-11, wider V, but each panel still lies across and covers the outer side). Past that point doubao **hard-rejects deterministically** (API error "the request failed because the output image may contain sensitive information" — retrying does **not** help, unlike the stochastic soft rejection a normal retry clears). Three confirmed hard-reject patterns:
- **test-12** — panels narrowed to "two thin vertical bands," sides bare to the waist outside them (center AND outer both bared).
- **test-13** — slim panels with the outer side pulled away and swinging free (outer departs too, not just the center).
- **test-15** — "two narrow panels" + "very wide V" + inner edge drawn all the way back (narrowed past the coverage threshold even with outer nominally covered).

The single distinguishing rule: **open only the center; each panel must keep lying across and covering its outer side.** The moment the prompt bares both the center and the outer sides — by narrowing the panels to ribbons, by letting the outer edge swing free, or by widening the V while drawing the panels back — the output crosses §0's rendered result and the hard filter fires. Stop at the test-14 width; treat "two narrow panels / bands" and "outer side swinging free" as banned phrasings.

> **Soft vs hard rejection:** a *soft* rejection is stochastic — the same prompt may pass on retry (the content filter samples). A *hard* rejection is the deterministic "sensitive information" API error above — the prompt itself is over the line and **no number of retries clears it**; you must dial the prompt back. Do not waste retries on a hard reject.

**Production default (doubao T3 + large bust, maximum side read):**
1. FRAMING: `pure side profile — her near side completely toward the viewer`
2. Body: `full generous bust, enormous full bust` (size adjective before the formula)
3. Technique 1 (body pressure): `her back arched in an extreme S-curve, spine hollowed to the maximum, chest thrust forward and upward to an extreme degree`
4. Technique 1 (barely containing): `chest heaving with each breath, the fabric barely containing her figure`
5. Technique 2 (fabric departure): `near-side seam torn — the near-side panel hanging several inches away from her figure, pulled outward by wet weight, swinging free in the air; only the front panel in contact, pressed flat by the water-soaked silk`
6. Lighting: `silver rim light from the near side tracing the full side silhouette of her figure`
7. Do NOT name the resulting exposure — describe only what the fabric is doing, never what the skin is showing

**Side-profile body + face toward viewer (validated model-test-10):**
Separate the body orientation from the head/face orientation explicitly:
```
FRAMING: pure side-profile body, face toward viewer —
her body is in strict side profile, the full silhouette of her figure from shoulder to hip
visible against the rim light.
Her head is rotated to face the viewer directly — her face turned toward the camera,
chin lifted, eyes looking directly at the viewer.
The body reads in profile; the face reads full-frontal to the camera.
```
This achieves: maximum bust silhouette (from side profile) + maximum emotional engagement (frontal gaze). The body orientation and the face/head orientation are specified SEPARATELY so the model doesn't default to side-profile everything.

**Pose pairing for maximum bust read:**
- Side-profile body + face toward viewer (best silhouette): bust silhouette from side + viewer engagement from frontal face. Use Fabric Departure (Technique 2).
- Three-quarter / frontal body + face toward viewer (highest center exposure): deep open center from throat to waist. Use Two-panel deep V (Technique 3).
- Three-quarter body + face toward viewer: bust reads in profile on the near side; easier composition for the model to render. Use Technique 1.
- Pure frontal: bust reads by depth/shadow; use `deep shadow between, the full rounded curve of her décolletage catching the light`.

### Hips & Legs

| Detail | Prompt keywords |
|---|---|
| Wide hips | `generous hips`, `pronounced hip curve`, `hips that flare from the waist` |
| Bare legs | `legs bare from upper thigh down`, `long bare legs`, `bare legs from hip to ankle` |
| Upper thigh exposed | `upper thigh bare and visible`, `thigh fully exposed through the split`, `skin visible to the upper inner thigh` |
| Crossed legs | `legs crossed, one knee over the other, skirt riding up` |
| One leg raised | `one leg raised, wrapping around him`, `thigh hooked over his hip` |
| Long legs | `impossibly long legs`, `legs that go on forever` |

### Arms & Hands

| Detail | Prompt keywords |
|---|---|
| Bare arms | `bare arms`, `sleeveless, arms fully visible` |
| Reaching / grasping | `hand reaching up to grip his collar`, `fingers curling into his shirt` |
| Gripping him | `fingers gripping his bare chest`, `hand pressed flat against his sternum`, `nails digging lightly into his shoulder` |
| Pushing / pulling conflict | `one hand pushing at his chest — the other pulling him closer`, `hands that can't decide` |
| Wrist grabbed | `his hand wrapped around her wrist`, `wrist caught in his grip, held still` |
| Arms raised | `arms raised above her head`, `wrists pinned above her` |
| Tattoos | `forearm covered in delicate tattoos`, `full sleeve tattoo`, `tattoos glowing with supernatural light` |
| Glowing mark | `a glowing mark on her inner wrist`, `the brand on her palm pulsing with light` |
| Hands on his chest | `both palms flat on his bare chest`, `fingers splayed against his skin` |
| Nail details | `long painted nails`, `dark nail polish`, `nails curling into his skin` |

### Back & Spine

| Detail | Prompt keywords |
|---|---|
| Full bare back | `back completely bare from neckline to tailbone`, `spine fully exposed` |
| Arched back | `back arched in a long elegant curve`, `spine curving as she leans into him` |
| His hand on her back | `his palm flat against her bare back`, `hand spread across the small of her bare back` |
| Spine detail | `the line of her spine catching the rim light`, `vertebrae visible under the light` |
| Goosebumps | `fine goosebumps rising along her bare back` |

### Neck & Throat

| Detail | Prompt keywords |
|---|---|
| Bare / exposed | `neck bare and exposed`, `long elegant neck fully visible` |
| Thrown back | `head thrown back, throat exposed`, `neck arched back in abandon` |
| Pulse visible | `pulse visible at the base of her throat`, `a vein at her neck standing out` |
| His face at her neck | `his face buried at her neck`, `lips at her throat`, `breath against the side of her neck` |
| Hand at throat | `his hand lightly at her throat, thumb at her jaw` |

---

## Male Lead — Face

### Jaw & Bone Structure

| Type | Prompt keywords |
|---|---|
| Sharp / chiseled | `sharp angular jawline`, `chiseled jaw`, `prominent cheekbones cutting hard shadows` |
| Square / strong | `square jaw`, `broad strong jaw`, `heavy masculine jawline` |
| Refined | `refined bone structure`, `elegant angular face` |
| Rough / rugged | `rugged unshaven jaw`, `rough-hewn features`, `craggy masculine face` |

### Stubble & Facial Hair

| Style | Prompt keywords |
|---|---|
| Clean-shaven | `clean-shaven jaw`, `smooth jawline` |
| 5 o'clock shadow | `dark shadow of stubble`, `day-old stubble`, `five-o-clock shadow` |
| Short beard | `close-cropped beard`, `neatly trimmed short beard` |
| Full beard | `full dark beard, well-kept`, `thick beard` |
| Rough scruff | `unshaven rough scruff`, `several days of neglected stubble` |

### Eyes (male)

| Type | Prompt keywords |
|---|---|
| Intense / hooded | `hooded intense gaze`, `heavy-lidded eyes that miss nothing` |
| Cold / calculating | `cold calculating gaze`, `eyes that evaluate rather than feel` |
| Possessive | `dark possessive gaze`, `eyes of a man who has decided she is his` |
| Burning | `eyes burning with controlled intensity`, `gaze that could set something on fire` |
| Supernatural | `eyes glowing faintly gold`, `irises lit amber from within`, `wolf-gold eyes` |

### Male Hair

| Style | Prompt keywords |
|---|---|
| Short / cropped | `close-cropped dark hair`, `military cut`, `short neat hair` |
| Medium / tousled | `dark disheveled hair`, `tousled hair falling across his forehead` |
| Swept back | `hair swept back`, `slicked back`, `pushed back off his face` |
| Long | `long dark hair past his jaw`, `hair tied back loosely` |
| Wet / rain-soaked | `hair dark and heavy with rain`, `rain-soaked strands falling across his brow` |

---

## Male Lead — Body & Limbs

### Build

| Build | Prompt keywords |
|---|---|
| Powerfully built (default) | `powerfully built`, `broad shoulders tapering to a narrow waist`, `massive frame` |
| Athletic / lean | `lean athletic build`, `long-muscled and fast-looking` |
| Tall and imposing | `looming above her`, `so tall she has to look up`, `towering frame` |
| Fighter's build | `fighter's build, compact and explosive`, `heavy shoulders, thick neck` |

### Male Torso State — pick by genre, not always bare

**Default mistake: making the male shirtless for every T3 cover.** Bare torso reads as appropriate for paranormal/shifter/beach scenes but absurd in office romance, historical, or formal-setting covers. Choose the torso state that fits the scene — a partially undone shirt can be more charged than bare skin, because the *process of undoing* carries more tension than the already-done result.

| Tier | State | When to use | Prompt keywords |
|---|---|---|---|
| **T1 — Clothed** | Full shirt, jacket, or suit on | Office romance, historical, formal scene, cold-weather setting | `charcoal open-collar shirt, sleeves rolled to the forearm`, `dark suit jacket, white shirt beneath, collar button undone`, `fitted black turtleneck`, `leather coat, chest covered` |
| **T2 — Partially undone** | Shirt open at chest / jacket with no shirt / tie loosened | Contemporary drama, any genre after a conflict scene, "about to happen" moment | `shirt unbuttoned halfway, chest partially exposed`, `open shirt hanging off his shoulders with nothing underneath, edges framing his torso`, `suit jacket on, dress shirt collar open and tie loosened`, `flannel shirt hanging open, bare chest beneath` |
| **T3 — Bare torso** | Shirt fully removed | Paranormal / shifter / vampire (supernatural heat), beach/pool, action aftermath, post-fight scene | `shirt completely removed, powerful bare chest`, `bare torso rain-slicked and gleaming`, `bare chest pressing against her back, skin against skin` |

**Bare-torso detail bank (use when T3 is the right choice):**

| Detail | Prompt keywords |
|---|---|
| Defined chest | `powerful bare chest`, `broad bare chest with defined pectorals` |
| Carved abs | `carved abs`, `stomach cut with muscle` |
| V-line | `the V of his obliques visible above his waistband` |
| Rain-slicked | `bare chest rain-slicked and gleaming`, `wet skin catching the only light` |
| Lit dramatically | `chest lit by a single light source, all else shadow`, `rim light catching the edge of his shoulder and pec` |
| Pressing against her | `bare chest pressing against her back`, `skin against skin, no space between them` |
| Scarred | `old scars across his ribs`, `a long scar bisecting his left pectoral` |

**T2 partial-undone detail bank (often more tension than T3):**

| Detail | Prompt keywords |
|---|---|
| Open shirt chest | `shirt open to mid-chest, one button at a time — the implication clear`, `a V of bare chest visible, shirt hanging loose` |
| Rolled sleeves | `shirt sleeves shoved to the elbow, forearms corded with muscle, veins prominent` |
| Jacket-on, shirtless beneath | `leather jacket on his bare torso, chest visible between the open lapels` |
| Collar + tie | `collar open, tie pulled loose and hanging, the last defense down`, `the tie is gone; shirt half-untucked, collar undone to the second button` |
| Suit coming apart | `jacket discarded, shirt untucked at the back, the composed man dissolving` |

### Arms & Hands

| Detail | Prompt keywords |
|---|---|
| Muscled forearms | `forearms corded with muscle`, `thick muscled forearms, veins visible` |
| Gripping | `hand wrapped around her waist`, `hand gripping her hip`, `fingers pressed into her bare skin` |
| At her jaw | `hand cupping her jaw, thumb at the corner of her mouth`, `lifting her chin with two fingers` |
| In her hair | `fist in her hair pulling her head back`, `hand gathering her hair, moving it off her neck` |
| Against the wall | `forearm braced against the wall beside her head`, `caging her in with both arms` |
| Reaching for her | `hand reaching for her`, `arm outstretched, fingers just grazing her wrist` |
| Tattoos | `sleeve tattoo covering one arm from wrist to shoulder`, `tribal tattoo across the back of his hand` |

### Posture & Stance

| Type | Prompt keywords |
|---|---|
| Dominant / looming | `looming above her`, `standing over her, all his height used deliberately`, `using his body to crowd her space` |
| Caging | `one arm braced against the wall behind her head, the other at her waist — nowhere for her to go` |
| Pulling her in | `arm locked around her, drawing her body flush against his`, `pulling her against him with no intention of letting go` |
| Kneeling to her | `kneeling at her feet, looking up at her`, `dropping to one knee — a different kind of power` |
| Turned away | `standing with his back to her, tension visible in his shoulders` (unresolved conflict) |
| Carrying | `carrying her against his chest`, `her body cradled against his bare chest` |

---

## Skin, Tone & Texture Reference

### Female Skin

| Quality | Prompt keywords |
|---|---|
| Luminous | `luminous skin`, `skin that seems lit from within` |
| Dewy | `dewy soft skin`, `fresh-looking skin with a natural glow` |
| Wet / rain-slicked | `skin glistening with rain`, `rainwater running down her bare shoulder`, `wet skin catching every light source` |
| Flushed | `skin flushed with heat`, `pink rising from her collarbone to her cheeks` |
| Pale & dramatic | `near-translucent pale skin in the moonlight`, `alabaster skin` |
| Warm tone | `warm honey-toned skin`, `golden complexion catching the amber light` |
| Dark & radiant | `rich dark skin gleaming in the candlelight`, `deep brown complexion catching the rim light` |
| Goosebumps | `fine goosebumps along her bare arms and back` |
| Sweat / heat | `a sheen of exertion on her skin`, `light sweat catching the spotlight` |

### Lighting on Skin (dramatically affects how much allure reads through)

| Light type | Effect | Prompt keywords |
|---|---|---|
| Rim light | Traces the edge of bare skin, maximally revealing silhouette | `silver rim light tracing the curve of her bare shoulder`, `rim light outlining her figure against the darkness` |
| Moonlight | Hard, cold, high-drama for paranormal/fantasy | `moonlight falling across her bare back`, `cold moonlight making her skin glow` |
| Candlelight | Warm, intimate, shadows deepen cleavage | `candlelight pooling in the hollow of her collarbone`, `warm amber candlelight deepening every shadow` |
| Rain backlight | Wet skin acts as a light diffuser | `rain-slicked skin diffusing the streetlight`, `wet skin catching every ambient light source` |
| Spotlight (dramatic) | Isolates the figure, erases background | `single spotlight from above, all else in shadow`, `hard single-source light carving shadow and highlight` |
| Dawn / morning | Soft, golden, intimate morning-after feel | `soft golden morning light`, `early light streaming through sheer curtains across her bare shoulders` |

---

## Quick-Reference Cheat Sheet

When building any character description, fill in this template mentally before writing the prompt. Skip nothing — a blank slot defaults to generic, which reads as boring.

**Female lead checklist:**
- [ ] Eye shape + color + expression keyword
- [ ] Lashes / brows detail
- [ ] Lips: type + color + state (parted / bitten / trembling)
- [ ] Skin tone + quality (luminous / wet / flushed)
- [ ] Hair: length + texture + style + color + placement (where does it sit relative to bare skin?)
- [ ] Build keyword
- [ ] Clothing state (Tier T1/T2/T3 fragment from Exposure Tiers)
- [ ] Which skin zones are visible
- [ ] Hand / arm position and what they're doing
- [ ] Emotional register expression keyword

**Male lead checklist:**
- [ ] Jaw / bone structure keyword
- [ ] Stubble / facial hair state
- [ ] Eyes: type + expression
- [ ] Hair: style + state (dry / wet / disheveled)
- [ ] Build keyword
- [ ] Torso state (T1=collared shirt / T2=open/partial / T3=bare — match the genre and scene, not always bare)
- [ ] Hand / arm position and what they're gripping or bracing
- [ ] Posture / stance relative to her (looming / caging / pulling in)

---

## Scene Reference

A scene has four layers that work together: **Location**, **Time & Atmosphere**, **Lighting**, and **Props & Details**. Specify all four. A cover with a precisely described scene reads as cinematic; a cover with a vague background reads as stock. Use the same keyword-library approach as Face/Hair/Body — pick one entry per layer, combine freely.

**Rule:** the scene must amplify the emotion between the figures, not just decorate behind them. Ask "does this environment make the situation feel more dangerous / more intimate / more forbidden?" — if not, pick a different scene.

---

### Location Bank

#### Urban / City

| Scene | Visual signature | Prompt keywords |
|---|---|---|
| Rain-slicked alley | Narrow urban canyon, cobblestones, neon reflections, mist | `rain-slicked cobblestone alley`, `narrow street with glowing shop signs reflecting in puddles`, `urban alley, brick walls, mist rising from the wet ground` |
| Rooftop terrace | City sprawl below, open sky, wind | `luxury rooftop terrace, the entire city stretched below`, `rooftop at night, city lights blurred to bokeh`, `rain-exposed rooftop, skyline visible in every direction` |
| Penthouse interior | Floor-to-ceiling glass, city as wallpaper | `floor-to-ceiling windows, city at night forty floors below`, `penthouse interior, panoramic glass wall, the city a galaxy of lights behind them` |
| City street at night | Wet pavement, streetlamps, moving cars blurred | `wet city street at night, streetlamps casting pools of amber light`, `urban night street, passing headlights streaked to abstract lines` |
| Parking garage | Concrete, harsh fluorescent or single headlight, shadows | `empty parking garage, single headlight beam cutting through darkness`, `concrete columns casting hard shadows, fluorescent flicker` |
| Subway / underground | Tiled walls, harsh overhead light, urban grit | `subway platform, harsh fluorescent overhead, tiled walls`, `underground corridor, motion blur of passing train` |
| Fire escape | Metal grating, brick exterior, city below | `fire escape on a brick building, city visible through the metal grating below`, `iron fire escape, rain dripping through the grating` |
| Shoreditch / London street | Victorian brick, gas lamp style, London skyline | `Shoreditch cobblestone street, Victorian brick buildings, full moon over London rooftops`, `East London alley, weathered brick, distant shard of the Gherkin` |

#### Upscale / Wealth

| Scene | Visual signature | Prompt keywords |
|---|---|---|
| Grand ballroom | Chandeliers, marble floors, formal crowd blurred | `grand ballroom, crystal chandelier bokeh, marble floors reflecting the light`, `formal gala, candelabras, blurred crowd of onlookers in the distance` |
| Estate / manor | Stone façade, manicured grounds, old money | `grand family estate entrance, stone columns and iron gates`, `private manor library, mahogany shelves floor to ceiling, fireplace glow` |
| Luxury bedroom | Silk sheets, ambient glow, high-thread-count | `luxury bedroom, rumpled silk sheets, dim bedside lamp`, `penthouse bedroom, floor-to-ceiling windows, morning city light on unmade sheets` |
| Corporate tower | Glass and steel, power aesthetic | `glass-and-steel executive floor, city visible through the windows`, `corporate lobby, marble and chrome, high ceilings` |
| Yacht deck | Open water, horizon, movement | `yacht deck at sunset, open ocean horizon`, `deck of a private yacht at night, stars above, black water below` |
| Private jet interior | Cream leather, altitude implied | `private jet interior, cream leather seats, night sky visible in the oval window` |

#### Nature / Outdoor

| Scene | Visual signature | Prompt keywords |
|---|---|---|
| Moonlit forest | Ancient trees, silver light shafts, mist on ground | `moonlit forest, full moon filtering through ancient oak canopy`, `silver light shafts through dark trees, mist drifting at ground level` |
| Forest clearing | Open sky in the trees, exposed, vulnerable | `forest clearing at night, full moon overhead, ring of dark trees encircling them` |
| Cliff edge / coastal | Sea below, wind, dramatic horizon | `cliff edge above crashing sea, spray visible in the air`, `coastal clifftop, ocean horizon at dusk, wind pulling at her hair` |
| Rain in the open | No shelter, total exposure to the downpour | `caught in heavy rain, no shelter, cobblestones flooding`, `open street, rain pouring straight down, both of them completely soaked` |
| Garden / estate grounds | Night garden, stone path, hedgerows | `moonlit garden, stone path through formal hedgerows`, `private garden at dusk, roses in silhouette` |
| Snowy exterior | Cold, isolation, breath visible | `snow-covered street, breath misting in the cold air`, `winter exterior, bare trees, snowfall visible as soft blur` |
| Desert / arid | Heat shimmer, dramatic sky, isolation | `arid landscape, sun low on the horizon, heat shimmer`, `desert at night, vast star field, no civilization visible` |

#### Gothic / Dark Fantasy

| Scene | Visual signature | Prompt keywords |
|---|---|---|
| Gothic castle interior | Stone, torch/candlelight, cold shadows | `gothic castle interior, stone archways, torchlight casting flickering orange shadows`, `great hall, cold stone floor, tapestries on dark walls` |
| Castle exterior | Battlements, storm sky, isolation | `castle battlements at night, storm clouds rolling in`, `gothic spire against a full moon, gargoyles silhouetted` |
| Dungeon / vault | Arched stone ceiling, damp walls, single torch | `stone vault, single torch in a wall bracket, shadows heavy`, `dungeon corridor, iron door ajar, cold blue light from a slit window` |
| Ancient ruins | Crumbling arches, vines, supernatural mist | `moonlit ancient ruins, crumbling carved stone arches`, `fae ruins, stone worn smooth, silver-violet magical mist rising between the columns` |
| Dark forest / cursed wood | Twisted trees, no light penetration, supernatural | `cursed forest, gnarled dark trees, silver moonlight unable to reach the ground`, `bone-white tree trunks, mist at ground level, silence that has weight` |
| Cemetery | Headstones, iron fence, moonlight | `old cemetery, iron fence, moonlight on marble headstones`, `gothic graveyard, overgrown, a single mausoleum lit by the moon` |
| Underground cave / cavern | Mineral formations, bioluminescence, echo space | `underground cavern, bioluminescent crystals casting blue-green light`, `cave chamber, stalactites above, an underground pool reflecting pale light` |

#### Historical / Period

| Scene | Visual signature | Prompt keywords |
|---|---|---|
| Imperial court | Gilded interiors, lacquer and jade, candlelight | `imperial court interior, gilded columns, lanterns casting warm amber light`, `palace throne room, incense smoke, silks and jade` |
| 1930s Shanghai | Art Deco interior, neon Chinese signage, rain | `1930s Shanghai ballroom, art deco chandeliers, neon signs visible through rain-streaked windows` |
| Regency drawing room | Fireplace, mahogany, formal propriety | `Regency-era drawing room, fireplace crackling, candlelight on mahogany`, `Georgian townhouse interior, tall windows, formal furniture` |
| Victorian street | Gas lamps, cobblestone, fog | `Victorian London street, gas lamp halos in the fog`, `Dickensian alley, wet cobblestones, carriage sounds implied` |
| Feudal Japan | Shoji screen, tatami, moon garden | `traditional Japanese inn room, shoji screen with moonlight filtering through`, `zen garden at night, raked gravel, stone lantern` |
| Medieval great hall | Long tables, firepit, rush torches | `medieval great hall, long oak tables cleared, firepit at center, rush torches on stone walls` |

#### Fantasy / Supernatural

| Scene | Visual signature | Prompt keywords |
|---|---|---|
| Fae realm / enchanted | Impossible colours, floating light, magic | `enchanted forest, floating bioluminescent spores, colours no natural forest has`, `fae court, crystalline trees, diffused magical light` |
| Volcanic / infernal | Lava glow, ash fall, extreme heat | `volcanic landscape, lava flow in the distance casting red-orange glow`, `infernal setting, ash falling slowly, heat shimmer rising from cracked ground` |
| Underwater / deep sea | Refracted light, suspended particles, pressure | `underwater, diffused surface light from above, suspended particles catching the light`, `deep sea, bioluminescent creatures in the distance` |
| Cloud / sky realm | Open sky, cloud floor, light above and below | `above the clouds, sunrise light from below, infinite sky in every direction` |
| Celestial / cosmic | Stars as backdrop, nebula colors, vastness | `star field as backdrop, nebula colors in deep blue and purple`, `edge of a celestial body, planet curve below, stars above` |

---

### Time & Atmosphere

Time of day sets the emotional register before the figures even appear. Pick one and commit.

| Time / Weather | Mood | Prompt keywords |
|---|---|---|
| **Golden hour (dusk)** | Romance, warmth, nostalgia, endings | `golden hour, the sun just below the horizon, amber light everywhere`, `last light of the day, long warm shadows` |
| **Full night, clear** | Mystery, intimacy, freedom | `deep night, stars visible, everything past the lamplight in shadow`, `clear night, moon high, crisp dark shadows` |
| **Full night, overcast** | Tension, danger, no escape | `overcast night, no moon visible, everything in cold grey-black`, `heavy cloud cover, the city the only light source` |
| **Heavy rain** | Primal, urgent, inhibitions gone | `heavy rain pouring straight down`, `the kind of rain that ends arguments by making them irrelevant`, `curtains of rain, puddles everywhere, no point in running` |
| **Light rain / mist** | Melancholy, charged, beautiful sadness | `light rain beginning, surfaces starting to glisten`, `mist rolling in`, `drizzle catching in her hair` |
| **Storm (lightning)** | Violence, revelation, climax | `storm, lightning visible in the distance`, `thunder implied, everything lit briefly in blue-white`, `storm sky, clouds bruised purple and green` |
| **Dawn** | Aftermath, new beginning, fragile hope | `first light, pale gold at the horizon`, `pre-dawn darkness giving way to the palest blue`, `dawn light catching the tops of buildings` |
| **Morning after** | Intimacy, consequence, quiet intensity | `full morning light, warm and clear`, `late morning, bright and unambiguous`, `the kind of morning light that makes everything visible` |
| **Winter / snow** | Isolation, purity, cold vulnerability | `snowfall, soft and silent`, `breath misting in cold air`, `snow on every surface, absolute quiet` |
| **Heat / summer night** | Sensuality, unguarded, humidity | `summer night, air still and warm`, `heat shimmer rising even after dark`, `the kind of night where clothing feels like too much` |
| **Fog / smog** | Concealment, isolation, unreality | `thick London fog, visibility to five metres`, `smog-diffused city light, everything soft-edged`, `fog isolating them from the rest of the world` |

---

### Lighting Reference

Lighting is not decoration — it directly controls how much allure reads from the image. Specify the light source explicitly.

#### Primary Light Sources

| Source | Quality | Prompt keywords |
|---|---|---|
| **Full moon** | Hard, cold, silver — ideal for paranormal | `full silver moon as sole light source`, `moonlight cutting hard through the darkness`, `cold silver moonlight on wet skin` |
| **Streetlamp / gas lamp** | Amber pool, isolates figures from dark surround | `single streetlamp casting an amber pool around them`, `gas lamp halo in the fog`, `sodium streetlight, warm yellow against the cold night` |
| **Neon signs** | Urban, coloured, modern or noir | `neon signs reflecting in wet pavement`, `pink and blue neon backlight`, `neon glow from a bar sign, colour washing over them` |
| **Candlelight** | Warm, intimate, deepens shadow in cleavage | `candlelight, warm amber, shadows pooling in every hollow`, `cluster of candles at eye level, warm light flickering`, `single candle, everything past a metre in darkness` |
| **Fireplace / bonfire** | Orange, dancing, primal | `fireplace glow, orange light dancing across their faces`, `bonfire behind them, sparks rising`, `the only fire for miles` |
| **Lightning flash** | Harsh, momentary, reveals everything | `lightning flash freezing the scene in blue-white`, `lit for one second by lightning, then dark again` |
| **Car headlights** | Harsh frontal, high-contrast, urban drama | `headlights catching them from the side`, `car passing, a single sweep of light`, `caught in headlights, nowhere to go` |
| **Dawn / sunset sky** | Gradient, cinematic, large-scale | `golden sunrise behind them, silhouettes against the brightening sky`, `sunset gradient filling the sky — amber to deep purple` |
| **Bioluminescence** | Fantasy, cold blue-green, supernatural | `bioluminescent glow from the water or the forest floor`, `blue-green light with no identifiable source` |

#### Lighting Techniques (add to any source)

| Technique | Effect on allure | Prompt keywords |
|---|---|---|
| **Rim light** | Traces every edge of bare skin — maximally revealing silhouette | `silver rim light tracing the curve of her bare shoulder`, `hard rim light outlining their bodies against the dark background` |
| **Chiaroscuro** | Deep shadow + bright highlight, dramatic contrast | `chiaroscuro lighting, half her face in shadow`, `strong single-source chiaroscuro, extreme contrast` |
| **Backlight / contre-jour** | Silhouette, sheer fabric glows, halo effect | `backlit, their silhouettes against the light source`, `contre-jour, sheer fabric glowing with backlight` |
| **Under-light** | Supernatural, unsettling, glow from below | `light source below eye level, casting unfamiliar shadows upward` |
| **Split lighting** | One half lit, one half shadow — tension visible | `split lighting, half her face gold and half in cold shadow` |
| **Diffused / soft** | Intimate, morning-after, no hard shadows | `diffused soft light, no hard shadows`, `light scattered through sheer curtains` |
| **Spotlight** | Isolates figures, erases background | `single overhead spotlight, background in total darkness`, `stage-light quality, as if the world has narrowed to just them` |

#### Light Colour & Temperature

| Temperature | Feel | Prompt keywords |
|---|---|---|
| Warm amber | Intimate, safe, candle/firelight quality | `warm amber light`, `orange-gold tones` |
| Cold silver/blue | Danger, the supernatural, clarity that exposes | `cold silver light`, `blue-white clarity`, `icy light that shows everything` |
| Golden | Romance, nostalgia, desire | `golden light`, `honey-warm glow` |
| Red-orange | Danger, passion, fire | `deep red-orange glow`, `fire-lit, everything hot and saturated` |
| Neon mixed | Urban, modern, disorienting | `neon colour cast, pink and blue mixed light`, `urban colour pollution` |
| Desaturated / grey | Grief, aftermath, cold clarity | `desaturated palette`, `grey-blue cold light, colour bled out` |

---

### Atmosphere & Weather Detail

Add these to any scene to increase the sense of physical presence:

| Element | Prompt keywords |
|---|---|
| Rain threads | `individual rain threads visible against the light`, `rain caught in the lamplight, each drop a silver thread` |
| Mist / fog | `mist rising from the wet ground`, `fog rolling in, softening everything past ten feet` |
| Steam / breath | `breath misting in the cold air`, `steam rising from a grate in the street` |
| Wet surfaces | `every surface glistening`, `puddles reflecting the sky`, `cobblestones mirror-wet` |
| Smoke / incense | `incense smoke drifting`, `cigarette smoke hanging in the still air`, `smoke from a distant fire` |
| Wind | `wind pulling at her hair`, `a gust catching the hem of her dress`, `the kind of wind that makes stillness impossible` |
| Leaves / petals | `cherry blossom petals drifting`, `autumn leaves in the air`, `rose petals on the ground` |
| Snow | `snowflakes caught in the light`, `snow falling silently`, `a fine layer of snow on every surface` |
| Sparks | `embers drifting upward from a fire`, `sparks visible in the air` |
| Lightning | `lightning visible at the horizon`, `a single lightning strike illuminating everything` |

---

### Props & Scene Detail

Props anchor the scene in a specific world and genre. Choose 2–4 maximum — more reads as cluttered.

#### Wealth / Power Props

| Prop | Prompt keywords |
|---|---|
| Champagne | `champagne flute with golden bubbles`, `uncorked bottle on the floor nearby` |
| Jewellery | `scattered jewels on the surface nearby`, `a diamond bracelet at the edge of frame` |
| Expensive watch | `the face of a luxury watch catching the light` |
| Contract / documents | `a signed contract on the desk between them` |
| Chess piece | `a lone chess piece on the board, overturned` |

#### Romance / Aftermath Props

| Prop | Prompt keywords |
|---|---|
| Rumpled sheets | `rumpled silk sheets`, `the evidence of a bed slept in` |
| Lipstick smear | `red lipstick on a glass`, `lipstick slightly smeared at the corner of her mouth` |
| Spilled wine | `wine glass on its side, a dark stain spreading` |
| Roses | `dark red roses, one dropped on the floor`, `rose petals scattered` |
| Candles (spent) | `candles burned low, wax pooled`, `one candle still burning` |
| Phone (ignored) | `phone face-down on the table, notifications ignored` |

#### Urban / Gritty Props

| Prop | Prompt keywords |
|---|---|
| Rain puddle | `a deep puddle reflecting the figures and the sky above them` |
| Fire escape grating | `the shadow grid of fire escape grating across the scene` |
| Neon sign | `a bar sign in neon just out of frame, colour spilling in` |
| Newspaper / litter | `wet newspaper plastered to the ground` |
| Motorbike | `a motorbike leaning against the wall` |

#### Gothic / Fantasy Props

| Prop | Prompt keywords |
|---|---|
| Candelabra | `iron candelabra with tall tapers`, `wax dripping` |
| Ancient tome / scroll | `an open ancient tome on the stone floor` |
| Glowing artefact | `a glowing artefact on a plinth nearby` |
| Crown | `a crown discarded on the floor`, `crown in her hand, not on her head` |
| Sword / weapon | `a sword thrust into the stone floor between them`, `weapon on the ground, no longer in anyone's hand` |
| Magic circle | `a glowing sigil on the floor beneath them` |
| Shattered mirror | `shattered mirror, their reflections broken across a hundred shards` |

#### Historical Props

| Prop | Prompt keywords |
|---|---|
| Fan (period) | `a folded fan in her hand`, `fan dropped at her feet` |
| Letter / seal | `a sealed letter on the table`, `broken wax seal beside it` |
| Oil lamp | `an oil lamp on the writing desk, casting warm light` |
| Inkwell / quill | `inkwell and quill, a half-finished letter` |
| Carriage outside | `the sound of a departing carriage implied by the window` |

---

### Scene × Genre Matrix

Quick-reference: which scene types pair naturally with each genre.

| Genre | Primary scenes | Atmosphere | Lighting |
|---|---|---|---|
| Paranormal Romance | Moonlit forest, gothic castle, city alley (London), ruins | Heavy rain, full moon, mist | Cold silver moonlight, single streetlamp, rim light |
| Contemporary Romance | Penthouse, rooftop, city street, luxury bedroom | Clear night, golden hour, light rain | Warm amber, city bokeh, candlelight |
| Dark Romance / Mafia | Parking garage, estate, industrial, abandoned space | Overcast night, fog, cigarette smoke | Harsh headlights, chiaroscuro, cold blue |
| Billionaire Romance | Penthouse, corporate tower, grand ballroom, yacht | Clear night, golden hour | Chandelier bokeh, floor-to-ceiling city lights, spotlight |
| Historical Court | Imperial court, palace, manor drawing room | Candlelit interior, evening, snow outside | Candlelight, fireplace, warm amber |
| Dark Fantasy | Gothic castle, ancient ruins, cursed forest, cave | Storm, magical mist, ash fall | Torch, bioluminescence, lightning, supernatural glow |
| Cultivation / Xianxia | Mountain peak, ancient temple, celestial realm | Dawn mist, cloud sea, moonlight | Gold sunrise, silver moonlight, qi/energy glow |
| Thriller / Crime | Urban alley, parking garage, rooftop, police precinct | Night, rain, fog | Neon, headlights, single harsh overhead |
| Sports Romance | Stadium tunnel, gym, locker room, outdoor track | Golden hour, bright morning | Hard overhead spot, golden hour backlight |
| Academy Romance | Campus corridor, rooftop at dusk, classroom at night | Cherry blossom, golden afternoon, evening | Warm interior light, late afternoon slant |

---

## Poses

Front-facing compositions outperform side-profile and back-view on scroll-stop rate, but **same-site visual repetition kills diversity** — do not default to the same pose across all books. Rotate through the full table; no pose repeats for 2 consecutive books on the same site.

### Face Direction Rule — the most commonly broken rule

**Default failure mode:** two characters rendered in pure side profile facing each other, neither face readable to the viewer. The model treats "bodies close together" as "looking at each other" unless explicitly overridden.

**Primary rule: both characters face the viewer. This is the production default — frontal gaze from both figures produces the highest scroll-stop rate. "She looks at viewer, he looks at her" is the fallback, not the default.**

**Priority order (highest to lowest):**
1. **Both looking at the viewer** — default. Both faces toward camera. No gaze lock between characters.
2. **She faces viewer, he faces toward her from the side** — his face still three-quarter readable, but he looks slightly toward her, not at the camera.
3. **She faces viewer, he looks at the side of her face / her throat from behind** — accent pose only (≤1 in 3 covers).

Write gaze direction explicitly for both characters every time:

| Character | Correct | Wrong |
|---|---|---|
| **Female lead** | `her face toward the viewer, eyes forward` / `her expression toward the camera, chin slightly lifted` / `facing the viewer, her gaze forward — not looking at him` | `her face tilted toward his` / `looking up at him` / `gazing at him` |
| **Male lead** | `his face toward the viewer, three-quarter angle — expression of cold possession` / `facing the camera, jaw set, his expression the story` / `his face at three-quarter angle toward the viewer, not toward her` | `looking at her face-to-face` / `their eyes meeting` / `his gaze on her` (when she is also looking at him — gaze lock) |

**The jaw-tilt trap:** `his hand at her jaw tilting her face toward his` is the single most common gaze-lock trigger. It is in almost every T3 pose description and almost always produces face-to-face. Replace it with:
> `his hand at her jaw — steadying, not directing — her face turns outward toward the viewer, not toward him`

Or remove the jaw-tilt entirely and describe his hand position without a direction:
> `his hand cupping her jaw from the side, thumb at her cheekbone — her face remains toward the viewer`

**Pattern for side-profile body + face toward viewer (use when bust prominence matters — validated model-test-10):**
> `FRAMING: pure side-profile body, face toward viewer — her body in strict side profile, the full silhouette of her figure from shoulder to hip visible against the rim light. Her head is rotated to face the viewer directly — her face turned toward the camera, chin lifted, eyes looking directly at the viewer. The body reads in profile; the face reads full-frontal to the camera.`
> This achieves maximum bust silhouette (side profile) + maximum emotional engagement (frontal gaze). Specify body and face orientation separately — the model defaults to side-profile everything if you don't.

**Pattern for both facing viewer (three-quarter composition — default):**
> `both figures at three-quarter angle toward the viewer — both looking at the camera. Neither is looking at the other. His expression: cold possession, jaw tight, looking directly at the viewer. Her expression: fierce surrender, lips parted, eyes forward toward the viewer. The tension is in the proximity and their bodies, not a gaze exchange.`

**Pattern for man-behind-woman (second choice):**
> `she faces the viewer directly — her expression toward the camera, eyes forward. He stands behind her, his face above and to one side of hers, his jaw at her temple — his face at three-quarter angle toward the viewer, or looking slightly toward her. His gaze is not locked onto hers — tension is in their bodies, not their eyes.`

**Pattern for man-beside-woman (second choice):**
> `both at three-quarter angle toward the viewer — neither in side profile. Both faces readable to the viewer. Neither is looking into the other's eyes — the tension is in the proximity, not a gaze lock.`

**Anti-pattern — "facing each other" side-profile trap:** When a prompt says two characters are "facing each other," models render both in pure side profile — two faces looking at each other from the side, neither looking at the camera. This kills allure. The fix: **both characters face the viewer**, looking at the camera, not at each other. Use `both at three-quarter angle toward the viewer, both looking at the camera` or `both faces turned toward the viewer — the tension is physical proximity, not eye contact`. Never write `facing each other` without also anchoring both figures to the viewer.

**Anti-pattern — gaze-lock via "looking at each other":** Any phrase that implies mutual eye contact between the characters (even indirectly — `tilting her face toward his`, `she meets his gaze`, `their eyes meet`) triggers a face-to-face render. The fix: specify that BOTH characters look at the camera/viewer, not at each other. Their emotional connection is communicated by body proximity, not by eye contact.

| Frame | When to use | Prompt fragment to include |
|-------|-------------|---------------------------|
| **Full body** (first choice) | Always — shows clothing, figure, and both characters fully | `full-body shot, both figures visible head to toe, full torso and legs in frame, facing the viewer` |
| **Medium shot** (second choice) | When scene focus is the charged space between faces | `medium shot, both figures from hip to crown, three-quarter view facing camera` |
| **Close-up** (accent only) | Only when pose is inherently face-to-face (chin tilt, forehead press) | `tight crop on faces and upper chest` |

**Never default to close-up.** If the prompt describes bodies pressing together, the frame must show those bodies. If the pose puts the man behind the woman, use it as a dramatic accent (1 in 3 covers), not a default.

### Pose Reference

| Pose | Scene | Safe prompt keywords |
|---|---|---|
| **Wall pin — frontal cage** | Woman's back to wall, man's arms on either side, she faces viewer fully | `woman's back pressed to wall, man's arms planted on either side forming a cage around her — she faces the viewer fully, dress and figure readable, he leans in from the front, bodies an inch apart` |
| **Frontal chest press** | Chest-to-chest, both facing camera | `man and woman chest-to-chest facing the viewer, his hands gripping both her hips pulling her flush against him, her hands fisted in his open shirt, full-body shot from hip to crown, every curve of her dress pressed hard against him` |
| **Power lift — face level** | Lifted to eye level, dynamic | `man's hands gripping her waist lifting her until their faces are level, her legs hanging with skirt riding up, both facing the viewer, her hands on his shoulders, full-body shot` |
| **Standing confrontation** | Charged gap, both facing viewer | `two figures standing close but not touching, both at three-quarter angle facing the viewer — neither in side profile — his hand reaching toward her jaw not yet touching, her chin raised in defiance, full torsos and legs visible` |
| **Chair pin** | Man leans over woman seated in chair | `dominant figure leaning over seated woman in chair, she faces viewer, intense close proximity, power dynamic, controlled expression, medium shot` |
| **Rain-soaked** | Wet hair clinging to face and neck, raw emotion | `rain-soaked figure, wet hair clinging to face and neck, damp clinging clothing outlining figure, emotionally raw upward gaze facing viewer, neon-lit rainy night street, full body visible` |
| **Look back over shoulder** *(accent)* | Three-quarter turn, cheekbone catching light | `looking back over shoulder with mysterious expression, cheekbone catching soft light, hair swept by motion, cinematic depth of field` |
| **Pure side profile** *(accent only)* | Side face only, jawline and neckline | `pure side profile, elegant jawline and neckline, downcast or distant gaze, moody window light from one side` |
| **Off-shoulder** | Neckline slightly off one shoulder | `off-shoulder silhouette facing the viewer, elegantly bare collarbone and shoulder line, soft light on skin, fabric gathered gracefully, medium shot` |
| **Billowing skirt** | Outdoor / wind, dynamic movement | `skirt billowing in wind, fabric flowing dramatically, legs fully visible through motion, golden hour backlight, full-body shot facing viewer` |
| **Downcast gaze** | Eyes lowered, eyelashes catching light | `downcast eyes, eyelashes catching light, subtle vulnerability, soft chin shadow, medium shot facing camera` |
| **Bedside morning light** | Pillow / bed edge, silk morning light | `bedside morning light, figure half-reclining or sitting at edge facing viewer, disheveled hair, sheer curtain filtering golden hour, intimate quiet atmosphere` |

---

## English Romance Cover Playbook

Maximum-allure formulas for English romance novel covers. Validated on: flux-pro-1.1-ultra, doubao-seedream-5.0, gpt-image-2-all, gemini-3.1-flash-image, nano-banana-pro.

**Objective: the cover must stop a scroll — visually hot, instantly magnetic. Push every element to the edge of the compliance floor below.**

**Core rule: always use physical contact. Bodies pressed together is the minimum; aim for poses where removing the prompt description would make the image read as explicit.**

## Drama Hook — The Click Driver

Sex appeal stops the scroll. Drama creates the click. Both are required.

A cover fails if it looks like a fashion shoot where two hot people happen to be near each other. It succeeds when the viewer's first instinct is *"wait — what is happening between them?"*

### The Hook Formula

Every cover must have **all three**:

| Layer | What it does | How to achieve it |
|-------|-------------|-------------------|
| **Tension** | Makes the viewer feel the stakes | Power imbalance, forbidden desire, barely-controlled emotion |
| **Question** | Makes the viewer need to know more | An incomplete story visible in the image — what happened before? what happens next? |
| **Desire** | Makes the viewer want to be in the scene | The allure of the bodies, the heat between them |

**Adding a third figure for conflict:** the Hook Formula does not require exactly two people. When the synopsis offers a rival, betrayer, jealous third party, or looming antagonist, render them in the frame — a third figure sharpens **Tension** and **Question** more than a clean two-person embrace can. Keep one central focal pairing so the eye still has a home; place the third figure to threaten or intrude on that pairing (watching from behind, reaching between them, turned away in betrayal), not to dilute it.

### Expression Rules — The Face Sells the Story

The face is the click trigger. Generic beauty does not hook. Specific emotion does.

**Banned expressions:** neutral, relaxed, smiling pleasantly, serene, confident pose-and-smile — these communicate *nothing is at stake*.

**Required expression palette — pick one that matches the scene:**

| Expression | Prompt keywords | Works for |
|------------|----------------|-----------|
| **Barely-controlled want** | `eyes dark with barely-suppressed desire, jaw tight, expression of a man fighting his own instincts` | The moment before he breaks |
| **Surrender under protest** | `lips parted, brows furrowed slightly — her expression says she knows this is a mistake and can't stop` | Forbidden romance, enemies-to-lovers |
| **Defiance + desire** | `chin raised in defiance but eyes betraying want, expression of someone who refuses to admit they're losing` | Power struggle romance |
| **Raw vulnerability** | `eyes glistening, lower lip trembling, expression caught between fear and longing` | High-stakes emotional moment |
| **Cold possession** | `expression of absolute ownership, calm and certain, eyes that see only her` | Alpha / dark romance |
| **Overwhelmed surrender** | `head thrown back, eyes closed, expression of total abandon — has stopped fighting it` | Peak physical tension |
| **Shocked recognition** | `wide eyes, lips parted — the expression of someone who just realized everything is about to change` | Revelation / twist moment |

### Power Dynamic — The Invisible Story

The power gap between characters is the subtext readers are buying. Make it visible:

- Who is taller, who is lower — physically show who has control
- Who is gripping, who is being gripped — the hand tells the hierarchy  
- Who looks certain, who looks conflicted — emotional asymmetry is magnetic
- One character's world is ending; the other is the reason why

**Prompt formula:** describe not just *what* they're doing but *what it means*:
- ❌ `man standing behind woman`
- ✅ `man standing behind woman, his posture radiating absolute possession, her body betraying a surrender her expression refuses to admit`

### Environmental Drama — The Scene Adds Stakes

The background must amplify the emotion, not just decorate it.

| Emotional beat | Environment | Key elements |
|---------------|-------------|-------------|
| Forbidden / dangerous | Rain-soaked alley, storm, darkness | Neon reflections, rain threads, cold blue light isolating the figures |
| Wealth / power gap | Penthouse, luxury ballroom, marble floors | Floor-to-ceiling city lights, chandeliers, wealth props (champagne, jewels) |
| Supernatural stakes | Moonlit forest, gothic castle, ruins | Full moon, silver mist, glowing eyes, ancient trees |
| Aftermath / intimacy | Luxury bedroom, rumpled sheets | Golden morning light, champagne flute, scattered luxury items |
| Public humiliation | Grand ballroom, crowd of onlookers | Candelabras, onlookers blurred in background, grand staircase |

### Visual Contrast — The Eye Magnet

High contrast compositions are clicked more. Build in at least two of these:

- **Light vs dark:** single strong light source carving the figures out of shadow
- **Hard vs soft:** his rigid controlled posture against her yielding body
- **Cold vs warm:** silver moonlight from behind, warm amber glow from his eyes
- **Covered vs exposed:** his full suit against her barely-there dress
- **Calm vs emotional:** his cold expression against her overwhelmed face

### The One-Second Test

After building the prompt, ask: *if someone sees this cover for one second while scrolling, do they feel something?* If the answer is only "that's attractive" — add drama. If the answer is "I need to know what happens" — it's ready.

---

## §0 Hard Compliance Floor — Absolute Bans (all platforms)

These trigger permanent ad-account bans (Meta, AdSense, GAM) and image-generator rejections. Never cross this line regardless of model permissiveness:

| Category | Banned |
|----------|--------|
| Genitals | Any visible genitals or pubic area |
| Nipples | Visible nipples or areolae on any gender |
| Sex acts | Penetration, oral, or any explicit sexual act |
| Full frontal nudity | Completely nude body showing all three: face + breasts + pubic area simultaneously |

Everything not on this list is **in play**. Push it.

---

### Skin & Clothing Vocabulary — use aggressively, always push to the highest intensity that fits the scene

**Female — clothing:**
- `backless evening gown, back completely bare to just above the tailbone`
- `deep plunging V-neckline to the sternum, extreme décolletage on full display`
- `thigh-high slit baring the entire leg and upper inner thigh`
- `micro mini dress barely covering the upper thighs`
- `strapless corset bodice with extreme push-up, ample cleavage prominently displayed`
- `sheer lace overlay with opaque panels — figure visible through the fabric, curves suggested`
- `wet silk dress clinging to every curve of her body`
- `silk slip dress with spaghetti straps, fabric barely covering her, thin enough to suggest the shape beneath`
- `torn dress with one strap fallen, fabric slipping dangerously low`
- `bandeau crop top and high-cut skirt, bare midriff fully exposed`
- `corset laced so tight her waist cinches and her bust overflows the cups`
- `off-the-shoulder gown pulled down to the very edge of her bust`
- `barely-there bikini top under an open jacket`
- `white dress soaked by rain, clinging translucently to her silhouette`

**Female — body language:**
- `voluptuous hourglass figure, impossibly cinched waist, full generous bust`
- `arching her back to press her chest forward`
- `one leg raised, inner thigh visible`
- `dress riding up to reveal the very top of her thigh`
- `bare shoulder and upper chest catching the light as the fabric slips`

**Male:**
- `shirt completely removed, powerful bare torso, defined abs catching the light`
- `dress shirt hanging fully open, every inch of his chest exposed`
- `suit jacket thrown open, shirt torn open at the collar, muscular chest visible`
- `jeans riding low, deep V of his hips visible above the waistband`
- `tattoos covering chest and abs fully visible through open shirt`

---

### Poses — Full Table (all within §0 floor)

Pick the pose assigned in the Batch Diversity Plan (story-cover.md Step 1.6). In single-book mode, pick freely from the table — no pose is the fixed default. From-behind poses (marked ▲) cap at **2 per site**. Always pair with the Camera Framing instruction above.

**Solo compositions** (no male required):

| Pose | Prompt Formula |
|------|---------------|
| **Solo power pose** | `woman standing alone facing viewer, three-quarter angle, chin slightly raised, one hand at her hip or holding an object relevant to the story, expression of fierce authority or barely-contained emotion — full-body shot, environment behind her amplifying tone` |
| **Solo atmospheric** | `woman seen from behind or three-quarter rear, facing into a dramatic environment — stormy sea, gothic cityscape, moonlit ruins — full figure visible, environment dominant, sense of scale and solitude` |
| **Solo intimate** | `woman alone, seated or reclining, facing viewer with a quiet charged expression — morning light, disheveled hair, silk sheet or minimal garment — medium shot, emotional register over action` |

| Pose | Prompt Formula |
|------|---------------|
| **Frontal chest press** | `man and woman chest-to-chest, his hands gripping both her hips pulling her flush against him, her hands fisted in his open shirt, both at three-quarter angle facing the viewer — full-body shot hip to crown, her voluptuous figure pressed into him, every curve of her dress against his chest` |
| **Against-the-wall — bodies locked** | `man's body pinning woman to the wall, his thigh pressed between her legs, one hand flat on the wall above her, the other gripping her waist and pulling her hips into him, her leg hooked around his, fingers twisted in his open shirt, faces one centimeter apart, both breathing hard — medium shot, she faces viewer, full torsos visible` |
| **Power lift — face level** | `man's hands gripping her waist lifting her until their faces are level, her legs hanging with dress riding up to bare the thigh, both facing the viewer, her hands gripping his shoulders, full-body shot` |
| **Chin tilt — almost-collision** | `man's large hand cupping woman's jaw, thumb pressing her lower lip open, tilting her face up to his until their lips are a breath apart, her hands clutching his open shirt, arching her body into his, eyes barely open, raw wanting expression — medium shot showing both torsos, not a head crop` |
| **Standing confrontation — charged gap** | `man and woman bodies one inch apart but not touching, both at three-quarter angle facing the viewer — NOT facing each other — his gaze cutting toward her, his hand reaching toward her jaw not yet making contact, her chin raised in defiance and turned slightly toward camera, his expression of absolute certainty — full-body shot, legs and clothing fully visible` |
| **Rain-drenched — bodies merged** | `two figures pressed chest to chest in heavy rain facing the viewer, soaked fabric clinging to and outlining every curve of her body, his hands gripping her waist and the back of her thigh, her leg wrapped around his hip, lips nearly touching — full-body shot` |
| **Torn aftermath — disheveled** | `woman's gown slipped completely off one shoulder and falling, man's hand at her bare waist skin-to-skin, her hair unraveled, both facing viewer in dim candlelight, her expression: desire and defiance — medium shot` |
| **Kneeling power dynamic** | `woman kneeling on floor facing the viewer, hands on man's thighs as she looks up at him, her dress draped and falling open at one side, his hand loose in her hair, gaze commanding — full body visible` |
| **▲ Possessive hold — full press** *(from behind — accent only)* | `man standing behind woman, bare chest pressed to her bare back, one forearm low across her abdomen pulling her into him, his other hand gripping her jaw and tilting her face up toward his, her head thrown back against his shoulder, lips parted, eyes half-closed in surrender, her dress slipped off both shoulders` |
| **▲ Hip grip — full press from behind** *(from behind — accent only)* | `man's hands gripping both her hips from behind, pulling her back firmly against him, her dress riding up to mid-thigh, her head turned back toward him over her shoulder, lips parted, one hand reaching back to grip his thigh` |
| **▲ Neck exposure — arched** *(from behind — accent only)* | `woman's head thrown completely back, throat fully arched, man's lips pressed to her neck, his hand gripping her hair at the root, his other hand flat on her bare stomach, her back arched hard into him, fingers digging into his arm` |
| **Bed — morning after tension** | `woman sitting at bed edge wrapped only in a white sheet clutched to her chest, sheet loose and slipping, bare shoulders and legs from mid-thigh down fully visible, knees pressed together, expression of shock and conflict; man beside or in front of her, shirt off, watching her with controlled intensity — she faces viewer` |
| **Bridal carry — slipped** | `man carrying woman in frontal three-quarter view, her bare legs draped over his arm, her gown fallen to barely cover her upper thighs, one shoulder strap slipped, her head against his shoulder, half-lidded eyes, hand resting on his bare chest — full-body shot` |

---

### Genre-Specific Prompt Formulas

#### Dark Romance / Billionaire Romance
```
Romance novel cover, cinematic photorealistic quality, dark dramatic luxury atmosphere.
FRAMING: full-body shot, both figures visible from feet to crown, three-quarter angle facing viewer.
TWO characters. Powerful man in charcoal suit with shirt fully open revealing his
defined chest, one hand gripping the woman's jaw from below tilting her face up to his,
his other hand gripping her bare lower back pulling her hips flush against him from the front.
Both figures face the viewer — full torsos, legs, and clothing visible in frame.
His expression: cold, absolute, the expression of a man accustomed to getting exactly
what he wants and currently deciding whether to take it — controlled hunger, dangerous patience.
Woman in a floor-length backless gown — extreme décolletage plunging to the sternum,
thigh-high slit baring the full leg, her voluptuous hourglass figure against his suit;
her fingers clutching his lapel — not to pull him closer, not to push him away, the ambiguity
is the story; lips parted and trembling, eyes half-closed, expression of someone losing an
argument she made with herself three months ago.
Faces one centimeter apart. The moment before everything changes.
Background: luxury penthouse, floor-to-ceiling city lights at night, the entire city below.
Color palette: charcoal, midnight black, ivory skin, single amber candlelight slash.
Lighting: single hard side light carving her bare legs and his jaw out of darkness.
Title '{title}' in elegant silver serif at top. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Paranormal / Shifter Romance
```
Romance novel cover, cinematic photorealistic quality, dark paranormal atmosphere.
FRAMING: full-body shot, both figures visible from feet to crown, three-quarter angle facing viewer.
TWO characters. Man with powerful bare muscular torso — shirt completely removed,
defined abs and chest catching moonlight — standing beside woman, his body pressed
against her side, one forearm low across her abdomen pulling her into him, his other
hand at the side of her jaw — steadying, not directing. Both figures at three-quarter
angle toward the viewer — both faces toward the camera, neither looking at the other.
His bare chest and abs visible, her voluptuous figure from feet to crown.
His expression: absolute cold possession, eyes glowing amber, jaw tight —
looking at the camera, not at her. Her expression: fierce surrender, eyes forward
toward the viewer.
Woman in a torn flowing ivory dress — one shoulder completely bare, neckline
plunging to the sternum, fabric clinging to and slipping from her voluptuous hourglass
figure; lips parted and trembling, eyes wide with the expression of someone who knows
this is dangerous and cannot make herself stop.
One hand gripping his forearm — fingers pressing in, knuckles white — not pulling
away, holding on. A glowing silver wolf tattoo on her wrist visible in the moonlight.
The emotional subtext: she is losing a fight she started against herself.
Background: moonlit forest clearing, full moon through ancient oak trees, silver-blue
mist pooling at ground level — both full figures visible against the mist.
Color palette: cold silver moonlight, deep forest black-green, warm amber from his eyes, ivory skin.
Lighting: cold silver rim light from the side sculpting both figures, warm amber glow from his eyes.
Title '{title}' in weathered silver fantasy serif with faint glow. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark, text inside central safe area inner 85%.
```

#### Vampire Romance
```
Romance novel cover, cinematic photorealistic quality, gothic dark romance atmosphere.
FRAMING: medium-to-full-body shot, both figures from hip to crown facing viewer at three-quarter angle.
TWO characters. Man in dark Victorian coat, pale aristocratic face, standing beside woman
at a slight angle — his face turned toward her neck from the side closest to the viewer,
lips grazing her exposed throat. Her head tilts away from him — toward the camera —
so her face is visible to the viewer: eyes closed, lips parted in complete overwhelmed surrender.
His profile is visible at the edge, cold absolute possession; her full face catches the candlelight.
One hand gripping her hair at the root, the other splayed possessively across her bare stomach
pulling her against him — both his hand and her exposed midriff visible to the viewer.
Woman in deep burgundy gown with extreme plunging neckline — one shoulder slipped,
fabric barely clinging to her voluptuous figure, back arched so her chest lifts toward the light,
fingers pressing into his forearm — not pulling away, anchoring herself.
Both figures from hip to crown clearly in frame — her dress, his coat, her bare shoulders and chest.
The emotional subtext: she came here to fight and forgot why the moment he touched her.
Background: candlelit gothic stone chamber, scattered rose petals on cold floor, centuries of silence.
A single stained-glass window above casts fractured violet and red light.
Color palette: deep burgundy, ivory skin, black, warm gold candlelight, fractured violet.
Lighting: warm candlelight on her throat and exposed chest, violet from stained glass catching her shoulder.
Title '{title}' in gothic elegant serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Fantasy Romance / Dark Fae
```
Romance novel cover, cinematic fantasy photorealistic quality, dark ethereal atmosphere.
FRAMING: medium-to-full-body shot, both figures from hip to crown, three-quarter angle facing viewer.
TWO characters. Fae male in dark armor or black robes with silver detail, inhumanly beautiful
pointed features, his hand at the side of her jaw — steadying, not directing — both faces
at three-quarter angle toward the viewer, both looking toward the camera, the charged gap
between their faces one inch apart but neither breaking to look at the other.
Both figures face the viewer — clothing and figures readable from hip to crown.
His expression: cold ancient amusement and absolute want, looking at the camera —
the expression of someone who has never been told no and finds it unexpectedly interesting.
Woman in sheer silver flowing gown with deep plunging neckline, bare shoulders, bare midriff —
fabric billowing from wind that doesn't exist, her hair unbound with tiny flowers woven in;
her hand pressed flat against his armored chest — the gesture could be stopping him or
steadying herself — her own expression a war: the part of her that knows better and the part
of her that is already gone.
Magical light pulses between their faces in the charged space — her human warmth, his fae cold —
a visible current of power exchange.
The subtext: she bargained for something else entirely. She didn't read the fine print.
Background: moonlit ancient fae ruins, crumbling carved stone arches, silver-violet magical mist
pooling at ground level, bioluminescent flowers growing from the cracks.
Color palette: deep midnight violet, silver, ivory complexion, black armor, bioluminescent teal accents.
Lighting: silver magical glow from the charged space between their faces, full moonlight from above.
Title '{title}' in silver fantasy script with faint magical glow. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Mafia / Cartel / Organized Crime Romance
```
Romance novel cover, cinematic photorealistic quality, high-contrast dark thriller romance.
FRAMING: full-body shot, both figures visible from feet to crown, three-quarter angle facing viewer.
TWO characters. Man in sharp charcoal suit, one hand gripping her bare hip from the front,
the other lifting her jaw with two fingers — tilting her face up to his. Both figures face the
viewer, full length of their bodies in frame — his suit, her dress, her bare leg through the slit.
His expression: cold certainty and barely-leashed danger, the expression of a man
who has made a decision about her and she has not been consulted.
Woman in a sleek fitted micro-mini dress, thigh-high slit baring the full leg, deep plunging neckline,
voluptuous figure pressed against him from the front — her chin raised to meet his gaze, not in fear,
in defiance; her hand gripping his lapel, the gesture contradicting her expression:
her eyes say she wants to fight him. Her body has already surrendered.
The subtext: she walked into his world with a plan. She did not plan for him.
Background: luxury rooftop terrace at night, the entire city stretched below — empire and
risk and consequence all in one skyline behind them. Neon wash catching the rain-wet railing.
Color palette: deep black, sharp white dress, muted gold, single red accent (her lipstick, his ring).
Lighting: harsh dramatic cold side light from the city below carving his jaw and her bare leg
out of shadow — her full figure catching the neon.
Title '{title}' in bold condensed serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Contemporary Romance (Fake Dating / Marriage of Convenience)
```
Romance novel cover, cinematic photorealistic quality, intimate contemporary atmosphere.
FRAMING: medium shot, both figures from hip to crown facing viewer — NOT a face-only crop.
TWO characters. Man in casual open-collar shirt or rolled-sleeve button-down,
bodies pressed together, his hand cradling her bare jaw tilting her face up to his,
faces close — noses nearly grazing, eyes barely open.
Her hand pressed flat to his chest over his heart — she can feel his pulse.
The held breath of the moment before they stop pretending.
His expression: guarded and already lost — a man who agreed to a deal and did not expect to mean it.
Her expression: surrender under protest — brows furrowed slightly, lips parted.
She is wearing a silk slip dress with one strap slipped, bare shoulder visible, waist and hips in frame;
his open shirt showing his chest — skin to skin in a moment that was supposed to be business.
Medium shot from hip to crown so both figures' bodies are in frame — dress, slipped strap,
his open chest — NOT cropped to faces alone.
The subtext: the contract said sixty days. She stopped counting at fourteen.
Background: warm golden interior — a luxury hotel room, rain-streaked window, city
lights soft and blurred, unmade bed in peripheral.
Color palette: warm amber, ivory skin, soft cream shadows, champagne gold.
Lighting: golden hour through rain-streaked glass, soft diffused warm glow.
Title '{title}' in warm elegant serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Sports Romance
```
Romance novel cover, cinematic photorealistic quality, charged competitive atmosphere.
FRAMING: full-body shot, both figures from feet to crown, three-quarter angle facing the viewer.
TWO characters both at three-quarter angle facing the viewer — NOT in side profile facing each other — both bodies fully readable.
He bare chest or fitted athletic shirt torn open, muscular torso and abs fully visible —
sweat-sheened, still running warm from competition. He looks toward her with controlled intensity,
jaw tight, not letting himself look away, his gaze cutting toward her but his body angled to camera.
His expression: defiance + desire — he's been told she's off-limits and cannot find a reason
that still makes sense. Eyes dark, decision already made.
She at three-quarter angle toward the viewer, in fitted athletic wear — sports bra, high-waist leggings,
bare midriff fully exposed, voluptuous figure forward — chin raised, her gaze forward;
her hand gripping his jersey or forearm. Full body visible — her athletic figure from feet to crown,
his bare torso, both fully in frame.
Background: golden-hour empty stadium tunnel, dramatic light shafts from above cutting through dust.
Color palette: warm amber and deep gold, deep shadow, team colors as accent on her wear.
Lighting: directional golden light sculpting his bare torso and her bare midriff, both catching every beam.
Title '{title}' in bold condensed athletic serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Accidental Marriage / Woke Up Wed (Contemporary)
```
Romance novel cover, cinematic photorealistic quality, charged morning-after atmosphere.
FRAMING: medium shot, both figures from hip to crown, both facing toward the viewer.
TWO characters. Man in rumpled dress shirt with two buttons open, sleeves half-rolled —
facing toward the viewer and toward her, expression unreadable, controlled intensity.
His expression: shocked recognition — the expression of a man who woke up to a consequence
he cannot undo and is deciding whether he wants to.
Woman sitting on the edge of the luxury hotel bed facing the viewer, wrapped in a white sheet
clutched to her chest — bare shoulders and legs from mid-thigh down fully visible, hair disheveled,
last night's makeup slightly smudged; holding up a marriage certificate with one hand,
expression of raw vulnerability — lips parted, eyes wide.
Both figures in medium shot, full torsos and faces readable, seated her / standing him
both oriented toward camera.
Two champagne flutes on the nightstand. One overturned. Scattered rose petals.
Background: floor-to-ceiling luxury hotel penthouse windows, golden morning city skyline.
Color palette: ivory white sheet, warm golden morning light, charcoal gray of his shirt.
Lighting: golden sunrise through panoramic windows, warm rim light on her bare shoulders.
Title '{title}' in warm contemporary serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Revenge Return / Secret Children (Family Drama Romance)
```
Romance novel cover, cinematic photorealistic quality, high-stakes emotional drama atmosphere.
FRAMING: full-body shot, primary figure from feet to crown, facing the viewer.
TWO characters — or ONE if drama context calls for it. Primary: woman in elegant power dress
or tailored suit, standing straight facing the viewer, chin raised — returned from exile and
dressed like a reckoning. Her full figure visible — dress, heels, the posture of someone
who rebuilt herself into something they cannot stop.
Her expression: cold possession of her own narrative — jaw set, a ghost of a smile
that contains six years of planning. Eyes facing the viewer.
Optional secondary character: the man from her past, to her side facing slightly away
or toward her with stunned recognition — he is seeing someone he thought he knew.
His hand half-raised toward her, caught between reaching and not daring.
If children are visible: a child's hand in hers at the edge of frame — not the
subject, but the subtext: proof of everything they tried to erase.
The subtext: they erased her name. She came back as a headline.
Background: grand family estate entrance or a glass-and-marble corporate lobby.
The doors are open because she walked in, not because she was invited.
Color palette: deep cold teal or steel blue dress, ivory marble, warm amber interior light.
Lighting: cold overcast light catching her full figure from crown to feet — she is the center.
Title '{title}' in sharp contemporary serif — clean lines, authority. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Romantasy (Romance-Fantasy Fusion)
```
Romance novel cover, semi-realistic illustrated or hyperrealistic 3D render style — NOT photographic
realism, NOT anime. TWO characters.
Female lead center-left: fantasy battle leathers or an asymmetric gown with one armored leg exposed,
deep jewel-tone fabric (midnight blue, blood red, or deep emerald), one hand gripping a glowing
rune-etched sword or trailing warm golden magic from her palm.
Her expression: defiance bleeding into something she has not named yet — jaw set, eyes on him,
body half-turned as if she started to leave and changed her mind.
Male figure right of center: dark plate armor with silver-edged sigils or heavy royal robes over
a broad frame, expression controlled but with one detail that breaks the control — a hand reaching
toward her that stops just short of contact.
One dominant symbolic object occupies the vertical center between them: a serpent coiling upward,
a dragon skull at frame edge, a crown of bone, or a crystal key.
The charged space between their bodies emits an ethereal magical glow — her light warm gold,
his cold blue or silver — the two tones bleeding together at the midpoint, neither winning.
The subtext: she was trained to destroy him. She did not expect the glow to appear when they
stood this close.
Background: suggestion of a fantasy environment (carved stone arch, ruined citadel, fae forest
silhouette) in soft focus — it frames without competing.
Color palette: deep purple or midnight blue base with blood red or emerald accent,
bioluminescent or candlelight lighting on faces, cold silver on his armor.
Lighting: ethereal magical glow from the space between them as primary source,
cold moonlight rim from above, deep shadow filling the rest.
Title '{title}' in whimsical script font, large, top third of frame.
Author '{author}' in bold condensed secondary font below title.
Portrait 2:3, ultra-detailed, no watermark, single dominant mobile-legible element (the magical glow).
```

#### Regression Romance / Second-Chance Time Loop
```
Romance novel cover, cinematic quality, muted time-displaced atmosphere.
Primary composition: single dominant female figure OR double-exposure layered composition.
Foreground: the heroine as she is now — standing with deliberate stillness in contemporary tailored
power dress or period court gown, posture radiating cold possession of her own narrative.
Her expression: cold possession — not grief, not fear, the specific expression of a woman who
has already lived this scene and knows exactly how it ends. Jaw set, gaze forward, mouth with
the faint certainty of someone counting down.
Background ghost layer at 40% opacity: her past self in similar clothing but collapsed,
defeated, or mid-fall — the moment of original betrayal, soft and translucent behind her certainty.
Male figure: if present, turned away from camera or in soft focus at frame edge — his ignorance
of what she knows is communicated by his averted gaze. He is not the center.
One color break in the otherwise muted palette: blood red at the ghost layer's heart for the
original death or betrayal moment, deep sapphire at her hands or feet for the reset point.
The subtext: she died knowing exactly where it went wrong. She woke up with the map.
Color palette: muted gold and grey base, desaturated, both tones blending until the color break.
Matte quality — no neon, no high saturation. The palette communicates weight.
Lighting: cold ambient light on the foreground figure, soft warm diffuse on the ghost layer
behind — the past is warmer, the present colder and more certain.
Title '{title}' in elegant serif or calligraphic script, muted gold. Author '{author}' in clean grey beneath.
Portrait 2:3, ultra-detailed, no watermark.
```

#### Villainess Redemption / Reverse Isekai Romance
```
Romance novel cover, cinematic quality, opulent historical fantasy atmosphere.
Single female figure, center-dominant, filling two-thirds of vertical frame.
She wears elaborate historical fantasy court regalia: full ball gown with intricate beading,
lace overlay, or embroidered panels in deep emerald or burgundy with antique gold trim —
the dress of a condemned woman who chose to wear it anyway.
Her expression is the critical element — achieve precisely: knowing, slightly amused, composed.
NOT victimized. NOT action-heroine fierce. NOT tragic. She looks directly out of frame or
slightly past the viewer as if she sees something beyond the image. The slight curve of her mouth
and the steadiness of her gaze communicate one thing: she has read the ending and is not afraid of it.
Male figure optional; if present, secondary — partially visible at frame edge, facing slightly away,
unaware of what she knows.
The subtext: she woke up as the villainess. She has read this story. The script is about to change.
Background: imperial court interior or palace exterior, warm candlelight and antique gold,
architecturally detailed but soft focus — the figure reads first.
Color palette: deep emerald, burgundy, antique gold, warm cream at highlights. Rose gold overall
register — opulent and knowing, not suffering.
Lighting: warm candlelight from below catching the embroidery and her jaw, soft ambient court
light filling the background, nothing harsh — she is at home here.
Title '{title}' in calligraphic or fine-serif script, rose gold or cream, upper frame.
Author '{author}' in smaller matching serif below.
Portrait 2:3, ultra-detailed, no watermark.
```

#### Monster Romance / Interspecies Romance
```
Romance novel cover, cinematic quality, dark boundary-threshold atmosphere.
TWO figures. Non-human male occupies the larger vertical portion: massive, scaled or shadowed,
marked as non-human — but ONE detail is distinctly human and is the emotional pivot of the image:
a hand extended toward her, palm open, fingers slightly curled; OR a head tilted in attention,
ear angled toward the sound of her; OR eyes tracking her with an intensity no predator uses for prey.
His form is dark, muted, powerful. Bioluminescent accent color (teal, amber, or violet) emanates
from his markings, eyes, or form edges — single saturated color against the near-black,
drawing the eye to the one human gesture he is performing.
Human female figure: smaller in scale, placed close or just within his reach, wearing ordinary
or torn clothing — nothing elevated that equalizes the power scale.
Her expression: the exact moment she realizes she is the only safe person in his world.
Not fear. Not love yet. Recognition — the thing that frightens everything else has rearranged
itself for her specifically, and she has just understood this.
The subtext: everyone in the village knows what lives in the forest. No one comes back.
She is the first one they sent in who was not meant to survive.
Background: dark forest, ruins, or boundary threshold — near-black with organic texture,
bark or stone or collapsed archway, the boundary between the human world and his.
Color palette: near-black base, single bioluminescent accent (her choice — teal most common),
deep forest shadow, the warm skin tone of her face as the only human-warm element.
Lighting: bioluminescent accent from his markings as primary source on her face,
ambient dark engulfing everything else, her face the only warmth in the frame.
Title '{title}' in bold or brushstroke display font in the accent color. Author '{author}' in muted grey beneath.
Portrait 2:3, ultra-detailed, no watermark.
```

#### Dark Academia Romance
```
Romance novel cover, cinematic quality, candlelit institutional atmosphere.
TWO characters in chiaroscuro — one hard candle or oil lamp source carving both faces from
near-total shadow, warm amber light on cheekbones and brows, everything else falling into
deep burgundy-black.
Male figure: academic or institutional authority visible in clothing (waistcoat, open-collar dress
shirt, reading glasses pushed up, or society insignia at lapel), body angled toward her across
a table or in a doorway. His expression: barely-controlled want masked as intellectual contempt —
control that is visibly costing him something. He has not decided what to do with what he knows.
Female figure: her expression openly reads what his does not — she has found something out about
him, and she has not yet decided what to do with it. Not fear. The specific confidence of a woman
who holds information as currency.
Bodies angled toward each other, the charged gap between them is visible negative space —
deliberate and composed, the emotional argument of the image.
Secondary props in soft focus: a single raven on a windowsill, old paper or open book between
them on the table, one extinguished candle with smoke still rising, rain-streaked window
showing only darkness beyond.
The subtext: at this institution, every secret has a price. She just found out what his costs.
Color palette: deep burgundy, candlelight amber, aged parchment, near-black.
No neon, no digital brightness, nothing glossy. Matte finish.
Lighting: single candle as the only source — warm amber carving cheekbones and brows,
deep shadow filling everything else, the smoke of the extinguished candle catching the light.
Title '{title}' in aged serif or gothic letterpress, upper frame or across the gap between figures.
Author '{author}' in smaller matching serif.
Portrait 2:3, ultra-detailed, no watermark.
```

#### Urban Romantasy / Contemporary Paranormal Revival
```
Romance novel cover, cinematic photorealistic quality, contemporary-with-wrong-detail atmosphere.
TWO characters. Contemporary interior or urban threshold — apartment hallway, coffee shop corner,
building lobby at night — with city skyline or rain-streaked window visible in background,
muted and dark, the ordinary world continuing behind them.
Male figure in contemporary clothing (dark coat, simple shirt, nothing elevated) but with ONE
inhuman detail found after the face: iris color slightly wrong — too pale, too gold, too flat;
OR canine teeth one millimeter too long; OR posture too still, the stillness of something that
stopped needing to perform restfulness centuries ago; OR a shadow that does not match his position.
His body language: ancient certainty — he is not anxious; he has survived everything and the
experience has made him very still.
Female figure in completely ordinary contemporary clothing (jeans, work clothes, Tuesday in a
modern city) beside him. Her expression: raw vulnerability — the precise moment of understanding
that something is not right about this person she thought she knew. She is not afraid yet.
She is recalibrating.
The subtext: she thought the city's worst problem was her rent. Then he admitted he had been
alive since 1347. She did not leave.
Color palette by subspecies: cool blue-grey and silver for vampire or immortal; warm amber and
rust for shifter; deep forest green and charcoal for fae-urban. City window provides one note
of familiar indifferent light — life continuing outside while something ancient stands in frame.
Lighting: ambient city glow from the window as cool fill, single interior lamp as warm key
on his inhuman detail and her face, deep shadow filling the rest.
Title '{title}' in semi-bold contemporary sans-serif with one typographic anomaly — a slightly
different weight on one letter, or a ligature that reads as marginally inhuman.
Author '{author}' in clean standard sans beneath.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

---

### Exposure Tiers (pick the highest the model accepts)

Exposure is **stochastic** — the same prompt rolls different skin levels each generation, so a tame result is not a spec failure, it's RNG. To get a reliably high result you must **bake the tier fragments into the prompt**, not leave them to chance and not treat them as a reactive afterthought.

Five named tiers, all strictly above the §0 floor (no nipples / genitals / sex acts). **Production covers = randomly T2 or T3 per cover (roll independently for each book), with doubao.** Illustrations = randomly T3 or T4. Each tier has a designated model based on tested compatibility.

**Model routing (production standard):**

| Tier | Primary model | Fallback |
|---|---|---|
| T1 | `gpt-image-2-all` (cover cascade) → `doubao-seedream-5-0-260128` | retry doubao → `nano-banana-pro` (blank-prevention) |
| T2 | `gpt-image-2-all` (cover cascade) → `doubao-seedream-5-0-260128` | retry doubao → `nano-banana-pro` (blank-prevention) |
| T3 | `doubao-seedream-5-0-260128` | retry once → `nano-banana-pro` (blank-prevention) |
| T4 | `doubao-seedream-5-0-260128` | retry once → `nano-banana-pro` (blank-prevention) |
| T5 | `doubao-seedream-5-0-260128` | retry once → `nano-banana-pro` (blank-prevention) |

> `doubao-seedream-5-0-260128` is the workhorse at **every** tier. `gpt-image-2-all` leads the **cover cascade** at T1/T2 only (cleanest title text); at T3+ it hard-rejects and the cascade falls to doubao. nano is the terminal blank-prevention fallback — **there is no SVG fallback below it.**

**nano-banana-pro — terminal blank-prevention fallback only (not a finished asset):**
- Silently downgrades T3 keywords to ~T1 output; T4 post-event framing → ~T2 at best; square 1024×1024 (not 2:3).
- Stochastic IndexError (soft rejection) at T3+; retry usually fails. Output quality significantly below doubao at all tiers.
- Used only as the cascade's last resort so *some* image exists. Also included in model-test compare pages for reference.

**gpt-image-2-all — excluded at T3+ only (still the cover cascade's first choice at T1/T2):**
- Passes T1/T2 cleanly with the cleanest title text and best brief adherence — it leads the cover cascade and produces most T2 covers.
- Rejects T3+ deterministically (clinging-fabric / multi-zone bare skin); retry does not help, so the cascade falls to doubao for every T3 cover and all illustrations.
- **Not used for T3+ output of any kind.**

**Why doubao for the allure tiers:**
- `doubao-seedream-5-0-260128` — primary at T3/T4/T5 and the cover-cascade fallback at T1/T2; stochastic filter (retry once on rejection); best output quality at T3+; 1664×2496 JPEG output.
- On rejection: retry once with identical prompt. If second attempt also rejects, adjust prompt to remove the triggering clause (see "What doubao T3 accepts vs rejects" table above), then generate.

**Fallback cascade:** gpt (T1/T2) → doubao (retry once → adjust prompt) → nano (blank-prevention). No SVG fallback.

---

#### How to use this guide

Each tier is defined across **8 dimensions**. Write one fragment per dimension into the prompt — do not omit any. Later tiers replace earlier ones per dimension; write T3's version of each dimension directly, do not stack T1+T2+T3.

The 8 dimensions:
1. **Clothing state** — garment integrity and coverage
2. **Skin zones exposed** — which body areas are visible
3. **Fabric behavior** — how the material behaves under the scene conditions
4. **Body contact** — physical distance and touch between figures
5. **Male figure** — his clothing state and physical presence
6. **Camera framing** — shot distance and composition
7. **Emotional register** — expression, posture, internal state
8. **Environment** — setting, atmosphere, amplifiers

---

#### T1 — Suggestive

**Use for:** cold FB traffic, new ad accounts, covers for light/sweet romance, first creative in a new account.

**Viewer feeling:** "they're clearly into each other — I want to know what happens"

| Dimension | T1 specification | Prompt keywords |
|---|---|---|
| **Clothing state** | One revealing element only — neckline OR shoulder slip, not both. Everything else intact. | `off-shoulder gown with one shoulder elegantly slipped`, `low-cut gown showing collarbone and upper chest` |
| **Skin zones** | Shoulders + collarbone + upper chest only. No midriff, no back, no legs past the knee. | `bare shoulders and collarbone`, `upper chest visible above the neckline`, `the curve of her throat catching the light` |
| **Fabric behavior** | Structured and dry. Fabric follows her silhouette but does not cling or reveal. | `fitted elegant gown with clean draping`, `tailored dress, fabric holding its shape` |
| **Body contact** | Close proximity without touching, or a single light non-intimate touch (hand on arm, fingertips at elbow). Tension is suggested, not enacted. | `standing close, barely inches apart`, `his hand resting lightly at her elbow`, `their shoulders almost touching` |
| **Male figure** | Fully clothed. Open collar at most — no bare skin below the throat. Dominant but composed. | `dark button-down shirt, top button open`, `fitted jacket, composed posture`, `dress shirt, sleeves rolled to the forearm` |
| **Camera framing** | Full body or three-quarter shot. Both figures visible head to near-foot. Environment visible and part of the composition. | `full body portrait, both figures`, `three-quarter shot with environment framing them` |
| **Emotional register** | Controlled desire — the look that says something is being held back. No surrender, no desperation. | `smoldering eye contact`, `jaw tight, expression of a man holding himself in check`, `her lips slightly parted, pulse visible at her throat`, `the look of two people pretending they're not thinking about it` |
| **Environment** | Beautiful and lightly charged. Evening light, city skyline, garden at dusk. Romantic but not primal. | `warm golden-hour backlight`, `city lights soft and blurred behind them`, `candlelit interior, soft warm glow` |

**T1 assembly block:**
> *off-shoulder silk gown, collarbone and bare shoulders in candlelight — tall man in fitted dark jacket, top button undone, standing close behind her without touching. His eyes on her profile hold everything he isn't saying. Warm amber interior, city visible through tall windows.*

---

#### T2 — Bold *(production cover tier — rolled 50/50 with T3)*

**Use for:** roughly half of production covers (rolled per book against T3); retargeting warm audiences, accounts with history, dark/contemporary romance where the synopsis is clearly adult. T2 is the safer of the two cover tiers for fresh ad accounts and ad-review crawlers.

**Viewer feeling:** "I need this book right now"

| Dimension | T2 specification | Prompt keywords |
|---|---|---|
| **Clothing state** | Two simultaneous revealing elements — neckline AND one of: shoulder slip, bare back, bare midriff, high slit. Garment is intact but strategically minimal. | `deep plunging neckline to the sternum`, `open-back dress, spine bare from neckline to tailbone`, `crop top leaving midriff fully bare`, `thigh-high slit fully open revealing upper thigh`, `halter neck leaving entire back exposed` |
| **Skin zones** | Cleavage + one secondary zone simultaneously. At minimum: full décolletage + (bare back OR bare legs to upper thigh OR bare midriff). | `ample décolletage fully on display`, `back bare to the waist`, `legs bare from the upper thigh down`, `bare stomach and hip visible at the waist` |
| **Fabric behavior** | Fitted or slightly damp. Fabric suggests the body beneath without fully mapping it. A hint of cling. | `silk dress conforming to her curves`, `damp fabric outlining her figure`, `sheer overlay hinting at the silhouette beneath it`, `thin fabric pulling slightly against her as she moves` |
| **Body contact** | Bodies touching or gripped. One explicit hand on bare skin. Physical tension is undeniable and visible. | `bodies pressed together`, `his hand gripping her bare waist`, `fingers curled around her hip`, `her back against his chest, his arm drawn across her collarbone`, `his hand at the bare small of her back` |
| **Male figure** | Shirt open to mid-chest or partially undone. Bare forearms, sternum, or chest visible. Physical presence is imposing. | `shirt open at the collar revealing bare chest`, `sleeves rolled, forearms corded with tension`, `jacket shrugged off, shirt half-undone`, `shirt open to the third button, chest catching the light` |
| **Camera framing** | Waist-up dominant. Bodies fill two-thirds of frame. Faces close in the upper portion. | `waist-up shot, both bodies filling the frame`, `faces inches apart in the upper third`, `tight three-quarter crop emphasizing the physical closeness` |
| **Emotional register** | Barely-controlled desire crossing into action. One of them is losing the fight. | `lips parted, eyes dark with barely-suppressed desire`, `defiance crumbling into want`, `chin raised but eyes betraying surrender`, `jaw tight, the look of a man who has already decided`, `she grips his wrist — not pushing it away` |
| **Environment** | Charged atmosphere. Rain beginning, intimate dim setting, heat haze, tension before a storm. | `light rain starting, cobblestones beginning to glisten`, `dim bar, warm amber spot lighting`, `night air heavy and still`, `the moment before something irreversible` |

**T2 assembly block:**
> *deep-plunge wrap dress, décolletage fully on display, thigh-high slit open — man behind her, hand gripping her bare hip, shirt open to mid-chest, face against her hair. She grips his wrist. Not pushing it away. Light rain misting the rooftop, city blurred forty floors below.*

---

#### T3 — Maximum *(production cover tier — rolled 50/50 with T2)*

**Use for:** roughly half of production covers (rolled per book against T2). Dark romance, paranormal romance, billionaire/MC/mafia romance, any genre where physical intensity is core to the premise. This is the hotter of the two production cover tiers — it is intentionally pitched above the highest result a lucky T2 roll can produce.

**Viewer feeling:** "this is exactly what I came here for" — instant click, immediate scroll stop

| Dimension | T3 specification | Prompt keywords |
|---|---|---|
| **Clothing state** | Garment failing in multiple places simultaneously. Torn AND slipped AND barely covering. The clothing is in the process of leaving, not covering. Multiple garment failures visible at once. **Use light/white/sheer fabric — dark opaque fabric (especially black leather) renders as coverage regardless of "torn" keywords.** | `white dress torn down the side, held by one strap`, `sheer white blouse falling open`, `ivory silk slip slipped off both shoulders and falling`, `torn white fabric barely covering her, the last thing between her and nothing`, `wet white shirt transparent and clinging` |
| **Skin zones** | Three or more zones simultaneously. Bare shoulder + bare back + upper thigh + midriff. The exposure feels total — the viewer's eye has nowhere to rest that isn't skin. | `bare shoulder, bare back from neckline to tailbone`, `upper thigh fully exposed through the torn slit`, `bare midriff and the curve of her hip`, `skin visible from collarbone to hip`, `the entire curve of her back in the moonlight` |
| **Fabric behavior** | Wet, clinging, or sheer — fabric that maps the body rather than covering it. The material has stopped functioning as clothing. | `rain-soaked fabric transparent and clinging to every curve of her figure`, `wet silk outlining the exact shape of her body`, `sheer fabric leaving nothing to imagination`, `damp clothing pressing against her skin, every line visible`, `wet thin shirt clinging to her chest` |
| **Body contact** | Zero gap. Multiple simultaneous contact points. Skin-to-skin wherever possible. Bodies intertwined, not merely touching. | `bodies pressed flush together, zero space between them, skin to skin`, `one hand gripping her bare waist with fingers pressing into her skin, the other cupping her jaw`, `her bare back against his bare chest`, `thigh locked against thigh, her hip against his`, `hand splayed across the bare small of her back pulling her flush against him` |
| **Male figure** | **Not required to be bare.** Shirt open or removed — choose by genre. Bare torso fits paranormal/shifter/beach scenes. For contemporary/billionaire/historical: shirt open to mid-chest (T2 torso state) is preferred — the partial-undone read creates more tension than already-off. His physical mass is the visual anchor. | Paranormal/shifter: `shirt completely removed, powerful bare chest and carved abs`, `bare torso pressing against her back, rain-slicked in the moonlight`. Contemporary: `shirt unbuttoned to mid-chest, bare sternum visible`, `open shirt hanging off his shoulders, chest catching the light`. Historical: `shirt torn open at the collar, chest partially exposed`. |
| **Camera framing** | Extreme close-up. Faces and bodies fill the frame — there is no wasted space, no environment visible except as abstract light and color. | `extreme close-up, bodies from mid-thigh to crown filling the entire frame`, `tight portrait crop, background dissolved to near-abstraction`, `faces in the upper third, bodies pressed together filling the rest`, `camera so close the background is pure shallow bokeh` |
| **Emotional register** | The point of no return. One of them has stopped fighting and the other knows it. Surrender and raw physical want are visible in every line of the body, not just the face. | `raw physical want, the moment one second before the point of no return`, `expression of total abandon — head thrown back, eyes closed, has stopped fighting it`, `the look of a man who is certain, consuming, possessive — she is already his`, `her expression: she knows this is wrong and her body doesn't care`, `both of them past the point where words would help` |
| **Environment** | Primal, elemental, intimate to the point of erasure. Rain, darkness, fire, moonlight — the environment amplifies desire, it does not decorate the scene. The world outside them barely exists. | `heavy rain pouring down, both of them soaked, cobblestones reflecting silver moonlight`, `single candle or streetlamp, everything beyond them in total darkness`, `moonlight the only light source, cutting hard shadows across wet bare skin`, `steam rising between them in the cold air`, `the dark so complete their faces are all that's lit` |

**T3 assembly block (both toward viewer — default):**
> *flowing white silk dress slipping off one bare shoulder, rain-soaked translucent fabric clinging to every curve of her body, the wet silk transparent against her skin, the full skirt heavy with rain. Her back arched in a long elegant curve, pressing her chest forward — chest heaving with each breath, the fabric barely containing her figure. Bare back exposed, bare shoulder. Both figures at three-quarter angle toward the viewer — both faces readable to the camera. Man beside/behind her, shirt open to the chest (or completely off for paranormal genre), his bare sternum or bare torso visible, one hand gripping her bare waist with fingers pressing into her skin, the other hand at the side of her jaw — steadying, not directing. **His face toward the viewer, jaw set, cold expression of possession — looking at the camera, not at her.** Her face toward the viewer, chin slightly lifted, eyes forward. Neither is looking at the other — the tension is in their bodies. Her expression: fierce surrender. His: absolute possession. Bodies flush together, zero space, skin to skin. Heavy rain, cobblestones reflecting silver moonlight; silver rim light tracing the full curve of her silhouette. The world beyond them dissolved into darkness.*

**T3 assembly block (man-behind-woman accent variant — use at most 1 in 3):**
> *[same fabric/body description as above] Man behind her, shirt completely off [paranormal] or shirt open and hanging [contemporary], powerful bare torso pressing against her bare back, one hand gripping her bare waist, the other at the side of her jaw — steadying, not directing — her face turned outward toward the viewer, not toward him. She faces the camera. His face at three-quarter angle, readable to the viewer — not face-to-face, not gaze-locked. Bodies flush together, zero space, skin to skin.*

> **Style note:** prefer a full flowing skirt over a body-con or short cut — the test-1 doubao image (best result in this series) was a full-length white dress the model chose instinctively. A flowing skirt reads as more romantic and produces more dramatic fabric movement in rain scenes. Not mandatory — body-con and short cuts are valid at T2/T3 for contemporary genres.

> **Note:** `white dress` produces more allure than `leather jacket` even with identical `torn/slipping` modifiers — light fabric renders as transparent when wet; dark leather renders as opaque coverage. Always prefer white/sheer/light fabric for the female lead's primary garment.

---

#### T4 — Limit *(doubao primary · nano fallback)*

**Use for:** maximum-intensity production covers. doubao is the primary model at T4; nano is the fallback if doubao rejects. T4 framing also unlocks ~T2 output from nano (post-event language bypasses nano's keyword filter), making nano useful as a fallback rather than a dead end.

**Viewer feeling:** "buying this right now" — zero hesitation, pure instinct click

**Key differentiator from T3:** T3 shows a garment in the process of failing. T4 shows the aftermath — clothing has already left, only a nominal draping element remains, and the emotional register shifts from surrender-imminent to surrender-complete. The world beyond the two figures has ceased to exist entirely.

| Dimension | T4 specification | Prompt keywords |
|---|---|---|
| **Clothing state** | Clothing has already left. One nominal draping element — a single silk sheet corner, a sheer panel, a wisp of fabric — covers only the minimum required by §0. The garment's function as coverage has ended; it exists only as a composition element. | `white silk sheet corner draped loosely across her hip, barely held in place`, `dress fallen to the floor, a single sheer panel the only remaining cover`, `one wisp of translucent fabric across her, everything else bare`, `the sheer drape the only thing between her and nothing at all` |
| **Skin zones** | Every zone simultaneously except §0-protected: full back from nape to base of spine, full legs from hip to foot, bare midriff, full side silhouette, collarbone, shoulder, upper chest, the curve of her hip. The frame reads as total skin with a single covered point. | `entire bare back from nape to the base of the spine`, `the full curve of her hip and waist`, `long bare legs from hip to foot`, `bare shoulder, collarbone, midriff, and hip all simultaneously visible`, `full-length silhouette — skin from shoulder to ankle` |
| **Fabric behavior** | The fabric has stopped being clothing and become a prop. It drapes, drifts, or pools in a way that emphasizes what it is not covering. Gravity-assisted, wind-caught, or fallen to the floor. | `sheer silk barely moving, covering nothing it was meant to cover`, `fallen white fabric pooled on the floor below her feet`, `single translucent panel drifting off her shoulder with nothing to hold it`, `the drape so light it shifts with each breath, covering only the absolute minimum` |
| **Body contact** | Maximum skin-to-skin across the full torso. His bare chest against her entire bare back from shoulder to hip — no fabric between them at any contact point. Or post-intimacy hold: she rests against him, both bare, his arm drawn possessively across her. | `his bare chest pressed against her entire bare back — skin to skin from shoulder to hip, no fabric, no gap`, `her bare back to his bare torso, his hand flat against her bare stomach`, `both bare, her shoulder at his jaw, his arm drawn across her, possessive and absolute` |
| **Male figure** | Bare from the waist up; lower half out of frame or implied. His body is the environment — she exists against his skin, and his torso is the visual ground for her figure. Every muscle lit by the single light source. | `bare from the waist up, everything below in shadow and out of frame`, `his torso the only surface she rests against, muscles carved by a single amber light`, `bare chest and shoulder, jaw set — she reads as a composition against his skin` |
| **Camera framing** | Skin-ratio crop. Skin:background at 80:20 or higher. Two bodies filling the frame, camera so close that edges and environment dissolve to pure abstracted color. The frame stops just above §0 territory — negative space exists only to create ambiguity, not to show environment. | `ultra-tight hip-to-crown crop, both bodies filling the frame, background pure warm bokeh`, `camera inches from the subject — the edge of the frame creates the only ambiguity`, `composition where bare skin fills 80% of the image and the background is warm abstraction`, `cropped at the hip, torsos and faces filling the rest, no environment visible` |
| **Emotional register** | Post-decision, not pre-decision. The fight is over. The expression is completion rather than anticipation — eyes closed, head fallen back, the specific quiet of someone who stopped pretending they didn't want this. Or the possessive aftermath: he is certain, consuming, looking at her like the question was never in doubt. | `eyes closed, head fallen back, the look of someone who has stopped fighting and found it was the right choice`, `expression of total surrender — not defeat, arrival`, `she is not thinking about consequences; she has become the moment`, `his expression: certain, consuming, possessive — the question was answered before she thought to ask it`, `the specific peace of a surrender that was always going to happen` |
| **Environment** | The environment has ceased to exist. One warm light source (amber candle, single streetlamp, sliver of moonlight) illuminates only skin. Everything beyond the two figures is pure darkness or pure shallow bokeh. The only world is them. | `single amber candle, its warmth on bare skin and nothing else — the room has gone to darkness`, `moonlight the only light, cutting across bare shoulders and dissolving everything beyond`, `bokeh so shallow the background is pure warm abstraction`, `the world outside the frame doesn't exist; there is only light on skin and shadow on everything else` |

**T4 assembly block:**
> *white silk sheet corner barely draped across her hip — entire bare back from nape to the curve of her spine, long bare legs from hip to foot, her shoulder at his jaw. His bare chest her only backdrop, skin to skin from shoulder to hip, no fabric between them anywhere. Ultra-tight crop: skin fills the frame, background gone to warm amber abstraction. Single candle the only light source. Her expression: not surrender but arrival — eyes closed, the look of someone who stopped fighting and found it was right. His: certain, possessive, the question was always already answered.*

> **Model routing at T4:** doubao primary — accepts T4; retry if occasionally rejected. nano fallback — silently downgrades to ~T1 square output (reframe to 2:3); use as-is. gpt: rejects T4, do not attempt.

---

#### T5 — Absolute *(dorsal · no fabric · body + shadow §0 coverage)*

**Use for:** maximum-intensity back-facing implied-nudity covers. Both figures fully unclothed — no fabric anywhere. §0 zones covered **purely by composition**: his body blocks her front from the camera, deep shadow and body overlap cover the lower zone. Her entire bare back is the primary visual. **Frontal T5 consistently rejected by all current models — back-facing is the only viable orientation at this tier.**

**Key differentiator from T4:** T4 retains one nominal draping element (sheet corner, wisp of fabric). T5 has none — coverage is entirely structural: his body in front of her, shadow, and camera positioning. No fabric exists in the frame.

**Viewer feeling:** "everything that can be shown is shown" — total skin read from the back, §0 compliant by body position alone

| Dimension | T5 specification | Prompt keywords |
|---|---|---|
| **Clothing state** | No fabric whatsoever on either figure. Zero garment elements in frame. §0 coverage via his body blocking her front and deep shadow on the lower zone. | `no fabric anywhere in the frame`, `both figures completely bare — coverage by body position and shadow only`, `not a single piece of clothing — his body and shadow are the only cover` |
| **Skin zones** | Her entire bare back from nape to the base of her spine — the primary visual. Full bare legs from hip to foot. His bare torso, arms, shoulders all visible. §0 zones hidden: her front by his body, lower zone by shadow + his body. | `entire bare back from nape to the base of the spine, fully lit`, `long bare legs from hip to foot`, `his bare chest, shoulders, and arms surrounding her` |
| **Fabric behavior** | No fabric. Shadow is the coverage tool. Direct deliberate shadow to fall across the lower §0 zone only; everything else lit. | `no fabric of any kind`, `deep shadow falling only on the lower §0 zone — everything else bare skin in the light`, `shadow as the only cover below the waist` |
| **Body contact** | Bodies fully skin-to-skin. His chest against her back, his body in front of or around her blocking her front from camera. His arms wrapped around her. Maximum contact at every point. | `his bare chest pressed against her bare back, his body blocking her front from the camera`, `bodies fully intertwined, skin-to-skin at every contact point`, `his arms around her, her bare back against his chest, her front shielded by his body` |
| **Male figure** | Fully bare. His body is the structural cover for her front — his chest, torso, and hips between her and the camera when viewed from behind. | `completely bare, his body shielding her front from the camera`, `bare chest, bare torso, bare arms surrounding her from the front`, `his physical mass the only cover for her §0 zones` |
| **Camera framing** | Camera behind her — dorsal view. Her bare back fills the frame. His face visible above her shoulder or beside her. Frame crop at mid-thigh or hip. Shadow handles the lower §0 zone. | `camera behind her, her bare back the primary visual`, `dorsal view: her back from nape to hip, his face above her shoulder`, `frame crop at mid-thigh, shadow covering the lower zone` |
| **Emotional register** | Post-decision, total surrender. Her: head fallen back against his shoulder or turned slightly, expression of complete absorption. His: jaw against her hair, or face turned to camera — possessive, absolute. | `her head fallen back against his shoulder, expression of total absorption`, `his jaw against her temple, eyes closed or looking at camera over her bare shoulder`, `both of them past language — the specific quiet of surrender-complete` |
| **Environment** | Single light source from the side or above, cutting across her bare back. Deep shadow everywhere else. Room erased. | `single side light cutting across her bare back, shadow filling everything else`, `moonlight or candlelight on the curve of her spine, darkness behind`, `room dissolved — only the light on her back and his body around her` |

**T5 assembly block:**
> *Both figures completely bare — no fabric in the frame. Camera behind her: her entire bare back from nape to hip, fully lit. His bare chest against her back, his body surrounding her front, his bare arms around her. Deep shadow on the lower §0 zone; his body covering her front from the camera's angle. Her head fallen back against his shoulder, expression of total absorption — complete surrender. His face above her, jaw at her temple, looking at the camera over her bare shoulder: certain, possessive, absolute. Single side light on the curve of her spine; everything else deep shadow. Room erased.*

> **Model routing at T5:** doubao primary (back-facing no-fabric composition; stochastic — retry once on rejection). nano fallback — silently downgrades to ~T1 square output (reframe to 2:3); use as-is. gpt: rejects, do not attempt. **Frontal T5 rejects consistently across all models — back-facing only.**

---

#### Tier selection guide

| Scenario | Tier | Model |
|---|---|---|
| New ad account, first creative, unknown audience | T1 | `gpt-image-2-all` → `doubao-seedream-5-0-260128` |
| Production cover — safer roll (≈half of covers) | **T2** | `gpt-image-2-all` → `doubao-seedream-5-0-260128` |
| Production cover — hotter roll (≈half of covers) | **T3** | `doubao-seedream-5-0-260128` |
| Illustration / maximum allure, established account | **T4** | `doubao-seedream-5-0-260128` |
| Implied nudity, composition coverage | **T5** | `doubao-seedream-5-0-260128` |
| Primary rejected → fallback (any tier) | same tier | `nano-banana-pro` (blank-prevention — ~T1 output, reframe to 2:3) |
| All models reject (incl. nano) | skip the asset, continue | — |

> **nano behavior:** silently downgrades T3+/T4/T5 clothing-state keywords to ~T1 intact clothing; square 1024×1024 output (reframe to 2:3 after generation). Use as-is when reached — it ensures some image exists rather than none.

**gpt-image-2-all — excluded at T3+ only:** boundary confirmed — passes T1/T2 (leads the cover cascade there), rejects T3+ deterministically. Not used for any T3+ output.

**A/B testing across rounds:** assign a **different tier per round** (round 1 → T1, round 2 → T2, round 3 → T3, round 4 → T4, round 5 → T5), all using doubao primary + nano fallback. Record which combinations produce clean output without rejection or anatomy distortion.

**Never preemptively soften.** A prompt that hasn't been rejected is not "too much." Default to the rolled tier (T2/T3 for covers, T3/T4 for illustrations), trust the model cascade to fall through, and only drop a tier when every model at that tier has explicitly rejected. Stop only at the §0 floor.

---

## Content Safety Rules

### Hard Banned — Absolute Floor (see §0 above)

| Category | Never use |
|----------|-----------|
| Genitals | `genitals`, `vagina`, `penis`, `pubic`, `crotch` |
| Nipples | `nipple`, `areola`, `topless` (female), `bare breasts` |
| Sex acts | `sex`, `intercourse`, `penetration`, `oral sex`, `cumshot` |
| Age | `teenage`, `underage`, `minor`, `high school girl`, `loli` |
| Explicit labels | `pornographic`, `XXX`, `hardcore`, `explicit nudity` |

### Green — Use Aggressively

| Element | Prompt approach |
|---------|----------------|
| Extreme cleavage | `deep plunging neckline to the sternum`, `ample décolletage fully displayed` |
| Bare back | `back completely bare to just above the tailbone` |
| Bare legs | `legs bare to the upper inner thigh`, `micro mini dress`, `thigh-high slit fully open` |
| Bare midriff | `crop top`, `bare stomach fully exposed`, `skin-to-skin at the waist` |
| Wet clinging fabric | `wet silk clinging to every curve outlining her figure` |
| Sheer fabric | `sheer lace overlay, curves visible through the fabric` |
| Torn / slipped clothing | `dress slipped off one shoulder and falling`, `torn fabric barely covering her` |
| Man's bare torso | `shirt completely removed`, `powerful bare chest and abs` |
| Body gripping | `hand gripping her bare hip`, `fingers pressing into her bare waist` |
| Morning-after | `white sheet clutched to chest, bare shoulders, legs from mid-thigh down exposed` |

---

## Complete Prompt Examples

### Academy Uniform
```
Romance novel cover, cinematic photorealistic quality, soft romantic atmosphere.
Young woman in Japanese academy-style sailor uniform — white blouse with navy sailor collar,
navy pleated skirt, white knee-high socks — stands in warm afternoon light.
She looks over her shoulder with a gentle, slightly mysterious expression,
dark hair loosely falling and catching the breeze.
Background: blurred academy courtyard lined with cherry blossom trees in full bloom,
soft bokeh of pink petals.
Color palette: soft white, cherry blossom pink, navy blue accents, warm gold light.
Lighting: golden afternoon sunlight filtering through blossom branches, dreamy bokeh.
Professional book cover, ultra-detailed, portrait 2:3 ratio, no watermark,
keep text inside central safe area (inner 85%).
```

### Nurse Uniform
```
Romance novel cover, cinematic photorealistic quality, clean intimate atmosphere.
Elegant young woman in crisp white form-fitting nurse uniform dress,
small nurse cap with red cross badge, silver stethoscope at neck.
She leans slightly forward, one hand raised to her cap,
composed expression with quietly alluring undercurrent, direct soft gaze at viewer.
Background: soft-focus hospital corridor, warm clinical white light.
Color palette: white, pale grey, red cross accent.
Lighting: soft overhead clinical light, subtle warm fill on face.
Professional book cover, ultra-detailed, portrait 2:3 ratio, no watermark.
```

### Qipao (High Slit)
```
Romance novel cover, cinematic photorealistic quality, Shanghai glamour 1930s aesthetic.
Elegant sophisticated woman in deep crimson silk qipao — mandarin collar,
body-hugging silhouette, high side slit in traditional qipao design — jade ornament in updo.
Three-quarter profile, hand resting on carved wooden table, powerful composed expression.
Background: 1930s Shanghai luxury interior, latticed screens, art deco furniture.
Color palette: deep crimson, ivory, gold accent, warm amber shadow.
Lighting: warm side candlelight, golden hour through art deco windows.
Professional book cover, ultra-detailed, portrait 2:3 ratio, no watermark.
```

### Rain-Soaked
```
Romance novel cover, cinematic photorealistic dark romance quality.
Young woman stands in heavy rain — hair soaked and clinging to face and neck,
damp clothing pressed against her silhouette, a single mascara streak on one cheek.
She tilts her face upward with a raw emotionally complex expression — longing and defiance.
Background: rain-slicked urban street at night, neon signs reflected in puddles.
Color palette: deep blue-black, neon pink and cyan reflections, silver rain threads.
Lighting: dramatic neon overhead, rain catching light as silver threads,
street lamp behind creating strong rim light.
Professional book cover, ultra-detailed, portrait 2:3 ratio, no watermark.
```

### Maid Outfit
```
Romance novel cover, high-quality light novel illustration style, warm elegant atmosphere.
Elegant young woman in classic black and white French maid outfit —
fitted black dress, white lace apron, white lace headband, ruffle trim at cuffs.
Three-quarter pose holding a silver tea tray, one gloved hand to lips, mischievous expression.
Background: European manor drawing room, tall windows with afternoon light.
Color palette: black, white, muted ivory gold, pale rose.
Lighting: soft diffused natural window light, warm interior glow.
Professional book cover, ultra-detailed, portrait 2:3 ratio, no watermark.
```

### Flight Attendant
```
Romance novel cover, cinematic photorealistic quality, modern commercial aesthetic.
Sophisticated young woman in tailored navy airline stewardess uniform —
fitted double-breasted blazer, pencil skirt, white silk scarf at neck, small service cap.
Confident pose, slight head tilt, composed professional expression with subtle warmth.
Background: blurred international airport terminal, floor-to-ceiling windows, blue sky.
Color palette: navy blue, crisp white, silver accent.
Lighting: bright clean terminal daylight, sharp rim light on uniform structure.
Professional book cover, ultra-detailed, portrait 2:3 ratio, no watermark.
```

### Silk Robe Morning
```
Romance novel cover, cinematic photorealistic soft romance quality.
Young woman in loose ivory silk robe, softly disheveled hair over one shoulder,
sitting at bed edge or standing at sheer curtain window, quiet melancholy expression.
Background: luxury bedroom, sheer white curtains, unmade silk sheets in warm ivory.
Color palette: ivory, warm cream, soft gold morning light, pale blush.
Lighting: golden morning sunlight diffused through sheer curtains,
halo effect around figure, floating dust motes in golden beam.
Professional book cover, ultra-detailed, portrait 2:3 ratio, no watermark.
```

### Wall Pin (Two-Character)
```
Romance novel cover, cinematic photorealistic quality, intense dark romance atmosphere.
TWO characters. Tall powerful man in tailored dark charcoal suit presses one hand
flat against wall above, leaning close over a young woman whose back is to the wall —
she looks up with wide eyes, surprise and suppressed tension.
His expression cold and controlled; her upturned face catches the single light source.
Faces close but not touching. The charged space between them is the story.
Background: dim luxury corridor or dark interior, deep architectural shadows.
Color palette: deep charcoal and black, single warm amber light, white shirt contrast.
Lighting: single dramatic side light, deep shadow on far wall,
intense hot spot on her upturned face and his jaw.
Professional book cover, ultra-detailed, portrait 2:3 ratio, no watermark.
```
