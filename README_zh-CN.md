<div align="center">

<a href="https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2.5-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2.5 提示词" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-209_cases-111111)](README_zh-CN.md#menu)
[![Try GPT Image 2.5 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2.5-on_APIKO-4F46E5)](https://apiko.app/zh/models/gpt-image-2.5-flare?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=model_try)
[![GPT Image 2.5 API docs](https://img.shields.io/badge/GPT_Image_2.5-API_docs-111111)](https://apiko.app/zh/docs/api-manual/image-series/gpt-image-2.5-flare/images?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-Current-111111)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome GPT Image 2.5 提示词

<a id="introduction"></a>
## 🌟 简介

**GPT Image 2.5 提示词：209 条可直接复制的示例，附效果图，涵盖人像、海报、界面设计、精灵图和图片编辑。**

复制一条已经出过好图的 GPT Image 2.5 提示词，或发送到试用台改几处细节再跑。

在线搜索和筛选： [apiko.app/gpt-image-2-5-prompts](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=intro).

> [!NOTE]
> 提示词保持作者发布时的原文，所以大多是英文；标题和简介是我们写的。每条都署名作者并链接原帖。

<a id="quick-start"></a>
## 🚀 快速开始

**网页上用：** 每条都有「在 APIKO 运行」链接，会在 [apiko.app](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=browser) 打开这条示例；点「使用」，提示词就会填进 GPT Image 2.5 试用台。

**用 API：** 先创建 [APIKO API Key](https://apiko.app/zh/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=api_key)，再创建异步任务并轮询，直到图片生成完成。

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

接口: `POST https://api.apiko.app/v1/images/generations` (创建任务) · `GET https://api.apiko.app/v1/tasks/{id}` (查询状态和结果)

<a id="how-to-write"></a>
## ✍️ GPT Image 2.5 提示词怎么写

这些提示词里反复出现的五种结构。

- **摄影** · `主体 + 动作 + 机位与镜头 + 光线 + 质感` — 人像提示词会写明镜头（如 50mm）、景别、光线和皮肤或材质细节，最后补一句要避免的内容，比如过度修图。
- **精确文字** · `加引号的文字 + 摆放位置 + 字体样式` — 画面里要出现的每个字都放进引号，说清每行放哪、长什么样，文字较长时要求拼写正确。
- **编辑** · `一处改动 + “其余保持不变”` — 编辑类提示词只说一处改动，结尾列出必须保留的部分：人脸、版式、光线。
- **整页或网格** · `数量 + 网格规格 + 每格内容 + 背景` — 贴纸、精灵图和海报阵列会写明格数、排列方式，以及背景是透明还是纯色。
- **结构化描述** · `标题、场景、主体、光线、构图等字段` — 长提示词写成 JSON 或 Markdown 大纲，可复用的会留出 {主体}、[OBJECT] 这样的占位符待填。

**从示例里能看到什么**

- **把画幅写进提示词。** 不少提示词在正文里写明 9:16、3:4、1:3 之类的比例和 4K 分辨率，让构图和输出尺寸对得上。
- **用真实媒介或年代定风格。** “昭和旅行海报”“1994 年电视购物”“90 年代赛璐璐动画”几个字就能交代整体画风。
- **把 emoji 变成材质。** 有几条提示词拿一个 emoji 渲染成镀铬、丝绸、绒毛、纸艺或充气物，很容易做出一套风格统一的图标。
- **按组件描述界面。** 界面类提示词会列出色彩模式、版式、字体层级和区块，而不是只说“好看的网站”。
- **给上传的图编号。** 参考图提示词会写“第二张图”“图 2”，让模型分清哪张提供主体、哪张提供场景。
- **动画帧要锁定比例。** 精灵图提示词固定帧数、网格和角色大小，方便后期切图时各帧对齐。

<a id="menu"></a>
## 📑 目录

- [⭐ 精选](#featured) (6)
- [📷 人像摄影](prompts/portrait-photography_zh-CN.md) (31) — 按摄影师的拍摄需求写：镜头、光线、皮肤质感和情绪。
- [🧩 角色与贴纸](prompts/characters-stickers_zh-CN.md) (35) — 角色设定页、Q 版手办、表情包和像素精灵图，按固定网格排布。
- [🏞️ 场景与插画](prompts/scenes-illustration_zh-CN.md) (35) — 城市、微缩模型、绘画和超现实画面，都指定了具体媒介或年代。
- [🪧 海报与品牌](prompts/poster-branding_zh-CN.md) (28) — 海报、封面、标志和卡片，文字必须一字不差。
- [📣 产品与广告](prompts/product-ads_zh-CN.md) (23) — 产品图、包装、广告牌和广告创意，包括把 emoji 变成实物。
- [🖥️ 界面与网页设计](prompts/ui-web_zh-CN.md) (24) — 应用界面、落地页区块和桌面截图，逐个组件写清楚。
- [📊 信息图](prompts/infographics_zh-CN.md) (14) — 图解、教学图、食谱和幻灯片，标签与版式都写明。
- [✏️ 图片编辑](prompts/image-editing_zh-CN.md) (19) — 只改上传照片里的一处，其余保持不动的提示词。
- [❓ 常见问题](#faq)
- [🔗 相关链接](#related)

<a id="featured"></a>
## ⭐ 精选

<a id="poster-branding-05"></a>
### 106. 昭和风日本旅行海报

作者 [@Goodmanprotocol](https://x.com/Goodmanprotocol/status/2097542746273726753) · 3:4 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-05#poster-branding-05)** · [原帖](https://x.com/Goodmanprotocol/status/2097542746273726753)

<a href="https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-05#poster-branding-05"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/poster-branding-05.webp" width="320" alt="昭和风日本旅行海报 – GPT Image 2.5"></a>

**提示词:**

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
### 79. 乐高积木版上海外滩

作者 [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/033-imported-.md) · 4:3 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-13#scenes-illustration-13)** · [原帖](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/033-imported-.md)

<a href="https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-13#scenes-illustration-13"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/scenes-illustration-13.webp" width="480" alt="乐高积木版上海外滩 – GPT Image 2.5"></a>

**提示词:**

```text
创作一幅高度精细且色彩鲜艳的乐高版上海外滩景象。前景是经典的外滩历史建筑群，用乐高砖块精致还原西式与新古典主义立面，包括钟楼、穹顶与柱廊；乐高小人们沿江漫步、拍照、观光，街道旁停着经典样式的乐高汽车。中景是蓝色半透明乐高砖拼出的黄浦江，江上有乐高渡轮与游览船。对岸陆家嘴高楼林立：东方明珠塔、上海中心、金茂大厦等超现代乐高摩天楼色彩丰富、造型逼真。天空为乐高明亮蓝色，点缀白色积木云朵，午后阳光，等距俯视全景。
```

<a id="characters-stickers-03"></a>
### 34. 九枚透明背景 3D 表情贴纸

作者 [@BAXSCTO](https://x.com/BAXSCTO/status/2097554076494102704) · 1:1 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=characters-stickers-03#characters-stickers-03)** · [原帖](https://x.com/BAXSCTO/status/2097554076494102704)

<a href="https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=characters-stickers-03#characters-stickers-03"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/characters-stickers-03.webp" width="480" alt="九枚透明背景 3D 表情贴纸 – GPT Image 2.5"></a>

**提示词:**

```text
基于我上传的图片，
设计一套  3D 表情包 1:1 透明贴纸页，
包含 9 个各不相同的贴纸，
按 3X3 网格排列每个贴纸呈现不同的表情、姿势或反应。贴纸之间留出较宽且完全透明的间隔。
无背景、阴影或重叠元素，融入🚀🎉🥳🤟
```

<a id="portrait-photography-01"></a>
### 1. 渔船上补网的饱经风霜的老水手

作者 [@OpenAI](https://developers.openai.com/api/docs/guides/image-prompting#control-style-and-lighting) · 2:3 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=portrait-photography-01#portrait-photography-01)** · [原帖](https://developers.openai.com/api/docs/guides/image-prompting#control-style-and-lighting)

<a href="https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=portrait-photography-01#portrait-photography-01"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/portrait-photography-01.webp" width="320" alt="渔船上补网的饱经风霜的老水手 – GPT Image 2.5"></a>

**提示词:**

```text
Create a photorealistic candid photograph of an elderly sailor standing on a small fishing boat.
He has weathered skin with visible wrinkles, pores, and sun texture, and a few faded traditional sailor tattoos on his arms.
He is calmly adjusting a net while his dog sits nearby on the deck. Shot like a 35mm film photograph, medium close-up at eye level, using a 50mm lens.
Soft coastal daylight, shallow depth of field, subtle film grain, natural color balance.
The image should feel honest and unposed, with real skin texture, worn materials, and everyday detail. No glamorization, no heavy retouching.
```

<a id="poster-branding-08"></a>
### 109. 中世纪现代风 3×3 海报阵列

作者 [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/06-mid-century-modern-posters.md) · 3:4 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-08#poster-branding-08)** · [原帖](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/06-mid-century-modern-posters.md)

<a href="https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-08#poster-branding-08"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/poster-branding-08.webp" width="320" alt="中世纪现代风 3×3 海报阵列 – GPT Image 2.5"></a>

**提示词:**

```text
Create a perfectly aligned 3 x 3 grid of nine mid-century modern motivational posters sharing one limited palette.
Exact headlines: Travel Farther, CREATE, GROW TOGETHER, LISTEN MORE, FIND YOUR BALANCE, DRINK MORE WATER, LEARN SOMETHING NEW, SEE THE BEAUTY, CHOOSE KINDNESS.
Flat printed poster aesthetic, equal gutters, no mockup frames.
```

<a id="scenes-illustration-04"></a>
### 70. 印象派水粉厚涂城市风景

作者 [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/11-impressionist-cityscape.md) · 3:4 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-04#scenes-illustration-04)** · [原帖](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/11-impressionist-cityscape.md)

<a href="https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-04#scenes-illustration-04"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/scenes-illustration-04.webp" width="320" alt="印象派水粉厚涂城市风景 – GPT Image 2.5"></a>

**提示词:**

```text
A vertical impressionist gouache and thick-oil painting of San Francisco on a bright clear day.
View downhill along a steep residential street toward San Francisco Bay. Pastel-colored houses and dense rounded trees frame both sides of the descending street.
In the distance, the Golden Gate Bridge stretches horizontally across brilliant blue water, painted in vivid vermilion red. Coit Tower appears on the right hillside.
Joyful saturated palette, loose confident brushwork, visible thick paint texture, palette-knife marks.
Mid-century California plein-air painting feeling. 3:4. No text. No photographic rendering.
```

- **[📷 查看「人像摄影」全部 31 条](prompts/portrait-photography_zh-CN.md)**
- **[🧩 查看「角色与贴纸」全部 35 条](prompts/characters-stickers_zh-CN.md)**
- **[🏞️ 查看「场景与插画」全部 35 条](prompts/scenes-illustration_zh-CN.md)**
- **[🪧 查看「海报与品牌」全部 28 条](prompts/poster-branding_zh-CN.md)**
- **[📣 查看「产品与广告」全部 23 条](prompts/product-ads_zh-CN.md)**
- **[🖥️ 查看「界面与网页设计」全部 24 条](prompts/ui-web_zh-CN.md)**
- **[📊 查看「信息图」全部 14 条](prompts/infographics_zh-CN.md)**
- **[✏️ 查看「图片编辑」全部 19 条](prompts/image-editing_zh-CN.md)**

<a id="faq"></a>
## ❓ 常见问题

<details>
<summary><b>这些 GPT Image 2.5 提示词可以免费使用吗？</b></summary>

提示词可以随意复制、修改和运行。提示词和效果图归每张卡片标注的创作者所有，想把效果图用于商业用途，请先看原帖。

</details>

<details>
<summary><b>GPT Image 2.5 提示词用中文还是英文写？</b></summary>

中文和英文都可以。这里的提示词保持作者的原文，没有翻译，直接复制即可。

</details>

<details>
<summary><b>怎样用 API 运行一条 GPT Image 2.5 提示词？</b></summary>

向图像生成接口发送提示词，model 填 gpt-image-2.5-flare 或 gpt-image-2.5-sunburst。prompt 必填，n 只能为 1。文档建议传 "async": true，每 5 到 10 秒轮询一次 GET /v1/tasks/:task_id，完成的结果保存 24 小时。

</details>

<details>
<summary><b>GPT Image 2.5 支持哪些尺寸？</b></summary>

分辨率有 1k、2k、4k，size 可选十种比例：3:1、21:9、16:9、3:2、4:3、1:1、3:4、2:3、9:16、1:3。每个比例在每档分辨率下对应固定像素，列在 API 页面。

</details>

<details>
<summary><b>GPT Image 2.5 能用参考图改图吗？</b></summary>

可以。API 支持 0 到 16 张参考图和蒙版，本页的图片编辑类卡片就是这么用的，蒙版可以把改动限制在某个区域。

</details>

<details>
<summary><b>GPT Image 2.5 怎么计费？</b></summary>

按每个结果实际用到的 token 计费，不按张数。画质可选 low、medium、high、xhigh、max 或 auto，画质越高输出 token 越多。当前费率见模型页。

</details>

<details>
<summary><b>gpt-image-2.5-flare 和 gpt-image-2.5-sunburst 有什么区别？</b></summary>

APIKO 文档里两者的参数、尺寸、参考图上限和 token 计费完全相同，没有写明其他区别。本页的提示词用哪个 ID 都能跑。

</details>

<details>
<summary><b>为什么我用 GPT Image 2.5 跑出来和卡片上的图不一样？</b></summary>

图像模型不是确定性的，同一条提示词每次跑结果都不同。作者也可能用了别的设置或工具，或在出图后做过修改。

</details>

<details>
<summary><b>怎样让 GPT Image 2.5 把文字写对？</b></summary>

把文字放进引号，说明每行的位置和字体样子，文字尽量短。上面的海报和品牌卡片可以参考，出图后仍要逐字检查拼写。

</details>


<a id="related"></a>
## 🔗 相关链接

- [GPT Image 2.5 提示词 · apiko.app](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2.5 Flare](https://apiko.app/zh/models/gpt-image-2.5-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2.5 Sunburst](https://apiko.app/zh/models/gpt-image-2.5-sunburst?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2](https://apiko.app/zh/models/gpt-image-2?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2 提示词](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [AI 图片生成器](https://apiko.app/zh/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [APIKO API 代码示例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示词合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-CN.md)
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts/blob/main/README_zh-CN.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_zh-CN.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_zh-CN.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-CN.md)
- [Awesome Claude Fable 5.2 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-fable-5.2-video-prompts/blob/main/README_zh-CN.md)
- [Awesome Seedream 5.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedream-5.5-prompts/blob/main/README_zh-CN.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-CN.md)

<a id="license"></a>
## 📄 许可与出处

提示词和效果图归每张卡片标注的创作者所有，卡片可跳转到原帖。标题、简介、译文和生成脚本采用 [CC BY 4.0](LICENSE) 许可。来源仓库的许可证见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

如果这份合集帮你省了时间，点个 ⭐ 能让更多人看到。
