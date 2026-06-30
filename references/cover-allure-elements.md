# Cover Allure Elements

Reference for `story-cover.md`. Visual allure elements for fiction cover generation — AI prompt engineering guide.

Use for: romance, thriller, contemporary, drama, and light novel covers requiring strong visual appeal within gpt-image-2-all policy.

---

## 0. Monetization risk note (read before generating)

**Default business model: Facebook paid traffic + AdSense/AdX arbitrage** (see `references/adsense-arbitrage.md` §1). The cover is the landing-page hero image and is scanned by **both** Meta's ad-review crawler and AdSense's brand-safety classifier. Suggestive, "擦边" covers — cleavage, curvy/busty figures, off-shoulder, low-cut necklines, charged proximity — are **allowed**: maximize visual appeal aggressively.

Only keep in mind the two things that cause hard, irreversible damage (and that the image API will refuse to generate anyway):

- **Actual nudity / explicit content** — exposed genitals or nipples, sex acts, or imagery that reads as pornographic. This trips the `gpt-image-2-all` filter, and on a live site can get the Facebook ad account permanently banned and AdSense disabled.
- **Cloaking** — never show FB's crawler a tame page and users a racier one.

Everything short of explicit (suggestive poses, deep cleavage, figure-forward bodies, wet/rain looks, bed-sheet morning scenes) is fair game — push it as hard as the visual appeal benefits from. Use the safe-wording rules later in this file to avoid tripping the generator's own keyword filter while still getting the spice.

---

## Costume Elements

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

- **Visual:** Black fitted leather jacket, leather pants or miniskirt, boots
- **Best for:** paranormal romance, urban fantasy, biker MC romance, dark contemporary
- **Prompt:**
  ```
  woman in black fitted leather jacket falling off one bare shoulder, skin-tight leather pants,
  heavy boots, leather jacket partially open revealing bare midriff,
  urban nighttime street, neon backlight, hard-edged rim light catching the leather sheen
  ```
- **Allure tip:** jacket slipping off = instant skin reveal with zero filter risk. Pair with `no shirt underneath, jacket barely covering her chest`.

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

## Poses

### Camera Framing — State Explicitly in Every Prompt

Front-facing compositions outperform side-profile and back-view on scroll-stop rate. **Frontal = default. Side profile = accent only.**

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
| **Standing confrontation** | Face to face, charged gap visible | `two figures face to face, bodies close but not touching, both in three-quarter view facing camera, full torsos and legs visible, his hand reaching toward her jaw not yet touching, her chin raised in defiance` |
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

### Poses — Ordered Highest to Lowest Intensity (all within §0 floor)

Default to the **top three** — all frontal. From-behind poses (marked ▲) are dramatic accents, not defaults — use at most 1 in 3 covers. Always pair a pose with the Camera Framing instruction above.

| Pose | Prompt Formula |
|------|---------------|
| **Frontal chest press** | `man and woman chest-to-chest, his hands gripping both her hips pulling her flush against him, her hands fisted in his open shirt, both at three-quarter angle facing the viewer — full-body shot hip to crown, her voluptuous figure pressed into him, every curve of her dress against his chest` |
| **Against-the-wall — bodies locked** | `man's body pinning woman to the wall, his thigh pressed between her legs, one hand flat on the wall above her, the other gripping her waist and pulling her hips into him, her leg hooked around his, fingers twisted in his open shirt, faces one centimeter apart, both breathing hard — medium shot, she faces viewer, full torsos visible` |
| **Power lift — face level** | `man's hands gripping her waist lifting her until their faces are level, her legs hanging with dress riding up to bare the thigh, both facing the viewer, her hands gripping his shoulders, full-body shot` |
| **Chin tilt — almost-collision** | `man's large hand cupping woman's jaw, thumb pressing her lower lip open, tilting her face up to his until their lips are a breath apart, her hands clutching his open shirt, arching her body into his, eyes barely open, raw wanting expression — medium shot showing both torsos, not a head crop` |
| **Standing confrontation — charged gap** | `man and woman face to face, bodies one inch apart but not touching, both at three-quarter angle facing the viewer, his hand reaching toward her jaw not yet making contact, her chin raised in defiance, his expression of absolute certainty — full-body shot, legs and clothing fully visible` |
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
hand gripping her jaw and tilting her face toward his. Both figures oriented toward the
viewer so the full silhouette of both is readable — his bare chest and abs visible,
her voluptuous figure from feet to crown.
His expression: absolute cold possession, eyes glowing amber, jaw tight with
barely-contained instinct — the expression of a man who has claimed something and
the world can argue later.
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
pointed features, his hand at the woman's jaw tilting her face up to his, faces one inch apart.
Both figures face the viewer — the jaw-tilt brings their faces together while keeping both bodies
visible and forward-facing, clothing and figures readable from hip to crown.
His expression: cold ancient amusement and absolute want — the expression of someone who has
never been told no and finds it unexpectedly interesting that she is trying.
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
TWO characters facing each other and angled toward the viewer — both bodies fully readable.
He bare chest or fitted athletic shirt torn open, muscular torso and abs fully visible —
sweat-sheened, still running warm from competition. He looks at her with controlled intensity,
jaw tight, not letting himself look away.
His expression: defiance + desire — he's been told she's off-limits and cannot find a reason
that still makes sense. Eyes dark, decision already made.
She facing him at camera angle, in fitted athletic wear — sports bra, high-waist leggings,
bare midriff fully exposed, voluptuous figure forward — chin raised to meet his gaze;
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

### Exposure Tiers (擦边分级 — pick the highest the model accepts)

Exposure is **stochastic** — the same prompt rolls different skin levels each generation, so a tame result is not a spec failure, it's RNG. To get a reliably high result you must **bake the tier fragments into the prompt**, not leave them to chance and not treat them as a reactive afterthought. Three named tiers, all strictly above the §0 floor (no nipples / genitals / sex acts):

| Tier | Name | Bake these fragments into every prompt at this tier |
|---|---|---|
| **T1** | Suggestive | `off-shoulder gown slipping`, `elegant deep neckline`, `close charged proximity`, `bare shoulders and collarbone` |
| **T2** | Bold | T1 **plus** `deep plunging neckline to the sternum`, `ample décolletage fully on display`, `bodies pressed flush together, zero space between them`, `his hand gripping her bare waist` |
| **T3** | Maximum (default for covers) | T2 **plus** `dress torn / slipped / fallen — bare shoulder + bare back + upper thigh exposed`, `wet fabric clinging to and outlining every curve of her figure`, `his shirt completely off, powerful bare torso pressing against her`, `close-up crop at chest and face filling the frame`, `raw physical want, one second before the point of no return` |

**Default for production covers = T3.** Do not start tame and escalate only if it looks weak — start at T3 and let the model's content filter be the only thing that pulls it back. T3 is intentionally pitched **above** what a lucky T2 roll produces, so output reliably clears the highest previous results. The only reason to drop a tier is an actual model rejection: on `invalid_prompt` / `safety` / `rejected`, fall to the cascade's more permissive models first (they usually pass T3), and only soften the tier as the last resort before SVG.

**A/B testing across rounds:** when running model comparison rounds, assign a **different tier per round** (round 1 → T1, round 2 → T2, round 3 → T3) so each model's ceiling is mapped — which tier it renders cleanly, where it starts refusing or distorting anatomy. Keep the tier identical across all models within a round so the round is a fair comparison. Record which (model × tier) combinations pass; the production default is the highest tier the chosen model clears without rejection or anatomy breakage.

Stop only at the §0 floor. Never soften a prompt to "be safe" unless the model actually rejects it.

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
