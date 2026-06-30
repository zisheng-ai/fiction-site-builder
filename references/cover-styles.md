# Cover Styles

Reference for `story-cover.md`. Genre-to-visual-style mapping for cover image generation prompts.

## Site-Level Style Decision

**Before generating any covers, determine the site's primary visual register.** All books on the same site use the same render style — do not mix styles across books unless the site explicitly mixes genres (e.g. a general fiction platform).

| Site theme | Visual register | When to use |
|---|---|---|
| **Cinematic Drama** | AI film-still quality, photorealistic real actors, high contrast, emotion-first composition | Site hosts Urban Drama / Contemporary Romance / Thriller / Historical Court Drama content — contemporary or historical drama where characters feel human and real |
| **Dark Fantasy Illustration** | Hyperrealistic 3D render, near-black atmospheric background, gold/silver metallic typography, epic world elements | Site hosts Cultivation Fantasy / Dark Fantasy / Sci-Fi content — power systems, fantasy worlds, sci-fi |

Determine which register fits the site during **Phase 6 (Design plan)** and record it in the design-system notes. All Phase 3 cover generation for that site uses the same register.

If the site mixes genres, default to **Cinematic Drama** for realism-leaning titles and **Dark Fantasy Illustration** for genre-fantasy titles, but keep color palettes harmonized across covers so the homepage grid feels cohesive.

---

## Visual Style Standard

Both registers target **photorealistic or hyperrealistic 3D render quality** — not painted, not anime, not watercolor. The reference aesthetic is:

- **Cinematic Drama** (Urban Drama / Contemporary Romance / Thriller / Historical Court Drama): AI-generated film-still quality. Characters look like real actors in a directed scene. High contrast, shallow depth of field, emotion-first composition. Think: prestige drama movie poster or streaming series thumbnail.
- **Dark Fantasy Illustration** (Cultivation Fantasy / Dark Fantasy / Sci-Fi): Hyperrealistic 3D render, dark gradient background (deep black → navy/purple), character in detailed fantasy or sci-fi attire, dramatic atmospheric lighting. Gold/silver/chrome metallic typography is large and dominant in the lower 35% of the frame.

**Shared quality keywords (include in every prompt):**
`photorealistic, ultra-detailed, cinematic lighting, 8K render, professional book cover, shallow depth of field, dramatic atmosphere`

---

## Composition Templates

Pick the template that best matches the book's core tension. These mirror the reference visual language.

| Template | When to use | Description |
|---|---|---|
| **Power Inversion** | Urban Drama / Contemporary Romance revenge, humiliation, domination arcs | **TWO characters.** One standing figure (powerful, cold, composed) looks down at a kneeling/crying/bound figure. Third character optional as witness. Setting: luxury interior, parking garage, ballroom. |
| **Intimate Tension** | Contemporary Romance / Urban Drama romance, billionaire arcs | **TWO characters.** Two figures in close proximity — woman wrapped in white bed sheet with bare shoulders and legs visible to mid-thigh, clutching sheet to chest, expression of shock or conflict; man in open-collar shirt at rest on rumpled bed watching her. Luxury penthouse bedroom, floor-to-ceiling cityscape windows. Foreground props: champagne flute, scattered luxury items (jewelry, lipstick). |
| **Rain Shelter** | Thriller / Contemporary Romance dark romance, protection arcs | **TWO characters.** Two figures on a wet night street, one holding a black umbrella over the other. The protected figure looks downcast; the protector looks stern or conflicted. City lights reflect on the wet pavement. Setting can be European street or neon city. |
| **Grand Humiliation** | Contemporary Romance / Urban Drama gala/elite society arcs | **TWO characters.** Glamorous dominant figure in deep-V plunging neckline floor-length gown (thigh-high slit, jeweled décolletage, red lips, chandelier jewels) stands elevated or turns away in contempt while a male figure kneels or collapses crying at her feet. Grand ballroom setting: chandeliers, champagne tower, roses, crowd of onlookers. |
| **Lone Hero** | Cultivation Fantasy / Sci-Fi / Historical War Epic | **ONE character.** Single powerful protagonist fills center-left frame, facing slightly away from camera. Epic world behind: ruined city + energy portal (sci-fi), snowy mountains + dark castle (fantasy), cloud sea + ancient pagodas (cultivation). Title in large metallic font occupies lower 35% of frame. |
| **Duo Confrontation** | Dark Fantasy / Historical Court Drama romance + power | **TWO characters.** Two characters pressed together — powerful male behind or beside protected female. Dark dramatic background. Matching detailed costumes. Both look into distance or at camera with intensity. |

---

## Genre Detection Keywords

| Keywords in title | Genre | Style tag |
|---|---|---|
| cultivat / sect / dao / qi / immortal / ascend / spirit realm / xianxia / clan / celestial | Cultivation Fantasy | `hyperrealistic 3D cultivation fantasy, dark misty atmosphere, divine golden light` |
| CEO / billionaire / revenge / empire / tycoon / steel / enemies / forbidden / office / heir | Urban Drama | `cinematic photorealistic urban drama, film still quality, high contrast` |
| palace / imperial / dynasty / court / throne / queen / crown / emperor / concubine / majesty | Historical Court Drama | `hyperrealistic historical court drama, rich imperial colors, candlelight` |
| arranged / contract / marriage / secretly / pretend / fake / fake-dating / forbidden / always / forever | Contemporary Romance | `cinematic photorealistic modern romance, soft luxury atmosphere, warm glow` |
| detective / murder / missing / suspect / truth / shadows / case / killer / silent / dark / lies | Thriller | `dark cinematic thriller, noir rainy atmosphere, chiaroscuro lighting` |
| space / mech / cyber / apocalypse / system / evolution / android / orbital / future / neon | Sci-Fi | `photorealistic sci-fi composite, dark blue black palette, glowing energy, futuristic cityscape` |
| dragon / realm / lord / elf / arcane / magic / shadow / prophecy / fae / chosen / blood / fallen | Dark Fantasy | `hyperrealistic dark fantasy 3D render, black background, gold silver metallic elements` |
| war / army / general / battle / soldier / medieval / crusade / knight / siege / conquer | Historical War Epic | `cinematic historical war epic, dramatic battlefield lighting, iron and fire` |
| ghost / haunted / demon / curse / ritual / possession / spirit / necromancer / eldritch / horror | Horror | `dark horror atmosphere, eerie green glow, cinematic supernatural tension` |
| isekai / reincarnated / another world / hero / quest / level / guild / academy / otome | Isekai / Slice of Life | `vibrant anime-adjacent illustration, bright colors, expressive characters` |

---

## Title Font Style by Genre

| Genre | Title font keywords |
|---|---|
| Cultivation Fantasy | `large bold golden embossed calligraphy with metallic glow, ornate separator lines above and below` |
| Urban Drama | `bold modern sans-serif in silver-white with subtle metallic sheen, clean layout` |
| Historical Court Drama | `elegant golden traditional serif, ornate red-gold border frame` |
| Contemporary Romance | `soft white rounded serif, warm glow, tagline in small italic below` |
| Thriller | `stark white or blood-red condensed sans, sharp and cold` |
| Sci-Fi | `chrome metallic condensed sans-serif, electric blue edge glow, large and aggressive` |
| Dark Fantasy | `large gold embossed fantasy serif with glow halo, tagline text above and below in small spaced serif` |
| Historical War Epic | `heavy stone-carved serif in deep red-gold` |
| Horror | `eerie dripping gothic in sickly green-black` |
| Isekai / Slice of Life | `colorful cartoon outlined bubbly font with star accents` |

---

## Author Name Style by Genre

| Genre | Author name keywords |
|---|---|
| Cultivation Fantasy | `small refined white serif, faint golden glow, flanked by cloud-scroll ornaments, thin gold horizontal line` |
| Urban Drama | `small clean white modern sans, subtle drop shadow, thin silver divider` |
| Historical Court Drama | `small elegant dark red traditional text, thin golden rectangular border` |
| Contemporary Romance | `small soft white serif, tiny heart or petal motif, light sparkle` |
| Thriller | `small pale grey, near-hidden in shadows, thin cracked line underneath` |
| Sci-Fi | `small crisp white monospace, cyan scanline overlay, geometric bracket flanks` |
| Dark Fantasy | `small bronze medieval script, decorative shield or crest shape` |
| Historical War Epic | `small dignified white serif, double red horizontal line` |
| Horror | `small faded grey-green, slightly tilted, dripping ink line above` |
| Isekai / Slice of Life | `small playful rounded white, pastel outline, star decorations` |

---

## Genre Visual Details

### Cultivation Fantasy
- **Render style:** Hyperrealistic 3D dark fantasy render. Character fills 60% of frame, atmospheric world behind.
- **Colors:** Deep black → cold blue gradient base; gold and teal accent; divine white light beams
- **Characters:** Male — long tied or loose hair, sword or artifact held up, flowing dark robes with gold trim. Female — translucent fairy dress, glowing spiritual beast companion, lotus motif.
- **Background:** Vast cloud sea, sacred snow-capped mountains, ancient glowing pagodas, spiritual energy vortex
- **Lighting:** `divine golden light rays breaking through storm clouds, mystical mist, spiritual energy glow radiating from artifact`
- **Composition:** Lone Hero template; title in large gold in lower 35%

### Urban Drama
- **Render style:** Cinematic photorealistic. Film still quality — characters look like real actors in a directed scene.
- **Colors:** Deep grey + cool blue base; warm amber/gold accent for luxury interiors; neon color for night streets
- **Characters:** Power dynamic compositions dominate. Male — tailored suit, sharp jawline, cold or dominant expression. Female — designer clothes or disheveled vulnerability.
- **Background:** Luxury penthouse interior, underground parking, corporate lobby, rainy city streets, gala ballroom
- **Lighting:** `dramatic chiaroscuro, harsh overhead light for power scenes, golden sunset for luxury interiors, neon reflections on wet streets`
- **Composition:** Power Inversion / Intimate Tension / Grand Humiliation templates

### Historical Court Drama
- **Render style:** Hyperrealistic period drama photography. Rich fabric textures, intricate costume detail.
- **Colors:** Imperial red + gold + deep ink black; jade green and imperial yellow accents
- **Characters:** Female — full elaborate court dress, phoenix crown, heavy ornate makeup, hair with gold hairpins. Male — emperor robes or general armor.
- **Background:** Grand palace halls, red-wall courtyards, silk curtains, golden lantern rows, cherry blossom garden
- **Lighting:** `warm golden candle and lantern glow, silk fabric shimmering, shafts of light through palace lattice`
- **Composition:** Duo Confrontation template; female in foreground, imperial setting dominant

### Contemporary Romance
- **Render style:** Cinematic photorealistic. Warm film grain quality, dreamy atmosphere.
- **Colors:** Warm cream + blush pink + soft gold; rainy blue-grey for dramatic variants
- **Characters:** Couple — emotional tension is the subject. Female often vulnerable (white bed sheet clutched to chest, bare shoulders and thighs exposed; or wet, disheveled). Male in open-collar shirt, at rest or looming, watching her. Foreground props: champagne flute, scattered jewelry, luxury items on glass table.
- **Background:** Luxury penthouse bedroom with floor-to-ceiling city skyline windows (golden sunset preferred); or rainy street
- **Lighting:** `golden sunset pouring through panoramic windows, warm rim light on her bare shoulders, cool shadow on the man behind`
- **Composition:** Intimate Tension template (white sheet variant at highest intensity) / Rain Shelter template

### Thriller
- **Render style:** Cinematic dark photography. Stark, high-contrast, emotionally cold.
- **Colors:** Near-black + deep charcoal + cold blue; single accent in blood red or pale yellow
- **Characters:** Silhouette or partial reveal; calm/stone-faced expression. Rain Shelter composition is common — power gap between protector and protected.
- **Background:** Rain-slicked cobblestone streets, European stone buildings, dark alleys, foggy night bridges
- **Lighting:** `dramatic chiaroscuro, single hard overhead light or street lamp, rain-slicked surface reflections`
- **Composition:** Rain Shelter template with cold power-gap energy

### Sci-Fi
- **Render style:** Photorealistic composite / dark digital painting. Gritty and cinematic.
- **Colors:** Deep blue-black base; electric blue / cyan / purple energy glow; chrome silver
- **Characters:** Male in tactical armor or mech suit, back or side profile, one knee up on a ledge. Expression: steely, determined.
- **Background:** Futuristic cityscape from high above; energy portal / dimensional rift in sky; floating structures, neon corporate towers, crashed ships
- **Lighting:** `electric blue energy glow from portal above, city neon light from below, rim light on armor edges`
- **Composition:** Lone Hero template (back-to-viewer); title in large chrome lower 40%
- **Tagline:** Small serif text at very bottom: short punchy lines referencing the system/power concept

### Dark Fantasy
- **Render style:** Hyperrealistic dark fantasy 3D render. Near-black background with dramatic spot lighting on characters.
- **Colors:** Near-black base; deep navy/charcoal atmosphere; gold, silver, and burgundy accent
- **Characters:** Male protagonist in dark ornate robes/armor with gold detailing; female in matching dark dress with crown or tiara. Together or side-by-side.
- **Background:** Snow-covered mountains and dark gothic castle with glowing windows; stormy clouded sky; falling snow or embers
- **Lighting:** `moody dramatic backlight from glowing castle, falling snow catching light, gold trim on costumes catching a rim light`
- **Composition:** Duo Confrontation template (upper 65%); large gold title lower 35%; tagline text top and bottom in small spaced serif
- **Typography note:** Title is the most visually prominent element after characters. Two-line title common: first line smaller, second line very large.

### Historical War Epic
- **Render style:** Cinematic historical epic photography. Textured, weighty, grand scale.
- **Colors:** Iron grey + deep red + earth yellow; amber fire glow accent
- **Characters:** General in battle-worn armor, sword or spear, commanding posture. Army or battlefield context.
- **Background:** Battlefield panorama, fortress walls at dusk, beacon fire towers, war smoke
- **Lighting:** `dramatic sunset over battlefield, beacon fire glow, smoke-filled sky, armor glinting in dying light`
- **Composition:** Lone Hero (general facing battlefield) or Duo Confrontation (rivals)

### Horror
- **Render style:** Dark atmospheric photography with supernatural compositing.
- **Colors:** Ink black + sickly green + dark red; faded paper yellow accent
- **Characters:** Ordinary person (fearful) contrasted with supernatural presence (ghost, demon). Hunter in ritual attire optional.
- **Background:** Night cemetery, crumbling ancient temple, dark alley with paper lanterns, coffin-lined passage
- **Lighting:** `eerie green ghost glow, flickering yellow candlelight, cold moonlight, shadows swallowing periphery`
- **Composition:** Lone figure at center, supernatural threat looming from darkness behind

### Isekai / Slice of Life
- **Render style:** High-quality anime illustration style — bright, clean linework, expressive faces.
- **Colors:** Bright multi-color; star / petal / sparkle accents; pastel or vivid depending on tone
- **Characters:** Cute protagonist; cat ears, wings, fantasy school uniform, chibi options
- **Background:** Fantasy isekai world, sparkling academy, starry night sky
- **Lighting:** `magical particle sparkles, soft luminous backlighting, vivid colored light`
- **Composition:** Character facing forward, friendly expression, colorful background

---

## Prompt Quality Checklist

Before sending a prompt to the image API, verify:
- [ ] Render style keyword included (`photorealistic`, `hyperrealistic 3D render`, `cinematic`)
- [ ] Color palette specified
- [ ] Lighting description included
- [ ] Composition template selected and described
- [ ] Title text placement described (lower 35–40% for fantasy/sci-fi; overlay for drama)
- [ ] `portrait orientation, 2:3 ratio, 1024x1536` specified
- [ ] `professional book cover, ultra-detailed, no watermark` included
- [ ] `keep text inside central safe area (inner 85%)` included
