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

## Poses

| Pose | Scene | Safe prompt keywords |
|---|---|---|
| **Wall pin** | Man stands over woman against wall, faces close | `man leaning one arm against wall over woman, woman back pressed to wall, faces close but not touching, charged tension, dramatic side lighting` |
| **Chair pin** | Man leans over woman seated in chair | `dominant figure leaning over seated woman in chair, intense close proximity, power dynamic, controlled expression` |
| **Rain-soaked** | Wet hair clinging to face and neck, raw emotion | `rain-soaked figure, wet hair clinging to face and neck, damp clothing, emotionally raw upward gaze, neon-lit rainy night street, silver rain threads in light` |
| **Look back over shoulder** | Three-quarter turn, cheekbone catching light | `looking back over shoulder with mysterious expression, cheekbone catching soft light, hair swept by motion, cinematic depth of field` |
| **Pure side profile** | Side face only, jawline and neckline | `pure side profile, elegant jawline and neckline, downcast or distant gaze, moody window light from one side` |
| **Off-shoulder** | Neckline slightly off one shoulder | `off-shoulder silhouette, elegantly bare collarbone and shoulder line, soft light on skin, fabric gathered gracefully` |
| **Billowing skirt** | Outdoor / wind, dynamic movement | `skirt billowing in wind, fabric flowing dramatically, legs partially visible through motion, golden hour backlight` |
| **Downcast gaze** | Eyes lowered, eyelashes catching light | `downcast eyes, eyelashes catching light, subtle vulnerability, soft chin shadow` |
| **Bedside morning light** | Pillow / bed edge, silk morning light | `bedside morning light, figure half-reclining or sitting at edge, disheveled hair, sheer curtain filtering golden hour, intimate quiet atmosphere` |

---

## English Romance Cover Playbook

Maximum-allure formulas for English romance novel covers within gpt-image-2-all policy.  
**Core rule: always use physical contact. Bodies pressed together is the minimum; aim for poses where removing the prompt description would make the image read as explicit.**

---

### Skin & Clothing Vocabulary (allowed — use aggressively)

**Female:**
- `backless evening gown, back gracefully revealed to the lower back`
- `deep V-neckline, décolletage catching the light`
- `thigh-high slit in gown, leg partially visible through the opening`
- `off-shoulder gown, collarbone and one shoulder elegantly uncovered`
- `sheer fabric overlay suggesting the figure beneath`
- `strapless bodice, shoulders and décolletage above the neckline`
- `corset lacing partially loosened at the back`
- `silk slip dress, thin straps, minimal coverage`

**Male:**
- `dress shirt hanging fully open, defined chest visible`
- `powerful muscular torso, shirt removed` (shifter / paranormal)
- `suit jacket thrown open, white shirt open at collar, glimpse of chest`
- `tattoos covering one arm and chest partially visible through open shirt`

---

### Poses — Ordered Highest to Lowest Intensity (all within policy)

| Pose | Prompt Formula |
|------|---------------|
| **Possessive hold from behind** | `man standing behind woman, one forearm across her collarbone, his lips at her temple or ear, her head tilted back against his chest, her hand gripping his forearm, eyes half-closed` |
| **Against-the-wall dominant** | `man's palm flat on wall beside her head, his knee pressing between her legs, faces one inch apart, her fingers twisted in his open shirt, both breathing hard, charged electric tension` |
| **Chin tilt / throat grip** | `man's large hand cupping woman's jaw from below, tilting her face up to his, his thumb brushing her lower lip, her eyes locked on his, lips parted` |
| **Hip grip in gown** | `man's hand splayed possessively on her lower back, fingers pressing in just above the gown's edge, pulling her flush against him, her hand pressed to his open shirt` |
| **Almost-kiss forehead-to-forehead** | `foreheads touching, noses nearly grazing, lips one centimeter apart, eyes closed or barely open, raw breath visible in cold air or charged stillness` |
| **Neck exposure** | `woman's head thrown back, throat arched and vulnerable, man's lips grazing her neck without biting, his hand in her hair, her fingers gripping his shoulder` |
| **Rain-drenched press** | `two figures pressed together in heavy rain, soaked fabric clinging to every curve, his hand cradling her face, looking down at her with controlled hunger` |
| **Torn/disheveled aftermath** | `gown slipped off one shoulder, hair unraveled from its updo, man's hand at her waist, both breathing heavily, dim candlelight, aftermath tension` |
| **Lap / floor kneeling power dynamic** | `woman kneeling on luxurious floor, hands braced on man's thighs as she looks up at him seated in a throne or chair, his hand loose at his side but gaze commanding` |
| **Bridal carry / lifted** | `man carrying woman, her legs draped over his arm, her gown trailing, one strap fallen, her head against his shoulder, half-lidded eyes` |

---

### Genre-Specific Prompt Formulas

#### Dark Romance / Billionaire Romance
```
Romance novel cover, cinematic photorealistic quality, dark dramatic luxury atmosphere.
TWO characters. Powerful man in charcoal suit, shirt open at the collar, one hand
gripping the woman's jaw from below and tilting her face up to his.
Woman in floor-length backless gown — back elegantly revealed to the waist —
her fingers clutching the lapel of his jacket, lips parted, eyes half-closed.
Faces one inch apart, charged electric tension, the moment before collision.
Background: penthouse interior, floor-to-ceiling city lights at night, deep shadow.
Color palette: charcoal, midnight black, ivory complexion, amber candlelight accent.
Lighting: single warm side light sculpting her back and his jaw, deep shadows everywhere else.
Title '{title}' in elegant serif at top. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Paranormal / Shifter Romance
```
Romance novel cover, cinematic photorealistic quality, dark paranormal atmosphere.
TWO characters. Man with powerful muscular torso — shirt removed —
standing behind woman, his forearm across her collarbone possessively,
her back pressed to his chest, head tilted back against his shoulder.
Woman in torn flowing dress, shoulder and collarbone catching moonlight.
His lips at her temple, eyes glowing faintly amber (werewolf / alpha tell).
Background: moonlit forest clearing, full moon through ancient trees, silver mist at ground.
Color palette: silver moonlight, deep forest black-green, warm amber eye glow, ivory complexion.
Lighting: cold silver rim light on both figures, warm amber from his eyes, misty blue-white ground fog.
Title '{title}' in weathered fantasy serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Vampire Romance
```
Romance novel cover, cinematic photorealistic quality, gothic dark romance atmosphere.
TWO characters. Man in dark Victorian or tailored black coat, pale aristocratic face,
standing behind woman whose head is thrown back — throat arched and vulnerable, pulse line visible.
His lips graze her neck (not biting — grazing), one hand splayed across her collarbone,
the other at her waist pulling her back against him.
Woman in deep burgundy off-shoulder gown, eyes closed, lips parted,
expression of surrender and want simultaneously.
Background: candlelit stone chamber or dark opulent ballroom, rose petals on floor.
Color palette: deep burgundy, ivory complexion, black, gold candlelight.
Lighting: warm flickering candlelight on her arched throat and his angled jaw, everything else shadow.
Title '{title}' in gothic elegant serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Fantasy Romance / Dark Fae
```
Romance novel cover, cinematic fantasy photorealistic quality, dark ethereal atmosphere.
TWO characters. Fae male in dark armor or black robes with silver detail, pointed features,
his hand at the woman's jaw tilting her face to his, faces one inch apart — almost-kiss.
Woman in sheer flowing gown, shoulders elegantly uncovered, hair unbound with flowers woven in,
her hand pressed flat against his armored chest, fingers curled slightly.
Magical light between their faces — the charged space — suggests power exchange.
Background: moonlit fantasy ruins, silver-violet magical light, dark ancient stone.
Color palette: deep violet, silver, ivory complexion, midnight black, faint bioluminescent teal.
Lighting: silver magical glow from between their faces, moonlight from above, violet shadow.
Title '{title}' in silver fantasy script. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Mafia / Cartel / Organized Crime Romance
```
Romance novel cover, cinematic photorealistic quality, high-contrast dark thriller romance.
TWO characters. Man in sharp dark suit, standing behind seated or standing woman,
one hand gripping her hip from the side, the other lifting her chin with two fingers.
Woman in fitted dress (or tactical clothing), looking up at him — not fear, defiance and want.
Bodies pressed close, power dynamic clear but mutual.
Background: luxury rooftop terrace at night, city below, dramatic storm clouds or neon wash.
Color palette: deep black, sharp white, muted gold, single red accent (lipstick / light).
Lighting: harsh dramatic side light on his jaw and her cheekbone, deep shadow fills the rest.
Title '{title}' in bold condensed serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Contemporary Romance (Fake Dating / Marriage of Convenience)
```
Romance novel cover, cinematic photorealistic quality, intimate contemporary atmosphere.
TWO characters. Man in casual open-collar shirt or rolled-sleeve button-down,
forehead pressed to woman's forehead — noses nearly grazing, both eyes closed or barely open.
His hand cradling her face, her hand pressed to his chest over his heart.
Lips millimeters apart, the held breath of the moment before they stop pretending.
Background: warm golden interior — kitchen, hotel room, rain-streaked window — soft bokeh.
Color palette: warm amber, ivory, soft shadows, natural skin tones.
Lighting: golden hour or warm practical interior light, soft shadows, intimate glow.
Title '{title}' in warm elegant serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

#### Sports Romance
```
Romance novel cover, cinematic photorealistic quality, charged competitive atmosphere.
TWO characters. Both in athletic or casual-athletic clothing — fitted, revealing physique.
He stands in front of her, chest close to hers, looking down with controlled intensity.
She tilts her chin up to meet his gaze — neither backing down, but the air between them
is not combat, it's want they're both refusing to admit.
Her hand briefly touching his arm or jersey, his hand near but not quite on her waist.
Background: stadium tunnel, track at golden hour, gym with dramatic light shafts.
Color palette: warm golden light, deep shadow, team colors as accent.
Lighting: directional golden athletic light, high contrast, sweat-sheened skin.
Title '{title}' in bold athletic serif. Author '{author}' at bottom.
Portrait 2:3, photorealistic, ultra-detailed, no watermark.
```

---

### Escalation Strategy (if first generation is too tame)

If the generated cover looks like two people standing politely near each other:
1. Add `bodies pressed flush against each other, no space between them`
2. Add `his hand visibly gripping her [waist / hip / jaw]`
3. Add `her [fingers clutching his shirt / hand pressed against his chest]`
4. Specify `close-up composition cropped at torso — faces and upper bodies fill the frame`
5. Add `raw sexual tension, the moment one second before the breaking point`

Do NOT add explicit content. The goal is maximum implication through body language, not description of acts.

---

## Content Safety Rules

### Banned Terms — Do Not Use

| Category | Banned | Safe alternative |
|---|---|---|
| Age | `teenage`, `underage`, `minor`, `high school girl`, `loli`, `young teen` | `young woman`, `elegant woman`, `college-aged woman`, `sophisticated` |
| Uniform + age | `high school uniform`, `teenage school girl` | `academy uniform`, `preparatory school uniform`, `Japanese-style school blazer` |
| Nudity | `naked`, `nude`, `topless`, `exposed breast` | `off-shoulder`, `bare collarbone`, `elegant neckline`, `decolletage` |
| Explicit | `erotic`, `sexual`, `explicit`, `lewd` | `alluring`, `intimate atmosphere`, `charged tension`, `romantic` |
| Wet transparency | `see-through wet shirt`, `wet transparent fabric` | `rain-soaked fabric`, `damp clothing`, `wet silk clinging` |

### Safety Level by Element

| Element | Safe for photorealistic? | Notes |
|---|---|---|
| Academy / school uniform (adult-appearing) | Safe | Do not pair with age terms |
| Nurse / flight attendant / police / maid / business | Safe | Professional uniforms are unrestricted |
| Qipao high slit | Safe | Describe as qipao design feature, not nudity |
| Rain-soaked hair | Safe | Avoid transparency emphasis; use `damp fabric` not `see-through` |
| Bedside morning light | Safe | `intimate atmosphere / morning light` — do not describe nudity |
| Wall pin | Safe | Emphasize tension / close proximity, not body contact details |
| Billowing skirt / legs | Safe | `legs partially visible through motion` is acceptable |
| Silk robe / slip | Safe | `silk slip dress / robe` is standard clothing description |
| Off-shoulder / collarbone | Safe | `off-shoulder`, `bare collarbone` both safe |

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
