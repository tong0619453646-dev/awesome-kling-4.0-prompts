<div align="center">

<a href="https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-kling-4.0-prompts"><img src="assets/banner.jpg" alt="Awesome Kling 4.0 提示詞" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-133_cases-111111)](README_zh-TW.md#menu)
[![Try Kling 4.0 on APIKO](https://img.shields.io/badge/Try_Kling_4.0-on_APIKO-4F46E5)](https://apiko.app/zh-tw/models/kling-4.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-kling-4.0-prompts&utm_content=model_try)
[![Kling 4.0 API docs](https://img.shields.io/badge/Kling_4.0-API_docs-111111)](https://apiko.app/zh-tw/docs/api-manual/video-series/kling/kling-4.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-kling-4.0-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-Current-111111)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome Kling 4.0 提示詞

<a id="introduction"></a>
## 🌟 簡介

**Kling 4.0 提示詞：133 個可複製的影片提示詞，每個都附上生成的片段，涵蓋一鏡到底動作、對白戲、參考圖廣告和影片編輯。**

每個提示詞旁邊就是它生成的影片：直接複製，或在模型頁開啟，長度和畫面比例已照範例設好。

線上搜尋與篩選： [apiko.app/kling-4-0-prompts](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-kling-4.0-prompts&utm_content=intro).

> [!NOTE]
> 提示詞保持作者發布時的原文，所以大多是英文；標題與簡介由我們撰寫。每則都署名作者並連結原帖。

<a id="quick-start"></a>
## 🚀 快速開始

**網頁上用：** 每則都有「在 APIKO 執行」連結，會在 [apiko.app](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-kling-4.0-prompts&utm_content=browser) 開啟這則範例；點「使用」，提示詞就會填進 Kling 4.0 試用台。

**用 API：** 先建立 [APIKO API 金鑰](https://apiko.app/zh-tw/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-kling-4.0-prompts&utm_content=api_key)，再建立任務並輪詢，直到影片生成完成。

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

介面: `POST https://api.apiko.app/v1/videos` (建立任務) · `GET https://api.apiko.app/v1/videos/{id}` (查詢狀態與結果)

<a id="how-to-write"></a>
## ✍️ Kling 4.0 提示詞怎麼寫

本頁提示詞裡反覆出現的四種結構。

- **分秒分鏡** · `鏡頭 1（0–5 秒）：景別 + 動作。鏡頭 2（5–10 秒）：……` — 長影片把每個鏡頭的時間段、景別和一個動作逐條列出，30 秒以內的順序和節奏都能掌握。
- **寫台詞** · `[角色名，聲音和口音]：「原話」` — 對白提示詞在每句引號台詞前寫明說話的人和聲音，Kling 4.0 會配上對應的嗓音並對上嘴型。
- **一鏡到底** · `一個連續鏡頭，不剪接 + 攝影機路徑 + 途中發生什麼` — 動作和 Vlog 提示詞常直接禁止剪接，把攝影機寫成穿過場景的人或設備。
- **鎖定參考圖內容** · `圖 1 = 誰。保留：臉、髮型、服裝。改變：場景、動作。` — 參考圖提示詞先說明哪張圖定義角色或商品、哪些不能變，再描述其餘部分。

**從範例裡看得出**

- **把聲音也寫上。** Kling 4.0 每次都會生成聲音，效果好的提示詞會寫明聽到什麼：音樂、環境音、一扇門、一句台詞。
- **寫明不要什麼。** 手機影片類提示詞排除字幕、配樂和電影調色，片段才像沒剪過的錄影。
- **留一段基礎片段做編輯。** 參考影片編輯卡都從同一段公園片段出發，只換狗、季節或人物，其餘保持不變。
- **短提示詞也能用。** 一句「多鏡頭甩尾」或一句萬聖節小故事也生成了可用的片段，細節主要是為了更好掌控。
- **控制在 8000 字以內。** 這是 APIKO 上 kling-4.0 的提示詞上限。別處發布的超長提示詞沒有收錄，因為按「使用」會被拒絕。

<a id="menu"></a>
## 📑 目錄

- [⭐ 精選](#featured) (6)
- [🎬 電影感](prompts/cinematic_zh-TW.md) (32) — 圍繞一個運鏡、一種光線和一件怪事展開的單場景。
- [🥊 動作與追逐](prompts/action_zh-TW.md) (28) — 打鬥、跑酷、飛車和特技，多半按鏡頭逐一安排。
- [💬 對白與劇情](prompts/dialogue_zh-TW.md) (16) — 有人說話的戲：台詞加引號，寫明口音、停頓和嘴型。
- [🐉 奇幻與科幻](prompts/fantasy-scifi_zh-TW.md) (21) — 外星世界、巨獸、神明和巨龍，場面都很大。
- [🧸 動畫](prompts/animation_zh-TW.md) (14) — 3D 卡通、日式動畫、黏土、厚塗 2.5D 和文字動效。
- [🤳 Vlog 與 UGC](prompts/vlog-ugc_zh-TW.md) (8) — 手機自拍和隨手拍，目標是看起來像真實素材。
- [👟 產品與廣告](prompts/product_zh-TW.md) (8) — 商品或房間必須保持原樣的廣告片。
- [🔁 參考影片編輯](prompts/reference-edit_zh-TW.md) (6) — 同一段基礎片段，用後續提示詞換動物、換季節或加人。
- [❓ 常見問題](#faq)
- [🔗 相關連結](#related)

<a id="featured"></a>
## ⭐ 精選

<a id="cinematic-08"></a>
### 7. 緊跟金鵰飛越草原

作者 [@minchoi](https://x.com/minchoi) · 30 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08)** · [原帖](https://x.com/minchoi/status/2104742876584218720)

<a href="https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-08.webp" width="560" alt="緊跟金鵰飛越草原 – Kling 4.0"></a>

**提示詞:**

```text
"Third-person chase shot from directly behind and slightly above a golden eagle as it flies over vast mountainous steppe. The camera follows at a fixed distance of a few metres, locked steady on the eagle, with smooth forward motion and no jitter. The whole bird stays in the lower centre of the frame with its full wingspan inside the frame and clear space on both sides. First it beats its wings powerfully, feathers flexing at the tips, then it spreads them wide and glides. Below and ahead, the landscape rushes toward the camera: winding rivers, open valleys, rocky peaks, with strong parallax. Bright late-afternoon sun from ahead, crisp air, a gentle rim light on its feathers, subtle lens flare. Realistic flight physics, motion blur from speed only, one continuous shot with no cuts."
```

<a id="fantasy-scifi-21"></a>
### 95. 長頸外星巨獸涉過潟湖

作者 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 15 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21)** · [原帖](https://x.com/Alin_Reaper05/status/2110982744247353611)

<a href="https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/fantasy-scifi-21.webp" width="560" alt="長頸外星巨獸涉過潟湖 – Kling 4.0"></a>

**提示詞:**

```text
Two enormous long-necked alien animals slowly walk through a shallow turquoise lagoon surrounded by bright red grass and exotic palm forests. Their massive bodies create realistic waves and splashes with every step while smaller creatures flee along the shoreline. The camera begins low near the water and smoothly cranes upward, revealing the gigantic animals against a glowing yellow-green sky and distant mountains. Realistic weight and inertia, detailed skin movement, volumetric mist, natural vegetation motion, cinematic alien wildlife documentary, smooth continuous camera movement, highly coherent anatomy.
```

<a id="cinematic-26"></a>
### 25. 水墨畫卷裡流出真實瀑布

作者 [@opener_ai](https://x.com/opener_ai) · 10 秒 · 9:16 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26)** · [原帖](https://x.com/opener_ai/status/2111666343447818617)

<a href="https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-26.webp" width="320" alt="水墨畫卷裡流出真實瀑布 – Kling 4.0"></a>

**提示詞:**

```text
A tall Korean ink-wash landscape scroll hangs against a warm plaster wall in a quiet hanok alcove. Painted misty mountains and a black pine surround one narrow painted waterfall. A shallow celadon basin rests directly below the scroll, already visible from the opening frame. The opening second reveals the striking ink waterfall gleaming faintly like liquid. Over the next three seconds only the waterfall's lower end gradually becomes a small continuous stream of real clear water, crossing the paper's lower edge and falling into the basin. For the remaining six seconds that stream keeps flowing from the same painted waterfall, producing contact splashes and expanding ripples; the basin's water level rises slightly without overflowing. The deliberate fantasy is only the painted waterfall producing real water: mountains, pine, paper borders and wall remain still and dry. Static full view of scroll and basin, warm side lighting, exquisite ink texture and glossy celadon, one continuous ten-second shot. No cuts, new objects or captions.
```

<a id="action-05"></a>
### 37. 六個鏡頭的夜市間諜追逐

作者 [@minchoi](https://x.com/minchoi) · 15 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05)** · [原帖](https://x.com/minchoi/status/2104743085087560174)

<a href="https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/action-05.webp" width="560" alt="六個鏡頭的夜市間諜追逐 – Kling 4.0"></a>

**提示詞:**

```text
"Multi-shot spy-thriller chase through a night market, 15 seconds, 6 shots with hard cuts, fast and relentless. [Cole]: early 30s, short dark-brown hair, clean-shaven, tailored charcoal suit, white shirt open at the collar, no tie. [Anton]: late 30s, ash-blond buzz cut, short blond beard, black leather jacket, dark grey henley. A packed night-market lane after rain: food stalls, red paper lanterns, string lights, grill smoke, steam, wet pavement reflecting the lights. Anton always runs toward frame right; Cole chases him. Shot 1 (0–2s): Telephoto close-up of Cole standing still in the moving crowd, shoppers blurring past in the foreground, eyes locked on something off-screen right. Shot 2 (2–4.5s): The camera whip-pans right along his eyeline and snaps sharp onto Anton under a red stall sign reading "DUMPLINGS". Anton sees Cole, drops his paper cup and bolts right. Shot 3 (4.5–7s): Fast side tracking shot racing alongside at full sprint, both men running frame right: Anton shoving shoppers aside, Cole ten metres behind and closing, string lights streaking past. Shot 4 (7–9.5s): Low angle: Anton yanks a stack of fruit crates down behind him and oranges spill across the wet ground; Cole leaps the crates in one stride, suit jacket flaring, lands hard and keeps running. Shot 5 (9.5–12.5s): Cole bursts into a crossroads of lanes beneath a stall sign reading "HOT TEA" and stops dead, breathing hard. Anton is gone. The camera orbits slowly halfway around Cole, circling past his left side to end over his shoulder, as he scans the crowd. Shot 6 (12.5–15s): Close on Cole. His eyes snap left and the camera whip-pans left, landing sharp on Anton climbing a metal stairway above the stalls, glancing back. Cole sprints out of frame after him. Gritty handheld spy-thriller look, anamorphic, shallow depth of field, teal shadows with warm amber lantern light, motion blur from speed only. No dialogue: pounding footsteps, crates crashing, oranges rolling, sizzling grills, crowd gasps, a pulsing percussion score with low brass stabs."
```

<a id="animation-12"></a>
### 109. 黏土小幽靈學會說「布」

作者 [@JasonHeatony7](https://x.com/JasonHeatony7) · 15 秒 · 9:16 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12)** · [原帖](https://x.com/JasonHeatony7/status/2115812533533581757)

<a href="https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/animation-12.webp" width="320" alt="黏土小幽靈學會說「布」 – Kling 4.0"></a>

**提示詞:**

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
### 28. 一滴水落入黑色水面的微距

作者 [@sebatheepan](https://x.com/sebatheepan) · 15 秒 · 9:16 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29)** · [原帖](https://x.com/sebatheepan/status/2113038301154164960)

<a href="https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-29.webp" width="320" alt="一滴水落入黑色水面的微距 – Kling 4.0"></a>

**提示詞:**

```text
A single droplet of water falls into a still black pool and the surface answers it.Shot 1 — 0.0s to 6.0s — ECU macro, eye level with the waterline, locked-off. At 0.0s the frame holds a still black water surface across the lower third, its meniscus drawn as one bright curve against a matte grey background. A single droplet hangs in the upper frame, out of focus, then falls. At 1.4s it strikes the surface and the impact throws a crown of water upward in real time, crisp-edged rather than blurred; the crown collapses inward on itself by 2.4s and a rebound droplet rises out of the collapse, hangs briefly at 2.6s, and falls back at 4.1s. Ripples run outward and reach the frame edge at 5.4s, and the surface settles into stillness indistinguishable from frame one.

Camera law: 100mm macro at minimum focus distance, locked-off, no camera move; the plane of focus sits exactly on the meniscus and depth of field is razor thin; 1/2000s shutter so droplet edges stay crisp through the fastest motion. Anti-default: a defocused beaker rim occupies the left fifteen percent of the frame, close to the lens, and is never racked away.Grade and audio: cool-daylight palette — black, steel-blue, one white specular — contrast low-key deep shadow. Key light is a single soft source directly above the pool, halation blooming on the specular highlight. Room tone as the bed under five diegetic events — surface tension snapping, impact into the pool, crown collapse, the rebound droplet returning, ripples sheeting across still water.Constraints: Count of cuts: zero. Count of droplets: one. Count of people in frame: zero. No music, no score, no bgm. No subtitles.
```

- **[🎬 查看「電影感」全部 32 則](prompts/cinematic_zh-TW.md)**
- **[🥊 查看「動作與追逐」全部 28 則](prompts/action_zh-TW.md)**
- **[💬 查看「對白與劇情」全部 16 則](prompts/dialogue_zh-TW.md)**
- **[🐉 查看「奇幻與科幻」全部 21 則](prompts/fantasy-scifi_zh-TW.md)**
- **[🧸 查看「動畫」全部 14 則](prompts/animation_zh-TW.md)**
- **[🤳 查看「Vlog 與 UGC」全部 8 則](prompts/vlog-ugc_zh-TW.md)**
- **[👟 查看「產品與廣告」全部 8 則](prompts/product_zh-TW.md)**
- **[🔁 查看「參考影片編輯」全部 6 則](prompts/reference-edit_zh-TW.md)**

<a id="faq"></a>
## ❓ 常見問題

<details>
<summary><b>這些 Kling 4.0 提示詞可以免費用嗎？</b></summary>

可以複製、修改和執行。提示詞和影片歸卡片標註的創作者所有，商用影片前請先看原文說明。

</details>

<details>
<summary><b>Kling 4.0 影片最長多久？</b></summary>

3 到 30 秒，720p 或 1080p，每段都有聲音。

</details>

<details>
<summary><b>Kling 4.0 支援哪些畫面比例？</b></summary>

16:9、9:16、1:1、21:9，或 adaptive（有參考圖時跟隨參考圖）。

</details>

<details>
<summary><b>能用參考圖和參考影片嗎？</b></summary>

可以：最多 10 張參考圖用於角色、商品或場景，最多 5 段參考影片（合計 3–30 秒）用於動作、運鏡或編輯。帶參考影片的任務按參考影片價計費。

</details>

<details>
<summary><b>提示詞最長多少字？</b></summary>

APIKO 上最多 8000 字元。台詞、聲音和運鏡都寫在提示詞裡。

</details>

<details>
<summary><b>提示詞用什麼語言寫？</b></summary>

提示詞保留作者原文，多數是英文，也有日文和韓文。台詞可以用和提示詞其他部分不同的語言。

</details>

<details>
<summary><b>為什麼我生成的和範例不一樣？</b></summary>

每次生成結果都不同，作者也可能用了參考圖、1080p、Kling 4.0 Flash 或其他應用程式。一次只改一處細節來比較。

</details>

<details>
<summary><b>怎麼透過 API 執行提示詞？</b></summary>

向 /v1/videos 發 POST，model 填 kling-4.0，prompt 填提示詞，輪詢任務後下載影片。API 文件列出了全部欄位。

</details>


<a id="related"></a>
## 🔗 相關連結

- [Kling 4.0 提示詞 · apiko.app](https://apiko.app/zh-tw/kling-4-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [試用 Kling 4.0](https://apiko.app/zh-tw/models/kling-4.0?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Kling 4.0 API 文件](https://apiko.app/zh-tw/docs/api-manual/video-series/kling/kling-4.0?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Seedance 2.5 提示詞](https://apiko.app/zh-tw/seedance-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Wan 3.0 提示詞](https://apiko.app/zh-tw/wan-3-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Seedance 2.5](https://apiko.app/zh-tw/models/seedance-2.5?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [APIKO API 程式碼範例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示詞合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_zh-TW.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_zh-TW.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-TW.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-TW.md)

<a id="license"></a>
## 📄 授權與出處

提示詞和影片歸每張卡片標註的創作者所有，卡片可連到 X 上的原文。標題、簡介、譯文與生成腳本採用 [CC BY 4.0](LICENSE) 授權。

如果這份合集幫你省了時間，按個 ⭐ 能讓更多人看到。
