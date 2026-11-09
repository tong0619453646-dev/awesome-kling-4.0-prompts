<div align="center">

<a href="https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-kling-4.0-prompts"><img src="assets/banner.jpg" alt="Awesome Kling 4.0 提示词" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-133_cases-111111)](README_zh-CN.md#menu)
[![Try Kling 4.0 on APIKO](https://img.shields.io/badge/Try_Kling_4.0-on_APIKO-4F46E5)](https://apiko.app/zh/models/kling-4.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-kling-4.0-prompts&utm_content=model_try)
[![Kling 4.0 API docs](https://img.shields.io/badge/Kling_4.0-API_docs-111111)](https://apiko.app/zh/docs/api-manual/video-series/kling/kling-4.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-kling-4.0-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-Current-111111)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome Kling 4.0 提示词

<a id="introduction"></a>
## 🌟 简介

**Kling 4.0 提示词：133 条可复制的视频提示词，每条附生成的片段，涵盖一镜到底动作、对白戏、参考图广告和视频编辑。**

每条提示词旁边就是它生成的视频：直接复制，或在模型页打开，时长和画幅已按示例设好。

在线搜索和筛选： [apiko.app/kling-4-0-prompts](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-kling-4.0-prompts&utm_content=intro).

> [!NOTE]
> 提示词保持作者发布时的原文，所以大多是英文；标题和简介是我们写的。每条都署名作者并链接原帖。

<a id="quick-start"></a>
## 🚀 快速开始

**网页上用：** 每条都有「在 APIKO 运行」链接，会在 [apiko.app](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-kling-4.0-prompts&utm_content=browser) 打开这条示例；点「使用」，提示词就会填进 Kling 4.0 试用台。

**用 API：** 先创建 [APIKO API Key](https://apiko.app/zh/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-kling-4.0-prompts&utm_content=api_key)，再创建任务并轮询，直到视频生成完成。

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

接口: `POST https://api.apiko.app/v1/videos` (创建任务) · `GET https://api.apiko.app/v1/videos/{id}` (查询状态和结果)

<a id="how-to-write"></a>
## ✍️ Kling 4.0 提示词怎么写

本页提示词里反复出现的四种结构。

- **分秒分镜** · `镜头 1（0–5 秒）：景别 + 动作。镜头 2（5–10 秒）：……` — 长视频把每个镜头的时间段、景别和一个动作逐条列出，30 秒以内的顺序和节奏都能控制住。
- **写台词** · `[角色名，声音和口音]："原话"` — 对白提示词在每句引号台词前写明说话人和声音，Kling 4.0 会配对应的嗓音并对上口型。
- **一镜到底** · `一个连续镜头，不剪切 + 摄影机路径 + 途中发生什么` — 动作和 Vlog 提示词常直接禁止剪切，把摄影机写成穿过场景的人或设备。
- **锁定参考图内容** · `图 1 = 谁。保留：脸、发型、服装。改变：场景、动作。` — 参考图提示词先说明哪张图定义角色或商品、哪些不能变，再描述其余部分。

**从示例里能看出**

- **把声音也写上。** Kling 4.0 每次都会生成声音，效果好的提示词会写明听到什么：音乐、环境声、一扇门、一句台词。
- **写明不要什么。** 手机视频类提示词排除字幕、配乐和电影调色，片段才像没剪过的录像。
- **留一段基础片段做编辑。** 参考视频编辑卡都从同一段公园片段出发，只换狗、季节或人物，其余保持不变。
- **短提示词也能用。** 一句「多镜头漂移」或一句万圣节小故事也生成了可用的片段，细节主要是为了更好控制。
- **控制在 8000 字以内。** 这是 APIKO 上 kling-4.0 的提示词上限。别处发布的超长提示词没有收录，因为点「使用」会被拒绝。

<a id="menu"></a>
## 📑 目录

- [⭐ 精选](#featured) (6)
- [🎬 电影感](prompts/cinematic_zh-CN.md) (32) — 围绕一个运镜、一种光线和一件怪事展开的单场景。
- [🥊 动作与追逐](prompts/action_zh-CN.md) (28) — 打斗、跑酷、飞车和特技，多数按镜头逐一安排。
- [💬 对白与剧情](prompts/dialogue_zh-CN.md) (16) — 有人说话的戏：台词加引号，写明口音、停顿和口型。
- [🐉 奇幻与科幻](prompts/fantasy-scifi_zh-CN.md) (21) — 外星世界、巨兽、神明和巨龙，场面都很大。
- [🧸 动画](prompts/animation_zh-CN.md) (14) — 3D 卡通、日式动画、黏土、厚涂 2.5D 和文字动效。
- [🤳 Vlog 与 UGC](prompts/vlog-ugc_zh-CN.md) (8) — 手机自拍和随手拍，目标是看起来像真实素材。
- [👟 产品与广告](prompts/product_zh-CN.md) (8) — 商品或房间必须保持原样的广告片。
- [🔁 参考视频编辑](prompts/reference-edit_zh-CN.md) (6) — 同一段基础片段，用后续提示词换动物、换季节或加人。
- [❓ 常见问题](#faq)
- [🔗 相关链接](#related)

<a id="featured"></a>
## ⭐ 精选

<a id="cinematic-08"></a>
### 7. 紧跟金雕飞越草原

作者 [@minchoi](https://x.com/minchoi) · 30 秒 · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08)** · [原帖](https://x.com/minchoi/status/2104742876584218720)

<a href="https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-08.webp" width="560" alt="紧跟金雕飞越草原 – Kling 4.0"></a>

**提示词:**

```text
"Third-person chase shot from directly behind and slightly above a golden eagle as it flies over vast mountainous steppe. The camera follows at a fixed distance of a few metres, locked steady on the eagle, with smooth forward motion and no jitter. The whole bird stays in the lower centre of the frame with its full wingspan inside the frame and clear space on both sides. First it beats its wings powerfully, feathers flexing at the tips, then it spreads them wide and glides. Below and ahead, the landscape rushes toward the camera: winding rivers, open valleys, rocky peaks, with strong parallax. Bright late-afternoon sun from ahead, crisp air, a gentle rim light on its feathers, subtle lens flare. Realistic flight physics, motion blur from speed only, one continuous shot with no cuts."
```

<a id="fantasy-scifi-21"></a>
### 95. 长颈外星巨兽涉过泻湖

作者 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 15 秒 · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21)** · [原帖](https://x.com/Alin_Reaper05/status/2110982744247353611)

<a href="https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/fantasy-scifi-21.webp" width="560" alt="长颈外星巨兽涉过泻湖 – Kling 4.0"></a>

**提示词:**

```text
Two enormous long-necked alien animals slowly walk through a shallow turquoise lagoon surrounded by bright red grass and exotic palm forests. Their massive bodies create realistic waves and splashes with every step while smaller creatures flee along the shoreline. The camera begins low near the water and smoothly cranes upward, revealing the gigantic animals against a glowing yellow-green sky and distant mountains. Realistic weight and inertia, detailed skin movement, volumetric mist, natural vegetation motion, cinematic alien wildlife documentary, smooth continuous camera movement, highly coherent anatomy.
```

<a id="cinematic-26"></a>
### 25. 水墨画卷里流出真实瀑布

作者 [@opener_ai](https://x.com/opener_ai) · 10 秒 · 9:16 · **[▶ 在 APIKO 运行](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26)** · [原帖](https://x.com/opener_ai/status/2111666343447818617)

<a href="https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-26.webp" width="320" alt="水墨画卷里流出真实瀑布 – Kling 4.0"></a>

**提示词:**

```text
A tall Korean ink-wash landscape scroll hangs against a warm plaster wall in a quiet hanok alcove. Painted misty mountains and a black pine surround one narrow painted waterfall. A shallow celadon basin rests directly below the scroll, already visible from the opening frame. The opening second reveals the striking ink waterfall gleaming faintly like liquid. Over the next three seconds only the waterfall's lower end gradually becomes a small continuous stream of real clear water, crossing the paper's lower edge and falling into the basin. For the remaining six seconds that stream keeps flowing from the same painted waterfall, producing contact splashes and expanding ripples; the basin's water level rises slightly without overflowing. The deliberate fantasy is only the painted waterfall producing real water: mountains, pine, paper borders and wall remain still and dry. Static full view of scroll and basin, warm side lighting, exquisite ink texture and glossy celadon, one continuous ten-second shot. No cuts, new objects or captions.
```

<a id="action-05"></a>
### 37. 六个镜头的夜市间谍追逐

作者 [@minchoi](https://x.com/minchoi) · 15 秒 · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05)** · [原帖](https://x.com/minchoi/status/2104743085087560174)

<a href="https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/action-05.webp" width="560" alt="六个镜头的夜市间谍追逐 – Kling 4.0"></a>

**提示词:**

```text
"Multi-shot spy-thriller chase through a night market, 15 seconds, 6 shots with hard cuts, fast and relentless. [Cole]: early 30s, short dark-brown hair, clean-shaven, tailored charcoal suit, white shirt open at the collar, no tie. [Anton]: late 30s, ash-blond buzz cut, short blond beard, black leather jacket, dark grey henley. A packed night-market lane after rain: food stalls, red paper lanterns, string lights, grill smoke, steam, wet pavement reflecting the lights. Anton always runs toward frame right; Cole chases him. Shot 1 (0–2s): Telephoto close-up of Cole standing still in the moving crowd, shoppers blurring past in the foreground, eyes locked on something off-screen right. Shot 2 (2–4.5s): The camera whip-pans right along his eyeline and snaps sharp onto Anton under a red stall sign reading "DUMPLINGS". Anton sees Cole, drops his paper cup and bolts right. Shot 3 (4.5–7s): Fast side tracking shot racing alongside at full sprint, both men running frame right: Anton shoving shoppers aside, Cole ten metres behind and closing, string lights streaking past. Shot 4 (7–9.5s): Low angle: Anton yanks a stack of fruit crates down behind him and oranges spill across the wet ground; Cole leaps the crates in one stride, suit jacket flaring, lands hard and keeps running. Shot 5 (9.5–12.5s): Cole bursts into a crossroads of lanes beneath a stall sign reading "HOT TEA" and stops dead, breathing hard. Anton is gone. The camera orbits slowly halfway around Cole, circling past his left side to end over his shoulder, as he scans the crowd. Shot 6 (12.5–15s): Close on Cole. His eyes snap left and the camera whip-pans left, landing sharp on Anton climbing a metal stairway above the stalls, glancing back. Cole sprints out of frame after him. Gritty handheld spy-thriller look, anamorphic, shallow depth of field, teal shadows with warm amber lantern light, motion blur from speed only. No dialogue: pounding footsteps, crates crashing, oranges rolling, sizzling grills, crowd gasps, a pulsing percussion score with low brass stabs."
```

<a id="animation-12"></a>
### 109. 黏土小幽灵学会说「布」

作者 [@JasonHeatony7](https://x.com/JasonHeatony7) · 15 秒 · 9:16 · **[▶ 在 APIKO 运行](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12)** · [原帖](https://x.com/JasonHeatony7/status/2115812533533581757)

<a href="https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/animation-12.webp" width="320" alt="黏土小幽灵学会说「布」 – Kling 4.0"></a>

**提示词:**

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

作者 [@sebatheepan](https://x.com/sebatheepan) · 15 秒 · 9:16 · **[▶ 在 APIKO 运行](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29)** · [原帖](https://x.com/sebatheepan/status/2113038301154164960)

<a href="https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-29.webp" width="320" alt="一滴水落入黑色水面的微距 – Kling 4.0"></a>

**提示词:**

```text
A single droplet of water falls into a still black pool and the surface answers it.Shot 1 — 0.0s to 6.0s — ECU macro, eye level with the waterline, locked-off. At 0.0s the frame holds a still black water surface across the lower third, its meniscus drawn as one bright curve against a matte grey background. A single droplet hangs in the upper frame, out of focus, then falls. At 1.4s it strikes the surface and the impact throws a crown of water upward in real time, crisp-edged rather than blurred; the crown collapses inward on itself by 2.4s and a rebound droplet rises out of the collapse, hangs briefly at 2.6s, and falls back at 4.1s. Ripples run outward and reach the frame edge at 5.4s, and the surface settles into stillness indistinguishable from frame one.

Camera law: 100mm macro at minimum focus distance, locked-off, no camera move; the plane of focus sits exactly on the meniscus and depth of field is razor thin; 1/2000s shutter so droplet edges stay crisp through the fastest motion. Anti-default: a defocused beaker rim occupies the left fifteen percent of the frame, close to the lens, and is never racked away.Grade and audio: cool-daylight palette — black, steel-blue, one white specular — contrast low-key deep shadow. Key light is a single soft source directly above the pool, halation blooming on the specular highlight. Room tone as the bed under five diegetic events — surface tension snapping, impact into the pool, crown collapse, the rebound droplet returning, ripples sheeting across still water.Constraints: Count of cuts: zero. Count of droplets: one. Count of people in frame: zero. No music, no score, no bgm. No subtitles.
```

- **[🎬 查看「电影感」全部 32 条](prompts/cinematic_zh-CN.md)**
- **[🥊 查看「动作与追逐」全部 28 条](prompts/action_zh-CN.md)**
- **[💬 查看「对白与剧情」全部 16 条](prompts/dialogue_zh-CN.md)**
- **[🐉 查看「奇幻与科幻」全部 21 条](prompts/fantasy-scifi_zh-CN.md)**
- **[🧸 查看「动画」全部 14 条](prompts/animation_zh-CN.md)**
- **[🤳 查看「Vlog 与 UGC」全部 8 条](prompts/vlog-ugc_zh-CN.md)**
- **[👟 查看「产品与广告」全部 8 条](prompts/product_zh-CN.md)**
- **[🔁 查看「参考视频编辑」全部 6 条](prompts/reference-edit_zh-CN.md)**

<a id="faq"></a>
## ❓ 常见问题

<details>
<summary><b>这些 Kling 4.0 提示词可以免费用吗？</b></summary>

可以复制、修改和运行。提示词和视频归卡片标注的创作者所有，商用视频前请先看原帖说明。

</details>

<details>
<summary><b>Kling 4.0 视频最长多久？</b></summary>

3 到 30 秒，720p 或 1080p，每段都带声音。

</details>

<details>
<summary><b>Kling 4.0 支持哪些画幅？</b></summary>

16:9、9:16、1:1、21:9，或 adaptive（有参考图时跟随参考图）。

</details>

<details>
<summary><b>能用参考图和参考视频吗？</b></summary>

可以：最多 10 张参考图用于角色、商品或场景，最多 5 段参考视频（合计 3–30 秒）用于动作、运镜或编辑。带参考视频的任务按参考视频价计费。

</details>

<details>
<summary><b>提示词最长多少字？</b></summary>

APIKO 上最多 8000 字符。台词、声音和运镜都写在提示词里。

</details>

<details>
<summary><b>提示词用什么语言写？</b></summary>

提示词保留作者原文，多数是英文，也有日文和韩文。台词可以用和提示词其他部分不同的语言。

</details>

<details>
<summary><b>为什么我生成的和示例不一样？</b></summary>

每次生成结果都不同，作者也可能用了参考图、1080p、Kling 4.0 Flash 或其他应用。一次只改一处细节来对比。

</details>

<details>
<summary><b>怎么通过 API 运行提示词？</b></summary>

向 /v1/videos 发 POST，model 填 kling-4.0，prompt 填提示词，轮询任务后下载视频。API 文档列出了全部字段。

</details>


<a id="related"></a>
## 🔗 相关链接

- [Kling 4.0 提示词 · apiko.app](https://apiko.app/zh/kling-4-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [试用 Kling 4.0](https://apiko.app/zh/models/kling-4.0?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Kling 4.0 API 文档](https://apiko.app/zh/docs/api-manual/video-series/kling/kling-4.0?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Seedance 2.5 提示词](https://apiko.app/zh/seedance-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Wan 3.0 提示词](https://apiko.app/zh/wan-3-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Seedance 2.5](https://apiko.app/zh/models/seedance-2.5?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [APIKO API 代码示例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示词合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_zh-CN.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_zh-CN.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-CN.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-CN.md)

<a id="license"></a>
## 📄 许可与出处

提示词和视频归每张卡片标注的创作者所有，卡片可跳转到 X 上的原帖。标题、简介、译文和生成脚本采用 [CC BY 4.0](LICENSE) 许可。

如果这份合集帮你省了时间，点个 ⭐ 能让更多人看到。
