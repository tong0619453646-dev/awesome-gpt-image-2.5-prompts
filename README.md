<div align="center">

<a href="https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2.5-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2.5 Prompts" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-209_cases-111111)](README.md#menu)
[![Try GPT Image 2.5 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2.5-on_APIKO-4F46E5)](https://apiko.app/models/gpt-image-2.5-flare?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=model_try)
[![GPT Image 2.5 API docs](https://img.shields.io/badge/GPT_Image_2.5-API_docs-111111)](https://apiko.app/docs/api-manual/image-series/gpt-image-2.5-flare/images?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Current-111111)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome GPT Image 2.5 Prompts

<a id="introduction"></a>
## 🌟 Introduction

**GPT Image 2.5 prompts: 209 copy-ready examples with result images, from portraits and posters to UI mockups, sprite sheets and image edits.**

GPT Image 2.5 prompts that already produced a good image: copy one, or send it to the playground and change the details.

Search and filter them on [apiko.app/gpt-image-2-5-prompts](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=intro).

> [!NOTE]
> Each prompt is kept exactly as its author posted it, so most are in English; titles and descriptions are ours. Every case credits the author and links to the original post.

<a id="quick-start"></a>
## 🚀 Quick start

**In the browser:** every case has a **Run on APIKO** link. It opens the example on [apiko.app](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=browser); press **Use** there to load the prompt into the GPT Image 2.5 playground.

**With the API:** create an [APIKO API key](https://apiko.app/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=api_key), then create an async task and poll it until the image is ready.

```bash
export APIKO_API_KEY="your_key_here"

TASK_ID=$(curl -s https://api.apiko.app/v1/images/generations \
  -H "Authorization: Bearer $APIKO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "model": "gpt-image-2.5-flare",
  "prompt": "A minimalist poster of a paper boat on a calm lake at sunrise, the title \"Morning\" in bold serif type.",
  "size": "16:9",
  "resolution": "1k",
  "quality": "medium",
  "async": true
}' | python3 -c 'import json,sys; print(json.load(sys.stdin)["id"])')

# When status is "completed", the image is at data[0].url (kept for 24 hours).
while :; do
  TASK=$(curl -s https://api.apiko.app/v1/tasks/$TASK_ID \
    -H "Authorization: Bearer $APIKO_API_KEY")
  printf '%s\n' "$TASK"
  printf '%s' "$TASK" | grep -qE '"status": *"(completed|failed)"|"error": *\{' && break
  sleep 5
done
```

Endpoints: `POST https://api.apiko.app/v1/images/generations` (create a task) · `GET https://api.apiko.app/v1/tasks/{id}` (read the status and result)

<a id="how-to-write"></a>
## ✍️ How to write a GPT Image 2.5 prompt

Five structures that recur in the prompts on this page.

- **Photo** · `Subject + action + camera and lens + light + texture` — Portrait prompts name a lens ("50mm"), the shot distance, the light and the skin or material detail, then say what to avoid, such as heavy retouching.
- **Exact text** · `Quoted words + where they sit + type style` — Put every word the image must show in quotes, say where each line goes and how it looks, and ask for correct spelling when the text is long.
- **Edit** · `One change + "keep everything else"` — Edit prompts state a single change and close with what must stay untouched: the face, the layout, the lighting.
- **Sheet or grid** · `Count + grid size + what each cell holds + background` — Sticker packs, sprite sheets and poster grids say how many cells there are, how they are arranged, and whether the background is transparent or a flat colour.
- **Structured spec** · `Fields such as title, scene, subject, lighting, composition` — Long prompts are written as JSON or a Markdown outline, and reusable ones leave a placeholder like {subject} or [OBJECT] to fill in.

**What the examples show**

- **State the shape in the prompt.** Many prompts include a ratio such as 9:16, 3:4 or 1:3 and a resolution like 4K in the text, which keeps the composition in step with the output size.
- **Anchor the style to a real medium or era.** "Showa-era travel poster", "1994 infomercial" and "90s cel animation" give the model a whole look in a few words.
- **Turn an emoji into a material.** Several prompts take one emoji and render it as chrome, silk, fur, paper or an inflatable, which makes a quick set of matching icons.
- **Describe screens as components.** The UI prompts list a colour mode, layout, type hierarchy and sections instead of saying "a nice website".
- **Number your uploads.** Reference prompts say "the second image" or "image 2" so the model knows which picture supplies the subject and which the setting.
- **Lock the scale for animation frames.** Sprite prompts fix the frame count, grid and character size so the frames line up when you cut them apart.

<a id="menu"></a>
## 📑 Menu

- [⭐ Featured](#featured) (6)
- [📷 Portrait photography](prompts/portrait-photography.md) (31) — People and candid scenes written like a photographer's brief: lens, light, skin texture and mood.
- [🧩 Characters and stickers](prompts/characters-stickers.md) (35) — Character sheets, chibi figures, emoji packs and pixel sprite sheets laid out on a fixed grid.
- [🏞️ Scenes and illustration](prompts/scenes-illustration.md) (35) — Cityscapes, miniatures, paintings and surreal scenes in a named medium or era.
- [🪧 Posters and branding](prompts/poster-branding.md) (28) — Posters, covers, logos and cards where the wording has to come out exactly right.
- [📣 Product and ads](prompts/product-ads.md) (23) — Product shots, packaging, billboards and ad concepts, including emoji turned into objects.
- [🖥️ UI and web design](prompts/ui-web.md) (24) — App screens, landing-page sections and desktop screenshots described component by component.
- [📊 Infographics](prompts/infographics.md) (14) — Diagrams, teaching charts, recipes and slides with labels and layout spelled out.
- [✏️ Image editing](prompts/image-editing.md) (19) — Prompts that change one thing in an uploaded photo and leave the rest alone.
- [❓ FAQ](#faq)
- [🔗 Related](#related)

<a id="featured"></a>
## ⭐ Featured

<a id="poster-branding-05"></a>
### 106. Showa-era Japanese travel poster

by [@Goodmanprotocol](https://x.com/Goodmanprotocol/status/2097542746273726753) · 3:4 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-05#poster-branding-05)** · [Original post](https://x.com/Goodmanprotocol/status/2097542746273726753)

<a href="https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-05#poster-branding-05"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/poster-branding-05.webp" width="320" alt="Showa-era Japanese travel poster – GPT Image 2.5"></a>

**Prompt:**

```text
Create a premium, ultra-refined Showa-era Japanese vintage travel poster for [LOCATION].

FORMAT: Vertical 3:4 | Collector’s travel poster | Mid-century Japanese railway tourism aesthetic

CORE CONCEPT

Create a beautifully composed, instantly recognizable travel scene representing [LOCATION]. Feature its most iconic landmark, architecture, landscape, streets, transportation, and atmospheric details, selecting elements that naturally define the destination.

Reimagine the scene as an authentic 1960s–1970s Japanese railway tourism poster, inspired by classic Japanese National Railways travel advertising and sophisticated vintage screen-printed graphics.

The result should feel like an originally designed vintage poster, not a modern photograph with a retro filter.

VISUAL STYLE

Use bold geometric forms, simplified architecture, clean perspective lines, strong silhouettes, and elegant flat graphic shapes.

Combine sophisticated mid-century Japanese graphic design with traditional screen-print and lithographic aesthetics. Keep the composition cinematic, balanced, spacious, and visually striking.

People and vehicles should be minimal and stylized rather than photorealistic.

COLOR & PRINT TEXTURE

Use a restrained vintage palette of:
deep navy blue, warm ivory/aged paper, muted mustard yellow, and vermilion red accents.

Use flat printed color fields rather than digital gradients. Add subtle paper grain, authentic ink texture, slight ink wear, and delicate vintage print misregistration for a convincing screen-printed feel.

Avoid neon colors, glossy 3D rendering, excessive photorealism, modern AI-art aesthetics, and overly saturated colors.

TYPOGRAPHY & LAYOUT

Reserve generous negative space at the bottom for elegant vintage typography.

Main title: "[LOCATION]"
Large, bold, geometric sans-serif lettering.

Add a refined, location-appropriate subtitle beneath it with generous letter spacing.

Place 2026 discreetly at the bottom left and No.01 at the bottom right.

Typography should feel authentic to a premium Japanese railway tourism poster: restrained, elegant, highly legible, and perfectly integrated into the artwork.

FINAL RESULT

Create a timeless, sophisticated Japanese Showa-era travel poster that feels like a rare original screen-printed railway advertisement from the 1960s–1970s, while showcasing the unique identity, beauty, and most recognizable visual characteristics of [LOCATION].

IMPORTANT: Make [LOCATION] immediately recognizable. Prioritize iconic local landmarks, authentic architecture, distinctive landscapes, and culturally characteristic details. Do not invent generic scenery that could represent any destination.
```

<a id="scenes-illustration-13"></a>
### 79. LEGO brick Shanghai Bund

by [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/033-imported-.md) · 4:3 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-13#scenes-illustration-13)** · [Original post](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/033-imported-.md)

<a href="https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-13#scenes-illustration-13"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/scenes-illustration-13.webp" width="480" alt="LEGO brick Shanghai Bund – GPT Image 2.5"></a>

**Prompt:**

```text
创作一幅高度精细且色彩鲜艳的乐高版上海外滩景象。前景是经典的外滩历史建筑群，用乐高砖块精致还原西式与新古典主义立面，包括钟楼、穹顶与柱廊；乐高小人们沿江漫步、拍照、观光，街道旁停着经典样式的乐高汽车。中景是蓝色半透明乐高砖拼出的黄浦江，江上有乐高渡轮与游览船。对岸陆家嘴高楼林立：东方明珠塔、上海中心、金茂大厦等超现代乐高摩天楼色彩丰富、造型逼真。天空为乐高明亮蓝色，点缀白色积木云朵，午后阳光，等距俯视全景。
```

<a id="characters-stickers-03"></a>
### 34. Nine transparent 3D emoji stickers

by [@BAXSCTO](https://x.com/BAXSCTO/status/2097554076494102704) · 1:1 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=characters-stickers-03#characters-stickers-03)** · [Original post](https://x.com/BAXSCTO/status/2097554076494102704)

<a href="https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=characters-stickers-03#characters-stickers-03"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/characters-stickers-03.webp" width="480" alt="Nine transparent 3D emoji stickers – GPT Image 2.5"></a>

**Prompt:**

```text
基于我上传的图片，
设计一套  3D 表情包 1:1 透明贴纸页，
包含 9 个各不相同的贴纸，
按 3X3 网格排列每个贴纸呈现不同的表情、姿势或反应。贴纸之间留出较宽且完全透明的间隔。
无背景、阴影或重叠元素，融入🚀🎉🥳🤟
```

<a id="portrait-photography-01"></a>
### 1. Weathered sailor mending a net on a fishing boat

by [@OpenAI](https://developers.openai.com/api/docs/guides/image-prompting#control-style-and-lighting) · 2:3 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=portrait-photography-01#portrait-photography-01)** · [Original post](https://developers.openai.com/api/docs/guides/image-prompting#control-style-and-lighting)

<a href="https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=portrait-photography-01#portrait-photography-01"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/portrait-photography-01.webp" width="320" alt="Weathered sailor mending a net on a fishing boat – GPT Image 2.5"></a>

**Prompt:**

```text
Create a photorealistic candid photograph of an elderly sailor standing on a small fishing boat.
He has weathered skin with visible wrinkles, pores, and sun texture, and a few faded traditional sailor tattoos on his arms.
He is calmly adjusting a net while his dog sits nearby on the deck. Shot like a 35mm film photograph, medium close-up at eye level, using a 50mm lens.
Soft coastal daylight, shallow depth of field, subtle film grain, natural color balance.
The image should feel honest and unposed, with real skin texture, worn materials, and everyday detail. No glamorization, no heavy retouching.
```

<a id="poster-branding-08"></a>
### 109. Mid-century 3 x 3 poster grid

by [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/06-mid-century-modern-posters.md) · 3:4 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-08#poster-branding-08)** · [Original post](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/06-mid-century-modern-posters.md)

<a href="https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-08#poster-branding-08"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/poster-branding-08.webp" width="320" alt="Mid-century 3 x 3 poster grid – GPT Image 2.5"></a>

**Prompt:**

```text
Create a perfectly aligned 3 x 3 grid of nine mid-century modern motivational posters sharing one limited palette.
Exact headlines: Travel Farther, CREATE, GROW TOGETHER, LISTEN MORE, FIND YOUR BALANCE, DRINK MORE WATER, LEARN SOMETHING NEW, SEE THE BEAUTY, CHOOSE KINDNESS.
Flat printed poster aesthetic, equal gutters, no mockup frames.
```

<a id="scenes-illustration-04"></a>
### 70. Impressionist gouache cityscape

by [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/11-impressionist-cityscape.md) · 3:4 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-04#scenes-illustration-04)** · [Original post](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/11-impressionist-cityscape.md)

<a href="https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-04#scenes-illustration-04"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/scenes-illustration-04.webp" width="320" alt="Impressionist gouache cityscape – GPT Image 2.5"></a>

**Prompt:**

```text
A vertical impressionist gouache and thick-oil painting of San Francisco on a bright clear day.
View downhill along a steep residential street toward San Francisco Bay. Pastel-colored houses and dense rounded trees frame both sides of the descending street.
In the distance, the Golden Gate Bridge stretches horizontally across brilliant blue water, painted in vivid vermilion red. Coit Tower appears on the right hillside.
Joyful saturated palette, loose confident brushwork, visible thick paint texture, palette-knife marks.
Mid-century California plein-air painting feeling. 3:4. No text. No photographic rendering.
```

- **[📷 All 31 Portrait photography cases](prompts/portrait-photography.md)**
- **[🧩 All 35 Characters and stickers cases](prompts/characters-stickers.md)**
- **[🏞️ All 35 Scenes and illustration cases](prompts/scenes-illustration.md)**
- **[🪧 All 28 Posters and branding cases](prompts/poster-branding.md)**
- **[📣 All 23 Product and ads cases](prompts/product-ads.md)**
- **[🖥️ All 24 UI and web design cases](prompts/ui-web.md)**
- **[📊 All 14 Infographics cases](prompts/infographics.md)**
- **[✏️ All 19 Image editing cases](prompts/image-editing.md)**

<a id="faq"></a>
## ❓ FAQ

<details>
<summary><b>Are these GPT Image 2.5 prompts free to use?</b></summary>

You can copy, edit and run any prompt. The prompts and result images belong to the creators credited on each card, so read the original post before reusing a result image commercially.

</details>

<details>
<summary><b>Which language should I write GPT Image 2.5 prompts in?</b></summary>

English or Chinese both work. The prompts here are shown in the author's original language and are not translated, so copy them as they are.

</details>

<details>
<summary><b>How do I run a GPT Image 2.5 prompt through the API?</b></summary>

Send the prompt to the image generation endpoint with model gpt-image-2.5-flare or gpt-image-2.5-sunburst. prompt is required and n must be 1. The docs recommend "async": true and polling GET /v1/tasks/:task_id every 5 to 10 seconds, and completed results are stored for 24 hours.

</details>

<details>
<summary><b>Which sizes does GPT Image 2.5 support?</b></summary>

Resolution is 1k, 2k or 4k, and size takes one of ten aspect ratios: 3:1, 21:9, 16:9, 3:2, 4:3, 1:1, 3:4, 2:3, 9:16 and 1:3. Each ratio maps to a fixed pixel size per tier, listed on the API page.

</details>

<details>
<summary><b>Can GPT Image 2.5 edit a photo with reference images?</b></summary>

Yes. The API takes 0 to 16 reference images and a mask, which is how the editing cards on this page work. The mask limits the change to a region.

</details>

<details>
<summary><b>How is GPT Image 2.5 billed?</b></summary>

By the tokens each result uses, not per image. Quality can be low, medium, high, xhigh, max or auto, and higher quality uses more output tokens. Current rates are on the model page.

</details>

<details>
<summary><b>What is the difference between gpt-image-2.5-flare and gpt-image-2.5-sunburst?</b></summary>

The APIKO docs list both with the same parameters, sizes, reference limits and token billing, and do not state any other difference. Either ID runs the prompts on this page.

</details>

<details>
<summary><b>Why does my GPT Image 2.5 result look different from the card?</b></summary>

Image models are not deterministic, so the same prompt gives different results on each run. The author may also have used other settings or tools, or edited the output afterwards.

</details>

<details>
<summary><b>How do I get exact text in a GPT Image 2.5 image?</b></summary>

Quote the words, say where each line sits and what the lettering looks like, and keep the text short. The poster and brand cards above show the pattern, so check every result for spelling before you use it.

</details>


<a id="related"></a>
## 🔗 Related

- [GPT Image 2.5 Prompts · apiko.app](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2.5 Flare](https://apiko.app/models/gpt-image-2.5-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2.5 Sunburst](https://apiko.app/models/gpt-image-2.5-sunburst?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2](https://apiko.app/models/gpt-image-2?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2 prompts](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [AI image generator](https://apiko.app/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [Code examples for the APIKO API](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**More prompt collections**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts)
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts)
- [Awesome Claude Fable 5.2 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-fable-5.2-video-prompts)
- [Awesome Seedream 5.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedream-5.5-prompts)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts)

<a id="license"></a>
## 📄 License and credits

Prompts and result images belong to the creators credited on each card, which links to the original post. Titles, descriptions, translations and the build scripts are released under [CC BY 4.0](LICENSE). Licenses of the source repositories: [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

If this list saves you time, a ⭐ helps others find it.
