<div align="center">

<a href="https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2.5-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2.5 프롬프트" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-209_cases-111111)](README_ko.md#menu)
[![Try GPT Image 2.5 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2.5-on_APIKO-4F46E5)](https://apiko.app/ko/models/gpt-image-2.5-flare?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=model_try)
[![GPT Image 2.5 API docs](https://img.shields.io/badge/GPT_Image_2.5-API_docs-111111)](https://apiko.app/docs/api-manual/image-series/gpt-image-2.5-flare/images?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-Current-111111)](README_ko.md)

</div>

# Awesome GPT Image 2.5 프롬프트

<a id="introduction"></a>
## 🌟 소개

**GPT Image 2.5 프롬프트 209개와 결과 이미지. 인물, 포스터, UI, 스프라이트 시트, 이미지 편집 예시를 바로 복사하세요.**

이미 좋은 결과를 낸 GPT Image 2.5 프롬프트를 복사하거나, 플레이그라운드로 보내 세부만 바꿔 실행해 보세요.

검색과 필터는 [apiko.app/gpt-image-2-5-prompts](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=intro).

> [!NOTE]
> 프롬프트는 작성자가 올린 원문 그대로라 대부분 영어입니다. 제목과 설명은 저희가 썼습니다. 모든 예시에 작성자와 원본 게시물 링크를 달았습니다.

<a id="quick-start"></a>
## 🚀 빠른 시작

**브라우저에서:** 모든 예시에 **APIKO에서 실행** 링크가 있습니다. [apiko.app](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=browser)에서 해당 예시가 열리며, **사용**을 누르면 프롬프트가 GPT Image 2.5 플레이그라운드에 채워집니다.

**API로:** [APIKO API 키](https://apiko.app/ko/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=api_key)를 만든 뒤 비동기 작업을 생성하고, 이미지가 완성될 때까지 상태를 조회합니다.

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

엔드포인트: `POST https://api.apiko.app/v1/images/generations` (작업 생성) · `GET https://api.apiko.app/v1/tasks/{id}` (상태와 결과 조회)

<a id="how-to-write"></a>
## ✍️ GPT Image 2.5 프롬프트 작성법

이 페이지의 프롬프트에서 반복되는 다섯 가지 구조입니다.

- **사진** · `피사체 + 동작 + 카메라와 렌즈 + 조명 + 질감` — 인물 프롬프트는 렌즈(예: 50mm), 촬영 거리, 조명, 피부나 소재의 디테일을 적고, 과한 보정처럼 피할 것을 덧붙입니다.
- **정확한 문구** · `따옴표 안의 문구 + 위치 + 글씨체` — 이미지에 들어갈 모든 글자를 따옴표로 묶고, 줄마다 위치와 모양을 적습니다. 문구가 길면 철자를 정확히 쓰라고 요청합니다.
- **편집** · `바꿀 한 가지 + "나머지는 그대로"` — 편집 프롬프트는 바꿀 것을 하나만 말하고, 마지막에 얼굴, 레이아웃, 조명처럼 유지할 것을 적습니다.
- **시트와 그리드** · `개수 + 그리드 크기 + 칸별 내용 + 배경` — 스티커, 스프라이트 시트, 포스터 그리드는 칸 수와 배치, 배경이 투명인지 단색인지를 적습니다.
- **구조화된 명세** · `제목, 장면, 피사체, 조명, 구도 같은 항목` — 긴 프롬프트는 JSON이나 마크다운 개요로 쓰고, 재사용용은 {subject}, [OBJECT] 같은 자리표시자를 남깁니다.

**예시에서 보이는 점**

- **화면 비율을 프롬프트에 적기.** 9:16, 3:4, 1:3 같은 비율과 4K 해상도를 본문에 적어 구도를 출력 크기에 맞춘 프롬프트가 많습니다.
- **실제 매체나 시대로 스타일 고정.** "쇼와 시대 여행 포스터", "1994년 홈쇼핑", "90년대 셀 애니메이션"처럼 몇 단어로 전체 화풍이 정해집니다.
- **이모지를 재질로 바꾸기.** 이모지 하나를 크롬, 실크, 털, 종이 공예, 풍선 질감으로 렌더링한 프롬프트가 여러 개 있어, 통일감 있는 아이콘 세트를 만들기 쉽습니다.
- **화면은 구성 요소별로 설명.** UI 프롬프트는 "예쁜 웹사이트" 대신 색상 모드, 레이아웃, 글자 위계, 섹션을 나열합니다.
- **올린 이미지에 번호 붙이기.** 참조 프롬프트는 "두 번째 이미지", "image 2"처럼 써서 어느 사진이 피사체이고 어느 사진이 배경인지 구분합니다.
- **애니메이션 프레임은 크기 고정.** 스프라이트 프롬프트는 프레임 수, 그리드, 캐릭터 크기를 고정해 잘라 낼 때 프레임이 어긋나지 않게 합니다.

<a id="menu"></a>
## 📑 목차

- [⭐ 추천](#featured) (6)
- [📷 인물 사진](prompts/portrait-photography_ko.md) (31) — 사진가의 촬영 지시서처럼 렌즈, 조명, 피부 질감, 분위기를 적습니다.
- [🧩 캐릭터와 스티커](prompts/characters-stickers_ko.md) (35) — 캐릭터 시트, SD 피규어, 이모티콘, 픽셀 스프라이트를 고정 그리드로 배치합니다.
- [🏞️ 장면과 일러스트](prompts/scenes-illustration_ko.md) (35) — 도시, 미니어처, 회화, 초현실 장면을 구체적인 매체나 시대로 지정합니다.
- [🪧 포스터와 브랜딩](prompts/poster-branding_ko.md) (28) — 문구가 정확해야 하는 포스터, 커버, 로고, 카드입니다.
- [📣 제품과 광고](prompts/product-ads_ko.md) (23) — 제품 컷, 패키지, 광고판, 광고 콘셉트와 이모지를 사물로 바꾼 예시입니다.
- [🖥️ UI와 웹 디자인](prompts/ui-web_ko.md) (24) — 앱 화면, 랜딩 페이지 섹션, 데스크톱 화면을 구성 요소별로 설명합니다.
- [📊 인포그래픽](prompts/infographics_ko.md) (14) — 라벨과 레이아웃을 구체적으로 적은 도식, 교육 자료, 레시피, 슬라이드입니다.
- [✏️ 이미지 편집](prompts/image-editing_ko.md) (19) — 올린 사진에서 한 가지만 바꾸고 나머지는 그대로 두는 프롬프트입니다.
- [❓ 자주 묻는 질문](#faq)
- [🔗 관련 링크](#related)

<a id="featured"></a>
## ⭐ 추천

<a id="poster-branding-05"></a>
### 106. 쇼와 시대풍 일본 여행 포스터

작성자 [@Goodmanprotocol](https://x.com/Goodmanprotocol/status/2097542746273726753) · 3:4 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-05#poster-branding-05)** · [원본 게시물](https://x.com/Goodmanprotocol/status/2097542746273726753)

<a href="https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-05#poster-branding-05"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/poster-branding-05.webp" width="320" alt="쇼와 시대풍 일본 여행 포스터 – GPT Image 2.5"></a>

**프롬프트:**

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
### 79. 레고 블록으로 만든 상하이 와이탄

작성자 [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/033-imported-.md) · 4:3 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-13#scenes-illustration-13)** · [원본 게시물](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/033-imported-.md)

<a href="https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-13#scenes-illustration-13"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/scenes-illustration-13.webp" width="480" alt="레고 블록으로 만든 상하이 와이탄 – GPT Image 2.5"></a>

**프롬프트:**

```text
创作一幅高度精细且色彩鲜艳的乐高版上海外滩景象。前景是经典的外滩历史建筑群，用乐高砖块精致还原西式与新古典主义立面，包括钟楼、穹顶与柱廊；乐高小人们沿江漫步、拍照、观光，街道旁停着经典样式的乐高汽车。中景是蓝色半透明乐高砖拼出的黄浦江，江上有乐高渡轮与游览船。对岸陆家嘴高楼林立：东方明珠塔、上海中心、金茂大厦等超现代乐高摩天楼色彩丰富、造型逼真。天空为乐高明亮蓝色，点缀白色积木云朵，午后阳光，等距俯视全景。
```

<a id="characters-stickers-03"></a>
### 34. 투명 배경 3D 이모티콘 9종

작성자 [@BAXSCTO](https://x.com/BAXSCTO/status/2097554076494102704) · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=characters-stickers-03#characters-stickers-03)** · [원본 게시물](https://x.com/BAXSCTO/status/2097554076494102704)

<a href="https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=characters-stickers-03#characters-stickers-03"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/characters-stickers-03.webp" width="480" alt="투명 배경 3D 이모티콘 9종 – GPT Image 2.5"></a>

**프롬프트:**

```text
基于我上传的图片，
设计一套  3D 表情包 1:1 透明贴纸页，
包含 9 个各不相同的贴纸，
按 3X3 网格排列每个贴纸呈现不同的表情、姿势或反应。贴纸之间留出较宽且完全透明的间隔。
无背景、阴影或重叠元素，融入🚀🎉🥳🤟
```

<a id="portrait-photography-01"></a>
### 1. 어선에서 그물을 손보는 늙은 선원

작성자 [@OpenAI](https://developers.openai.com/api/docs/guides/image-prompting#control-style-and-lighting) · 2:3 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=portrait-photography-01#portrait-photography-01)** · [원본 게시물](https://developers.openai.com/api/docs/guides/image-prompting#control-style-and-lighting)

<a href="https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=portrait-photography-01#portrait-photography-01"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/portrait-photography-01.webp" width="320" alt="어선에서 그물을 손보는 늙은 선원 – GPT Image 2.5"></a>

**프롬프트:**

```text
Create a photorealistic candid photograph of an elderly sailor standing on a small fishing boat.
He has weathered skin with visible wrinkles, pores, and sun texture, and a few faded traditional sailor tattoos on his arms.
He is calmly adjusting a net while his dog sits nearby on the deck. Shot like a 35mm film photograph, medium close-up at eye level, using a 50mm lens.
Soft coastal daylight, shallow depth of field, subtle film grain, natural color balance.
The image should feel honest and unposed, with real skin texture, worn materials, and everyday detail. No glamorization, no heavy retouching.
```

<a id="poster-branding-08"></a>
### 109. 미드센추리 3x3 포스터 그리드

작성자 [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/06-mid-century-modern-posters.md) · 3:4 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-08#poster-branding-08)** · [원본 게시물](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/06-mid-century-modern-posters.md)

<a href="https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=poster-branding-08#poster-branding-08"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/poster-branding-08.webp" width="320" alt="미드센추리 3x3 포스터 그리드 – GPT Image 2.5"></a>

**프롬프트:**

```text
Create a perfectly aligned 3 x 3 grid of nine mid-century modern motivational posters sharing one limited palette.
Exact headlines: Travel Farther, CREATE, GROW TOGETHER, LISTEN MORE, FIND YOUR BALANCE, DRINK MORE WATER, LEARN SOMETHING NEW, SEE THE BEAUTY, CHOOSE KINDNESS.
Flat printed poster aesthetic, equal gutters, no mockup frames.
```

<a id="scenes-illustration-04"></a>
### 70. 인상주의 구아슈 도시 풍경

작성자 [@LaplaceYoung](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/11-impressionist-cityscape.md) · 3:4 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-04#scenes-illustration-04)** · [원본 게시물](https://github.com/LaplaceYoung/awesome-gpt-image-2.5/blob/main/docs/cases/11-impressionist-cityscape.md)

<a href="https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2.5-prompts&utm_content=scenes-illustration-04#scenes-illustration-04"><img src="https://media.apiko.app/prompts/gpt-image-2-5-prompts/scenes-illustration-04.webp" width="320" alt="인상주의 구아슈 도시 풍경 – GPT Image 2.5"></a>

**프롬프트:**

```text
A vertical impressionist gouache and thick-oil painting of San Francisco on a bright clear day.
View downhill along a steep residential street toward San Francisco Bay. Pastel-colored houses and dense rounded trees frame both sides of the descending street.
In the distance, the Golden Gate Bridge stretches horizontally across brilliant blue water, painted in vivid vermilion red. Coit Tower appears on the right hillside.
Joyful saturated palette, loose confident brushwork, visible thick paint texture, palette-knife marks.
Mid-century California plein-air painting feeling. 3:4. No text. No photographic rendering.
```

- **[📷 인물 사진 전체 31개 보기](prompts/portrait-photography_ko.md)**
- **[🧩 캐릭터와 스티커 전체 35개 보기](prompts/characters-stickers_ko.md)**
- **[🏞️ 장면과 일러스트 전체 35개 보기](prompts/scenes-illustration_ko.md)**
- **[🪧 포스터와 브랜딩 전체 28개 보기](prompts/poster-branding_ko.md)**
- **[📣 제품과 광고 전체 23개 보기](prompts/product-ads_ko.md)**
- **[🖥️ UI와 웹 디자인 전체 24개 보기](prompts/ui-web_ko.md)**
- **[📊 인포그래픽 전체 14개 보기](prompts/infographics_ko.md)**
- **[✏️ 이미지 편집 전체 19개 보기](prompts/image-editing_ko.md)**

<a id="faq"></a>
## ❓ 자주 묻는 질문

<details>
<summary><b>이 GPT Image 2.5 프롬프트는 무료로 쓸 수 있나요?</b></summary>

프롬프트는 자유롭게 복사, 수정, 실행할 수 있습니다. 프롬프트와 결과 이미지는 각 카드에 표시된 제작자의 것이니, 결과 이미지를 상업적으로 쓰려면 원문 게시물을 먼저 확인하세요.

</details>

<details>
<summary><b>GPT Image 2.5 프롬프트는 어떤 언어로 써야 하나요?</b></summary>

영어와 중국어 모두 됩니다. 이 페이지의 프롬프트는 작성자의 원문 그대로이며 번역하지 않았으니 그대로 복사하세요.

</details>

<details>
<summary><b>GPT Image 2.5 프롬프트를 API로 실행하려면 어떻게 하나요?</b></summary>

이미지 생성 엔드포인트에 프롬프트를 보내고 model에 gpt-image-2.5-flare 또는 gpt-image-2.5-sunburst를 넣습니다. prompt는 필수이고 n은 1이어야 합니다. 문서는 "async": true를 권장하며, GET /v1/tasks/:task_id를 5~10초마다 조회하고, 완료된 결과는 24시간 보관됩니다.

</details>

<details>
<summary><b>GPT Image 2.5는 어떤 크기를 지원하나요?</b></summary>

해상도는 1k, 2k, 4k이고 size는 3:1, 21:9, 16:9, 3:2, 4:3, 1:1, 3:4, 2:3, 9:16, 1:3 열 가지 비율 중에서 고릅니다. 비율마다 해상도별 고정 픽셀 크기가 있으며 API 페이지에 나와 있습니다.

</details>

<details>
<summary><b>GPT Image 2.5로 참조 이미지를 넣어 사진을 편집할 수 있나요?</b></summary>

가능합니다. API는 참조 이미지 0~16장과 마스크를 받으며, 이 페이지의 이미지 편집 카드가 그렇게 쓰입니다. 마스크로 바꿀 영역을 한정할 수 있습니다.

</details>

<details>
<summary><b>GPT Image 2.5는 요금이 어떻게 계산되나요?</b></summary>

장수가 아니라 결과마다 실제로 쓴 토큰 기준입니다. 품질은 low, medium, high, xhigh, max, auto 중에서 고르며, 품질이 높을수록 출력 토큰이 늘어납니다. 현재 요금은 모델 페이지에서 확인하세요.

</details>

<details>
<summary><b>gpt-image-2.5-flare와 gpt-image-2.5-sunburst는 무엇이 다른가요?</b></summary>

APIKO 문서에는 두 모델의 파라미터, 크기, 참조 이미지 한도, 토큰 과금이 같게 적혀 있고 그 밖의 차이는 명시되어 있지 않습니다. 이 페이지의 프롬프트는 어느 ID로든 실행할 수 있습니다.

</details>

<details>
<summary><b>GPT Image 2.5 결과가 카드의 이미지와 다른 이유는 무엇인가요?</b></summary>

이미지 모델은 결정적이지 않아 같은 프롬프트도 실행할 때마다 결과가 달라집니다. 작성자가 다른 설정이나 도구를 썼거나 출력 후 수정했을 수도 있습니다.

</details>

<details>
<summary><b>GPT Image 2.5 이미지에 문구를 정확히 넣으려면 어떻게 하나요?</b></summary>

문구를 따옴표로 묶고, 줄마다 위치와 글씨 모양을 적고, 글자는 짧게 유지하세요. 위의 포스터와 브랜드 카드가 참고가 되며, 결과의 철자는 항상 직접 확인해야 합니다.

</details>


<a id="related"></a>
## 🔗 관련 링크

- [GPT Image 2.5 프롬프트 · apiko.app](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2.5 Flare](https://apiko.app/ko/models/gpt-image-2.5-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2.5 Sunburst](https://apiko.app/ko/models/gpt-image-2.5-sunburst?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2](https://apiko.app/ko/models/gpt-image-2?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [GPT Image 2 프롬프트](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [AI 이미지 생성기](https://apiko.app/ko/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2.5-prompts)
- [APIKO API 코드 예시](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**다른 프롬프트 모음**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_ko.md)
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts/blob/main/README_ko.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_ko.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_ko.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_ko.md)
- [Awesome Claude Fable 5.2 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-fable-5.2-video-prompts/blob/main/README_ko.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_ko.md)

<a id="license"></a>
## 📄 라이선스와 출처

프롬프트와 결과 이미지는 각 카드에 표시된 제작자의 것이며, 카드에서 원문 게시물로 이동할 수 있습니다. 제목, 설명, 번역, 빌드 스크립트는 [CC BY 4.0](LICENSE)으로 배포합니다. 출처 저장소의 라이선스는 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)에 있습니다.

이 목록이 도움이 됐다면 ⭐ 를 눌러 다른 사람도 찾을 수 있게 해 주세요.
