<div align="center">

<a href="https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-kling-4.0-prompts"><img src="assets/banner.jpg" alt="Awesome Kling 4.0 Prompts" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-133_cases-111111)](README.md#menu)
[![Try Kling 4.0 on APIKO](https://img.shields.io/badge/Try_Kling_4.0-on_APIKO-4F46E5)](https://apiko.app/models/kling-4.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-kling-4.0-prompts&utm_content=model_try)
[![Kling 4.0 API docs](https://img.shields.io/badge/Kling_4.0-API_docs-111111)](https://apiko.app/docs/api-manual/video-series/kling/kling-4.0?utm_source=github&utm_medium=badge&utm_campaign=awesome-kling-4.0-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Current-111111)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome Kling 4.0 Prompts

<a id="introduction"></a>
## 🌟 Introduction

**Kling 4.0 prompts: 133 copyable video prompts with the clips they made, from one-take action and dialogue scenes to reference-image ads and video edits.**

Every prompt sits next to the clip it produced. Copy it, or open it on the model page with the duration and aspect already set.

Search and filter them on [apiko.app/kling-4-0-prompts](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-kling-4.0-prompts&utm_content=intro).

> [!NOTE]
> Each prompt is kept exactly as its author posted it, so most are in English; titles and descriptions are ours. Every case credits the author and links to the original post.

<a id="quick-start"></a>
## 🚀 Quick start

**In the browser:** every case has a **Run on APIKO** link. It opens the example on [apiko.app](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-kling-4.0-prompts&utm_content=browser); press **Use** there to load the prompt into the Kling 4.0 playground.

**With the API:** create an [APIKO API key](https://apiko.app/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-kling-4.0-prompts&utm_content=api_key), then create a task and poll it until the video is ready.

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

Endpoints: `POST https://api.apiko.app/v1/videos` (create a task) · `GET https://api.apiko.app/v1/videos/{id}` (read the status and result)

<a id="how-to-write"></a>
## ✍️ How to write a Kling 4.0 prompt

Four structures that recur in the prompts on this page.

- **Timed shots** · `Shot 1 (0–5 s): framing + action. Shot 2 (5–10 s): …` — Longer clips list each shot with its time range, framing and one action, which keeps the order and pacing under control for up to 30 seconds.
- **Spoken lines** · `[Name, voice and accent]: "exact line"` — Dialogue prompts name the speaker and the voice before each quoted line, so Kling 4.0 assigns the right voice and syncs the lips.
- **One continuous take** · `One continuous shot, no cuts + camera path + what happens on the way` — Action and vlog prompts often forbid cuts outright and describe the camera as a person or rig moving through the scene.
- **Lock what comes from a reference** · `Image 1 = who. Keep: face, hair, outfit. Change: scene, action.` — Reference prompts say which picture defines the character or product and what must not change, then describe everything else.

**What the examples show**

- **Write the sound too.** Kling 4.0 always generates audio, and the stronger prompts say what is heard: music, ambience, a door, a single line of dialogue.
- **Ban what you do not want.** The phone-video prompts exclude subtitles, music and cinematic grading so the clip reads as an unedited recording.
- **Keep a base clip for edits.** The reference-edit cards start from one park scene and change only the dog, the season or the cast, with everything else held.
- **Short prompts still work.** A one-line request for multi-shot drifting or a one-sentence Halloween story gave usable clips; detail mainly adds control.
- **Stay under 8,000 characters.** That is the prompt limit of kling-4.0 on APIKO. Very long prompts posted elsewhere were left out because Use would reject them.

<a id="menu"></a>
## 📑 Menu

- [⭐ Featured](#featured) (6)
- [🎬 Cinematic](prompts/cinematic.md) (32) — Single scenes built around one camera move, one light and one strange event.
- [🥊 Action and chases](prompts/action.md) (28) — Fights, parkour, car chases and stunts, often planned shot by shot.
- [💬 Dialogue and drama](prompts/dialogue.md) (16) — People talking: lines in quotes, accents, pauses and lip sync.
- [🐉 Fantasy and sci-fi](prompts/fantasy-scifi.md) (21) — Alien worlds, creatures, gods and dragons at large scale.
- [🧸 Animation](prompts/animation.md) (14) — 3D cartoon, anime, claymation, painterly 2.5D and kinetic type.
- [🤳 Vlogs and UGC](prompts/vlog-ugc.md) (8) — Phone selfies and casual clips meant to pass as real footage.
- [👟 Products and ads](prompts/product.md) (8) — Commercial spots where the product or the room has to stay exact.
- [🔁 Reference video edits](prompts/reference-edit.md) (6) — One base clip changed by later prompts: swap an animal, the season or add a person.
- [❓ FAQ](#faq)
- [🔗 Related](#related)

<a id="featured"></a>
## ⭐ Featured

<a id="cinematic-08"></a>
### 7. Following a golden eagle over the steppe

by [@minchoi](https://x.com/minchoi) · 30s · 16:9 · **[▶ Run on APIKO](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08)** · [Original post](https://x.com/minchoi/status/2104742876584218720)

<a href="https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-08.webp" width="560" alt="Following a golden eagle over the steppe – Kling 4.0"></a>

**Prompt:**

```text
"Third-person chase shot from directly behind and slightly above a golden eagle as it flies over vast mountainous steppe. The camera follows at a fixed distance of a few metres, locked steady on the eagle, with smooth forward motion and no jitter. The whole bird stays in the lower centre of the frame with its full wingspan inside the frame and clear space on both sides. First it beats its wings powerfully, feathers flexing at the tips, then it spreads them wide and glides. Below and ahead, the landscape rushes toward the camera: winding rivers, open valleys, rocky peaks, with strong parallax. Bright late-afternoon sun from ahead, crisp air, a gentle rim light on its feathers, subtle lens flare. Realistic flight physics, motion blur from speed only, one continuous shot with no cuts."
```

<a id="fantasy-scifi-21"></a>
### 95. Long-necked alien giants wade a lagoon

by [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 15s · 16:9 · **[▶ Run on APIKO](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21)** · [Original post](https://x.com/Alin_Reaper05/status/2110982744247353611)

<a href="https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/fantasy-scifi-21.webp" width="560" alt="Long-necked alien giants wade a lagoon – Kling 4.0"></a>

**Prompt:**

```text
Two enormous long-necked alien animals slowly walk through a shallow turquoise lagoon surrounded by bright red grass and exotic palm forests. Their massive bodies create realistic waves and splashes with every step while smaller creatures flee along the shoreline. The camera begins low near the water and smoothly cranes upward, revealing the gigantic animals against a glowing yellow-green sky and distant mountains. Realistic weight and inertia, detailed skin movement, volumetric mist, natural vegetation motion, cinematic alien wildlife documentary, smooth continuous camera movement, highly coherent anatomy.
```

<a id="cinematic-26"></a>
### 25. A waterfall pours out of an ink-wash scroll

by [@opener_ai](https://x.com/opener_ai) · 10s · 9:16 · **[▶ Run on APIKO](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26)** · [Original post](https://x.com/opener_ai/status/2111666343447818617)

<a href="https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-26.webp" width="320" alt="A waterfall pours out of an ink-wash scroll – Kling 4.0"></a>

**Prompt:**

```text
A tall Korean ink-wash landscape scroll hangs against a warm plaster wall in a quiet hanok alcove. Painted misty mountains and a black pine surround one narrow painted waterfall. A shallow celadon basin rests directly below the scroll, already visible from the opening frame. The opening second reveals the striking ink waterfall gleaming faintly like liquid. Over the next three seconds only the waterfall's lower end gradually becomes a small continuous stream of real clear water, crossing the paper's lower edge and falling into the basin. For the remaining six seconds that stream keeps flowing from the same painted waterfall, producing contact splashes and expanding ripples; the basin's water level rises slightly without overflowing. The deliberate fantasy is only the painted waterfall producing real water: mountains, pine, paper borders and wall remain still and dry. Static full view of scroll and basin, warm side lighting, exquisite ink texture and glossy celadon, one continuous ten-second shot. No cuts, new objects or captions.
```

<a id="action-05"></a>
### 37. Six-shot spy chase through a night market

by [@minchoi](https://x.com/minchoi) · 15s · 16:9 · **[▶ Run on APIKO](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05)** · [Original post](https://x.com/minchoi/status/2104743085087560174)

<a href="https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/action-05.webp" width="560" alt="Six-shot spy chase through a night market – Kling 4.0"></a>

**Prompt:**

```text
"Multi-shot spy-thriller chase through a night market, 15 seconds, 6 shots with hard cuts, fast and relentless. [Cole]: early 30s, short dark-brown hair, clean-shaven, tailored charcoal suit, white shirt open at the collar, no tie. [Anton]: late 30s, ash-blond buzz cut, short blond beard, black leather jacket, dark grey henley. A packed night-market lane after rain: food stalls, red paper lanterns, string lights, grill smoke, steam, wet pavement reflecting the lights. Anton always runs toward frame right; Cole chases him. Shot 1 (0–2s): Telephoto close-up of Cole standing still in the moving crowd, shoppers blurring past in the foreground, eyes locked on something off-screen right. Shot 2 (2–4.5s): The camera whip-pans right along his eyeline and snaps sharp onto Anton under a red stall sign reading "DUMPLINGS". Anton sees Cole, drops his paper cup and bolts right. Shot 3 (4.5–7s): Fast side tracking shot racing alongside at full sprint, both men running frame right: Anton shoving shoppers aside, Cole ten metres behind and closing, string lights streaking past. Shot 4 (7–9.5s): Low angle: Anton yanks a stack of fruit crates down behind him and oranges spill across the wet ground; Cole leaps the crates in one stride, suit jacket flaring, lands hard and keeps running. Shot 5 (9.5–12.5s): Cole bursts into a crossroads of lanes beneath a stall sign reading "HOT TEA" and stops dead, breathing hard. Anton is gone. The camera orbits slowly halfway around Cole, circling past his left side to end over his shoulder, as he scans the crowd. Shot 6 (12.5–15s): Close on Cole. His eyes snap left and the camera whip-pans left, landing sharp on Anton climbing a metal stairway above the stalls, glancing back. Cole sprints out of frame after him. Gritty handheld spy-thriller look, anamorphic, shallow depth of field, teal shadows with warm amber lantern light, motion blur from speed only. No dialogue: pounding footsteps, crates crashing, oranges rolling, sizzling grills, crowd gasps, a pulsing percussion score with low brass stabs."
```

<a id="animation-12"></a>
### 109. A clay ghost learns to say boo

by [@JasonHeatony7](https://x.com/JasonHeatony7) · 15s · 9:16 · **[▶ Run on APIKO](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12)** · [Original post](https://x.com/JasonHeatony7/status/2115812533533581757)

<a href="https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/animation-12.webp" width="320" alt="A clay ghost learns to say boo – Kling 4.0"></a>

**Prompt:**

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
### 28. One water droplet in macro

by [@sebatheepan](https://x.com/sebatheepan) · 15s · 9:16 · **[▶ Run on APIKO](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29)** · [Original post](https://x.com/sebatheepan/status/2113038301154164960)

<a href="https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29"><img src="https://media.apiko.app/prompts/kling-4-0-prompts/cinematic-29.webp" width="320" alt="One water droplet in macro – Kling 4.0"></a>

**Prompt:**

```text
A single droplet of water falls into a still black pool and the surface answers it.Shot 1 — 0.0s to 6.0s — ECU macro, eye level with the waterline, locked-off. At 0.0s the frame holds a still black water surface across the lower third, its meniscus drawn as one bright curve against a matte grey background. A single droplet hangs in the upper frame, out of focus, then falls. At 1.4s it strikes the surface and the impact throws a crown of water upward in real time, crisp-edged rather than blurred; the crown collapses inward on itself by 2.4s and a rebound droplet rises out of the collapse, hangs briefly at 2.6s, and falls back at 4.1s. Ripples run outward and reach the frame edge at 5.4s, and the surface settles into stillness indistinguishable from frame one.

Camera law: 100mm macro at minimum focus distance, locked-off, no camera move; the plane of focus sits exactly on the meniscus and depth of field is razor thin; 1/2000s shutter so droplet edges stay crisp through the fastest motion. Anti-default: a defocused beaker rim occupies the left fifteen percent of the frame, close to the lens, and is never racked away.Grade and audio: cool-daylight palette — black, steel-blue, one white specular — contrast low-key deep shadow. Key light is a single soft source directly above the pool, halation blooming on the specular highlight. Room tone as the bed under five diegetic events — surface tension snapping, impact into the pool, crown collapse, the rebound droplet returning, ripples sheeting across still water.Constraints: Count of cuts: zero. Count of droplets: one. Count of people in frame: zero. No music, no score, no bgm. No subtitles.
```

- **[🎬 All 32 Cinematic cases](prompts/cinematic.md)**
- **[🥊 All 28 Action and chases cases](prompts/action.md)**
- **[💬 All 16 Dialogue and drama cases](prompts/dialogue.md)**
- **[🐉 All 21 Fantasy and sci-fi cases](prompts/fantasy-scifi.md)**
- **[🧸 All 14 Animation cases](prompts/animation.md)**
- **[🤳 All 8 Vlogs and UGC cases](prompts/vlog-ugc.md)**
- **[👟 All 8 Products and ads cases](prompts/product.md)**
- **[🔁 All 6 Reference video edits cases](prompts/reference-edit.md)**

<a id="faq"></a>
## ❓ FAQ

<details>
<summary><b>Are these Kling 4.0 prompts free to use?</b></summary>

Copy, edit and run any of them. The prompts and videos belong to the creators credited on each card, so check the original post before reusing a clip commercially.

</details>

<details>
<summary><b>How long can a Kling 4.0 video be?</b></summary>

3 to 30 seconds, at 720p or 1080p. Sound is generated with every clip.

</details>

<details>
<summary><b>Which aspect ratios does Kling 4.0 support?</b></summary>

16:9, 9:16, 1:1 and 21:9, or adaptive, which follows the reference image when there is one.

</details>

<details>
<summary><b>Can I use reference images and videos?</b></summary>

Yes: up to 10 reference images for characters, products or scenes, and up to 5 reference videos (3–30 s in total) for motion, camera or editing. A task with a reference video is billed at the reference-video rate.

</details>

<details>
<summary><b>How long can a prompt be?</b></summary>

Up to 8,000 characters on APIKO. Dialogue, sound and camera directions all go in the prompt.

</details>

<details>
<summary><b>Which language should I write prompts in?</b></summary>

The prompts keep the author's language, mostly English with some Japanese and Korean. Spoken lines can be in another language from the rest of the prompt.

</details>

<details>
<summary><b>Why does my clip differ from the example?</b></summary>

Each run gives a different result, and authors may have used reference images, 1080p, Kling 4.0 Flash or another app. Change one detail at a time to compare.

</details>

<details>
<summary><b>How do I run a prompt through the API?</b></summary>

POST it as prompt to /v1/videos with model kling-4.0, poll the task, then download the video. The API docs list every field.

</details>


<a id="related"></a>
## 🔗 Related

- [Kling 4.0 Prompts · apiko.app](https://apiko.app/kling-4-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Run Kling 4.0](https://apiko.app/models/kling-4.0?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Kling 4.0 API docs](https://apiko.app/docs/api-manual/video-series/kling/kling-4.0?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Seedance 2.5 prompts](https://apiko.app/seedance-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Wan 3.0 prompts](https://apiko.app/wan-3-0-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Seedance 2.5](https://apiko.app/models/seedance-2.5?utm_source=github&utm_medium=related&utm_campaign=awesome-kling-4.0-prompts)
- [Code examples for the APIKO API](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**More prompt collections**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts)

<a id="license"></a>
## 📄 License and credits

Prompts and result videos belong to the creators credited on each card, which links to the original post on X. Titles, descriptions, translations and the build scripts are released under [CC BY 4.0](LICENSE).

If this list saves you time, a ⭐ helps others find it.
