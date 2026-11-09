<div align="center">

<a href="https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-kling-4.0-prompts"><img src="assets/banner.jpg" alt="Awesome Kling 4.0 프롬프트" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-133_cases-111111)](README_ko.md#menu)
[![Try Kling 4.0 on APIKO](https://img.shields.io/badge/Try_Kling_4.0-on_APIKO-4F46E5)](https://apiko.app/ko/models/kling-4.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-kling-4.0-prompts&utm_content=model_try)
[![Kling 4.0 API docs](https://img.shields.io/badge/Kling_4.0-API_docs-111111)](https://apiko.app/docs/api-manual/video-series/kling/kling-4.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-kling-4.0-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-Current-111111)](README_ko.md)

</div>

# Awesome Kling 4.0 프롬프트

<a id="introduction"></a>
## 🌟 소개

**Kling 4.0 프롬프트: 결과 클립이 붙은 복사 가능한 영상 프롬프트 133개. 원테이크 액션과 대화 장면부터 참고 이미지 광고, 영상 편집까지.**

프롬프트마다 그 프롬프트로 만든 클립이 옆에 있습니다. 복사하거나, 길이와 화면 비율이 맞춰진 채로 모델 페이지에서 여세요.

검색과 필터는 [apiko.app/kling-4-0-prompts](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-kling-4.0-prompts&utm_content=intro).

> [!NOTE]
> 프롬프트는 작성자가 올린 원문 그대로라 대부분 영어입니다. 제목과 설명은 저희가 썼습니다. 모든 예시에 작성자와 원본 게시물 링크를 달았습니다.

<a id="quick-start"></a>
## 🚀 빠른 시작

**브라우저에서:** 모든 예시에 **APIKO에서 실행** 링크가 있습니다. [apiko.app](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-kling-4.0-prompts&utm_content=browser)에서 해당 예시가 열리며, **사용**을 누르면 프롬프트가 Kling 4.0 플레이그라운드에 채워집니다.

**API로:** [APIKO API 키](https://apiko.app/ko/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-kling-4.0-prompts&utm_content=api_key)를 만든 뒤 작업을 생성하고, 영상이 완성될 때까지 상태를 조회합니다.

```bash
export APIKO_API_KEY="your_key_here"

TASK_ID=$(curl -s https://api.apiko.app/v1/videos \
  -H "Authorization: Bearer $APIKO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "model": "kling-4.0",
  "duration": 5,
  "resolution": "720p",
  "aspect_ratio": "16:9",
  "prompt": "A paper boat drifting across a calm lake at sunrise, slow dolly-in, soft wind and birdsong."
}' | python3 -c 'import json,sys; print(json.load(sys.stdin)["id"])')

while :; do
  TASK=$(curl -s https://api.apiko.app/v1/videos/$TASK_ID \
    -H "Authorization: Bearer $APIKO_API_KEY")
  printf '%s\n' "$TASK"
  printf '%s' "$TASK" | grep -qE '"status": *"(completed|failed)"|"error": *\{' && break
  sleep 10
done
```

엔드포인트: `POST https://api.apiko.app/v1/videos` (작업 생성) · `GET https://api.apiko.app/v1/videos/{id}` (상태와 결과 조회)

<a id="how-to-write"></a>
## ✍️ Kling 4.0 프롬프트 작성법

이 페이지의 프롬프트에 반복해서 나오는 네 가지 구조.

- **초 단위 샷** · `샷 1 (0–5초): 구도 + 동작. 샷 2 (5–10초): …` — 긴 클립은 샷마다 시간 구간, 구도, 동작 하나를 적어 30초까지 순서와 속도를 잡습니다.
- **대사 쓰기** · `[이름, 목소리와 억양]: "정확한 대사"` — 대화 프롬프트는 따옴표 대사 앞에 화자와 목소리를 적어 Kling 4.0이 맞는 목소리를 입히고 입 모양을 맞추게 합니다.
- **원테이크** · `컷 없이 하나의 연속 샷 + 카메라 경로 + 그 사이 일어나는 일` — 액션과 브이로그 프롬프트는 컷을 아예 금지하고, 카메라를 장면을 지나가는 사람이나 장비처럼 묘사합니다.
- **참고 이미지에서 고정할 것** · `이미지 1 = 누구. 유지: 얼굴, 머리, 의상. 변경: 장면, 동작.` — 참고 이미지 프롬프트는 어떤 그림이 캐릭터나 제품을 정하는지, 무엇이 바뀌면 안 되는지 먼저 말하고 나머지를 묘사합니다.

**예시에서 보이는 것**

- **소리도 적으세요.** Kling 4.0은 항상 오디오를 만듭니다. 좋은 프롬프트는 음악, 주변음, 문 소리, 대사 한 줄처럼 들리는 것을 적습니다.
- **원하지 않는 것을 금지하세요.** 휴대폰 영상 프롬프트는 자막, 배경음악, 영화 같은 색보정을 빼서 편집하지 않은 녹화처럼 보이게 합니다.
- **편집용 기본 클립을 남기세요.** 참고 영상 편집 카드는 같은 공원 장면에서 시작해 개, 계절, 인물만 바꾸고 나머지는 유지합니다.
- **짧은 프롬프트도 됩니다.** 「멀티샷 드리프트」 한 줄이나 핼러윈 이야기 한 문장으로도 쓸 만한 클립이 나왔습니다. 디테일은 주로 통제를 위한 것입니다.
- **8,000자 이내로 쓰세요.** APIKO의 kling-4.0 프롬프트 한도입니다. 다른 곳에 올라온 아주 긴 프롬프트는 「사용」이 거부되므로 넣지 않았습니다.

<a id="menu"></a>
## 📑 목차

- [⭐ 추천](#featured) (6)
- [🎬 시네마틱](prompts/cinematic_ko.md) (32) — 카메라 움직임 하나, 빛 하나, 이상한 사건 하나로 만든 단일 장면.
- [🥊 액션과 추격](prompts/action_ko.md) (28) — 격투, 파쿠르, 카체이스, 스턴트. 대부분 샷 단위로 짰습니다.
- [💬 대화와 드라마](prompts/dialogue_ko.md) (16) — 사람이 말하는 장면: 따옴표 대사, 억양, 멈춤, 립싱크.
- [🐉 판타지와 SF](prompts/fantasy-scifi_ko.md) (21) — 외계 행성, 괴수, 신, 드래곤이 등장하는 큰 스케일 장면.
- [🧸 애니메이션](prompts/animation_ko.md) (14) — 3D 카툰, 애니, 클레이, 페인터리 2.5D, 키네틱 타이포.
- [🤳 브이로그와 UGC](prompts/vlog-ugc_ko.md) (8) — 실제 촬영처럼 보이도록 만든 휴대폰 셀카와 일상 클립.
- [👟 제품과 광고](prompts/product_ko.md) (8) — 제품이나 공간이 그대로 유지돼야 하는 광고.
- [🔁 참고 영상 편집](prompts/reference-edit_ko.md) (6) — 기본 클립 하나를 후속 프롬프트로 바꿉니다: 동물, 계절, 인물 추가.
- [❓ 자주 묻는 질문](#faq)
- [🔗 관련 링크](#related)

<a id="featured"></a>
## ⭐ 추천

<a id="cinematic-08"></a>
### 7. 초원 위를 나는 검독수리 추적샷

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08)** · [원본 게시물](https://x.com/minchoi/status/2104742876584218720)

<a href="https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-08.webp" width="560" alt="초원 위를 나는 검독수리 추적샷 – Kling 4.0"></a>

**프롬프트:**

```text
"Third-person chase shot from directly behind and slightly above a golden eagle as it flies over vast mountainous steppe. The camera follows at a fixed distance of a few metres, locked steady on the eagle, with smooth forward motion and no jitter. The whole bird stays in the lower centre of the frame with its full wingspan inside the frame and clear space on both sides. First it beats its wings powerfully, feathers flexing at the tips, then it spreads them wide and glides. Below and ahead, the landscape rushes toward the camera: winding rivers, open valleys, rocky peaks, with strong parallax. Bright late-afternoon sun from ahead, crisp air, a gentle rim light on its feathers, subtle lens flare. Realistic flight physics, motion blur from speed only, one continuous shot with no cuts."
```

<a id="fantasy-scifi-21"></a>
### 95. 석호를 건너는 긴 목의 외계 거수

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2110982744247353611)

<a href="https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/fantasy-scifi-21.webp" width="560" alt="석호를 건너는 긴 목의 외계 거수 – Kling 4.0"></a>

**프롬프트:**

```text
Two enormous long-necked alien animals slowly walk through a shallow turquoise lagoon surrounded by bright red grass and exotic palm forests. Their massive bodies create realistic waves and splashes with every step while smaller creatures flee along the shoreline. The camera begins low near the water and smoothly cranes upward, revealing the gigantic animals against a glowing yellow-green sky and distant mountains. Realistic weight and inertia, detailed skin movement, volumetric mist, natural vegetation motion, cinematic alien wildlife documentary, smooth continuous camera movement, highly coherent anatomy.
```

<a id="cinematic-26"></a>
### 25. 수묵화 족자에서 쏟아지는 폭포

작성자 [@opener_ai](https://x.com/opener_ai) · 10초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26)** · [원본 게시물](https://x.com/opener_ai/status/2111666343447818617)

<a href="https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-26.webp" width="320" alt="수묵화 족자에서 쏟아지는 폭포 – Kling 4.0"></a>

**프롬프트:**

```text
A tall Korean ink-wash landscape scroll hangs against a warm plaster wall in a quiet hanok alcove. Painted misty mountains and a black pine surround one narrow painted waterfall. A shallow celadon basin rests directly below the scroll, already visible from the opening frame. The opening second reveals the striking ink waterfall gleaming faintly like liquid. Over the next three seconds only the waterfall's lower end gradually becomes a small continuous stream of real clear water, crossing the paper's lower edge and falling into the basin. For the remaining six seconds that stream keeps flowing from the same painted waterfall, producing contact splashes and expanding ripples; the basin's water level rises slightly without overflowing. The deliberate fantasy is only the painted waterfall producing real water: mountains, pine, paper borders and wall remain still and dry. Static full view of scroll and basin, warm side lighting, exquisite ink texture and glossy celadon, one continuous ten-second shot. No cuts, new objects or captions.
```

<a id="action-05"></a>
### 37. 6개 샷 야시장 스파이 추격

작성자 [@minchoi](https://x.com/minchoi) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05)** · [원본 게시물](https://x.com/minchoi/status/2104743085087560174)

<a href="https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/action-05.webp" width="560" alt="6개 샷 야시장 스파이 추격 – Kling 4.0"></a>

**프롬프트:**

```text
"Multi-shot spy-thriller chase through a night market, 15 seconds, 6 shots with hard cuts, fast and relentless. [Cole]: early 30s, short dark-brown hair, clean-shaven, tailored charcoal suit, white shirt open at the collar, no tie. [Anton]: late 30s, ash-blond buzz cut, short blond beard, black leather jacket, dark grey henley. A packed night-market lane after rain: food stalls, red paper lanterns, string lights, grill smoke, steam, wet pavement reflecting the lights. Anton always runs toward frame right; Cole chases him. Shot 1 (0–2s): Telephoto close-up of Cole standing still in the moving crowd, shoppers blurring past in the foreground, eyes locked on something off-screen right. Shot 2 (2–4.5s): The camera whip-pans right along his eyeline and snaps sharp onto Anton under a red stall sign reading "DUMPLINGS". Anton sees Cole, drops his paper cup and bolts right. Shot 3 (4.5–7s): Fast side tracking shot racing alongside at full sprint, both men running frame right: Anton shoving shoppers aside, Cole ten metres behind and closing, string lights streaking past. Shot 4 (7–9.5s): Low angle: Anton yanks a stack of fruit crates down behind him and oranges spill across the wet ground; Cole leaps the crates in one stride, suit jacket flaring, lands hard and keeps running. Shot 5 (9.5–12.5s): Cole bursts into a crossroads of lanes beneath a stall sign reading "HOT TEA" and stops dead, breathing hard. Anton is gone. The camera orbits slowly halfway around Cole, circling past his left side to end over his shoulder, as he scans the crowd. Shot 6 (12.5–15s): Close on Cole. His eyes snap left and the camera whip-pans left, landing sharp on Anton climbing a metal stairway above the stalls, glancing back. Cole sprints out of frame after him. Gritty handheld spy-thriller look, anamorphic, shallow depth of field, teal shadows with warm amber lantern light, motion blur from speed only. No dialogue: pounding footsteps, crates crashing, oranges rolling, sizzling grills, crowd gasps, a pulsing percussion score with low brass stabs."
```

<a id="animation-12"></a>
### 109. 「부」를 배우는 점토 유령

작성자 [@JasonHeatony7](https://x.com/JasonHeatony7) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12)** · [원본 게시물](https://x.com/JasonHeatony7/status/2115812533533581757)

<a href="https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/animation-12.webp" width="320" alt="「부」를 배우는 점토 유령 – Kling 4.0"></a>

**프롬프트:**

```text
Style: classic claymation stop-motion, smooth plasticine figures with visible thumbprints and sculpting marks, glossy clay highlights, miniature handmade autumn set with clay leaves and a painted backdrop of a moonlit sky, warm golden lantern light with soft purple shadows, slightly choppy stop-motion movement at 12 frames per second.
0-3s (HOOK): A tiny round white clay ghost with big googly eyes peeks out from behind a chunky clay pumpkin, its little body squishing and wobbling nervously.
3-6s: Bigger clay ghosts float past on visible thin wires, booming "BOO!" at a clay bat hanging from a twisted branch, which squeaks and flaps away. The little ghost tries and lets out a tiny "meep."
6-10s: A plump clay frog hops by with a squishy plop. The little ghost takes a deep breath, its body inflating slightly, rises up, and squeaks again. The frog blinks slowly, then gives it a sticky little pat on the head.
10-13s: Feeling brave, the ghost spins, stretches tall like rubbery clay, and lets out a real, loud "BOO!" Every clay jack-o'-lantern in the patch bursts alight with flickering candle glow.
13-15s (BUTTON): The ghost startles itself, squishes flat like a pancake, and slides back behind the pumpkin with a soft splat.
Camera: low, close-up tabletop view, with a quick push-in on the big "BOO."
Audio: squishy clay sounds, a soft frog croak, crunchy clay leaves, and a tiny echoing "meep." Music is a bouncy bassoon and a plucky ukulele, light and silly with a spooky theremin twist.
No subtitles.
```

<a id="cinematic-29"></a>
### 28. 검은 수면에 떨어지는 물방울 매크로

작성자 [@sebatheepan](https://x.com/sebatheepan) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29)** · [원본 게시물](https://x.com/sebatheepan/status/2113038301154164960)

<a href="https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-29.webp" width="320" alt="검은 수면에 떨어지는 물방울 매크로 – Kling 4.0"></a>

**프롬프트:**

```text
A single droplet of water falls into a still black pool and the surface answers it.Shot 1 — 0.0s to 6.0s — ECU macro, eye level with the waterline, locked-off. At 0.0s the frame holds a still black water surface across the lower third, its meniscus drawn as one bright curve against a matte grey background. A single droplet hangs in the upper frame, out of focus, then falls. At 1.4s it strikes the surface and the impact throws a crown of water upward in real time, crisp-edged rather than blurred; the crown collapses inward on itself by 2.4s and a rebound droplet rises out of the collapse, hangs briefly at 2.6s, and falls back at 4.1s. Ripples run outward and reach the frame edge at 5.4s, and the surface settles into stillness indistinguishable from frame one.

Camera law: 100mm macro at minimum focus distance, locked-off, no camera move; the plane of focus sits exactly on the meniscus and depth of field is razor thin; 1/2000s shutter so droplet edges stay crisp through the fastest motion. Anti-default: a defocused beaker rim occupies the left fifteen percent of the frame, close to the lens, and is never racked away.Grade and audio: cool-daylight palette — black, steel-blue, one white specular — contrast low-key deep shadow. Key light is a single soft source directly above the pool, halation blooming on the specular highlight. Room tone as the bed under five diegetic events — surface tension snapping, impact into the pool, crown collapse, the rebound droplet returning, ripples sheeting across still water.Constraints: Count of cuts: zero. Count of droplets: one. Count of people in frame: zero. No music, no score, no bgm. No subtitles.
```

- **[🎬 시네마틱 전체 32개 보기](prompts/cinematic_ko.md)**
- **[🥊 액션과 추격 전체 28개 보기](prompts/action_ko.md)**
- **[💬 대화와 드라마 전체 16개 보기](prompts/dialogue_ko.md)**
- **[🐉 판타지와 SF 전체 21개 보기](prompts/fantasy-scifi_ko.md)**
- **[🧸 애니메이션 전체 14개 보기](prompts/animation_ko.md)**
- **[🤳 브이로그와 UGC 전체 8개 보기](prompts/vlog-ugc_ko.md)**
- **[👟 제품과 광고 전체 8개 보기](prompts/product_ko.md)**
- **[🔁 참고 영상 편집 전체 6개 보기](prompts/reference-edit_ko.md)**

<a id="faq"></a>
## ❓ 자주 묻는 질문

<details>
<summary><b>이 Kling 4.0 프롬프트는 무료로 써도 되나요?</b></summary>

복사, 수정, 실행 모두 가능합니다. 프롬프트와 영상은 카드에 표시된 크리에이터의 것이니 클립을 상업적으로 쓰기 전에 원문을 확인하세요.

</details>

<details>
<summary><b>Kling 4.0 영상은 얼마나 길게 만들 수 있나요?</b></summary>

3~30초, 720p 또는 1080p입니다. 모든 클립에 소리가 함께 생성됩니다.

</details>

<details>
<summary><b>Kling 4.0은 어떤 화면 비율을 지원하나요?</b></summary>

16:9, 9:16, 1:1, 21:9, 또는 참고 이미지가 있으면 그 비율을 따르는 adaptive입니다.

</details>

<details>
<summary><b>참고 이미지와 참고 영상을 쓸 수 있나요?</b></summary>

네. 캐릭터, 제품, 장면용 참고 이미지 최대 10장, 동작·카메라·편집용 참고 영상 최대 5개(합계 3~30초)를 넣을 수 있습니다. 참고 영상이 있는 작업은 참고 영상 요금으로 청구됩니다.

</details>

<details>
<summary><b>프롬프트는 얼마나 길게 쓸 수 있나요?</b></summary>

APIKO에서는 최대 8,000자입니다. 대사, 소리, 카메라 지시는 모두 프롬프트에 씁니다.

</details>

<details>
<summary><b>프롬프트는 어떤 언어로 써야 하나요?</b></summary>

프롬프트는 작성자 원문 그대로이며 대부분 영어, 일부는 일본어와 한국어입니다. 대사는 프롬프트의 나머지와 다른 언어로 써도 됩니다.

</details>

<details>
<summary><b>결과가 예시와 다른 이유는?</b></summary>

실행할 때마다 결과가 다르고, 작성자가 참고 이미지, 1080p, Kling 4.0 Flash 또는 다른 앱을 썼을 수 있습니다. 한 번에 하나씩 바꿔 비교하세요.

</details>

<details>
<summary><b>API로는 어떻게 실행하나요?</b></summary>

model을 kling-4.0으로, prompt에 프롬프트를 넣어 /v1/videos로 POST하고, 작업을 조회한 뒤 영상을 내려받습니다. 모든 필드는 API 문서에 있습니다.

</details>


<a id="related"></a>
## 🔗 관련 링크

- [Kling 4.0 프롬프트 · apiko.app](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Kling 4.0 실행](https://apiko.app/ko/models/kling-4.0?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Kling 4.0 API 문서](https://apiko.app/docs/api-manual/video-series/kling/kling-4.0?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Seedance 2.5 프롬프트](https://apiko.app/ko/seedance-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Wan 3.0 프롬프트](https://apiko.app/ko/wan-3-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Seedance 2.5](https://apiko.app/ko/models/seedance-2.5?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [APIKO API 코드 예시](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**다른 프롬프트 모음**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_ko.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_ko.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_ko.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_ko.md)

<a id="license"></a>
## 📄 라이선스와 출처

프롬프트와 결과 영상은 각 카드에 표시된 크리에이터의 것이며, 카드는 X 원문으로 연결됩니다. 제목, 설명, 번역, 빌드 스크립트는 [CC BY 4.0](LICENSE)으로 배포합니다.

이 목록이 도움이 됐다면 ⭐ 를 눌러 다른 사람도 찾을 수 있게 해 주세요.
