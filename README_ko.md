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

프롬프트마다 그 프롬프트로 만든 클립이 옆에 있습니다. 복사하거나, 길이와 화면 비율이 맞춰진 채로 모델 페이지에서 여세요. 결과 영상은 모두 GitHub에서 바로 재생됩니다.

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

- [🎬 시네마틱](#cinematic) (32)
  - [지하 신전의 최면에 걸린 무사들](#cinematic-01)
  - [서리 내린 밤 숲을 달리는 스케이트보드](#cinematic-02)
  - [도시가 질주하는 동안 멈춰 선 한 사람](#cinematic-03)
  - [휴대폰으로 찍은 듯한 고양이 피자 배달](#cinematic-04)
  - [TV 생중계처럼 찍은 스타디움 콘서트](#cinematic-05)
  - [30초 초자연 스릴러 예고편](#cinematic-06)
  - [초원 위를 나는 검독수리 추적샷](#cinematic-08)
  - [빨간 장미를 들고 벤치에서 기다리기](#cinematic-09)
  - [비 내리는 골목의 4컷 호러](#cinematic-10)
  - [흔들리는 전구 아래 지하실로](#cinematic-11)
  - [절벽에서 뛰어 구름 위를 나는 장면](#cinematic-12)
  - [노을 진 옥상의 탭댄스](#cinematic-13)
  - [해 질 녘 블랙우드 숲을 달리는 여성](#cinematic-14)
  - [보트 옆 혹등고래 점프, 두 시점](#cinematic-15)
  - [고양이의 한밤 모험을 따라가는 핸드헬드](#cinematic-16)
  - [종탑 위 박쥐 떼가 만드는 글자](#cinematic-17)
  - [식당 근무를 마치고 귀가하는 루시](#cinematic-18)
  - [갑옷 사냥꾼의 함바그 요리](#cinematic-19)
  - [항구에서 유령이 되는 빅토리아 시대 여인](#cinematic-20)
  - [1981년 슬래셔 풍 안개 숲 추격](#cinematic-21)
  - [프롬프트 하나로 만든 VFX 전후 비교](#cinematic-22)
  - [3컷 스토리보드로 만든 햄스터 록스타](#cinematic-23)
  - [야생 다큐처럼 찍은 고양이와 로봇청소기](#cinematic-24)
  - [로봇청소기 탄 고양이, 두 개의 카메라](#cinematic-25)
  - [수묵화 족자에서 쏟아지는 폭포](#cinematic-26)
  - [콘크리트 방파제를 덮치는 폭풍 해일](#cinematic-27)
  - [해 질 녘 갠트리 크레인 컨테이너 추적](#cinematic-28)
  - [검은 수면에 떨어지는 물방울 매크로](#cinematic-29)
  - [셔터가 내려가기 전 마지막 배달](#cinematic-30)
  - [바위 해안을 따라가는 보트 추적샷](#cinematic-31)
  - [밤거리 위로 떠오르는 금 간 바이올린](#cinematic-32)
  - [해안 도시로 떨어지는 달](#cinematic-33)
- [🥊 액션과 추격](#action) (28)
  - [불꽃이 남는 두 장면 초능력 격투](#action-01)
  - [복면 특수부대의 원테이크 야간 급습](#action-02)
  - [7개 샷으로 엮은 파우더 스키 영상](#action-03)
  - [한 문장으로 만든 멀티샷 드리프트](#action-04)
  - [6개 샷 야시장 스파이 추격](#action-05)
  - [스케이트파크 30초 로우 트래킹](#action-06)
  - [홀로 성문을 지키는 기사](#action-07)
  - [아파트 세 공간을 관통하는 맨손 격투](#action-08)
  - [추락하며 코드로 흩어지는 사이버 암살자](#action-09)
  - [70년대 서부극 살롱 난투](#action-10)
  - [JSON으로 쓴 창고 격투](#action-11)
  - [네온 야시장 파쿠르 탈출](#action-12)
  - [위에서 본 나선계단 칼싸움](#action-13)
  - [달리는 지하철 안 격투](#action-14)
  - [SUV가 머리 위로 넘어가도 꿈쩍 않는 남자](#action-15)
  - [은행 강도를 막는 청소부](#action-16)
  - [절벽 사찰 테라스의 쿵푸 대결](#action-17)
  - [도쿄 옥상 8컷 파쿠르](#action-18)
  - [사무라이 사극 예고편](#action-19)
  - [네온 우주항 1인칭 외계인 슈터](#action-20)
  - [몬순 폭우 속 슈퍼히어로 추격](#action-21)
  - [첫 프레임에서 시작하는 카체이스](#action-22)
  - [폐허 도시 프리러닝](#action-23)
  - [사막의 복면 전사 결투](#action-24)
  - [1차 대전 복엽기 공중전](#action-25)
  - [1950년대 흑백 경찰 추격](#action-26)
  - [핸드헬드로 찍은 창고 스턴트 격투](#action-27)
  - [바위 해안의 연쇄 폭발](#action-28)
- [💬 대화와 드라마](#dialogue) (16)
  - [카페에서 빵집 이야기를 나누는 두 친구](#dialogue-01)
  - [스토리보드로 만든 사교클럽의 밤](#dialogue-02)
  - [막배 위의 사랑 고백](#dialogue-03)
  - [머그컵이 끝까지 남는 부엌 대화](#dialogue-04)
  - [우연히 미슐랭이 된 요리 시험](#dialogue-05)
  - [남편의 늦은 밤 부엌 고백](#dialogue-06)
  - [겨울 강변길의 이별](#dialogue-07)
  - [다섯 장면 30초 일본 로맨스](#dialogue-08)
  - [바로크 홀에서의 입맞춤](#dialogue-10)
  - [크리스마스 파티 드레스코드 소동](#dialogue-11)
  - [1950년대 가족과 업데이트 중인 로봇](#dialogue-12)
  - [도서관에서 대화하는 여우와 부엉이](#dialogue-13)
  - [미래 토크쇼의 안드로이드 게스트](#dialogue-14)
  - [브르타뉴 절벽길 산책 대화](#dialogue-15)
  - [조용한 해변의 절제된 대화](#dialogue-16)
  - [왕자와 숲 마녀의 저주받은 종](#dialogue-17)
- [🐉 판타지와 SF](#fantasy-scifi) (21)
  - [시골 침실의 작은 구름 요정](#fantasy-scifi-01)
  - [전장에서 깨어나는 뇌제](#fantasy-scifi-02)
  - [밤 옥상 위에 떠오르는 빛의 도형](#fantasy-scifi-05)
  - [캠코더로 찍은 도시 크기의 괴수](#fantasy-scifi-06)
  - [작은 불의 정령을 부르는 연금술사](#fantasy-scifi-07)
  - [공성 전의 성문 파괴자](#fantasy-scifi-08)
  - [창백한 용의 무덤에 들어선 기사](#fantasy-scifi-09)
  - [살아 있는 외계 터미널 1인칭 산책](#fantasy-scifi-10)
  - [실험실에서 깨어나는 안드로이드](#fantasy-scifi-11)
  - [거대한 손이 마을로 던지는 바위](#fantasy-scifi-12)
  - [폭풍 만에서 솟아오르는 괴물](#fantasy-scifi-13)
  - [빙원을 건너 외계 유적으로 가는 탐사대](#fantasy-scifi-14)
  - [거대한 외계 고리 아래의 전투](#fantasy-scifi-15)
  - [정글을 누비는 기계 포식자](#fantasy-scifi-16)
  - [해 뜰 무렵 깨어나는 구형 외계 마을](#fantasy-scifi-17)
  - [소환된 괴수를 향해 달리는 거대 사자](#fantasy-scifi-18)
  - [대전된 성운을 통과하는 우주선](#fantasy-scifi-19)
  - [육족 짐승 무리 곁을 걷는 탐험가](#fantasy-scifi-20)
  - [석호를 건너는 긴 목의 외계 거수](#fantasy-scifi-21)
  - [붐비는 외계 시장 산책](#fantasy-scifi-22)
  - [두 개의 태양 아래 첫 접촉](#fantasy-scifi-23)
- [🧸 애니메이션](#animation) (14)
  - [엄마를 위해 생일 케이크를 굽는 아들](#animation-01)
  - [셰이커 네 개를 다루는 문어 바텐더](#animation-02)
  - [두 애니 캐릭터의 옥상 파쿠르](#animation-03)
  - [「절대 누르지 마」 3D 키네틱 타이포](#animation-04)
  - [햇살 가득한 만화 숲의 요정](#animation-05)
  - [코드 같은 프롬프트로 만든 추상 영상](#animation-06)
  - [백발 여전사의 하늘 전투](#animation-07)
  - [사무실에서 커피 마시려는 뱀](#animation-08)
  - [90년대 애니 풍 거리의 만남](#animation-09)
  - [페인터리 2.5D 드래곤과 기수](#animation-10)
  - [핼러윈 밤에 열리는 그림 같은 문](#animation-11)
  - [「부」를 배우는 점토 유령](#animation-12)
  - [분홍 머리 꼬마 마녀와 불꽃 정령](#animation-13)
  - [한 문장으로 만든 소녀의 핼러윈 비밀](#animation-14)
- [🤳 브이로그와 UGC](#vlog-ugc) (8)
  - [브런치 셀카 영상, 원테이크](#vlog-ugc-01)
  - [노을 해변 셀카 브이로그](#vlog-ugc-02)
  - [남자친구 시점의 여름 산책](#vlog-ugc-04)
  - [도시를 걷는 고양이 브이로거](#vlog-ugc-05)
  - [주차된 차 안에서 찍은 고백](#vlog-ugc-06)
  - [공항 게이트 셀카 영상](#vlog-ugc-07)
  - [길을 걸으며 찍는 셀카 브이로그](#vlog-ugc-08)
  - [2010년대 감성 옷가게 라이브](#vlog-ugc-09)
- [👟 제품과 광고](#product) (8)
  - [로켓처럼 루프를 도는 향수병](#product-01)
  - [럭셔리 나이트 크림 ASMR 광고](#product-02)
  - [럭셔리 거실 멀티샷 광고](#product-03)
  - [애니 풍 프렌치토스트 광고](#product-04)
  - [자작나무 탄산수 광고](#product-05)
  - [냉장고에서 파티까지 원테이크](#product-06)
  - [제품은 고정, 배경만 휩팬](#product-08)
  - [손이 캔을 들고 장면을 넘나들기](#product-09)
- [🔁 참고 영상 편집](#reference-edit) (6)
  - [참고 영상 음악에 맞춰 춤추게 하기](#reference-edit-01)
  - [기본 클립: 두 친구, 개, 공](#reference-edit-02)
  - [편집: 여우, 가을, 플란넬 셔츠](#reference-edit-03)
  - [편집: 개를 공룡으로](#reference-edit-04)
  - [편집: 벤치에 친구 한 명 추가](#reference-edit-05)
  - [편집: 여름을 가을로](#reference-edit-06)
- [❓ 자주 묻는 질문](#faq)
- [🔗 관련 링크](#related)

<a id="cinematic"></a>
## 🎬 시네마틱

> 카메라 움직임 하나, 빛 하나, 이상한 사건 하나로 만든 단일 장면. · 32개

<a id="cinematic-01"></a>
### 1. 지하 신전의 최면에 걸린 무사들

작성자 [@itxsarmadd](https://x.com/itxsarmadd) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-01#cinematic-01)** · [원본 게시물](https://x.com/itxsarmadd/status/2108520829604745408)

https://github.com/user-attachments/assets/ff9924a9-4be6-436e-8936-73f71609a756

**프롬프트:**

```text
DURATION: EXACTLY 10 SECONDS
ASPECT RATIO: 16:9
STYLE: Premium Hollywood live-action psychological horror, ultra-photorealistic humans, grounded CGI, realistic physics, elegant Japanese dark fantasy, desaturated cinematic photography. No anime rendering.

ENVIRONMENT
Vast abandoned underground Japanese temple. Aged wooden pillars, black stone flooring, shallow reflective water, old oil lanterns, faint moonlight and floor-level mist. Deep architectural layers create oppressive atmosphere and strong spatial depth.

LIGHTING / COLOR
Cold blue-gray moonlight, restrained amber lanterns, detailed shadows, subtle haze, realistic reflections, natural skin tones. Desaturated charcoal, black, gray, and weathered wood. No neon.

ACEN
Calm, composed, elegant, intimidating. Natural human performance. Zanpakutō remains physically consistent.

CORE CONCEPT
Kyōka Suigetsu manifests gradually:

EMPTY SPACE → SUBTLE DISTORTION → TRANSPARENT ACEN → INCREASING DENSITY → FULLY REALISTIC ACEN.

Approximately 12–14 manifestations emerge asynchronously across different depths and positions, never in formations. No instant appearance, teleportation, holograms or pop-in. Each has subtle, independent human movements.

ACTION / CAMERA

0.0–1.5s — ACTIVATION
Medium-wide shot. Camera slowly arcs around Acen as he draws his Zanpakutō. Cold light catches the blade. He quietly says “Kudakero, Kyōka Suigetsu.” Metallic blade sound and distant ambience only. No aura or explosion.

1.5–3.0s — FIRST MANIFESTATIONS
Camera continues moving. Empty space behind a pillar subtly distorts, gradually forming a transparent Acen. Three more emerge independently near a wall pillar, and water. Background remains visible through them. Subtle blinking and head movements.

3.0–5.0s — THE ROOM BEGINS TO FILL
Lateral tracking reveals additional Acens behind pillars and near the water. Some are faint, others 50–70% opaque and one nearly solid. Natural breathing, posture adjustments, and subtle sword-grip movements. No synchronization.

5.0–7.0s — COMPLETE HYPNOSIS ESCALATES
Camera passes foreground architecture, revealing 9–11 scattered manifestations across different depths. Some are partially hidden or visible through reflections. Skin, fabric, shadows, reflections and mist gradually respond like real physical bodies.

7.0–8.8s — REALITY BECOMES UNTRUSTWORTHY
Passing another pillar reveals 12–14 Acens throughout the sanctuary.Some are solid, some translucent others obscured. Every manifestation develops gradually from empty space. No attacks or theatrical reactions.

8.8–10.0s — FINAL REVEAL
Camera passes a final pillar, revealing a fully solid Acen close to the lens. No glow or distortion.He calmly looks toward the camera with a faint smile. Numerous manifestations remain scattered behind him in different states of solidity.The original is indistinguishable.CUT TO BLACK.

CAMERA LANGUAGE
Continuous lateral tracking with a subtle orbital arc. Use pillars darkness, and parallax to reveal manifestations naturally. Maintain spatial depth. No frantic handheld random shake, or unnecessary cuts.

VFX / PHYSICS:Grounded CGI, realistic human integration, progressive solidity, consistent shadows and reflections natural fabric movement, mist displacement and water interaction. No holograms, glowing edges particles, dissolves or teleportation.

PERFORMANCEAcen remains unnervingly calm. No screaming, exaggerated expressions, attacks, or unnecessary sword choreography. Horror comes from numerous realistic versions occupying the sanctuary.

NEGATIVE: Anime, cartoon, videogame render plastic skin, holograms, clone formations synchronized movements, static mannequins, instant materialization teleportation, magical explosions, neon, distorted anatomy duplicated limbs, floating sword inconsistent reflections or shadows rubber physics excessive camera shake chaotic editing cheap horror oversaturated colors.
```

<a id="cinematic-02"></a>
### 2. 서리 내린 밤 숲을 달리는 스케이트보드

작성자 [@MahiraEhan](https://x.com/MahiraEhan) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-02#cinematic-02)** · [원본 게시물](https://x.com/MahiraEhan/status/2114671326413701226)

https://github.com/user-attachments/assets/4c4a574e-4459-4de2-a39a-fc07a8036250

**프롬프트:**

```text
Nighttime medium shot of a girl skateboarding swiftly through a dark, cold forest, her breath visible in the frosty air. The camera follows close behind, capturing her focused expression as she sings softly and sorrowfully, "Am I dead? Am I dreaming? I can't feel anything—I can't feel a thing." Pale moonlight filters through bare branches, casting cool blue shadows. She comes to a gentle stop on a leaf-strewn path, picks up her skateboard, and steps deeper into the dense woods. She whispers, "I must remain unseen," as the camera slowly dollies forward, enhancing the eerie, quiet ambiance. Audio: raw on-set sound only — natural dialogue, ambient room tone, and diegetic sound effects.
```

<a id="cinematic-03"></a>
### 3. 도시가 질주하는 동안 멈춰 선 한 사람

작성자 [@AIwithSynthia](https://x.com/AIwithSynthia) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-03#cinematic-03)** · [원본 게시물](https://x.com/AIwithSynthia/status/2113237971449348351)

https://github.com/user-attachments/assets/6f6e233d-e1a8-4dbd-904a-2177bca108b6

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Create a hyper-realistic cinematic time-lapse featuring the woman as the central subject, standing completely motionless in her original pose.

Keep her face, hairstyle, clothing, body position, and facial expression perfectly unchanged throughout the entire video, as if she is frozen in time.

Animate only the surrounding environment, with crowds walking rapidly in different directions, people passing behind and in front of her, and vehicles moving quickly through the background.

Gradually increase the speed of the surrounding activity, creating dramatic time-lapse motion with realistic directional blur and flowing movement trails.

Allow natural shadows, sunlight, and background activity to shift subtly, emphasizing the passage of time while the woman remains perfectly still and sharply focused.

Maintain realistic depth, natural movement, consistent scene geometry, and strong contrast between the frozen subject and the fast-moving environment.

The camera must remain completely fixed on a tripod, with no panning, tilting, zooming, or camera shake.

Toward the end, gradually return the surrounding movement to normal speed while the woman remains frozen in precisely the same position.

Negative prompt: Subject movement, blinking, facial changes, body deformation, identity drift, camera movement, flickering, background warping, unnatural motion blur, duplicated limbs, text, logos, watermark.
```

<a id="cinematic-04"></a>
### 4. 휴대폰으로 찍은 듯한 고양이 피자 배달

작성자 [@Strength04_X](https://x.com/Strength04_X) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-04#cinematic-04)** · [원본 게시물](https://x.com/Strength04_X/status/2105889942958440671)

https://github.com/user-attachments/assets/37b5b512-7f7b-443b-869d-a96f9aebee6d

**프롬프트:**

```text
Create an exactly 20 second ultra-realistic live-action comedy video, filmed as if recorded on an iPhone 18 Pro Max. Vertical 16:9, 1080×1920, 24fps.

Everything must look like authentic real-world smartphone footage. The cat is a completely realistic domestic cat with natural fur, realistic anatomy, whiskers, eyes, paws, and believable movement.

The cat wears only a realistic pizza-company delivery jacket. No pants, shoes, hat, or other clothing.

SCENE 1 — 0.0–3.5s — PACKING THE PIZZA

Inside a realistic neighborhood pizza shop.

The cat stands at the preparation counter.

The cat physically takes the freshly prepared pizza and places it into a pizza box.

The cat then manually closes the pizza box.

The cat picks up the closed pizza box and physically places it inside the pizza delivery bag.

The cat then manually closes the delivery bag.

Every action must be clearly visible and happen in the correct order.

Pizza → pizza box → close pizza box → place box inside delivery bag → close delivery bag.

Nothing appears or disappears automatically.

SCENE 2 — 3.5–6.5s — SCOOTER AND DRIVING

The cat carries the closed delivery bag to its scooter.

The cat physically places the delivery bag onto the scooter, secures it, climbs onto the scooter, starts the engine, and rides away.

Cut to a front-facing camera angle showing the cat and scooter driving toward the camera.

The cat drives naturally through a realistic neighborhood road.

The cat's face is normal and clean during the driving sequence.

Natural iPhone handheld movement, autofocus, exposure changes, motion blur, realistic road movement, scooter engine and street ambience.

SCENE 3 — 6.5–10.0s — ARRIVING AND TAKING THE PIZZA

The cat arrives outside the customer's house.

It stops the scooter and physically puts the scooter on its stand.

The cat gets off and walks to the delivery bag.

The cat manually opens the delivery bag, reaches inside, grips the closed pizza box, and physically pulls the pizza box completely out of the bag.

The cat then closes the delivery bag.

The cat carries the pizza box toward the customer's front door.

As the cat approaches the house, clearly show a small amount of pizza sauce and a little melted cheese around its mouth, making it obvious that the cat has secretly eaten some pizza.

The pizza residue must not appear suddenly. It must remain naturally visible.

SCENE 4 — 10.0–12.0s — DOORBELL FIRST

The cat reaches the front door while holding the pizza box.

The door is completely closed.

The cat raises its paw and physically presses the doorbell.

Only after the doorbell is pressed, the customer opens the door.

Strict order:

Cat reaches closed door → cat presses doorbell → door opens.

The door must NOT open before the bell is pressed.

SCENE 5 — 12.0–14.5s — HANDING OVER THE PIZZA

After the door opens, use a camera angle facing the cat from the customer's side.

Do not show the customer's face or body. Only the cat should be visible.

The cat holds the pizza box forward and says:

Cat: "Here is your pizza."

The cat physically hands the pizza box to the customer.

The pizza box must visibly transfer from the cat's paws into the customer's hands.

The pizza residue around the cat's mouth remains clearly visible.

SCENE 6 — 14.5–17.0s — THE MISSING PIZZA

Cut to the customer's POV.

The customer is physically holding the same pizza box.

The customer manually opens the pizza box.

The cat is standing behind the open box and becomes naturally hidden by the box.

Inside the box:

- One pizza slice is missing.
- Another remaining slice has a small realistic bite taken from it.
- All other pizza remains physically present.
- Nothing disappears during the shot.

The customer looks shocked and says:

Customer: "Where is my missing slice?"

The customer manually closes the pizza box and looks toward the road.

SCENE 7 — 17.0–20.0s — ESCAPE AND FLYING KISS

The cat is already moving toward its scooter.

The cat climbs onto the scooter, starts it, and physically rides away down the road.

The customer runs out toward the road and shouts:

Customer: "Stop! Stop!"

The cat keeps riding farther away.

While actively riding away, the cat turns its head back toward the customer and raises one paw, clearly making a flying-kiss gesture directly toward the customer.

The flying kiss must happen mid-ride while the cat is moving away, not before riding away and not after stopping.

The cat then faces forward and continues riding farther down the road.

End naturally with the cat getting smaller in the distance while the customer remains on the road.

STRICT PHYSICAL CONTINUITY

Every action must happen physically and in logical order.

Nothing may appear automatically. Nothing may disappear automatically.

No teleportation, morphing, object replacement, duplicated objects, or sudden prop changes.

The exact pizza box used in the shop must remain the same pizza box throughout the entire video.

The exact delivery bag must remain the same bag throughout.

The pizza must be physically packed into the box, the box physically placed into the bag, the bag physically placed on the scooter, the box physically removed from the bag, and the box physically handed to the customer.

The door must remain closed until the cat physically presses the doorbell.

The customer must physically open and close the pizza box.

The missing pizza slice must simply not be present when the box is opened; it must not disappear during the shot.

REALISM REQUIREMENTS

- Exactly 20.0 seconds
- 9:16 vertical
- 1080×1920
- 24fps
- iPhone 18 Pro Max realistic footage
- Realistic domestic cat
- Realistic fur and anatomy
- Only pizza-company delivery jacket
- Realistic scooter physics
- Natural handheld camera movement
- Natural autofocus and exposure
- Realistic shadows and reflections
- Realistic road and house
- Natural environmental audio
- No CGI appearance
- No cartoon style
- No animation
- No exaggerated expressions
- No extra limbs
- No distorted paws
- No morphing
- No teleportation
- No automatic object movement
- No subtitles 
- No text overlays
- No watermark
```

<a id="cinematic-05"></a>
### 5. TV 생중계처럼 찍은 스타디움 콘서트

작성자 [@minchoi](https://x.com/minchoi) · 42초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-05#cinematic-05)** · [원본 게시물](https://x.com/minchoi/status/2111471577522921832)

https://github.com/user-attachments/assets/4a7af664-9a87-43f5-9add-5a72559e7eb1

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
GLOBAL: Real live concert footage filmed outdoors at an open-air stadium at night. Shot by a live TV broadcast crew on broadcast cameras with long zoom lenses. Natural, imperfect live look: 24 fps with natural motion blur, light digital grain and noise in the shadows, slightly crushed blacks, stage lights blooming and flaring, exposure shifting as the lights flash, occasional quick focus corrections, slight handheld shake. Stage lights are the only light source; haze drifts in the night wind and the wind moves the singer's hair. THE SINGER IS THE FOCUS: Nova <Character reference>; she sings into a silver wireless handheld microphone always in her right hand (no headset). She just performs the song like at a real concert: singing with emotion, natural movement, free-hand gestures, connecting with the crowd; she does not act out the lyrics. THE BAND IS NEVER SHOWN: they play from a dark riser far upstage, hidden in haze and backlight. VENUE: sold-out stadium, 60,000 fans; wide main stage with a huge LED screen showing abstract graphics, a runway into the crowd ending in a small round B-stage, photo pit and barricade; moving-head beams in magenta, teal and warm amber. CROWD: always moving with the music, never still: jumping, swaying, waving raised arms side to side, clapping on the beat, singing along, phones and lights held up and waving; packed tight at the barricade. EDIT: cut like a live concert broadcast between fixed camera positions (front-of-house long lens, photo-pit handheld, stage-side handheld, crane over the crowd, cable-cam, wide from the back of the stadium); operators zoom and reframe live, no cinematic camera tricks. SYNC: 98 BPM, one bar = 2.45 s; hard cuts only at the shot times below; her mouth follows the lyric timing exactly and stays closed in the gaps.CLIP 1 of 10 — INTRO + VERSE 1 — 28.7 seconds. A soft pulsing synth intro, then an intimate verse. She is at the front of the main stage in low, cool blue and magenta light.VOCAL TIMING (lip-sync):0.0–8.0s instrumental, no singing8.0–14.5s "I brought a list of reasons I was running late"14.8–19.4s "Then lost the list somewhere beside the gate"19.6–23.8s "You said, 'You always make an entrance somehow'"23.9–28.6s "I said, 'I'm working on the exit now'"SHOTS:0.0–5.2s SHOT 1 — High wide from the back of the stadium: a dark stage with slow neon graphics on the LED screen and beams cutting through the haze; the crowd sways and waves arms and phones side to side; the singer stands small and alone at the front of the stage in a white spotlight.5.2–10.1s SHOT 2 — Front-of-house long lens, medium shot: she sways gently to the synth pulse, lifts the mic and begins singing at 8.0s.10.1–15.0s SHOT 3 — Front-of-house long lens, close-up, with crowd hands moving in the soft foreground blur: she sings with her eyes half-closed.15.0–19.9s SHOT 4 — Photo-pit handheld, low angle looking up at her: she sings while front-row arms sway through the bottom of the frame.19.9–24.8s SHOT 5 — Handheld from the barricade looking back over the crowd: fans sing along, sway, and wave arms and phones side to side; her voice continues off-screen.24.8–28.7s SHOT 6 — Front-of-house long lens close-up with a slow live zoom-in: she sings with a small smile as the lights start to warm toward amber.

PROMPT (2nd clip): 
GLOBAL: Real live concert footage filmed outdoors at an open-air stadium at night. Shot by a live TV broadcast crew on broadcast cameras with long zoom lenses. Natural, imperfect live look: 24 fps with natural motion blur, light digital grain and noise in the shadows, slightly crushed blacks, stage lights blooming and flaring, exposure shifting as the lights flash, occasional quick focus corrections, slight handheld shake. Stage lights are the only light source; haze drifts in the night wind and the wind moves the singer's hair. THE SINGER IS THE FOCUS: Nova <Character reference>; she sings into a silver wireless handheld microphone always in her right hand (no headset). She just performs the song like at a real concert: singing with emotion, natural movement, free-hand gestures, connecting with the crowd; she does not act out the lyrics. THE BAND IS NEVER SHOWN: they play from a dark riser far upstage, hidden in haze and backlight. VENUE: sold-out stadium, 60,000 fans; wide main stage with a huge LED screen showing abstract graphics, a runway into the crowd ending in a small round B-stage, photo pit and barricade; moving-head beams in magenta, teal and warm amber. CROWD: always moving with the music, never still: jumping, swaying, waving raised arms side to side, clapping on the beat, singing along, phones and lights held up and waving; packed tight at the barricade. EDIT: cut like a live concert broadcast between fixed camera positions (front-of-house long lens, photo-pit handheld, stage-side handheld, crane over the crowd, cable-cam, wide from the back of the stadium); operators zoom and reframe live, no cinematic camera tricks. SYNC: 98 BPM, one bar = 2.45 s; hard cuts only at the shot times below; her mouth follows the lyric timing exactly and stays closed in the gaps.CLIP 2 of 10 — PRE-CHORUS 1 — 12.4 seconds. The build: the kick drum enters and the lights warm up, ending in a drum fill and a crowd roar. She stays at the front of the main stage.VOCAL TIMING (lip-sync):0.0–0.9s breath, no singing0.9–3.0s "I can turn a simple sorry"3.0–5.8s "Into three acts and a bow"5.9–8.4s "But you're looking at me kindly"8.5–11.6s "So I'll try the honest version now"11.6–12.4s drum fill and crowd cheer, no singingSHOTS:0.0–3.5s SHOT 1 — Stage-side handheld from a three-quarter front angle, with the crowd behind her: she sings as she walks slowly toward the stage edge.3.5–5.9s SHOT 2 — Wide from the back of the stadium: amber beams sweep up on the beats and the crowd starts to bounce, arms going up.5.9–8.3s SHOT 3 — Front-of-house long lens close-up: she sings straight out to the crowd.8.3–10.8s SHOT 4 — Photo-pit handheld, low angle, with a live zoom-in: she sings with feeling, her free hand open.10.8–12.4s SHOT 5 — Crane moving over the crowd toward the stage: on the drum fill the lights ramp up to white and the crowd cheers and jumps with arms raised, while she lifts her free arm.
```

<a id="cinematic-06"></a>
### 6. 30초 초자연 스릴러 예고편

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-06#cinematic-06)** · [원본 게시물](https://x.com/EndFolding79421/status/2111482327842930903)

https://github.com/user-attachments/assets/0c427874-8f3a-4eb7-b2ba-868e9c6b3c20

**프롬프트:**

```text
30-Second Cinematic Thriller Trailer
Create a dark, intense, photorealistic 30-second theatrical movie trailer for a supernatural psychological murder mystery. Serious adult thriller tone, realistic actors, cinematic 35mm photography, deep shadows, cold desaturated nighttime colors contrasted with warm candlelit church interiors, rain, subtle film grain, shallow depth of field, dramatic camera movement, rapid escalating editing. The trailer begins slowly and mysteriously, then builds into a frantic final 10 seconds. Maintain the same main male character and the same sister throughout every appearance.0–4 seconds: BLACK SCREEN. Complete silence except for the faint sound of a woman breathing nervously.A sudden flash reveals a terrified young woman running alone through a dark rain-soaked alley at night. Handheld camera races backward directly in front of her as she runs toward camera, repeatedly looking behind her.SMASH CUT to an extreme close-up of the MAIN CHARACTER asleep in bed, sweating and twitching violently during a nightmare.Inside the nightmare, a deep distorted male whisper says:“Three…”A huge blood-red number 3 flashes briefly against black.4–8 seconds: Rapid nightmare fragments: the frightened woman reaches a dead end. A shadowy male figure approaches behind her, but his face is NEVER visible. Extreme close-up of the killer's hand reveals a distinctive ornate silver ring.The whisper returns:“Two…”Blood-red 2.The main character suddenly wakes with a violent gasp.Hard cut to morning television news footage showing the SAME WOMAN'S photograph.Female television reporter:“Police discovered the body early this morning…”The man's face drains of color.8–12 seconds: Police interrogation room. Harsh overhead fluorescent light. The main character sits across from two suspicious detectives.Detective, coldly:“You described the murder before we found the body.”Close-up on the main character.“Because I saw it happen.”Detective:“In a dream?”Silence. Fast close-up of the detective staring at him like he no longer believes a word he says.12–16 seconds: Warm Sunday sunlight streams through stained-glass windows inside a beautiful old church. The man's younger sister walks beside him down the aisle. She gently takes his arm.SISTER:“Maybe coming back here is exactly what you need.”He gives her a conflicted look.A friendly pastor approaches and shakes the sister's hand.CLOSE-UP:The pastor's hand.The silver ring.Everything suddenly goes silent.Extreme close-up of the main character's eyes widening.FLASH CUT back to the nightmare—the killer's hand wearing THE SAME RING.16–20 seconds: Music suddenly becomes a pounding cinematic pulse.Rapid investigative montage:The main character frantically covers his apartment wall with photographs of murdered women, newspaper articles, church bulletins and handwritten notes.He searches through old records late at night.A newspaper headline:SECOND WOMAN FOUND DEADA woman nervously enters a church confession booth.A shadow moves behind the confessional screen.A detective slams a crime-scene photograph onto a table.Police lights explode across the main character's face as he runs through a wet nighttime street.Detective shouting:“STOP!”20–24 seconds: Suddenly—Silence.The main character is asleep again.His nightmare begins.His sister stands completely alone beneath a flickering streetlight.She slowly turns toward him.Terrified.A dark figure appears several yards behind her.His sister whispers:“Michael?”The distorted voice begins:“Three…”FLASH — red 3.His sister running.“Two…”FLASH — red 2.Extreme close-up of Michael screaming awake:“NO!”24–28 seconds: The trailer erupts into extremely fast cinematic cuts synchronized with thunderous impacts:Michael sprinting through pouring rain.His sister pounding desperately against a locked door.Police racing toward the church.Michael smashing through a church doorway.A pastor turning suddenly in a dark hallway.A flashlight sweeping across rows of empty pews.Michael struggling with an unseen person.His sister screaming.The ornate silver ring hitting the floor and spinning across stone.A handgun trembling in Michael's hand. Church bells violently ringing.Michael enters a dark confession booth and sits down.Everything becomes silent.From behind the wooden screen:PRIEST: “What would you like to confess?”Michael stares straight ahead.Calm now.MICHAEL: “I'm going to kill someone tonight.”28–30 seconds: BLACK.A woman's frightened whisper:“One…”A gigantic blood-red 1 flashes onto screen with a violent bass hit.TITLE:3 2 1 — RED LIGHTThe numbers briefly flicker like a countdown. Final extremely fast shot: Michael standing alone inside the dark church as red-and-blue police lights pulse through the stained-glass windows.CUT TO BLACK.TRAILER STYLE: Psychological thriller mixed with supernatural mystery and serial-killer suspense. The dreams should feel surreal and fragmented but the real world must remain grounded and photorealistic. Avoid excessive gore; create fear through shadows, implication, facial expressions, sound, and rapid glimpses. Never clearly reveal the killer's identity during the trailer—the silver ring is the major visual clue. The pastor should initially appear completely trustworthy and ordinary. Michael's emotional progression should move from confusion → fear → obsession → desperation → grim determination. The final confession-booth line should be the trailer's biggest dramatic moment.
```

<a id="cinematic-08"></a>
### 7. 초원 위를 나는 검독수리 추적샷

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-08#cinematic-08)** · [원본 게시물](https://x.com/minchoi/status/2104742876584218720)

https://github.com/user-attachments/assets/fbdd85b0-a9c7-4951-955b-17408720334c

**프롬프트:**

```text
"Third-person chase shot from directly behind and slightly above a golden eagle as it flies over vast mountainous steppe. The camera follows at a fixed distance of a few metres, locked steady on the eagle, with smooth forward motion and no jitter. The whole bird stays in the lower centre of the frame with its full wingspan inside the frame and clear space on both sides. First it beats its wings powerfully, feathers flexing at the tips, then it spreads them wide and glides. Below and ahead, the landscape rushes toward the camera: winding rivers, open valleys, rocky peaks, with strong parallax. Bright late-afternoon sun from ahead, crisp air, a gentle rim light on its feathers, subtle lens flare. Realistic flight physics, motion blur from speed only, one continuous shot with no cuts."
```

<a id="cinematic-09"></a>
### 8. 빨간 장미를 들고 벤치에서 기다리기

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-09#cinematic-09)** · [원본 게시물](https://x.com/EndFolding79421/status/2112371662452601207)

https://github.com/user-attachments/assets/3d0a763e-e4d2-4983-98f1-1974b423ff6e

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
"subject": "A woman in a black sundress sits on a wooden bench outside a sunlit roadside building, holding a single red rose loosely in her hand. She looks up with a thoughtful, slightly melancholic expression. Her hair moves gently in a soft breeze as she sits calmly [slow reveal camera, starting behind her left shoulder and circling smoothly around to the front to frame her face and the parked van in the background].","scene": "A quiet small-town street in late afternoon. A green VW van is parked across the road in the background and stays completely still with no driver inside. Farther down the road, two blurred cars drive away slowly like normal traffic, their movement subtle but noticeable. Heat shimmer rises from the pavement. Warm golden sunlight streams in, casting long shadows and creating a nostalgic atmosphere. The camera lingers on the woman and the rose as it completes the slow reveal, keeping the van static but showing the distant cars in motion. A soft breeze moves her hair and the rose petals slightly.","style": "Ultra-realistic cinematic moment with warm color tones, shallow depth of field, and a soft nostalgic mood. Smooth camera movement to build a gentle reveal while maintaining stillness around the van and life-like movement in the far background."
```

<a id="cinematic-10"></a>
### 9. 비 내리는 골목의 4컷 호러

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-10#cinematic-10)** · [원본 게시물](https://x.com/EndFolding79421/status/2111076586514489818)

https://github.com/user-attachments/assets/caf72523-92dd-41d5-8955-7706ebfc2aee

**프롬프트:**

```text
First Panel:  A low-angle view of muddy boots stepping through a rain-soaked alleyway. The water is darker than normal, almost oily, rippling unnaturally as rain strikes it. Reflections in the puddles are slightly distorted, hinting at shapes that do not match the surroundings. A torn black umbrella edge intrudes at the top of the frame, barely holding together as rain pours down.Second panel:A disturbing macro close-up of a human hand trembling beneath falling rain. A single droplet hangs in midair just before touching the skin—but within the droplet’s reflection is a vague, humanoid silhouette that is not visible anywhere else in the scene. The background is an indistinct blur of flickering, dying streetlights.Third panel:A tight close-up of a woman’s face, partially obscured by wet strands of hair clinging to her skin. One eye is visible, wide and alert, reflecting a dim light source behind her. Rain streaks down her face like tears. Her lips are parted as if she has just heard something behind her. The background is pitch black, offering no sense of safety or space.Bottom panel:A long, rain-drenched street at night. The woman walks away from the viewer, her silhouette small and vulnerable beneath a single flickering streetlight. The wet pavement reflects the light—but in the reflection, a second elongated shadow trails behind her, far closer than it should be. The rain intensifies, blurring the distance as darkness slowly consumes the street.The overall palette remains cold and oppressive—muted greens, deep blues, and heavy blacks—while subtle visual inconsistencies across panels suggest a presence that cannot be fully seen, reinforcing the sense of being watched and followed.
```

<a id="cinematic-11"></a>
### 10. 흔들리는 전구 아래 지하실로

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-11#cinematic-11)** · [원본 게시물](https://x.com/EndFolding79421/status/2112376857773428953)

https://github.com/user-attachments/assets/3946fc57-e7ce-4474-98c9-3d571fc7bca7

**프롬프트:**

```text
A nervous woman in jeans and a hoodie descends into a damp basement lit only by a swinging bulb [crane down, slow]. Sweat glistens on her forehead as the shadows stretch unnaturally—revealing a hooded figure watching silently from the far corner.
```

<a id="cinematic-12"></a>
### 11. 절벽에서 뛰어 구름 위를 나는 장면

작성자 [@bmx_ai13](https://x.com/bmx_ai13) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-12#cinematic-12)** · [원본 게시물](https://x.com/bmx_ai13/status/2105168764681453666)

https://github.com/user-attachments/assets/d62e6f2a-812b-46e8-a58a-1f982ea50842

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
CRITICAL: Perfect character continuity across every shot. One lone athletic man, bare-chested, simple dark charcoal athletic shorts, barefoot, short dark hair, lean defined build, same body and hair in every frame. No wings, no superhero suit, no costume, no visible technology. Anatomy stays correct at all times: two arms, two legs, no extra limbs, no warped or floating body parts, no sudden pose changes.

SUBJECT LOCK: The man is 30s, athletic, natural muscle definition, tanned skin with visible pores and subtle sweat sheen. Dark charcoal shorts only. Hair and shorts react naturally to wind in every shot.

WORLD PLATE: A tiny grassy cliff floats impossibly high above an endless ocean of dense volumetric silver-white clouds thousands of meters below. Gigantic pale twisted cable-like structures stretch across the cloudscape and vanish into infinity. A colossal luminous planetary ring system crosses the sky diagonally, filled with countless bright parallel streaks catching sunlight. Massive distant floating rock formations sit partially silhouetted in the sky. Clear blue upper atmosphere, brilliant sunlight, realistic aerial haze, strong atmospheric perspective. The structures feel physically present and real, never abstract or psychedelic.

PALETTE: Cool blue sky, soft silver-white clouds, muted natural green grass, dark charcoal shorts, bright white ring highlights. Realistic sunlight with deep shadows and true highlights. Slight dreamy softness while textures stay sharp and photoreal.

SHOT 1 (0-3s): Wide cinematic rear shot, low angle. The man stands at the edge of the grassy plateau facing the impossible cloud world, his long shadow stretching behind him. After a brief still moment he bursts into a run toward the cliff edge. The camera tracks smoothly behind and low to the grass, building speed with him. Accurate foot contact, real momentum and body weight, grass blades bending under each step. Giant celestial structures dominate the background.

SHOT 2 (3-5s): He reaches the edge and launches forward into empty space. The camera follows the leap as the ground vanishes beneath him. It begins as a real human dive, arms extending naturally, then eases into a smooth horizontal glide. Reveal the enormous vertical depth of the clouds below him.

SHOT 3 (5-9s): Cut to a dramatic fast side-profile tracking close shot. He flies rapidly just above the cloud tops. Wind pushes across his body and hair, muscles subtly reacting to the airflow. One colossal twisted structure passes overhead, emphasizing scale and speed. Clouds streak beneath him with strong parallax, sunlight flashing across his skin, realistic motion blur.

SHOT 4 (9-15s): Epic rear pursuit shot, centered composition. The camera follows directly behind him as he flies deeper into the surreal world. Two gigantic twisted pathways stretch forward on either side of him. Far ahead the luminous rings rise across the entire sky while a huge dark floating rock formation hangs overhead. Slowly pull the camera wider as he becomes smaller against the vast scale. Final beat: he continues toward the brilliant horizon, arms slightly open, surrounded by clouds and celestial architecture.

CAMERA: Smooth cinematic tracking only, no handheld shake. Grounded low-angle tracking, then wide aerial perspective, then fast side-profile tracking, then centered rear chase. Strong foreground-to-background parallax.

MOTION: Flight is smooth and aerodynamic, controlled and human, never stiff or superhero-like. Hair, clouds and atmospheric particles react naturally to strong high-altitude wind.

SOUND BED: Diegetic and atmospheric only, no dialogue. Quiet high-altitude wind and distant ambience at open. Footsteps accelerate across grass. A powerful wind rush hits at the leap. During flight build layered deep air movement, subtle cinematic bass and expansive melodic progressive-trance energy. Close on an uplifting atmospheric swell as he disappears into the infinite landscape.

LAST FRAME: The man small in the center of the frame flying toward the bright horizon, arms slightly open, clouds and twisted structures on both sides, luminous rings above. No on-screen text, no subtitles, no logos, no watermarks, no UI elements, no branding of any kind.
```

<a id="cinematic-13"></a>
### 12. 노을 진 옥상의 탭댄스

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-13#cinematic-13)** · [원본 게시물](https://x.com/EndFolding79421/status/2110785773456838793)

https://github.com/user-attachments/assets/a7de831c-f2de-4cbc-b68b-031130a8aca9

**프롬프트:**

```text
A beautiful woman in a flowing dress is joyfully tap dancing on a rooftop at sunset. Her skirt twirls as she moves with light, expressive energy. The golden light of the sun reflects off her skin and hair while a gentle breeze lifts the hem of her dress. [tracking shot, low angle] as the camera follows her lively steps, capturing her rhythm and grace in the open rooftop space. Her smile glows with pure happiness as she dances against the silhouette of the city skyline.[tracking shot, low angle] begins as she starts dancing and follows her tapping steps across the rooftop.Mood: Joyful, lighthearted, energetic with warmth and motion.sunset rooftop, flowing dress, soft breeze, happy expression, energetic movement, golden hour light, cinematic joy, expressive motion, warm colors
```

<a id="cinematic-14"></a>
### 13. 해 질 녘 블랙우드 숲을 달리는 여성

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 13초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-14#cinematic-14)** · [원본 게시물](https://x.com/EndFolding79421/status/2110781238374207618)

https://github.com/user-attachments/assets/2edae58c-9d5b-4a7a-92a3-05017258e995

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Late afternoon fading toward dusk in Blackwood Forest.Endless North Georgia pine and oak forest stretches in every direction. The forest is completely wild and undeveloped, with no visible trails, roads, paths, markers, campsites, fences, or signs of human maintenance.The woman 📷runs alone through the woods.Begin with a high overhead shot looking down through the canopy before descending toward her.Cut to a handheld tracking shot behind her shoulder as she moves through dense woodland, weaving between pine trunks, stepping over roots and fallen branches, forcing her way through untouched forest undergrowth.She glances behind her while continuing forward.Cut to a low-angle shot from the forest floor as she rushes past.A crow suddenly bursts from a nearby tree and flies away.Cut to a wide shot revealing how small she is compared to the massive forest surrounding her.The camera slowly pulls back as she continues deeper into Blackwood. No slasher. No other humans.The forest is completely wild and undeveloped, with no visible trails, roads, paths, markers, campsites, fences, or signs of human maintenance.
```

<a id="cinematic-15"></a>
### 14. 보트 옆 혹등고래 점프, 두 시점

작성자 [@umesh_ai](https://x.com/umesh_ai) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-15#cinematic-15)** · [원본 게시물](https://x.com/umesh_ai/status/2109174567352824224)

https://github.com/user-attachments/assets/fa8195cf-5385-4945-a4b8-0dc188d90cf2

**프롬프트:**

```text
Create a 15-second ultra-realistic cinematic video showing a spectacular humpback whale breaching beside a small boat in the ocean.0:00–0:07.5 | Perspective 1: Boat-Level ViewA cinematic eye-level shot from a small boat floating on turquoise ocean water at golden hour. Suddenly, a gigantic humpback whale bursts vertically out of the water just meters away. Its enormous body rises into the air, twists gracefully, and crashes back into the ocean, creating a massive, dramatic splash. The entire event, from the calm water to the final splash, finishes within 7.5 seconds. Camera stays in one position with subtle realistic boat movement.0:07.5–0:15 | Perspective 2: Aerial Drone ViewAt exactly 7.5 seconds, hard cut to a breathtaking overhead drone perspective. Time resets to the exact beginning of the previous event. Show the SAME whale performing the EXACT SAME breach beside the EXACT SAME boat, with perfectly matching timing, movement, sunlight, and water splash. From above, the viewer can see the whale's enormous scale, the tiny boat, the circular ripples, and the spectacular splash pattern. The complete event finishes again at exactly 15 seconds. Style: Photorealistic, cinematic natural lighting, 4K detail, realistic water physics, immersive ocean sound, dramatic scale, 16:9 aspect ratio. One continuous shot per perspective. No slow motion, no narration, no text, no extra cuts. The second half must be a synchronized replay of the first half, not a continuation of the action.
```

<a id="cinematic-16"></a>
### 15. 고양이의 한밤 모험을 따라가는 핸드헬드

작성자 [@umesh_ai](https://x.com/umesh_ai) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-16#cinematic-16)** · [원본 게시물](https://x.com/umesh_ai/status/2110797376827035806)

https://github.com/user-attachments/assets/f680e472-b914-40ec-9935-be558353fd75

**프롬프트:**

```text
An amateur handheld recording in third-person perspective rapidly follows a cat through its nighttime adventures in one continuous shot, with no cuts, no stopping, and no pause. The sequence feels like fast-forward, showing all the curious, mischievous, funny, and chaotic things a cat might do while the town, house, garden, and everything around it are half-asleep.The cat races through about ten places a cat would naturally explore at night, each one flowing into the next in a single continuous chase: a quiet bedroom, a dim hallway, a kitchen, a living room, a backyard garden, a fence line, a garage, a rooftop, a tree, and a sleepy street or alley. The camera is shaky and imperfect, always struggling to keep up as it follows close behind. In every location, the cat causes some kind of chaos. In the bedroom it jumps onto furniture and disturbs sleeping people. In the hallway it sends small objects tumbling. In the kitchen it knocks items off the counter. In the living room it darts across shelves and tips things over. In the garden it rustles plants, digs, or startles birds. On the fence it rattles loose objects. In the garage it weaves through clutter and causes things to wobble or fall. On the rooftop it skids across surfaces and startles other animals. In the tree it shakes branches and scatters leaves. In the street or alley it darts through trash, shadows, and unexpected little messes, always leaving brief chaos behind before sprinting onward.The cat behaves like a restless, curious nighttime troublemaker: climbing, leaping, squeezing through gaps, chasing tiny movements, staring at strange things, swatting objects, knocking things over, and vanishing into corners before bursting back out again. Every scene should contain a clear action, reaction, or small disaster caused by the cat.Everything around it feels sleepy and still, with dark houses, quiet gardens, dim windows, silent rooftops, and empty streets. The contrast is that the cat is pure energy, moving so quickly that the world smears into motion blur and fragmented glimpses of chaos. The overall feeling is funny, lively, mischievous, and cinematic, like a whole secret night of cat behavior compressed into one rapid continuous chase.
```

<a id="cinematic-17"></a>
### 16. 종탑 위 박쥐 떼가 만드는 글자

작성자 [@Shinebynous](https://x.com/Shinebynous) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-17#cinematic-17)** · [원본 게시물](https://x.com/Shinebynous/status/2113746281663238357)

https://github.com/user-attachments/assets/ab5052a7-3f29-4354-a758-7d630cf1a780

**프롬프트:**

```text
A colossal bat swarm blotting the sky, leathery wings in inky ebony and subtle wine-red veins.Effect: Wingbeats weave "SWARM," pulsing with ultrasonic waves.Location: A gothic belfry tower pierced by lightning during a tempest.Texture: Supple, fluttering, enveloping.Mood: Overwhelming, vampiric, eclipsing, halloween music
```

<a id="cinematic-18"></a>
### 17. 식당 근무를 마치고 귀가하는 루시

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-18#cinematic-18)** · [원본 게시물](https://x.com/EndFolding79421/status/2110800090897973405)

https://github.com/user-attachments/assets/f15bb13d-3df7-4e0a-bd89-3d5a7ff01675

**프롬프트:**

```text
Lucy stepped out of the small diner where she worked, the doorbell jingling softly behind her. The night air was cool and crisp, a welcome change from the stuffy warmth inside. She took a deep breath, feeling the slight chill of the evening settle on her skin. The street was quiet, only the distant hum of traffic breaking the silence. Her shift had been long and exhausting, filled with the clatter of dishes and the constant chatter of customers. Now, the quiet seemed almost surreal, a stark contrast to the noise and chaos she had just left behind. Lucy adjusted her bag on her shoulder, glancing around as she began her walk home. The dim streetlights cast long shadows across the pavement, their flickering bulbs adding an eerie quality to the otherwise peaceful night. Lucy's footsteps echoed softly, a rhythmic accompaniment to her thoughts. She felt a strange mix of relief and unease; relief that her shift was over, and unease that she had to walk home alone at this hour. She tried to shake off the feeling, telling herself it was just her imagination. But as she walked, the sensation of being watched grew stronger. Lucy's eyes darted to the darkened alleyways and the shadowy corners of the street, half-expecting to see someone lurking there. Each time, there was nothing but the oppressive darkness. Her thoughts wandered to the events of the day, the usual frustrations of work blending with snippets of conversations she'd had with her coworkers. She thought of Megan, her closest friend at the diner, and their plans to go out together on the weekend. The thought brought a small smile to her lips, momentarily easing her tension. But the feeling of being watched persisted. Lucy quickened her pace, her heartbeat matching the rapid rhythm of her footsteps. She turned down a quieter street, the buildings looming tall and silent on either side. The oppressive silence pressed in on her, amplifying every sound, every rustle of leaves, every distant car horn. A sudden noise behind her made Lucy stop in her tracks. She spun around, eyes wide, searching the shadows for the source. The street was empty, the only movement the gentle sway of a tree branch in the breeze. She stood there for a moment, heart pounding, before forcing herself to turn back and keep walking. "It's just your imagination," she muttered under her breath, trying to steady her nerves. But the cold knot of fear in her stomach told her otherwise.
```

<a id="cinematic-19"></a>
### 18. 갑옷 사냥꾼의 함바그 요리

작성자 [@tokyo_Valentine](https://x.com/tokyo_Valentine) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-19#cinematic-19)** · [원본 게시물](https://x.com/tokyo_Valentine/status/2115085474973073710)

https://github.com/user-attachments/assets/223294d0-6173-4545-b441-2da77815bcaf

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Create a 15-second cinematic cooking sequence, 16:9 landscape, using the two supplied reference images.

REFERENCE CONSISTENCY
Reference Image 1 defines the single character: preserve the exact black-and-red armor, helmet, mechanical dreadlock tubes, visible eyes, armored hands, proportions, materials, and surface details. The character wears the gas mask while cooking. Only the gas mask is removed before eating; the helmet, tubes, and body armor remain unchanged. Keep all weapons secured and inactive.
Reference Image 2 defines the kitchen: preserve its black marble island, dark wood cabinetry, warm amber lighting, pendant lamps, appliances, and spatial layout.

Treat both reference sheets as design references. Render a full-screen cinematic scene with one character, not the diagrams, multiple views, labels, or panels.

CONCEPT AND VISUAL STYLE
A formidable armored character expertly prepares an irresistibly appetizing Japanese hamburger steak topped with a sunny-side-up egg and glossy brown demi-glace sauce, then removes the gas mask and enjoys the meal alone.

Use realistic cinematic materials, warm highlights on black metal, delicate steam, a deeply browned meat crust, glossy sauce, and a rich golden egg yolk. Serve one hamburger steak and one fried egg on a white ceramic plate.
DIRECTING
Use action-film camera language: fast low-angle tracking, precise whip pans, short orbital moves, motivated push-ins, and action-matched cuts. Let the camera follow the hands, utensils, and food. Finish each fast move with a clear, readable composition.

Use a brisk cooking montage during the first eight seconds, followed by controlled camera movement for mask removal and eating. Compress actual cooking time through editorial cuts. The hamburger steak is fully cooked before plating; the egg white is set while the yolk remains runny.

The timestamps below describe consecutive one-second action beats. Preserve the order and allocate enough time for the physical mask removal and the final bite.
SECOND-BY-SECOND SEQUENCE

00:00–00:01
An armored hand lowers a thick hamburger steak into a hot skillet with a spatula. It immediately sizzles. Begin at skillet-rim height with a fast lateral dolly toward the point of contact. Tiny oil droplets and steam catch the warm kitchen light.

00:01–00:02
CUT FORWARD IN COOKING TIME. The character smoothly flips the steak once with the spatula, revealing a beautifully browned crust. The camera follows the turn in a tight upward arc, then settles as the steak lands firmly in the pan.

00:02–00:03
CUT to both armored hands cracking one egg over a second skillet. A quick whip pan follows the forearm and resolves into a steady close-up as the shell opens and the egg drops into the pan. Keep the yolk whole.

00:03–00:04
Continue the egg shot. The camera makes a short, low macro slide beside the pan as the egg white begins sizzling around the domed golden yolk. Emphasize delicate bubbles and the clean, glossy yolk surface.
00:04–00:05
CUT FORWARD IN COOKING TIME to the browned hamburger steak. The character pours a small stream of thick demi-glace sauce around it. A fast push-in follows the stream down to the bubbling sauce, ending on the glistening meat.

00:05–00:06
The character lifts the cooked steak with a spatula and transfers it onto the white plate immediately beside the skillet. The camera tracks the short movement horizontally, keeping the steak sharp as sauce clings to its surface.
00:06–00:07
CUT to the cooked sunny-side-up egg being lifted from the second skillet. The camera follows the spatula in a tight descending movement as the character gently slides the egg onto the center of the steak. The yolk remains intact.

00:07–00:08
The character slides the completed plate a short distance into its dining position on the island. A brisk 30-degree camera orbit reveals the imposing masked character behind the steaming food. End with the golden yolk prominent in the foreground.
00:08–00:09
CUT to the character seated alone at the island. Both hands release the gas mask’s side catches. Begin a controlled push-in from a three-quarter angle. Clearly show the hands gripping the mask while it still covers the face.

00:09–00:10
Continue without cutting. The character physically pulls the gas mask forward, away from the face, then lowers it. Reveal the mouth naturally while preserving the same visible eye region and skin tone. The helmet and mechanical dreadlock tubes remain completely unchanged.
00:10–00:11
Continue the same action. The character places the removed mask on the countertop to the right of the plate. The camera tilts down with the hand, clearly showing the mask touch the surface and remain there as a solid object.

00:11–00:12
CUT to a low close-up of the plate. Using a fork and table knife, the character cuts through the egg and cooked hamburger steak. The camera makes a short push-in as golden yolk flows over the browned meat and blends with the glossy sauce. Show a moist, fully cooked interior.
00:12–00:13
Continue the food shot. The fork lifts one small bite coated with yolk and sauce. The camera rises smoothly with the fork, maintaining sharp focus on the appetizing bite and its delicate steam.

00:13–00:14
CUT to a three-quarter facial close-up. The character brings the fork to the exposed mouth, takes the bite, and begins chewing naturally. Use a gentle forward camera drift. The gas mask remains on the countertop.
00:14–00:15
Continue without cutting. The character’s eyes soften with quiet satisfaction and the shoulders relax slightly. Make a small, smooth dolly backward to include the steaming plate and warm kitchen surroundings. End on the character peacefully enjoying the meal alone.

SOUND
No background music, narration, or dialogue.
Use synchronized cooking and environmental sounds: strong sizzling, an egg cracking, sauce bubbling, subtle armor movement, spatula contact, mask catches clicking, the mask touching the countertop, and quiet cutlery sounds. Let the intense cooking sounds transition into calm kitchen ambience during the final seconds.
CONTINUITY AND QUALITY
Exactly one character, one hamburger steak, and one fried egg.
Maintain consistent hands, utensils, armor, kitchen geometry, and food placement.
The gas mask stays on during cooking, is physically removed at 00:09–00:10, and remains beside the plate afterward.
Use ordinary kitchen utensils for cooking.
Keep food and hand movements readable despite the energetic camera.
Avoid duplicated fingers, floating utensils, teleporting ingredients, changing faces, dissolving masks, extra people, explosive flames, excessive camera shake, subtitles, captions, and reference-sheet text.
```

<a id="cinematic-20"></a>
### 19. 항구에서 유령이 되는 빅토리아 시대 여인

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-20#cinematic-20)** · [원본 게시물](https://x.com/EndFolding79421/status/2112367087242891434)

https://github.com/user-attachments/assets/08cf38cd-6906-40ea-8bf1-37eca9f71281

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
A beautiful woman in a deep burgundy Victorian dress stands at the harbor, facing the camera, holding a lace parasol. Her expression is calm and focused [static shot]. After 2 seconds, she slowly turns and begins walking away down the stone walkway [pan right, truck back]. As she continues walking, her entire body begins to gradually fade, slowly becoming transparent — until she disappears completely just before reaching the end of the dock.[static shot] (first 2 seconds), then [pan right, truck back] as she walks and fades smoothlyMood: Elegant, haunting, timeless.Victorian dress, parasol, harbor walkway, soft breeze, smooth dissolve, cinematic tone, subtle elegance, ethereal presence, fading ghost
```

<a id="cinematic-21"></a>
### 20. 1981년 슬래셔 풍 안개 숲 추격

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 12초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-21#cinematic-21)** · [원본 게시물](https://x.com/EndFolding79421/status/2116238431307157751)

https://github.com/user-attachments/assets/93b0a031-0ecf-423d-bb0b-6ce733d6ddac

**프롬프트:**

```text
integrated_multimodal_description: [Shot 1] Live-action 1981 35mm slasher look, night pine woods, wet leaves, fog, weak moonlight, visible film grain, muted greens, crushed blacks. A young woman in a worn flannel and jeans sprints toward camera down a narrow dirt path, breathing hard, looking back. The camera tracks backward in front of her with large amplitude at fast speed and shakes slightly. [Shot 2] At 00:05.00, the camera trucks right with small amplitude at fast speed as a tall slasher in dark work clothes and a crude cloth mask bursts from the trees behind her, weapon raised, closing the gap. [Shot 3] At 00:10.00, the camera pushes in with small amplitude at fast speed on her face as she stumbles, recovers, and keeps running; the slasher stays behind her in the dark trees through 12.00 seconds.overall_soundscape: Night insects, crunching leaves, snapping twigs, her panicked breathing and footsteps, heavier footsteps behind her. No dialogue.non_diegetic_music: Low analog slasher strings and sparse stingers.
```

<a id="cinematic-22"></a>
### 21. 프롬프트 하나로 만든 VFX 전후 비교

작성자 [@onofumi_AI](https://x.com/onofumi_AI) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-22#cinematic-22)** · [원본 게시물](https://x.com/onofumi_AI/status/2108487232302805020)

https://github.com/user-attachments/assets/70ca63dd-6aa2-435e-b4ed-d439af21d06f

**프롬프트:**

```text
A dramatic before/after VFX breakdown, one continuous 10-second locked-off shot of a small plain white studio apartment in daylight: a young woman sits on a chair in the middle of the room reading a book, beige carpet, white walls, a window. The camera never moves and the woman keeps reading, turning a page, the whole time. A thin bright lime vertical wipe line, rendered as a flat 2D screen overlay with a small round lime handle, travels horizontally across the frame; everything on the side the line has already passed changes to the next stage, the other side keeps the previous stage, and the room geometry stays perfectly aligned. Stage 1 (0-2s): raw footage, ordinary empty white room. Stage 2 (2-4s, line sweeps left to right): the room becomes untextured matte grey clay: grey clay coral shapes, grey clay whale and fish models floating in the air, flat grey light. Stage 3 (4-7s, line sweeps right to left): final composite, the whole room is now deep underwater: turquoise water fills the space with god rays from the window, vivid coral reef grows over the floor and walls, a huge humpback whale swims slowly past behind her, schools of bright tropical fish swirl around, bubbles rise, her hair floats gently while she keeps reading calmly. 7-9s: the line sweeps quickly back and forth once, flashing between the plain white room and the underwater world to compare them. 9-10s: the line exits, full underwater shot holds. The before and after are extremely different. Photorealistic, cinematic, clean VFX breakdown style.
```

<a id="cinematic-23"></a>
### 22. 3컷 스토리보드로 만든 햄스터 록스타

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 16초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-23#cinematic-23)** · [원본 게시물](https://x.com/EndFolding79421/status/2115559321916375478)

https://github.com/user-attachments/assets/f0a2fcf6-e7a4-4b25-aca7-4f70adea20f3

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
The supplied three-panel storyboard showing the hamster playing guitar, the two shocked cats watching from the bed, and the hamster eating a sunflower seed.Use this single storyboard as the visual reference for the entire video. Each panel represents a different scene in chronological order, from top to bottom.Preserve the exact appearances of the hamster, both cats, miniature electric guitar, hamster cage, bedroom, and lighting throughout.Photorealistic live-action animal comedy, professional 35mm cinematic appearance, natural indoor lighting, realistic fur, detailed textures, believable animal movements, and clean image quality. No cartoon appearance or excessive saturation.00:00–00:05 — THE ROCK STARBegin with the TOP PANEL of the storyboard.Inside its hamster cage in a cozy bedroom, a tiny golden hamster stands on its hind legs, enthusiastically playing a miniature black electric guitar.Its tiny paws rapidly move across the strings, perfectly synchronized with the fast heavy-metal guitar riffs in the supplied audio.The hamster rocks its little body back and forth, furiously headbanging while playing.The camera slowly pushes closer to the hamster.00:05–00:09 — THE SHOCKED AUDIENCE Cut to the MIDDLE PANEL of the storyboard.Two cats sit together on the bed, staring toward the hamster cage.Both cats have wide, astonished eyes and slightly open mouths.The orange cat slowly turns its head toward the gray-and-white cat in complete disbelief.The gray-and-white cat remains frozen, staring at the hamster's outrageous performance.The heavy-metal music continues uninterrupted.00:09–00:13 — THE GRAND FINALECut back to the TOP PANEL.The hamster performs its final furious guitar solo, rapidly strumming and rocking its tiny body with incredible enthusiasm.Its movements follow the rhythm of the supplied music. As the final guitar notes ring out, the hamster finishes with one dramatic flourish.00:13–00:16 — COMIC RELIEFCut to the BOTTOM PANEL of the storyboard.The music has ended.The miniature guitar rests against the wooden hamster house.The hamster sits peacefully inside its cage, holding a sunflower seed between its tiny paws. It quietly nibbles the sunflower seed, its cheeks moving naturally as it eats.The camera remains completely stationary.Only the faint natural sounds of the hamster eating are heard.The hamster looks innocently toward the viewer and continues chewing as though absolutely nothing unusual happened.IMPORTANT:The three storyboard panels are separate sequential scenes, NOT a split-screen composition.Generate a full-frame 9:16 vertical video, using the individual storyboard panels to guide each shot.Maintain exact character consistency and the same bedroom environment throughout.Synchronize the guitar performance with the supplied music
```

<a id="cinematic-24"></a>
### 23. 야생 다큐처럼 찍은 고양이와 로봇청소기

작성자 [@aiIgnatius](https://x.com/aiIgnatius) · 30초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-24#cinematic-24)** · [원본 게시물](https://x.com/aiIgnatius/status/2114669067189584367)

https://github.com/user-attachments/assets/799a309e-f5cd-4042-bc6c-73c57d7fb00b

**프롬프트:**

```text
Style: Photorealistic, 8K telephoto wildlife look, living room as savannah, hushed original narrator voice.0-3s: Wide of shag carpet at golden hour through the blinds as a robot vacuum glides across. Narrator: “On the vast shag-pile plains, the Roomba begins its daily migration.”3-6s: Macro of the spinning brush swallowing a dust bunny.6-9s: Telephoto on a cat behind a couch leg, pupils dilating. Narrator: “But it is not alone. An apex predator, weighing eleven pounds.”9-12s: Low-angle slow-mo, the cat’s haunches wiggling, tail twitching.12-15s: The pounce, the cat landing squarely on top of the Roomba.15-18s: The cat rides it with total dignity. Narrator: “Remarkably, the cat has not yet realised it is not in control.”18-21s: Wide as the cat glides past a stunned golden retriever.21-24s: The Roomba hits a wall and spins, flinging the cat off. It lands on its feet and immediately starts grooming. Narrator: “Dignity is restored. Grooming is deployed.”24-27s: The Roomba beeps and returns to its dock with a sad little tune.27-30s: Close-up of the cat watching the dock. Narrator: “Tomorrow, the hunt begins again.”
```

<a id="cinematic-25"></a>
### 24. 로봇청소기 탄 고양이, 두 개의 카메라

작성자 [@yarakashiyama_](https://x.com/yarakashiyama_) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-25#cinematic-25)** · [원본 게시물](https://x.com/yarakashiyama_/status/2112651320209600627)

https://github.com/user-attachments/assets/281819d7-1f3d-415d-bdb2-c4843e3e160f

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
【外から撮る場面】
参照画像の猫・掃除機・部屋を保つ。掃除機は最初のコマから最後まで、一定の速さで前進する。撮影カメラは掃除機の前方から後退しながら撮る。猫と掃除機の大きさを画面内でほぼ一定に保つ。床の継ぎ目が機体の下を通り、後ろの家具が遠ざかる。しっぽは1本で、掃除機の右側、この画面では左側に垂れている。

【掃除機の目線の場面】
参照画像の低いカメラ位置と、前向きの方向を保つ。カメラは一定の速さで前進する。見えるのは前方の床・部屋・右から入る1本のしっぽ。機体の天板や縁は映さない。床の継ぎ目が画面の下へ流れ、前方の戸口に近づく。しっぽはレンズへ近づくにつれて大きく見える。
```

<a id="cinematic-26"></a>
### 25. 수묵화 족자에서 쏟아지는 폭포

작성자 [@opener_ai](https://x.com/opener_ai) · 10초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-26#cinematic-26)** · [원본 게시물](https://x.com/opener_ai/status/2111666343447818617)

https://github.com/user-attachments/assets/cba8c702-11d2-4fa0-8662-5867c8c2697a

**프롬프트:**

```text
A tall Korean ink-wash landscape scroll hangs against a warm plaster wall in a quiet hanok alcove. Painted misty mountains and a black pine surround one narrow painted waterfall. A shallow celadon basin rests directly below the scroll, already visible from the opening frame. The opening second reveals the striking ink waterfall gleaming faintly like liquid. Over the next three seconds only the waterfall's lower end gradually becomes a small continuous stream of real clear water, crossing the paper's lower edge and falling into the basin. For the remaining six seconds that stream keeps flowing from the same painted waterfall, producing contact splashes and expanding ripples; the basin's water level rises slightly without overflowing. The deliberate fantasy is only the painted waterfall producing real water: mountains, pine, paper borders and wall remain still and dry. Static full view of scroll and basin, warm side lighting, exquisite ink texture and glossy celadon, one continuous ten-second shot. No cuts, new objects or captions.
```

<a id="cinematic-27"></a>
### 26. 콘크리트 방파제를 덮치는 폭풍 해일

작성자 [@sebatheepan](https://x.com/sebatheepan) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-27#cinematic-27)** · [원본 게시물](https://x.com/sebatheepan/status/2113038301154164960)

https://github.com/user-attachments/assets/1807758a-f641-4564-80db-73a9fd5d102a

**프롬프트:**

```text
A storm surge detonates against a concrete sea wall and the entire structure shudders through to its foundation.
Shot 1 — 0.0s to 5.0s — WS, low angle looking up from the waterline, crane mount. At 0.0s the frame is already wet: a brutalist concrete tidal barrier runs from frame left toward a vanishing point right, its vertical buttress fins stained dark by decades of salt, and a single sodium floodlight on a rusted mast burns orange against a bruised graphite sky. A swell arrives from behind camera and the first fraction of it — a wall of grey-green water, no crest, freight-train mass — climbs the parapet at 0.6s and detonates over it at 1.4s into a sheet of white spray that crosses the whole frame. The crane lifts with the impact at 1.2 m/s, rising from just above the waterline toward eye height on the parapet. Spray hangs airborne after the surge retreats, thinning slowly across the floodlight beam.
Hard cut.
Shot 2 — 5.0s to 10.5s — MCU, low, locked-off at the parapet. The last of the water drains back through the expansion joints in vertical ropes, and the retreat drags debris on gravity rather than wind: a length of splintered timber, a burst orange buoy, a scatter of stone aggregate, each tumbling with rotation and settling where physics puts it against the buttress fins. Residual water sheets off the concrete in one continuous film, then breaks into drips. Two gulls cross frame right to left, small and unhurried, and are gone.
Hard cut.
Shot 3 — 10.5s to 15.0s — EWS, high angle looking down from behind and above the barrier, slow dolly forward at 0.3 m/s. The ocean beyond is still working — long ground swell lines stacked to the horizon under the bruised sky — while the barrier itself has gone motionless and the suspended spray from the impact turns slowly in the floodlight beam. Nothing settles twice; the scene arrives at stillness with the water still moving behind it.
Camera law: 24mm anamorphic; movement family is crane rise at 1.2 m/s through shot one, locked-off through shot two, slow dolly forward at 0.3 m/s through shot three; the camera stays low for shots one and two and lifts above the parapet line only for shot three; 180 degree motion blur. Anti-default: droplets on the lens glass in the near foreground of shot two, defocused, never wiped.
Grade and audio: storm-desat palette — graphite, sodium-orange, cold grey-green — contrast pushed high with blacks crushed. Key light is the single sodium floodlight on the rusted mast, halation blooming where it burns through suspended spray. A gale ambient bed under five diegetic events — deep water impact on concrete, spray hiss across stone, water draining through expansion joints, timber cracking against the barrier, a distant fog signal.
Constraints: Count of people in frame: zero. Count of gulls: two. Count of light sources: one. No music, no score, no bgm. No subtitles.
```

<a id="cinematic-28"></a>
### 27. 해 질 녘 갠트리 크레인 컨테이너 추적

작성자 [@sebatheepan](https://x.com/sebatheepan) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-28#cinematic-28)** · [원본 게시물](https://x.com/sebatheepan/status/2113038301154164960)

https://github.com/user-attachments/assets/dd973cb4-e6f3-4715-96e3-f8ff76179fbc

**프롬프트:**

```text
A gantry crane walks a loaded shipping container across a working port at last light, and the camera never leaves it.

Shot 1 — 0.0s to 10.0s — one continuous unbroken take, WS opening to MCU, crane-mounted arc into a dolly-zoom, subject held in the right third. At 0.0s the frame sits inside the machinery's own logic: a blue-grey container hangs twelve metres above quay level on four steel cables that are the only diagonal in a composition built from horizontals — stacked containers running to the frame edge, a flat leaden canal, a hard horizon. At 1.2s the trolley travels right along the gantry boom at 1.0 m/s and the camera arcs with it; the cables pass from slack to taut and the container answers with a slow pendulum that gravity kills by 3.0s. Below, a stub of loose tarpaulin on a container roof lifts and folds in the crosswind, then drops. At 6.0s the trolley brakes, the container floats its last half metre of travel, and the cables hand the load's momentum to the frame as a single lurch the camera takes rather than hides. At 8.0s the lens dolly-zooms into the container's corrugated face, the world flattening and compressing against the steel, and holds to the end while the port keeps working behind it.

Camera law: 35mm anamorphic, one continuous unbroken take with no cut and no gap; movement family is a crane-mounted arc at 1.0 m/s through the travel, then a dolly-zoom for the final beat; height holds just above container-roof level, high angle looking down on the quay, never eye level with the machinery; 180 degree motion blur. Anti-default: a defocused steel cable passes within twenty centimetres of the lens twice during the arc, and neither pass is wiped.

Grade and audio: cool-daylight palette — leaden blue, rust-brown, sodium-amber — contrast soft lifted blacks. Key light is the dying sun low behind the gantry, halation blooming through salt haze and diesel exhaust. Port rumble and water slap as the bed under five diegetic events — steel cable loading, trolley motor, a container meeting its quay guide, crosswind through tarpaulin, a far ship's horn.

Constraints: Count of cuts: zero. Count of people in frame: zero. No music, no score, no bgm. No subtitles.
```

<a id="cinematic-29"></a>
### 28. 검은 수면에 떨어지는 물방울 매크로

작성자 [@sebatheepan](https://x.com/sebatheepan) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-29#cinematic-29)** · [원본 게시물](https://x.com/sebatheepan/status/2113038301154164960)

https://github.com/user-attachments/assets/198438b9-7f46-41a9-9655-3161fad74b18

**프롬프트:**

```text
A single droplet of water falls into a still black pool and the surface answers it.Shot 1 — 0.0s to 6.0s — ECU macro, eye level with the waterline, locked-off. At 0.0s the frame holds a still black water surface across the lower third, its meniscus drawn as one bright curve against a matte grey background. A single droplet hangs in the upper frame, out of focus, then falls. At 1.4s it strikes the surface and the impact throws a crown of water upward in real time, crisp-edged rather than blurred; the crown collapses inward on itself by 2.4s and a rebound droplet rises out of the collapse, hangs briefly at 2.6s, and falls back at 4.1s. Ripples run outward and reach the frame edge at 5.4s, and the surface settles into stillness indistinguishable from frame one.

Camera law: 100mm macro at minimum focus distance, locked-off, no camera move; the plane of focus sits exactly on the meniscus and depth of field is razor thin; 1/2000s shutter so droplet edges stay crisp through the fastest motion. Anti-default: a defocused beaker rim occupies the left fifteen percent of the frame, close to the lens, and is never racked away.Grade and audio: cool-daylight palette — black, steel-blue, one white specular — contrast low-key deep shadow. Key light is a single soft source directly above the pool, halation blooming on the specular highlight. Room tone as the bed under five diegetic events — surface tension snapping, impact into the pool, crown collapse, the rebound droplet returning, ripples sheeting across still water.Constraints: Count of cuts: zero. Count of droplets: one. Count of people in frame: zero. No music, no score, no bgm. No subtitles.
```

<a id="cinematic-30"></a>
### 29. 셔터가 내려가기 전 마지막 배달

작성자 [@bmx_ai13](https://x.com/bmx_ai13) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-30#cinematic-30)** · [원본 게시물](https://x.com/bmx_ai13/status/2113727196858904605)

https://github.com/user-attachments/assets/76e5d376-58d1-47b8-8370-f06478ddaa53

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
TITLE: LAST DELIVERY BEFORE THE SHUTTER

FORMAT: 15 seconds exactly, 16:9, ultra photorealistic, 24fps, one single unbroken physical camera take from first frame to last. Zero cuts, zero hidden edits, zero transitions, zero teleportation, zero slow motion, zero static moments.

CHARACTER: Mochi, an adult female long-haired miniature dachshund with a very long low body, short muscular legs, glossy chestnut coat soaked dark by rain, floppy ears, bright amber eyes and a white star on her chest. She wears a snug bright yellow waterproof courier vest with a small zipped delivery pouch on her back and a reflective strip along her spine. She runs, she does not ride anything. Every movement is real dog behavior, real canine gait, real weight and traction, no human gestures, no cartoon expressions.

LOCATION: Crowded downtown street during a heavy evening rainstorm. Wet asphalt mirroring neon storefronts, red taxi tail lights, buses, umbrellas, gutters overflowing, wind pushing sheets of rain sideways.

CAMERA: Handheld FPV style gimbal rig flying at dog height, aggressive banking, extreme foreground parallax, rain droplets hitting and streaking across the lens, constant acceleration, shallow depth of field with bokeh from headlights.

0 to 3 seconds: Begin in violent motion. Mochi's front paws slap through a deep puddle as she leans hard around a wet street corner, ears flying back, claws scrabbling for grip on painted lane lines. The camera skims inches off the asphalt beside her paws, rolls up along her long body, and whips around her shoulder as a bus and taxis roar past in a blur of light.

3 to 6 seconds: A taxi door suddenly swings open from the curb. Mochi skids, back legs sliding sideways, then ducks low and threads underneath the opening door with her belly almost touching the water. The camera executes a fast 270 degree orbit around her, scraping past the dripping door edge and a parked car mirror, then snaps back alongside her as she accelerates.

6 to 9 seconds: TWIST ONE. A gust rips the pouch zipper open and the waterproof envelope flips out, spinning into the wind above the bike lane. Mochi stops for a split second, eyes locking on it, then launches into a full sprint after it as loose cardboard sheets tumble across the lane. She hops over a broken drainage grate, the camera plunging inches above her racing legs, then swinging upward as a passing bus throws a huge curtain of water across the street.

9 to 12 seconds: TWIST TWO. Mochi bursts through the spray with the envelope now clamped carefully in her mouth, ears soaked flat. A startled pigeon flock explodes off a ledge across her path and she weaves through them low and fast. She scrambles up a low curb ramp toward a small glowing bakery where an elderly shopkeeper in a cardigan is pulling down the metal shutter against the storm. The camera sweeps around her, revealing the warm storefront reflected across the flooded pavement.

12 to 15 seconds: TWIST THREE. Mochi drops into a long belly slide across the wet tiles, her long body skimming like a sled under the descending shutter edge, and pushes the envelope into the shopkeeper's hands just in time. He laughs in surprise, opens it, and pulls out a single small dog biscuit wrapped in paper, the delivery was addressed to her all along. He drops the biscuit, she catches it midair. The camera violently swings around his hands and her face, then rockets backward out into the rain as the shutter slams shut and rainwater explodes off the pavement, leaving the glowing gap of light under the shutter.

PHYSICS AND REALISM: Authentic canine anatomy and gait, real paw slip and recovery on wet surfaces, water shaking off fur, believable rain interaction, natural human reactions from pedestrians stepping aside and pointing. No superhero movement, no impossible jumps, nothing exaggerated. Ordinary reality made unbelievably cinematic.

AUDIO: Diegetic only. Heavy rain drumming on awnings and car roofs, paws slapping puddles, claws scraping asphalt, taxi door thunk, bus engine roar and hiss of the water curtain, pigeon wings flapping, short excited panting and one happy bark, shopkeeper's warm surprised laugh, rattling metal shutter crash. No music, no score.

LAST FRAME: Wide pulled back view of the rain soaked street, the closed bakery shutter glowing with a thin line of warm light beneath it, Mochi's silhouette visible through the gap, rain streaking across the lens. No on screen text, no titles, no captions, no logos, no watermarks, no signage readable in frame.

NEGATIVE: No cuts, no transitions, no slow motion, no freeze frames, no bicycle, no dog walking upright, no human like dog hands, no cartoon look, no distorted legs, no extra limbs, no morphing fur, no floating objects, no text.
```

<a id="cinematic-31"></a>
### 30. 바위 해안을 따라가는 보트 추적샷

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-31#cinematic-31)** · [원본 게시물](https://x.com/shikoba_86/status/2107845433938653337)

https://github.com/user-attachments/assets/f6ebb40a-7aa4-415f-bda5-454b90951e41

**프롬프트:**

```text
Use the start image as the opening frame and preserve the same coastal location.

Create one continuous shot only.
No cuts.
No multishot.

The shot starts calm and still at dusk.

Then the camera turns toward the sea.

Two boats appear far in the distance and race quickly toward the camera across the water.

The boats grow rapidly larger as they approach.

When they pass close to the camera, the camera immediately follows them in the same uninterrupted shot as they continue racing fast along the coastline.

Maintain the geography of the original location throughout the entire camera movement.

The shoreline, cliffs and bay must remain recognizable while the camera changes direction and begins tracking the boats.

Sound: quiet sea ambience at first, followed by approaching engines, water spray and rushing wind.
No background music.
No captions.
```

<a id="cinematic-32"></a>
### 31. 밤거리 위로 떠오르는 금 간 바이올린

작성자 [@NigelWatsonTFTC](https://x.com/NigelWatsonTFTC) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-32#cinematic-32)** · [원본 게시물](https://x.com/NigelWatsonTFTC/status/2111149088569766380)

https://github.com/user-attachments/assets/58698afb-2b87-4d55-bfe3-b38e6e715d7a

**프롬프트:**

```text
A street musician sits alone on wet pavement at night under a single streetlight. He plays a violin. The violin slowly cracks and falls silent. As the pieces break, they lift into the air and reassemble into floating, glowing shards that continue the melody. Slow continuous camera move, rain and neon reflections stay consistent. Emotional, restrained, 20 seconds.
```

<a id="cinematic-33"></a>
### 32. 해안 도시로 떨어지는 달

작성자 [@FlyAIgh](https://x.com/FlyAIgh) · 25초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=cinematic-33#cinematic-33)** · [원본 게시물](https://x.com/FlyAIgh/status/2115849741925781584)

https://github.com/user-attachments/assets/ac0b0bfb-d749-487b-a480-d25228ae3c2e

**프롬프트:**

```text
A coastal city at dusk. Realistic disaster-film look, 16:9 widescreen framing, a huge sense of scale. 25 seconds in total, five shots. No main characters, only a few small passers-by in the distance.

Shot 1 (0 to 5s, wide, slow push-in): a seafront boulevard at dusk, palm trees moving in the sea breeze, the sea still calm. On the horizon the moon is three times its usual size and still slowly growing. The camera pushes forward slowly from low on the boulevard. A few passers-by stop and look up at the moon.

Shot 2 (5 to 10s, close, hard cut): a parked car at the roadside. A raindrop on its roof starts to float upward, then gravel, leaves and drink cans leave the ground one after another and drift slowly skyward. A lamppost gives off a metallic hum.

Shot 3 (10 to 15s, extreme wide, hard cut): the moon now fills half the sky, its craters and rifts sharp. The sea is pulled up by the moon's gravity, the whole surface bulging upward into a leaning wall of water at the edge of the city, ships lifted into the air.

Shot 4 (15 to 21s, tracking, hard cut): weightlessness grows stronger. Cars on the street leave the ground one after another and tumble upward, billboards tear off the rooftops, palm trees are pulled out by the roots. The camera moves like a drone, threading between the floating cars and rising higher and higher.

Shot 5 (21 to 25s, looking up, hard cut): the camera stops among the floating debris and looks straight up. The craters fill the frame and keep coming closer, the ridges in the shadows clearly visible, until the lunar surface fills the frame completely.

Sound: waves and wind at the start. When weightlessness begins, a rising low hum drowns out everything. Metal creaks as the cars leave the ground. At the end only a huge low rumble, then sudden silence. No background music.

No subtitles, no watermark.
```

<a id="action"></a>
## 🥊 액션과 추격

> 격투, 파쿠르, 카체이스, 스턴트. 대부분 샷 단위로 짰습니다. · 28개

<a id="action-01"></a>
### 33. 불꽃이 남는 두 장면 초능력 격투

작성자 [@itxabdullaa](https://x.com/itxabdullaa) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-01#action-01)** · [원본 게시물](https://x.com/itxabdullaa/status/2108154459268448461)

https://github.com/user-attachments/assets/e6461762-b378-4272-9323-c647bd0f569e

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
SCENE 1 — MICIN KUAHKARI: SUPREME SPEED
10s | 16:9

Premium Hollywood live-action, ultra-photorealistic, grounded physics, practical destruction, cinematic lighting. Semi-CGI only for extreme speed, motion trails and crimson-black flames. No anime, cartoon, game CGI or plastic skin.

@image_1 = EXACT MICIN KUAHKARI REFERENCE. Preserve face, identity, proportions, wardrobe, accessories and katana exactly. Male. No redesign.

CONTINUITY: Start directly inside the previous scene's gigantic crimson-black flame burst. No reset, location change or time jump.

00:00–00:02
Micin blitzes through soldiers: elbow → spinning kick → knee strike. Extreme acceleration, realistic impacts and short motion trails.

00:02–00:04
Three soldiers attack. Micin ducks, punches one into another, launches upward and lands an aerial spinning kick to another's face. 0.3–0.5s slow motion only at impact, then full speed.

00:04–00:06
Extreme-speed katana draw. Micin clearly says “Moyase.” Crimson-black flames instantly erupt across the blade. Immediate forward launch.

00:06–00:08
High-speed katana rampage: horizontal slash → direction change → upward slash → aerial slash → landing slash → dash through formation. Huge crimson-black flame arcs, realistic enemy reactions and debris. No posing.

00:08–00:10
Micin spits thick crimson-red liquid onto the flaming blade. Flames violently expand. He delivers one devastating forward slash. A gigantic crimson-black flame burst destroys the formation and fills the frame.

END MID-ATTACK. No pose, freeze or fade.

CAMERA: medium-wide → close impact → rear 3/4 → side blitz → katana close-up → low-angle flame burst.

SCENE 2 — MICIN KUAHKARI: CRIMSON AFTERBURN
10s | 16:9

Same style and exact @image_1 character. Begins DIRECTLY from Scene 1's flame-filled final frame. No reset or location change.

00:00–00:02
Micin bursts through the flames attacking: flaming slash → reverse slash → elbow → flaming thrust.

00:02–00:04
Enemy launches upward. Micin follows instantly: horizontal slash → reverse slash → spinning kick → downward katana strike. Realistic gravity, no teleportation.

00:04–00:06
Landing slash → duck behind attack → flaming elbow → torso slash → enemy crashes through battlefield debris.

00:06–00:08
Debris launch → zig-zag blitz → horizontal slash → reverse → upward slash → aerial slash → downward slash → katana thrust. Massive crimson-black flame arcs.

00:08–00:10
Two formations attack from opposite sides. Micin blitzes through the gap and bursts out the other side. Two huge crossing flame arcs remain behind him.

Brief silence.

DELAYED IMPACT: BOOM — BOOM — BOOM.

Soldiers, dust, concrete and sparks explode outward as Micin continues advancing.

END MID-MOVEMENT. No pose, freeze or fade.

CRITICAL: Relentless continuous combat. Every attack flows into the next. No idle frames, slow walking, repetitive swings, teleportation, floaty movement or choreography resets.
```

<a id="action-02"></a>
### 34. 복면 특수부대의 원테이크 야간 급습

작성자 [@iamrealsnow](https://x.com/iamrealsnow) · 23초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-02#action-02)** · [원본 게시물](https://x.com/iamrealsnow/status/2115300539902869533)

https://github.com/user-attachments/assets/72738013-ab9b-4824-a06a-77d866bda27c

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Duration: Exactly 23 seconds | Aspect ratio: 16:9 | Style: Ultra photorealistic, next level military action.

Create a relentless covert special forces operation in a war-torn Middle Eastern city at night. Six elite masked commandos wear premium matte-black and desert-tan tactical armor, angular full-face ballistic masks, dark mirrored visors, high-cut helmets, night-vision optics, communication headsets, reinforced plate carriers, tactical gloves, and detailed military equipment. Their appearance is intimidating, sophisticated, and consistent. Each carries a realistic modern military rifle with optics, weapon light, and suppressor.

ACTION, 0–23 SECONDS: From the very first frame, the squad sprints through a narrow dusty street as incoming gunfire strikes the walls around them. The camera tracks backward smoothly as the masked leader signals an immediate advance. The team takes cover behind concrete barriers, returns controlled fire, and pushes forward through thick smoke. Without interrupting the movement, the camera swings alongside the operators as they rush through a damaged entrance into a fortified courtyard. Sparks, concrete fragments, dust, and muzzle flashes fill the scene. One operator provides cover while the others advance in tight formation. Armed hostiles appear ahead, triggering an intense firefight. The leader signals the final push, and the squad moves together across the courtyard toward an armored extraction vehicle. In the final seconds, the operators board rapidly as the vehicle accelerates into the dust-filled darkness under incoming fire. End with the vehicle still moving and the operation visibly in progress.

CAMERA: One continuous, fluid tracking take for all 23 seconds. Natural handheld energy with professional stabilization, realistic camera inertia, clear spatial continuity, uninterrupted operator movement, and consistent screen direction. No cuts, no transitions, no scene changes, no time jumps, no missing frames, no frozen poses, no slow motion, no speed ramps, no filler, and no unnecessary close-ups.

CINEMATIC REALISM: Photorealistic faces concealed by masks, highly detailed armor textures, authentic fabric movement, physically plausible recoil, realistic weapon handling, volumetric dust, harsh muzzle flashes, moonlit architecture, deep shadows, natural motion blur, powerful engine sounds, gunfire, radio chatter, and immersive cinematic sound design.

STRICT NEGATIVES: No character morphing, no duplicated soldiers, no changing masks, no costume alterations, no floating weapons, no deformed hands, no teleportation, no flickering, no stuttering, no abrupt camera jumps, no artificial frame interpolation artifacts, no logos, no subtitles, and no title cards.

PRIORITY: Continuous action, stable character identity, premium tactical costumes, coherent movement, and maximum cinematic intensity from the first frame to the last.
```

<a id="action-03"></a>
### 35. 7개 샷으로 엮은 파우더 스키 영상

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-03#action-03)** · [원본 게시물](https://x.com/minchoi/status/2111471581461426236)

https://github.com/user-attachments/assets/f4df3e4a-2c29-42ce-a608-cfabe6055ca5

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
A 30-second, seven-shot ski film edit of Kai <Character reference> skiing one steep, untracked mountain face at golden hour, cut together from several real cameras: a drone, a helmet-mounted action camera, an action camera on a pole, a camera planted in the snow, a chase skier and a long lens across the valley. Photoreal action-sports look, real speed, hard cuts on the action, no slow motion. Kai: athletic man in his 20s, red insulated ski jacket, black ski pants, black gloves, white helmet, mirrored orange goggles, black poles, twin-tip skis. Same outfit and gear in every shot, exactly as in the character sheet. Same mountain face, same powder, and the low sun always on his left as he skis down, throwing long blue shadows across the snow. Shot 1 (0-4s), drone: high aerial view of a sunlit ridge and the whole golden face below it. Kai, small in frame, drops in off the ridge and carves his first big turn, a plume of powder behind him. The drone pushes forward and tilts down to follow. Hard cut. Shot 2 (4-8s), helmet cam: first-person view from an action camera on his helmet, ultra-wide with curved edges. His ski tips and pole baskets at the bottom of the frame, snow rushing underneath, the horizon tilting hard left and right with each carve, powder spraying across the lens. Hard cut. Shot 3 (8-12s), pole cam: an action camera on a short pole held out in his left hand, ultra-wide, pointing back at him. His goggles and helmet fill one side of the frame, his body leaning into a turn, the mountain and sky swinging behind him, snow flecks stuck to the lens. He lets out a wordless shout into the wind. Hard cut. Shot 4 (12-17s), planted cam: a camera set low in the snow just below a wind-lip, pointing up at the sky. Kai launches off the lip and flies straight over the lens, skis crossing the low sun, snow raining down onto the camera, then he lands out of frame behind it. Hard cut. Shot 5 (17-21s), chase skier: a camera on a handheld stabiliser, skiing a few metres behind him at the same speed. He drops into a tuck and straight-lines the fall line, spray from his tails hitting the lens, the slope streaking past. Hard cut. Shot 6 (21-25s), long lens: a telephoto shot from across the valley, slightly shaky, compressing the slope. Kai lays a huge carve and throws a wall of powder backlit gold by the sun. Hard cut. Shot 7 (25-30s), low static camera at the bottom of the run: he skis straight at the lens and skids a hard hockey stop right in front of it, a sheet of snow blasting the camera. As it clears, he pushes his goggles up onto his helmet, breathing hard and laughing. Look: every action-camera shot ultra-wide and crisp with curved edges, small lens flares and snow on the lens; the drone and long-lens shots clean and natural. Warm low sun, long blue shadows, glittering ice crystals in the spray, natural colour, real motion blur. Sound, in stereo, loud and up front like real action-camera audio, never quiet: constant wind roaring and buffeting the camera mics, gusting harder as he picks up speed; the crunch of snow under his skis as he drops in; friends whooping and yelling "Go!" from the ridge at the start; the hiss, scrape and chatter of his edges biting the snow on every carve; poles planting with a crisp crunch; powder spraying off his tails with a soft roar; his hard breathing, and a grunt on the landing; a loud whoosh and the clack of skis as he flies over the planted camera, then the thud of the landing; distant ravens calling across the valley; the ripping sheet of snow blasting the lens on the hockey stop, then his panting laugh and his friends cheering from up the slope. A driving instrumental track with punchy drums sits low underneath, cut on the beat, never covering the natural sound. No subtitles.
```

<a id="action-04"></a>
### 36. 한 문장으로 만든 멀티샷 드리프트

작성자 [@minchoi](https://x.com/minchoi) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-04#action-04)** · [원본 게시물](https://x.com/minchoi/status/2104743218722267597)

https://github.com/user-attachments/assets/6b20ad98-42e8-4951-9504-f041145eb7f6

**프롬프트:**

```text
Generate a multi-shot car drifting action scene.
```

<a id="action-05"></a>
### 37. 6개 샷 야시장 스파이 추격

작성자 [@minchoi](https://x.com/minchoi) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-05#action-05)** · [원본 게시물](https://x.com/minchoi/status/2104743085087560174)

https://github.com/user-attachments/assets/6f278a10-89e6-4bd8-8493-f6d59ccb1084

**프롬프트:**

```text
"Multi-shot spy-thriller chase through a night market, 15 seconds, 6 shots with hard cuts, fast and relentless. [Cole]: early 30s, short dark-brown hair, clean-shaven, tailored charcoal suit, white shirt open at the collar, no tie. [Anton]: late 30s, ash-blond buzz cut, short blond beard, black leather jacket, dark grey henley. A packed night-market lane after rain: food stalls, red paper lanterns, string lights, grill smoke, steam, wet pavement reflecting the lights. Anton always runs toward frame right; Cole chases him. Shot 1 (0–2s): Telephoto close-up of Cole standing still in the moving crowd, shoppers blurring past in the foreground, eyes locked on something off-screen right. Shot 2 (2–4.5s): The camera whip-pans right along his eyeline and snaps sharp onto Anton under a red stall sign reading "DUMPLINGS". Anton sees Cole, drops his paper cup and bolts right. Shot 3 (4.5–7s): Fast side tracking shot racing alongside at full sprint, both men running frame right: Anton shoving shoppers aside, Cole ten metres behind and closing, string lights streaking past. Shot 4 (7–9.5s): Low angle: Anton yanks a stack of fruit crates down behind him and oranges spill across the wet ground; Cole leaps the crates in one stride, suit jacket flaring, lands hard and keeps running. Shot 5 (9.5–12.5s): Cole bursts into a crossroads of lanes beneath a stall sign reading "HOT TEA" and stops dead, breathing hard. Anton is gone. The camera orbits slowly halfway around Cole, circling past his left side to end over his shoulder, as he scans the crowd. Shot 6 (12.5–15s): Close on Cole. His eyes snap left and the camera whip-pans left, landing sharp on Anton climbing a metal stairway above the stalls, glancing back. Cole sprints out of frame after him. Gritty handheld spy-thriller look, anamorphic, shallow depth of field, teal shadows with warm amber lantern light, motion blur from speed only. No dialogue: pounding footsteps, crates crashing, oranges rolling, sizzling grills, crowd gasps, a pulsing percussion score with low brass stabs."
```

<a id="action-06"></a>
### 38. 스케이트파크 30초 로우 트래킹

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-06#action-06)** · [원본 게시물](https://x.com/minchoi/status/2111471588256207357)

https://github.com/user-attachments/assets/43d9f61d-d9c4-4716-b9c3-8dfafa4342f0

**프롬프트:**

```text
30-second continuous low tracking shot of a skateboarder in a concrete park at golden hour. Large dynamic motion, realistic weight and physics.[Skater]: young man, early 20s, faded red T-shirt, black shorts, short hair. Consistent face and outfit.0–6s: He rides toward camera, pushes once, centers his weight. Camera tracks low beside the board.6–12s: He approaches a set of stairs. Knees bend, weight shifts back. Board rises on the tail.12–18s: He clears the stairs. Wheels leave the ground. Cloth and hair react to the motion. He lands with knees absorbing impact.18–24s: He rolls out, slight speed check, then carves hard left. Camera stays locked low and follows.24–30s: Final wide as he rides away into the warm light, board still under him.Natural late-afternoon sun, long shadows, realistic dust and board sound. No slow motion unless specified. Preserve exact clothing and face.
```

<a id="action-07"></a>
### 39. 홀로 성문을 지키는 기사

작성자 [@AiwithBloodline](https://x.com/AiwithBloodline) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-07#action-07)** · [원본 게시물](https://x.com/AiwithBloodline/status/2112796958045896801)

https://github.com/user-attachments/assets/e56d21e2-0e5a-45fc-9970-fe737c7e9ca2

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Create a photorealistic medieval battle sequence featuring a lone male knight defending the entrance to an ancient stone fortress. The scene must resemble a premium Hollywood historical film, with realistic armor, physically accurate movement, natural lighting, and consistent character identity.
Character reference: Use the uploaded knight image as the strict visual reference. Maintain the same helmet, silver plate armor, dark-blue cloak, sword, shield, and body proportions throughout the video.
0–5 seconds: The knight stands alone in front of a massive fortress gate. Wind moves his dark-blue cloak as dust drifts across the stone courtyard. The camera slowly pushes toward him.
5–10 seconds: A line of armored soldiers emerges through the distant dust. The knight raises his shield and positions his sword defensively. Sunlight glints naturally off the edges of his armor.
10–15 seconds: The first opponent charges. The knight blocks the incoming sword strike with his shield, pivots, and pushes the opponent backward. His armor moves naturally with his body.
15–20 seconds: Two more opponents approach from opposite directions. The knight turns to face them, maintaining a defensive stance. The camera tracks around the combatants while preserving spatial continuity.
20–25 seconds: The knight deflects another strike and forces the opponents to retreat. Dust rises from their boots as they move across the courtyard.
25–30 seconds: The knight lowers his shield slightly and turns toward the fortress gate as it begins to open behind him. Warm sunlight spills through the opening, illuminating his armor and revealing reinforcements arriving inside the fortress.
Audio: No music. Metal armor clanking, swords colliding, boots striking stone, wind, distant battle ambience, and natural breathing.
Negative prompt: Cartoon armor, inconsistent weapons, changing character appearance, extra limbs, floating swords, graphic gore, dismemberment, exaggerated fighting, unrealistic physics, background music, text, watermark.
```

<a id="action-08"></a>
### 40. 아파트 세 공간을 관통하는 맨손 격투

작성자 [@boke_ai](https://x.com/boke_ai) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-08#action-08)** · [원본 게시물](https://x.com/boke_ai/status/2112740231497859258)

https://github.com/user-attachments/assets/2dca28bc-debe-49cd-8a0b-7c9b48c6e24b

**프롬프트:**

```text
SCENE: three places in one continuous bare-handed fight, each change of place triggered by a body crashing through something: an apartment corridor, then the cramped entrance hall of an apartment full of scattered shoes, then a concrete outdoor stairwell high above the street.
CAST: two women, one in a plain grey sweatshirt, the other in a plain navy sweatshirt.
CAMERA:
- Corridor (0-4s): over the grey fighter's shoulder as the navy fighter rushes her with a flurry of punches, fluorescent white light, apartment doors flashing past.
- The grey fighter's back slams through a half-open apartment door; the camera whip-pans with the impact, the motion blur carrying us into the entrance hall.
- Entrance hall (4-8s): three fast angle changes, one from floor level among the shoes, as they wrestle; the door chain swinging; a shoe spinning through the air past the lens. Warm yellow bulb light.
- A focus pull from the swinging door chain in the foreground to the navy fighter's face as she catches her breath for half a second.
- The camera pushes straight through a hanging coat on the coat hook as both women tumble through a second door onto the outdoor stairwell.
- Stairwell (10-15s): grey daylight, wind, the street far below; the camera drops from above as they fight down the stairs, then a crash zoom on the final throw.
MOTION RULES:
- Every place change happens exactly on an impact; the world gets bigger with each one: a door, then a wall of shoes and coats, then open sky.
- In the corridor the rush runs at five strikes per second; in the entrance hall it becomes grappling and elbows in the tight space; on the stairwell it becomes leaps from landing to landing.
- The navy fighter leaps down a whole flight of stairs feet-first; the grey fighter sidesteps, pivots 180 degrees mid-sprint and suplexes her onto the landing: the single maximum hit, one-third speed for half a second, the railing shuddering, dust blasting off the concrete.
- The grey fighter starts laughing in the middle of the fight and her strength drains for a moment; the navy fighter gains the upper hand until the suplex turns it back.
Impacts come in three tiers. Normal hits: a two-frame hold, a jump in brightness, a two-to-four-frame camera jolt, sleeves and hair trailing 0.1 seconds behind. Heavy hits: a three-frame dead stop, then sweat, dust or water bursts radially from the contact point, a six-frame hard shake, the struck body carried by momentum, fabric settling 0.4 seconds later. One maximum hit only: the whole frame flashes toward white, radial blur spreads from the contact point, and the surroundings break.
```

<a id="action-09"></a>
### 41. 추락하며 코드로 흩어지는 사이버 암살자

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-09#action-09)** · [원본 게시물](https://x.com/EndFolding79421/status/2111076586514489818)

https://github.com/user-attachments/assets/e44476a8-d8e0-44d4-adea-1c2edc15777b

**프롬프트:**

```text
A cyber-assassin leaps off a skyscraper [tracking shot from above]. She disintegrates into glowing code mid-fall and reappears on a rooftop across the city.
```

<a id="action-10"></a>
### 42. 70년대 서부극 살롱 난투

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 13초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-10#action-10)** · [원본 게시물](https://x.com/EndFolding79421/status/2112376857773428953)

https://github.com/user-attachments/assets/34288cf4-59df-46da-bb4e-acc12b603560

**프롬프트:**

```text
cinematic widescreen. Gritty 1970s Western film aesthetic with weathered textures, natural film grain, dusty smoky saloon atmosphere, worn wood, dirty period clothing, sweat and grime on faces. Warm practical saloon lighting mixed with dusty window light, automatically balanced so faces remain clearly visible. Two rugged Old West cowboys are involved in a rough, untrained, knock-down-drag-out saloon fistfight following an accusation of cheating during a poker game.IMPORTANT CAMERA AND ACTION RULES: Keep facial shots close or extremely close throughout the sequence. Avoid distant views of faces. Use aggressive Spaghetti-Western close-ups, tight medium shots, over-the-shoulder angles and low angles. Rapidly change camera positions to increase intensity while keeping every physical action readable. No martial arts. No kicking. No elaborate blocking. No modern boxing combinations. The men fight like angry, rough frontier cowboys: big swinging haymakers, body punches, grabbing shirts, ducking punches, shoving, staggering and crashing into furniture. Every strike must have a clear attacker, impact and physical reaction.[Shot 1] 00:00.000-00:03.000Extreme low-angle close-up looking upward at Cowboy 1, a mean, ugly, weather-beaten frontier cowboy in his late 40s, with a battered hat, heavy stubble, crooked nose, deeply lined face and an angry scowl. He looms over the camera, staring furiously toward Cowboy 2 just off-screen. His jaw tightens and his eyes narrow.(S1, Cowboy 1): <d>[English] did you call me a cheat?</d>Hold briefly on his hostile expression after the question. Background saloon patrons remain indistinct and out of focus.[Shot 2] At 00:03.000CUT sharply to a tight over-the-shoulder angle as Cowboy 2 suddenly steps in from off-screen and throws a huge looping right-hand haymaker directly into Cowboy 1's jaw. The punch visibly connects. Cowboy 1's head snaps sideways and his upper body staggers hard into the wooden bar. Glasses jump and rattle from the impact. No defensive block; the punch lands cleanly.[Shot 3] At 00:05.500CUT to a tight waist-up side angle. Cowboy 1 immediately surges back angrily and drives one heavy fist into Cowboy 2's stomach. The body punch visibly lands. Cowboy 2 folds forward around the fist with a harsh grunt, momentarily losing his breath.[Shot 4] At 00:08.000CUT to a close over-the-shoulder angle behind Cowboy 1. Cowboy 1 grabs Cowboy 2 by the front of his shirt with one hand, jerks him upright and swings another huge fist toward his face. Cowboy 2 suddenly ducks underneath it. Cowboy 1's fist clearly sweeps through the empty space directly above Cowboy 2's head.[Shot 5] At 00:10.500CUT immediately to a tight low-angle shot from beside Cowboy 2. As Cowboy 1 is still recovering from the missed swing, Cowboy 2 rises explosively and lands a massive upward right-hand punch squarely on Cowboy 1's jaw. Clear fist-to-jaw impact. Cowboy 1's face and shoulders whip backward from the force.[Shot 6] At 00:12.500CUT to the widest shot of the sequence, but remain close enough that both men's bodies and reactions stay visually clear. Cowboy 1 stumbles violently backward from the punch, crashes hip-first into a wooden poker table and falls backward across it. The table collapses beneath him with a tremendous wooden crack; cards, poker chips and glasses scatter across the floor. Cowboy 2 remains in the foreground, breathing hard with fists still raised.End on Cowboy 1 sprawled amid the broken table while Cowboy 2 stands over him ready for the fight to continue. This should feel like only the first brutal exchange of a much longer old-fashioned Western saloon brawl.overall_soundscape:Full synchronized saloon sound. Low background murmur before the fight, subtle poker chips and glasses, wooden floorboards creaking under boots. Cowboy 1's spoken accusation is clear and foregrounded. Each punch has a heavy, realistic old-fashioned movie fist impact accompanied by appropriate grunts and breath reactions. Boots scrape hard across wooden floorboards during staggering movement. Glasses rattle when Cowboy 1 hits the bar. Clothing strains during the shirt grab. Final collision produces a loud wooden table crack, scattering poker chips, cards and glassware, followed by the clatter of debris across the wooden floor. Background patrons react with startled shouts but do not enter or interfere with the fight.non_diegetic_music:No music. The tension and intensity come entirely from dialogue, saloon ambience, breathing, fist impacts, movement and the final furniture crash.
```

<a id="action-11"></a>
### 43. JSON으로 쓴 창고 격투

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-11#action-11)** · [원본 게시물](https://x.com/EndFolding79421/status/2112376857773428953)

https://github.com/user-attachments/assets/b1124a33-735f-4d85-b02d-eb229dafd7cf

**프롬프트:**

```text
{ "subject": "a woman in tactical gear fighting a masked attacker in a warehouse", "scene": "abandoned warehouse with flickering lights and crates stacked around", "camera": { "movement": "handheld, following the action tightly", "angle": "eye-level", "framing": "close-up with fast motion blur" }, "action": "the woman parries a strike and delivers a spinning kick to the attacker’s chest", "motion": "fast, fluid, brutal hand-to-hand combat", "style": "gritty, realistic, low-light action", "mood": "urgent, raw, high-stakes" }
```

<a id="action-12"></a>
### 44. 네온 야시장 파쿠르 탈출

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-12#action-12)** · [원본 게시물](https://x.com/EndFolding79421/status/2110790580678574391)

https://github.com/user-attachments/assets/4d43d55c-d77c-4cfa-a0c0-291dab7cb22e

**프롬프트:**

```text
{ "subject": "A free-runner in a hooded jacket and sneakers vaults over street stalls and flips off a neon sign, pursued by two security guards close behind.", "scene": "A crowded neon night market with steam from food carts, hanging lanterns, and flickering holographic ads.", "camera": "Handheld shaky cam following at shoulder height for 4 seconds as he runs and vaults, then whip-pan to show him flipping off the sign and disappearing down an alley in the last second.", "style": "Urban kinetic parkour, dynamic lighting with neon reflections in puddles, motion blur on jumps." },
```

<a id="action-13"></a>
### 45. 위에서 본 나선계단 칼싸움

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-13#action-13)** · [원본 게시물](https://x.com/EndFolding79421/status/2110790580678574391)

https://github.com/user-attachments/assets/ab66189b-05c7-4145-838c-3612b020a655

**프롬프트:**

```text
Two figures fight on a spiral staircase [top-down rotating shot]. Sparks from clashing blades light their faces as the camera spins faster around the stairwell.
```

<a id="action-14"></a>
### 46. 달리는 지하철 안 격투

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-14#action-14)** · [원본 게시물](https://x.com/EndFolding79421/status/2110785773456838793)

https://github.com/user-attachments/assets/77745bd8-c7b0-472b-99dc-acb161ffc0f3

**프롬프트:**

```text
Inside a speeding subway car, a woman in a blood-smeared trench coat fights off three attackers with brutal efficiency. The lights strobe as the train barrels into a dark tunnel.
```

<a id="action-15"></a>
### 47. SUV가 머리 위로 넘어가도 꿈쩍 않는 남자

작성자 [@kaanakz](https://x.com/kaanakz) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-15#action-15)** · [원본 게시물](https://x.com/kaanakz/status/2107204923146321922)

https://github.com/user-attachments/assets/b1eed132-4dfa-4c37-a550-fa6089add324

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
[Generation Goal]
Generate a vertical 9:16 cinematic commercial video in one continuous locked-off take. The core subject is a man who remains seated and stoic while a black rugged off-road SUV launches over him and lands behind him, with a thick dust cloud engulfing the frame before settling.

[Reference Asset Roles]
image-ref, is used only for the man's facial features, short curly brown hair, blue eyes, skin texture, and overall likeness. Do not use the navy suit, white shirt, or blue patterned tie from the image; replace the clothing completely with the specified casual attire.

[Subjects and Relationships]
The man maps exclusively to image-ref, for face and head only. He wears an all-black casual jacket and trousers with sand/tan boots. He sits perfectly still in a small folding camp chair at the exact center of the field. There is one black rugged off-road SUV (Land Rover Defender / Ford Bronco-style with round LED headlights). The man never moves from his chair or changes posture except for the subtle hand and arm motions required to smoke.

[Event Script]
At the start: Ultra-low ground-level camera, static tripod, eye-level with the soil, symmetrical one-point perspective, centered medium-wide full-body framing. The man sits in the camp chair in the middle of a freshly plowed red-brown dirt field, stoic and deadpan, relaxed posture, hands resting on his lap. He holds a cigarette between his fingers and actively smokes throughout, taking slow casual drags and gently exhaling visible smoke. The black SUV appears far in the background at the end of the field.

Principal event: The SUV charges toward the camera, kicking up a huge orange dust cloud. It launches airborne, wheels off the ground, and flies directly over the seated man and the camera. It lands behind him and brakes hard. A thick orange dust wall engulfs the frame; the truck stops inches behind the man with headlights blazing through the dust (strong bloom, lens flare, volumetric god rays). The dust slowly settles, revealing the truck parked right behind him with high beams still on; the man remains completely untouched and continues smoking.

At the end: The truck and man are silhouetted as the frame slowly fades to black, leaving centered empty space for an end-card logo.

[Maintain Consistency]
Keep the man's identity and face from image-ref, all-black casual jacket and trousers with sand/tan boots, exact centered seated position, camp chair, continuous smoking action, single SUV, spatial relationships (truck always ends behind the man), and the continuous locked-off camera. Never allow the man to flinch, stand, or change expression beyond the subtle smoking motions. No clothing from the reference image may appear.

LOCATION: Open agricultural farmland with rows of green crops on the horizon, power line on the left, overcast sky with soft clouds at the top of frame, golden hour.

LIGHT: Low-angle golden hour sunlight diffused by dust and overcast clouds, soft contrasty natural light, strong backlight from the truck headlights (warm white, 5000K) cutting through dust, rim light on the man's silhouette, atmospheric haze, Tyndall effect, specular highlights on the truck body.

COLOR GRADE: Teal-and-orange cinematic grade, saturated terracotta orange dust, deep red-brown soil, desaturated gray-blue sky, crushed blacks, rolled-off highlights, subtle film grain, slight vignette, high dynamic range.

MOTION/FX: Practical dust and debris simulation, slight camera shake only at the moment of the jump/impact, 180° shutter motion blur on the truck, particles flying toward the lens. Heavy low-frequency engine roar and landing thud, then silence.

Style: Hollywood car commercial, high-energy yet calm hero shot, hyper-realistic, sharp detail. Cinema camera with 24–35mm wide-angle lens, shallow-to-medium depth of field (~f/2.8), subject and truck sharp, background slightly soft with natural lens compression.
```

<a id="action-16"></a>
### 48. 은행 강도를 막는 청소부

작성자 [@MayorKingAI](https://x.com/MayorKingAI) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-16#action-16)** · [원본 게시물](https://x.com/MayorKingAI/status/2104974109050535941)

https://github.com/user-attachments/assets/484adb1c-a61e-4e0c-8116-d7a5383c8cf7

**프롬프트:**

```text
High-octane cinematic action-comedy, gritty realistic thriller look, teal & orange grade,
subtle film grain, fast-paced editing.
Interior of a modern bank, polished marble and glass, cold fluorescent + window light.
Terrified hostages kneeling with hands behind their heads, heads bowed against the wall.

Shot 1 (0-4s): wide handheld shot, tense. Three masked robbers wave guns and shove people.
Robber 1 (shouting): "Nobody moves! Fill the bag, now!"
Robber 2 (kicking a chair): "Down! Stay down!"

Shot 2 (4-8s): slow dolly-in on a thin old Chinese janitor calmly mopping, unbothered.
He mutters: "So much noise for a Tuesday." His eyes narrow — calculation.
He flicks the wet mop; water splashes across a robber's visor.

Shot 3 (8-9s): whip-pan. Robber 3 spins: "Sit down, gramp—"
The mop handle cracks across his jaw mid-word. Impact freeze, bass hit.

Shot 4 (9-16s): explosive continuous martial-arts sequence, escalating. He vaults over
the counter, disarms Robber 1 with a spinning mop strike, sends the gun sliding across
marble. Hand-to-hand blur: elbow, sweep, a robber crashes through a glass partition
in slow-motion shards. He kicks a rolling office chair into the third, springboards off
the desk, and takes him down in a fast combo. Orbiting dynamic camera, quick cuts,
snap-zooms, brief slow-mo on each impact, debris and papers flying.

Shot 5 (16-18s): the three robbers groaning, sprawled among broken glass and scattered cash.
Wide low-angle hero shot, the janitor standing calm, mop over his shoulder.

Shot 6 (18-20s): he wrings out the mop and resumes cleaning.
Old man (deadpan): "Now I have to mop again." Static medium shot. Camera settles.

Lighting: cold realistic base, rim light on the janitor during the fight, hard shadows,
sparks and dust catching the light.
Audio: fearful murmurs, tense silence before the first hit, bone-crunch impacts, whooshes,
glass shatter, driving percussive music surging through the fight.
Constraints: no watermark, no on-screen text, no logos, keep the janitor's face and
outfit consistent across shots.
```

<a id="action-17"></a>
### 49. 절벽 사찰 테라스의 쿵푸 대결

작성자 [@yourPlugAI](https://x.com/yourPlugAI) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-17#action-17)** · [원본 게시물](https://x.com/yourPlugAI/status/2105587110639985048)

https://github.com/user-attachments/assets/51a4edee-d59b-451a-8c7a-641395de6626

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
[ENGINE DIRECTIVE]
Generate a single continuous 20-second fast-paced, high-velocity photorealistic live-action kung fu fight sequence using Kling 4.0 Flash at 35mm sports-cinema quality in 16:9 horizontal format. Maintain 100% strict visual consistency with the provided asset sheets: "Mei" (Female student, slate-blue linen tunic, leather bracers, high braided bun) and "Master Zhen" (Grandmaster, silvering hair topknot, layered ochre and mahogany silk robes, dark ebony staff). Setting strictly follows "Cliffside Stone Courtyard at Dawn". Style: High-speed aggressive martial arts choreography, fast shutter speed, sharp directional motion blur, realistic weight and momentum transfer, zero slow-motion, zero anime look, continuous high kinetic energy.

[AUDIO DIRECTIVE]
• MUSIC: High-tempo, intense traditional Asian combat score with rapid taiko drum rolls, aggressive wooden percussion, fast-paced guzheng plucks, and energetic rhythm.
• SOUND DESIGN: Sharp high-velocity staff air-swoshes, aggressive cloth snaps, heavy leather bracer impact clangs, cracking stone footwork, swirling leaves.

[TIMELINE BREAKDOWN]

00:00 - 00:03 | HIGH-SPEED PALM THRUST & RAPID LEAF SWEEP
• VISUAL: Dynamic low-angle tracking shot moving rapidly across the wet flagstones.
• ACTION: Begin mid-action at maximum speed. Mei explodes forward with a rapid palm thrust; Master Zhen swiftly redirects her arm with a high-velocity flick of his ebony staff. His staff sweeps low across wet flagstones at high speed, violently blasting fallen red maple leaves into a swirling vortex.
• SOUND: Rapid taiko drum roll, sharp staff swish, explosive leaf scatter sound.

00:03 - 00:06 | RAPID THREE-PUNCH FLURRY & AGGRESSIVE DODGE
• VISUAL: Close-quarters handheld tracking camera with fast whip-pans.
• ACTION: Mei instantly steps inside his guard, launching a rapid three-punch flurry. Master Zhen executes lightning-fast head slips and torso evasions, dodging her blows by millimeters while maintaining aggressive forward leverage.
• SOUND: Rapid fabric snapping, heavy breath exhales, fast leather bracer friction.

00:06 - 00:09 | EXPLOSIVE PILLAR REBOUND & STAFF IMPACT
• VISUAL: Wide-angle pursuit tracking shot following her leap.
• ACTION: Mei sprints and wall-drives off a wooden pavilion pillar, launching into a high-speed downward kick. Master Zhen snaps his ebony staff up horizontally with both hands, blocking her kick with a violent impact that vibrates the staff and showers red maple leaves outward.
• SOUND: Heavy wooden impact clang, cracking timber recoil, fast wind whiplash.

00:09 - 00:12 | FAST PALM TRAPPING & SASH WHIP-SPIN
• VISUAL: Fast 360-degree orbital camera tracking the close-quarters exchange.
• ACTION: Mei lands and accelerates into a rapid palm-trapping sequence. Master Zhen parries every strike with aggressive wrist deflections before hooking her waist sash with his staff, aggressively spinning her across the wet courtyard floor.
• SOUND: Rapid leather-on-wood parry clangs, whipping silk fabric snaps, surging drum pulse.

00:12 - 00:15 | HIGH-VELOCITY BALUSTRADE REBOUND & MOMENTUM LOCK
• VISUAL: Low-angle crash zoom tracking her spring-back motion.
• ACTION: Mei plant-kicks off a stone balustrade, springing straight back toward him like an arrow. Master Zhen steps inside her trajectory, catching her wrist mid-thrust and driving his staff into the stone floor, forcefully halting her momentum with a sharp jolt.
• SOUND: Sharp boot impact on stone, sudden high-pitched impact ring, abrupt pause.

00:15 - 00:18 | HIGH-TENSION INCH-CHECK & FAST RELEASE
• VISUAL: Tight medium close-up tracking their intense facial expressions and rapid breathing.
• ACTION: High tension. Mei's palm rests suspended one inch from his ochre silk chest robe, completely checked by his firm wrist lock. Mei yields rapidly, stepping back into an aggressive stance; Master Zhen releases her wrist with a swift, decisive step back onto two feet.
• SOUND: Heavy combat exhales, fast cloth rustle, quiet wind.

00:18 - 00:20 | RAPID COMBAT BOW & FINAL FROZEN FRAME
• VISUAL: Center-framed shot settling into a crisp final freeze-frame.
• ACTION: Both fighters snap into a fast classical martial stance. Red maple leaves settle quickly onto the damp stone floor as Mei and Master Zhen perform a rapid, crisp palm-and-fist bow under the morning light. Final frozen frame.
• SOUND: Final sharp taiko strike fading into ambient ocean wind.
```

<a id="action-18"></a>
### 50. 도쿄 옥상 8컷 파쿠르

작성자 [@Ayu_AI_0912](https://x.com/Ayu_AI_0912) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-18#action-18)** · [원본 게시물](https://x.com/Ayu_AI_0912/status/2104860921051168859)

https://github.com/user-attachments/assets/6fac4e7b-db4e-41b8-9e38-5dca34c4f094

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
15秒、16:9、8カット構成のシネマティックな超上級パルクール映像。
主人公は image_1
 の人物。
添付画像をキャラクターデザインの参照として使用し、髪型、髪色、服装、配色、年齢感、体格、全体の雰囲気を全カットで一貫して維持すること。
舞台は快晴の現代日本の都市。
東京、渋谷、横浜を思わせる屋上、路地、階段、手すり、配管、コンクリート壁を舞台に、主人公が世界トップレベルのフリーランニングを披露する。
【カット1｜00:00〜00:01.60】
ローアングル後方追従。
主人公が一気に加速し、腰ほどの高さの障害物をコングヴォルトで飛び越える。
【カット2｜00:01.60〜00:03.40】
正面ローアングル。
ウォールランからティックタックを決め、向かいの屋上へジャンプして着地する。
【カット3｜00:03.40〜00:05.20】
横方向トラッキング。
プレシジョンジャンプで細い足場へ着地し、そのままキャットリープで高い壁へ飛びついて登る。
【カット4｜00:05.20〜00:07.20】
屋上追従ショット。
ダッシュヴォルトで障害物を越え、そのままウェブスターで屋上の隙間を飛び越える。
【カット5｜00:07.20〜00:09.20】
俯瞰移動カメラ。
ダイブロールで着地の衝撃を吸収し、そのまま長い手すりをスピードヴォルトで攻略する。
【カット6｜00:09.20〜00:11.30】
正面から後退するハンドヘルド撮影。
アンダーバーで低い障害物を通過し、その直後にサイドフリップで次の障害物を越える。
【カット7｜00:11.30〜00:13.20】
後方斜め上からのドローン撮影。
パームスピンからコングヴォルトへ滑らかにつなぎ、最後のジャンプへ向けて全力で加速する。
【カット8｜00:13.20〜00:15.00】
クライマックス。
大きな屋上の隙間へ向かって跳躍し、高く美しいコークスクリューを決める。
カメラは空中で主人公の周囲を回り込む。
正確に着地した後、そのままスピードを落とさず画面奥へ走り去る。
【映像スタイル】
実写映画品質。
世界大会レベルのフリーランニング。
リアルな重心移動。
自然な筋肉の動き。
リアルな着地衝撃。
髪や衣装が風や動きに合わせて自然に揺れる。
背景は鮮明に保ち、高速移動中のみ自然なモーションブラーを使用する。
【禁止】
人物の雰囲気や服装が大きく変化すること。
髪型や配色の不自然な変化。
顔や身体の崩れ。
手足の増殖。
分身。
身体の融合。
貫通。
電線を通過すること
ワープ。
浮遊。
不自然な着地。
アニメ調。
CG調。
```

<a id="action-19"></a>
### 51. 사무라이 사극 예고편

작성자 [@NigelWatsonTFTC](https://x.com/NigelWatsonTFTC) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-19#action-19)** · [원본 게시물](https://x.com/NigelWatsonTFTC/status/2111445384128069747)

https://github.com/user-attachments/assets/5cb59a76-e602-45e6-82c9-560ba73da603

**프롬프트:**

```text
VAGABOND — Epic Historical Samurai Drama — Cinematic Movie Trailer

[VISUAL STYLE LOCK]
Ultra-realistic, premium live-action, large-scale historical samurai film trailer.
A lost 1960s–1970s Japanese epic, rediscovered and restored as a legendary masterpiece of chanbara cinema.
The setting is feudal Japan in a violent era of war, wandering swordsmen, shattered clans, monastery courtyards, mountain roads, rice fields under storm clouds, bamboo forests, burning villages, river crossings, castle towns and lonely shrines.
The atmosphere is savage, philosophical, mournful, intimate and transcendent.
Everything must feel lived-in, ancient, human and physically real.
No fantasy powers, no exaggerated anime stylization, no glossy superhero action. Sword combat must feel terrifyingly fast, human, messy and final.
Balance raw violence with moments of meditative stillness and existential loneliness.

[CINEMATOGRAPHY LOCK]
Shot on ARRI Alexa XT with vintage anamorphic lenses and a rich 35mm Kodak film aesthetic.
Soft haze, muted natural color palette, earthy browns, rain-soaked blacks, pale sky tones, subtle grain, slight vignette, soft bloom and optical imperfections.
Composition should feel painterly yet immediate: wide landscapes, low-angle silhouettes, deep environmental staging, intimate close-ups of eyes, hands, fabric, wounds and blade edges.
Use handheld camera in combat, restrained dolly movement in contemplative scenes, sudden crash zooms, whip-pans and impact vibration during moments of violence.
Lighting is entirely naturalistic: dawn mist, dusk firelight, overcast daylight, candlelit interiors, sun filtered through trees, rain reflecting on steel.

[MUSIC AND EDITING LOCK]
Create a 30-second high-intensity cinematic trailer with a strong dramatic arc.
The score should begin sparse and ceremonial, then escalate into a thunderous rhythmic climax.
Use a score built from taiko drums, low bowed strings, biwa or shamisen textures, shakuhachi breaths, deep sub-percussive impacts, strained choral tones and a rising ominous tonal bed.
The first 8–10 seconds should feel tense and mythic, with space and breath.
The middle section should accelerate through rhythmic drum patterns and layered percussion.
The final 8 seconds should explode into rapid, beat-synced montage and overwhelming emotional force.
Every musical hit should correspond to a blade clash, footstep, body movement, cut, reveal or emotional glance.
Include one short suspended silence before the final rush.
No spoken dialogue is required, though one brief whispered line may be used if helpful: “Strength… is born in solitude.”
If text appears on screen, keep it minimal and elegant.

[CHARACTER LOCK]
The central figure is MIYAMOTO MUSASHI, early twenties, raw and untamed.
He has long dark hair loosely tied, a weathered and severe face, intense dark eyes, a lean but powerful physique, dirt and scars across his skin, and the aura of a man becoming a myth through violence.
His clothing is rough, worn and practical: weather-beaten kimono layers, travel cloth, rope ties, sandals, mud and blood.
He must remain visually consistent across all scenes: feral, restless, solitary, frighteningly alive.

Supporting figures:
- OTSU: graceful, emotionally luminous, quietly tragic, a grounding human presence amid violence.
- SASAKI KOJIRO: elegant, haunting, serene and lethal, the beautiful shadow waiting at the far end of Musashi’s journey.
- INSHUN: a disciplined warrior monk, fierce and calm, representing skill refined into spiritual force.

These figures should appear briefly but memorably, with clear visual distinction and emotional weight.

[THE TRAILER]
BLACK.
A low wind.
One distant taiko strike.

A wide shot of morning mist over a field of fallen bodies.
The camera slowly pushes in.
Musashi kneels among the dead, covered in mud and blood, breathing like an animal.

HARD CUT ON THE NEXT STRIKE.

Extreme close-up: Musashi’s hand tightening around a sword hilt.
CUT.

Feet splashing through rainwater.
CUT.

A blade flashes through frame.
CUT.

Musashi charges across a battlefield under gray skies.
CUT.

A still image of Otsu watching him from a temple veranda, sorrow in her eyes.
CUT.

A bamboo grove.
Two blades collide with shocking speed.
The camera whips violently as Musashi duels Inshun among bending stalks.

The rhythm builds.

CUT.
Musashi walking alone down a mountain road at dusk.
CUT.
A village burning at night.
CUT.
A close-up of Musashi’s face, rain and sweat running down his skin.
CUT.
A riverbank at dawn: Kojiro stands in pale blue-gray light, silent, elegant, almost unreal.

Half-second of near silence.

Then the score erupts.

Rapid montage synchronized tightly to the percussion:
Musashi shouting as he swings downward.
A body collapsing into mud.
Sword steel clashing in torchlight.
A temple gate thrown open.
Musashi running through falling rain.
Otsu reaching out but failing to stop him.
Kojiro turning his head slowly toward camera.
A close-up of a blade edge catching white sunlight.
Musashi standing on a ridge, alone against the sky.
A final violent duel fragment in bamboo, shot handheld at close range.
A last close-up: Musashi’s eyes, exhausted but burning with destiny.

BLACK.

Weathered title lettering appears:
VAGABOND

Then a second line, smaller:
THE PATH OF THE SWORD

One last drum impact.
Silence.

[FINAL PRODUCTION LOCK]
This is a fictional live-action film trailer for Vagabond, presented as a rediscovered 1970s samurai epic of enormous artistic prestige.
Preserve the spirit of classic Japanese cinema, brutal realism, poetic solitude and mythic character transformation.
Prioritize physical sword choreography, muddy historical texture, emotional gravity, severe beauty and rhythmic editorial intensity.
The heart of the trailer is the transformation of a wild young killer into a legendary swordsman through suffering, solitude and relentless combat.

Use sharp percussive edit points, low-frequency drum impacts, breathy shakuhachi phrases, strained strings and one overwhelming final crescendo. The music must feel ancient, martial and tragic rather than conventionally triumphant.
FINAL PRIORITY: beat-synced percussion editing, authentic chanbara atmosphere, tactile realism, emotionally charged close-ups and the sense of a lost cinematic masterpiece.
```

<a id="action-20"></a>
### 52. 네온 우주항 1인칭 외계인 슈터

작성자 [@aymducking](https://x.com/aymducking) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-20#action-20)** · [원본 게시물](https://x.com/aymducking/status/2117008462701810159)

https://github.com/user-attachments/assets/8dc2be0b-87b5-4474-8939-6fc187e82fff

**프롬프트:**

```text
15-second 16:9 1080p first-person gameplay recording of a competitive sci-fi alien-invasion shooter, squad vs. alien horde, captured from a PC screen. Next-gen graphics: rainy neon night, crisp PBR, wet reflective surfaces, high frame rate. The player’s purple armored gloves hold an original white-chrome plasma rifle with glowing hot-pink and teal energy coils, lower right of frame; rain beads and sizzles into steam on the hot coils. He wears a jetpack; teal thruster glow and rain-mist trails at frame edges when boosting. HUD off: only a small green crosshair. Snappy movement with peeks, strafes, jetpack boosts and precise flicks. One continuous fight, no cuts.

Setting: neon-drenched futuristic cliffside spaceport above a dark canyon during a heavy rainstorm at night, original map. Black-glass hangars with magenta and cyan neon strips, landing pads with pulsing teal edge lights, cargo shuttles, hover-crates, fuel canisters, catwalks, a glass sky bridge, radar dishes, flickering holographic signs of abstract shapes. Purple storm clouds, lightning flashes, puddles mirroring neon, rain streaking through light beams, drifting fog.

Enemies are original alien creatures: tall, slick, four-armed insectoid aliens with bioluminescent acid-green veins and glowing eyes, some with leathery wings. They spit green plasma bolts and leap or glide between platforms. When hit they burst into glowing green goo and sparks.

[00:00–00:02] He strafes out from a hover-crate and drops an alien at the hangar entrance with a plasma burst; it ragdolls in a splash of glowing green goo that hisses on the wet ground.
[00:02–00:04] Wide-swings around a shuttle as green plasma bolts streak past through the rain and two-taps an alien crawling behind its landing gear, neon sparks scattering.
[00:04–00:06] Shoots a fuel canister beside an alien on a catwalk; a magenta fireball with an expanding cyan energy ring blasts it off, rain flash-evaporating into a steam cloud.
[00:06–00:08] Jetpacks up to a higher pad through sheets of rain and swaps energy cells mid-air with a glowing steam puff, a lightning bolt lighting the sky behind.
[00:08–00:10] Two winged aliens swoop up out of the canyon; he taps one mid-air, it shrieks, wings shredding into green embers, and spirals down into the canyon.
[00:10–00:11] Throws a plasma grenade that sticks to a radar dish and detonates in a pink-white shockwave with electric arcs crackling across the wet metal, launching the second alien.
[00:11–00:13] Two aliens charge across the glass sky bridge; he boosts sideways and taps both down as glass cracks and neon reflections shatter across it.
[00:13–00:15] Wave cleared. Alone at the pad’s edge in the pouring rain, he looks down at the glowing canyon as lightning flashes, then inspects his rifle with a flip animation, coils pulsing and steaming.
Style: authentic high-skill gameplay footage caught on stream, confident clean play, stable camera with natural bob, recoil and jetpack sway. Heavy VFX: volumetric neon light shafts through rain, rain droplets on the lens edges, lens flares, chromatic glow bloom, particle sparks, energy trails, heat distortion, glowing goo splatter, electric arcs, steam and fog. No text, logos, watermark or IP characters, creatures, weapons or maps.
Audio: heavy rain and thunder, electric plasma bursts, wet sizzling impacts, alien shrieks and clicks, spitting plasma bolts, jetpack whooshes, footsteps splashing on metal and glass, deep explosion booms, crackling electricity, grenade beep, steam-hiss reload, short wave-cleared sting. No dialogue.
```

<a id="action-21"></a>
### 53. 몬순 폭우 속 슈퍼히어로 추격

작성자 [@bmx_ai13](https://x.com/bmx_ai13) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-21#action-21)** · [원본 게시물](https://x.com/bmx_ai13/status/2113620690129862944)

https://github.com/user-attachments/assets/0800ef2f-88e3-45a7-a6fb-5d4cea5a3b7c

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
TITLE: MONSOON VELOCITY

FORMAT: 20 seconds, 16:9, 24fps, photoreal live-action superhero action, anamorphic lens feel, handheld chase camera with whip pans, heavy motion blur on the speedster only. Pure text to video, no on-screen text, no logos, no subtitles at any point.

WORLD: A monsoon evening in a dense South Asian city. Narrow wet street between old pastel colonial buildings with iron balconies, hanging shop signs blurred and unreadable, rickshaws parked, tangled overhead wires, steam rising from a tea stall. Light rain falls steadily. Sodium orange streetlamps and cyan neon spill reflections across ankle-deep puddles. Color grade: teal shadows, warm amber highlights, wet glossy surfaces.

CHARACTERS:
NIRA, the speedster. Mid 20s South Asian woman, athletic, long black hair tied in a high braid, sleek charcoal grey running suit with thin copper seams, bare forearms, calm fierce eyes. When she moves at speed she leaves a crackling copper-crimson energy trail with small electric sparks, never gold.
THE ASHEN MONK, the rival. Tall lean man in layered ash-grey wrap robes, deep hood, cloth mask covering nose and mouth, leather wrist bindings, barefoot. Moves with martial calm. He can phase into a burst of grey smoke and reappear a few meters away.

SHOT LIST:
0 to 2s. Wide low angle down the rainy street. Pedestrians with umbrellas in the background. The Ashen Monk stands still in the middle of the road, rain bouncing off his hood. Far behind him a copper streak ignites at the end of the street.
2 to 4s. Time slows. Every raindrop freezes in midair like suspended glass beads. Nira runs through them in real speed, her body shattering the frozen drops into glittering spray, copper trail crackling behind her. Camera tracks beside her at shoulder height.
4 to 6s. Impact. Nira tackles the Monk at full speed. Both bodies fly sideways and slam into the hood of a parked white car, the metal crumples, windshield cracks into a spiderweb, water sheets off the roof in a wave.
6 to 8s. Tight close up, handheld shake. The Monk grabs her braid and twists. Nira's face strains, sparks jump from her skin. He bursts into grey smoke in her hands and she falls through empty air onto wet asphalt.
8 to 10s. Over the shoulder of the Monk as he reforms beside a crumbling plaster wall, smoke curling off his robes, eyes narrowing above the mask. Behind him puddles ripple outward as something approaches too fast to see.
10 to 13s. Nira circles him at super speed, a ring of copper light spinning around the Monk, the rain inside the ring spiraling upward into a vortex. Rickshaw canopies flap, shop shutters rattle, a tea glass tips off the stall and hangs frozen midair.
13 to 15s. The Monk throws a sharp palm strike into the ring. It connects. Nira is knocked out of speed, skidding on one knee across the flooded road, a wake of water spraying behind her, copper sparks hissing in the puddle.
15 to 17s. Low angle on Nira rising, rain streaming down her face, she exhales, lowers into a sprinter crouch. The asphalt under her fingertips glows hot and steams.
17 to 19s. She launches. One continuous blur of copper light straight at the Monk. He tries to phase but too late. She drives him backward into the plaster wall. Massive impact, the wall cracks outward in a radial web, brick dust and rainwater explode together in a dense cloud, a balcony above shakes and drips.
19 to 20s. LAST FRAME. Locked wide shot. Dust settling in the rain. A Monk shaped crater in the wall, empty, wisps of grey smoke drifting out of it. Nira stands in front of the crater breathing hard, copper sparks fading off her hands, back to camera, staring left down the street where a faint smoke trail disappears. Hold still. No text, no title card, no letters, no signage legible anywhere in frame.

AUDIO, diegetic only, no music, no narration:
Steady rain hiss on tin awnings and puddles, distant rickshaw bells, a tea kettle whistle. Sharp electric crackle and whoosh whenever Nira moves at speed. Near silence with single tinkling drops during the frozen rain moment. Metal crunch and glass crack on the car impact. Soft smoke whump when the Monk phases. Low rising whirlwind roar inside the speed ring. Heavy concrete crack and rumble of the wall impact, then debris trickle, rain returning, Nira's heavy breathing.

STYLE NOTES: Realistic physics for water, debris and cloth. Speed effect only on Nira, everything else stays sharp. Consistent faces and costumes in every shot. No extra superheroes, no flying, no weapons, no blood.
```

<a id="action-22"></a>
### 54. 첫 프레임에서 시작하는 카체이스

작성자 [@PromptSin](https://x.com/PromptSin) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-22#action-22)** · [원본 게시물](https://x.com/PromptSin/status/2111042032135553463)

https://github.com/user-attachments/assets/eb39781e-c763-442d-8b64-dd0e7bd9fe5b

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
15-second widescreen 16:9 photorealistic cinematic action sequence, Kling 4.0 full model, 720p, native sound. Use the supplied image as the opening-frame and vehicle-identity reference. Exactly two cars: the same red sports coupe leads and the same black sports sedan pursues. Preserve car shapes, colors, wheels and the four adult occupants throughout. Driver in each car controls the vehicle; passengers perform the fictional action-film gunfire. No pedestrians.

PACE: relentless real-time action from the first frame. No slow motion, freeze frames, speed ramps, introductory establishing shots or pauses. Believable wheel contact, steering, suspension and momentum. Maintain clear lead/pursuer relationship and forward screen direction across cuts.

0–4 SECONDS — IMMEDIATE HOOK:
Begin matching the reference, already mid-drift around a city street corner. Red coupe leads, black sedan follows close behind. Tires howl, smoke streams backward and road grit sprays. Brief gunfire from the pursuing passenger, small muzzle flashes and impacts on road or vehicle bodywork, no injuries. Low moving three-quarter tracking camera keeps both cars legible.

4–10 SECONDS — ESCALATING PURSUIT:
A fast lateral tracking shot shows both cars surging along the riverside avenue. The red car passenger briefly returns fire toward the black car; driver keeps both hands on the wheel. Alternate short readable bursts of gunfire with tire squeal, sparks from impacts and rapid lane changes. Cut to a low rear chase view as both cars drift through a second bend toward the bridge approach, red car still leading. No extra vehicles, explosions or unrelated action. Preserve geography and continuous acceleration.

10–15 SECONDS — CAMERA PASS, SMALL CREST JUMP AND LANDING:
A low roadside camera catches the red coupe then the black sedan roaring past close to camera. The camera pans to follow them rear three-quarter as they reach a small smooth convex crest on the intact bridge roadway. Show continuous unbroken asphalt across the entire crest and beyond, with intact guardrails. Each car briefly lifts its four wheels only slightly off the road over the crest, red first, black following. A short low hop, not a long aerial leap. BOTH cars visibly land back on the same asphalt by second 14, suspension compresses and rebounds, and they keep accelerating along the continuous road until the cut at second 15. Real-time speed, no slow motion. The river remains far below the intact bridge and neither car leaves the roadway corridor.

ENVIRONMENT:
Same fictional modern riverside city as reference, late-afternoon daylight, coherent shadows and reflections. The bridge is structurally intact with a continuous road surface, a gentle raised crest and visible road continuing beyond it. Stylized blockbuster stunt physics with realistic-looking cars and materials.

AUDIO:
Powerful engines with Doppler shifts, tire squeals, short cinematic gunfire, metallic impact ticks, debris, wind and brief tire lift followed by tire contact and suspension compression on landing. No dialogue, narration or music needed.

AVOID:
Slow motion, motionless cars, reversing direction accidentally, car-color swaps, shape morphing, extra cars, duplicated occupants, drivers firing weapons, excessive smoke hiding the action, gratuitous explosions, blood, injuries, text overlays, captions, visible real-world logos or watermarks.

CRITICAL ENDING: no broken bridge, missing road, chasm, ramp, fall into river, or cut while airborne. Show a modest road-crest hop, asphalt landing and continued driving.
```

<a id="action-23"></a>
### 55. 폐허 도시 프리러닝

작성자 [@DjajaYerry75](https://x.com/DjajaYerry75) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-23#action-23)** · [원본 게시물](https://x.com/DjajaYerry75/status/2114992691801215463)

https://github.com/user-attachments/assets/c979fb9e-6fbb-4b39-901d-0353ffb43827

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
JANE — WASTELAND FREERUNNING

[DURATION & RATIO]
Total duration: 30 seconds
Aspect ratio: 16:9
Resolution: 1080p
Style: Photorealistic live-action cinematic parkour
[CHARACTER & ENVIRONMENT]
The protagonist is Jane from the attached Wasteland Explorer character sheet. Preserve her exact facial identity, green eyes, brunette vintage victory-roll hairstyle, physique, weathered Fallout-style outfit, backpack, utility belts, wrist device, and rugged boots.
Use the attached wasteland environment sheet as the location reference. The setting is a vast post-apocalyptic city of collapsed highways, ruined skyscrapers, crumbling rooftops, rusted industrial structures, abandoned vehicles, broken concrete, and dust-covered alleys. Muted charcoal, rust brown, faded steel, and dusty amber sunlight.
16 rapid cinematic cuts. Jane performs elite freerunning through the ruins, maintaining continuous momentum and realistic biomechanics.
[CUT 01 | 00:00–00:01.60]
Low rear follow shot. Jane instantly accelerates and executes a kong vault over a broken concrete barrier. Grit scatters from her takeoff and landing.

[CUT 02 | .60–00:03.40]
Front low-angle tracking shot. She performs a wall-run and tic-tac against a fractured wall, jumping onto the opposite rooftop. Loose masonry crumbles beneath her push-off.
[CUT 03 | .40–00:05.20]
Horizontal tracking shot. Jane precision-jumps onto a narrow concrete ledge, performs a cat leap to a higher wall, catches its edge, and climbs up as small stones tumble below.

[CUT 04 | .20–00:07.00]
Rooftop follow shot. She dash-vaults a rusted ventilation unit, then performs a running Webster across a narrow gap, landing with bent knees and immediately sprinting onward.

[CUT 05 | .00–00:08.80]
Overhead moving camera. Jane drops into a dive roll across dusty rubble, rises without stopping, then speed-vaults over a rusted handrail. Metal rattles from physical contact.

[CUT 06 | .80–00:10.60]
Front-facing handheld retreat. She performs an underbar through a collapsed structure, then transitions directly into a sideflip over concrete debris. Fabric and backpack straps react naturally to motion.
[CUT 07 | .60–00:12.40]
Drone shot from diagonally behind and above. Jane uses a controlled palm spin around a sturdy pillar, kong-vaults a broken barrier, and accelerates toward staggered rooftop platforms.
[CUT 08 | .40–00:14.20]
Low lateral tracking shot. Jane executes three rapid precision jumps across uneven concrete platforms. Loose gravel falls from each takeoff point as she changes direction.

[CUT 09 | .20–00:16.00]
Three-quarter front tracking shot. She performs a wall spin around a damaged concrete corner and lands on a narrow elevated walkway. Dust drifts through warm sunlight.
[CUT 10 | .00–00:17.80]
Side-follow shot with strong parallax. Jane performs a lazy vault over a corroded railing, then precision-jumps onto a neighboring ledge. The railing vibrates briefly after contact.
[CUT 11 | .80–00:19.60]
High-angle descending camera. She drops from the ledge, executes a compact aerial rotation, and lands in a controlled dive roll. Dust and grit scatter as she rises into a sprint through a ruined alley.

[CUT 12 | .60–00:21.40]
Fast front three-quarter tracking shot. Jane speed-vaults a broken concrete barrier, transitions into an aerial cartwheel over scattered debris, and lands running toward an industrial rooftop.
[CUT 13 | .40–00:23.20]
Drone shot descending from behind. Jane traverses a narrow rusted rail with controlled balance, jumps to a lower platform, and performs a corkscrew-style aerial rotation over a clear landing zone.
[CUT 14 | .20–00:25.00]
Low-angle tracking shot. Jane sprints up a sloped concrete slab, plants one foot against a sturdy wall, rebounds into a backflip, and lands on a broad platform. A collapsed highway gap appears ahead.

[CUT 15 | .00–00:27.50]
Climactic side-follow shot transitioning into a controlled camera orbit. Jane takes three powerful strides and launches across the major rooftop gap, executing a high corkscrew aerial. Brief selective speed ramp at the apex. She lands firmly on the opposite rooftop; dust and loose gravel burst outward from the impact.
[CUT 16 | .50–00:30.00]
Low front tracking shot transitions into a wide rear view. Jane converts her landing into a sprint, vaults one final piece of rubble, and runs deeper into the ruined city. The camera swings behind her, revealing collapsed highways and skeletal skyscrapers. End with Jane still running at full speed.
[CHOREOGRAPHY & PHYSICAL VFX]
Chain every movement through momentum: takeoff, flight, contact, recoil, landing, recovery, acceleration. Use realistic center-of-gravity shifts, planted feet, accurate grips, and believable airborne trajectories.

Dust, grit, gravel, rust flakes, falling masonry, vibrating rails, and flexing sheet metal must originate from actual contact or disturbed structures. Environmental damage accumulates and never resets between shots. Debris follows gravity. Preserve realistic physical weight.
Dynamic tracking, low-angle follow shots, aerial camera movement, strong parallax, natural motion blur at high speed, and subtle impact camera shake. Keep stunt movements readable and maintain consistent spatial direction.
Audio: diegetic ambience only—wind through ruins, boots on concrete, gravel impacts, metal rattles, fabric movement, and distant structural creaks. No background music.

[STRICT NEGATIVES]
No character identity or outfit changes. No hairstyle changes, face distortion, duplicate bodies, extra limbs, clipping, warped anatomy, teleportation, levitation, impossible mid-air direction changes, weightless landings, or unexplained destruction. No magic aura, energy beams, shockwave rings, spatial rifts, or artificial afterimage duplicates. No passing through solid objects or electrical wires. No anime, video-game rendering, or obvious CGI.
Final result: A relentless, physically grounded 30-second wasteland parkour showcase with escalating acrobatics, environmental cause-and-effect, cinematic camera choreography, and a spectacular rooftop-gap finale.
```

<a id="action-24"></a>
### 56. 사막의 복면 전사 결투

작성자 [@fromjtown](https://x.com/fromjtown) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-24#action-24)** · [원본 게시물](https://x.com/fromjtown/status/2112974523670638644)

https://github.com/user-attachments/assets/6188e50e-dafe-43c2-9ead-3c0d19331693

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
HYPER-KINETIC DESERT COMBAT — 30-SECOND CINEMATIC SEQUENCE

WARRIOR — FIRST REFERENCE IMAGE: Use the exact masked tribal warrior with red-and-black wrapped dreadlocks, metallic ornaments, skull-covered shoulders, muscular build, layered black armor, wrapped forearms, bone accessories, distressed red-and-black hanging garments, and rugged footwear. Preserve his exact appearance and costume throughout the sequence.

DARK REAPER — SECOND REFERENCE IMAGE: Use the exact hooded supernatural reaper with flowing, tattered black robes, glowing molten-orange cracks, fiery skeletal details, and an enormous curved flaming scythe. Preserve the same silhouette, weapon design, and spectral appearance throughout the sequence.

VISUAL STYLE: Hyper-kinetic desert combat spectacle, extreme high-intensity CGI action, thick volumetric cinematic haze, golden-hour dust storms, aggressive anamorphic 35mm lens, heavy motion blur, relentless handheld tracking, whip pans, deep shadows, heat distortion, ultra-realistic particle systems.

0–4s — EXTREME WIDE CRASH-IN

Instant violent collision. The tribal warrior explodes forward through a dense dust cloud, his tattered red garments whipping violently. The dark reaper swings its massive flaming scythe in a wide horizontal arc. The impact detonates a shockwave of sand and embers. No pause.

4–8s — DYNAMIC LOW TRACKING

Rapid exchange. The warrior ducks beneath the scythe, delivers a spinning elbow to the reaper’s ribs, then an upward knee. The reaper phases partially out of existence, reforms mid-strike, and counters with a spectral claw rake across the warrior’s chest. Fabric, sparks, ash, and dust explode outward.

8–13s — ORBITING MEDIUM + DUTCH ANGLE

Acrobatic mid-air clash. The warrior vaults off the scythe shaft, his tattered red garments fully extended, and lands a dual-fist hammer blow against the reaper’s hood. The reaper retaliates with a vertical scythe slam that cracks the ground. The warrior rolls and rises into a spinning back-kick that shreds the reaper’s robe into black ribbons.

13–18s — HANDHELD CLOSE-COMBAT FRENZY

Brutal ground scramble. The warrior grapples the scythe pole, headbutts the reaper’s shadowed hood, then unleashes three distinct strikes: an upward palm, a horizontal elbow, and a downward axe-kick. The reaper absorbs the attacks before unleashing a tendril-whip of living shadow that lashes the warrior’s back, drawing blood and dust.

18–23s — SLOW-MOTION IMPACT MONTAGE

Escalating power. The warrior catches the scythe mid-swing, twists, drives a knee into the reaper’s midsection twice, then delivers a spinning heel kick that sends the figure airborne. The reaper crashes down in an explosion of ash and sand, its robes partially dissolved. The warrior advances without mercy.

23–28s — WIDE TO TIGHT PUSH-IN

Finishing sequence. The warrior seizes the collapsing reaper by its remaining hood, delivers a savage rising uppercut followed by a final two-handed overhead smash. The reaper’s entire form shatters into swirling black ash and ember particles that scatter across the desert floor. The warrior stands over the dissipating cloud, breathing hard.

28–30s — HARD-CUT REVERSE EXTREME CLOSE-UP

The blurred tribal warrior fills the foreground, chest heaving, sweat and dust streaking his mask, mouth open in ragged breath. In sharp focus in the deep background, the dark reaper slowly reconstitutes from residual ash. Its enormous flaming scythe reforms in its hand as it rises and begins stalking forward with predatory stillness.

FINAL QUALITY REQUIREMENTS

Photorealistic, ultra-detailed fabric physics and particle simulation, precise character consistency, physically convincing combat, coherent anatomy and proportions, realistic weapon interactions, intense fire and shadow effects, perfect motion blur, maximum-density volumetric haze, cinematic color grading, and movie-level VFX polish.
```

<a id="action-25"></a>
### 57. 1차 대전 복엽기 공중전

작성자 [@PromptSin](https://x.com/PromptSin) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-25#action-25)** · [원본 게시물](https://x.com/PromptSin/status/2112499136620810684)

https://github.com/user-attachments/assets/7f41914e-bd77-46c8-b04b-e11f7566ec52

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Create a 10-second photorealistic World War I aerial pursuit, horizontal 16:9, using the supplied image as the exact opening frame.

AIRCRAFT AND CONTINUITY
Exactly two single-seat biplane fighters throughout. The burgundy aircraft with black cross markings is the pursuer, nearest the camera. The olive aircraft with roundels is the target, ahead and slightly lower. Preserve their reference designs, colors, markings, wing structures, rigging, open cockpits, pilots and fixed landing gear. They fly in the same direction, with the olive aircraft leading at all times.

0–3 SECONDS — IMMEDIATE ACTION
Continue directly from the reference without a static hold. Both propellers spin rapidly. The olive aircraft banks hard left and descends toward a gap between clouds. The burgundy aircraft immediately banks left in pursuit and fires one short machine-gun burst forward from its nose-mounted guns. Brief muzzle flashes and a few thin, fast tracer streaks pass behind the target without hitting it.

3–7 SECONDS — DIVING PURSUIT
The olive aircraft steepens its descending turn along the edge of a cloud. The burgundy aircraft follows the same curved flight path several aircraft lengths behind, firing one more brief burst before ceasing fire. Wisps of vapor sweep past; the distant fields and river move rapidly across the background. Both aircraft remain identifiable, with clear separation and no complete cloud occlusion.

7–10 SECONDS — LOW SWEEP AND PULL-OUT
Both aircraft emerge below the cloud edge. The olive aircraft smoothly levels its wings and pulls out of the dive; the burgundy aircraft follows a moment later. The camera drops slightly behind and below the pursuer, revealing both planes racing forward over the landscape. End mid-pursuit with both aircraft intact and the olive plane still ahead.

CAMERA
One continuous airborne tracking shot starting at the supplied rear three-quarter viewpoint. The camera follows the burgundy aircraft smoothly while keeping the olive target visible ahead. Subtle airframe-like vibration, strong background parallax, readable silhouettes. No cuts, teleportation, reverse angles or slow motion.

PHYSICS AND LOOK
Real-time motion, convincing weight, aerodynamic banking and smooth pull-out. Aircraft turn through banked flight, never skid sideways, hover or fly backward. Consistent sunlight, photorealistic weathered fabric, wood, metal and taut rigging. Natural propeller motion blur and cinematic cloud depth. No modern jet-like speeds or maneuvers.

AUDIO
Continuous period piston-engine roar, rushing wind and two short synchronized machine-gun bursts from the burgundy pursuer. Engine pitch rises during the dive. No music, dialogue or narration.

AVOID
Extra aircraft, swapped pursuer and target, changing markings, morphing wings, missing rigging, extra propellers, detached wheels, missiles, jets, lasers, fireballs, collisions, crashes, visible injuries, repeated loops, frozen opening, text, subtitles, logos or watermarks.
```

<a id="action-26"></a>
### 58. 1950년대 흑백 경찰 추격

작성자 [@PromptSin](https://x.com/PromptSin) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-26#action-26)** · [원본 게시물](https://x.com/PromptSin/status/2113216352832061872)

https://github.com/user-attachments/assets/3d1be610-2a47-4b13-b25c-04992d9ddd6a

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
15-second horizontal 16:9 photorealistic black-and-white police pursuit, filmed as a tense 1950s crime movie. Use the supplied opening image as the first frame and the supplied ending image as the final composition. Animate a coherent physical chase; do not dissolve or morph between still images.

CONTINUITY: Exactly two early-1950s American sedans: the dark getaway sedan with its distinctive split chrome grille, and the black-and-white police sedan with white doors, star badge and single roof beacon. Preserve both reference designs and drivers. Same empty wet warehouse district at night, period streetlamps and brick buildings.

0–4s — IMMEDIATE ACTION: Begin in the opening composition, already moving fast. The dark sedan rounds the wet corner, throwing water from its tires. The police follows the same turn a few car lengths behind. Low front three-quarter tracking camera retreats ahead of them. Engines roar, a period siren wails, tires squeal. Realistic suspension roll, wheel rotation and forward momentum.

4–8s — OVERTAKE: Cut to a moving side view with both vehicles visible. On the straight, the police accelerates up the getaway car's left side, draws level and clearly overtakes. Show the full passing maneuver with space between the vehicles. Water spray and streetlamp reflections emphasize speed.

8–12s — INTERCEPTION: Once safely ahead at a broad intersection, the police brakes and swings into a tight controlled turn across the escape route. The getaway brakes hard. Show the police turning and the getaway decelerating together in a wide shot. Tire squeal, spray and suspension compression. No collision or teleportation.

12–15s — ENDING: The getaway stops short. Settle into the ending reference's elevated sidewalk three-quarter view: dark sedan at left, angled police sedan at right blocking its route, both intact with a clear gap between them. Hold this composition for the final second as spray settles and engines idle. Drivers remain inside. Headlights and roof beacon remain active.

LOOK: True monochrome, rich blacks, luminous wet-road reflections, hard film-noir lighting, restrained 35mm grain, realistic metal and glass. Fast action at normal speed, decisive cuts and clear spatial continuity.
AUDIO: Engines with natural pitch changes, period siren, tire squeal and water spray. No music, dialogue or narration.
AVOID: Color, sepia, modern objects, extra cars, pedestrians, swapped vehicle identities, disappearing cars, deformed wheels, impossible acceleration, collisions, explosions, gunfire, slow motion, dissolves, text, subtitles and watermarks.
```

<a id="action-27"></a>
### 59. 핸드헬드로 찍은 창고 스턴트 격투

작성자 [@SilentNightX97](https://x.com/SilentNightX97) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-27#action-27)** · [원본 게시물](https://x.com/SilentNightX97/status/2111489279767761391)

https://github.com/user-attachments/assets/cbf9df31-630b-4395-9950-aca8d40137e7

**프롬프트:**

```text
Cinematic 15-second realistic action stunt fight scene, ARRI Alexa 32mm lens, shallow-to-deep depth of field, handheld camera with natural shake and occasional whip pans, natural warehouse lighting with dusty skylight beams, cool desaturated grade with warm lamp accents, subtle motion blur, practical stunt realism, no wire-work, no CGI enhancement.

SETTING: Large dusty warehouse, metal shelving stacked with boxes and wooden pallets, concrete floor with scattered debris, shafts of light cutting through a high window.

0-2s: Wide static shot with slight push-in. Two men in their late 20s stand facing each other, breathing hard, sweat on their foreheads, fists raised. Dust floats in the light beams.
Man A (low, steady, dangerous): "Last chance. Walk away."
Man B (grinning, out of breath): "You first."

2-5s: Handheld medium shot at a 45° angle. Man A lunges forward with a straight right punch — Man B slips it, blocks with his forearm, counters with a body shot into A's ribs. A grunts, twists away. Real physical impact, natural body weight, feet planted with realistic footwork, no floating motion.

5-8s: Low-angle wide shot at ground level. Man B throws a knee — Man A jumps back, B pivots and drives an elbow into A's shoulder, shoving A hard into a metal shelving unit. The shelf rattles, boxes shift. Camera shakes on impact.

8-11s: Handheld close-up with slight Dutch angle. Man A grabs Man B by the collar and slams him against the wall — dust puffs from the concrete, boxes tumble off the shelf and crash to the floor. Man B grabs A's throat in return, both grappling, breathing ragged, faces inches apart, real strain in their arms and necks.

11-13s: Whip pan with a speed-ramp into 0.5x slow motion. Man A lands a sharp elbow strike to Man B's jaw. Man B's head snaps back, his body spins and he crashes down onto a stack of wooden pallets — real impact, real weight, pallets crack and shift, dust bursts up around him.

13-15s: Static wide shot with a slow push-in. Man B lies on the pallets, chest heaving, one hand twitching. Man A stands over him, shoulders rising and falling, blood at the corner of his mouth, dust settling around them both in the light beam. Fade to black.

NATURAL REALISM: realistic fight choreography with proper weight transfer and momentum, natural footwork, real physical contact and impact recoil, realistic skin texture with sweat and dirt, natural micro-expressions of pain and exhaustion, natural English dialogue with lip-sync, ambient warehouse sound — echoing footsteps, metal rattling, boxes crashing, heavy breathing, no stiff movement, no robotic motion, no cartoon physics, no over-choreographed wire-fu.
```

<a id="action-28"></a>
### 60. 바위 해안의 연쇄 폭발

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=action-28#action-28)** · [원본 게시물](https://x.com/shikoba_86/status/2107845437705097483)

https://github.com/user-attachments/assets/982b15c3-e02d-4e80-ab14-1810130e4e27

**프롬프트:**

```text
Use the start image as the exact opening frame and preserve the identity of the coastal location: the rocky shoreline, small beach, calm bay, dirt path on the right, wooden posts in the foreground water, distant pier, and the large rock wall across the cove.

Create a cinematic multi-shot environmental destruction sequence.

The scene begins calm and still at dusk.

A sudden bright impact appears in the distance near the far side of the cove.

A powerful explosion erupts along the rocky coastline, throwing debris, dust, smoke and water high into the air.

The shockwave spreads across the bay. The water reacts violently, waves push toward the shoreline, loose debris falls into the sea and smoke expands across the background.

A second larger explosion follows closer to the shoreline, briefly illuminating the rock wall, beach and water.

Structure the sequence as:
1. Wide establishing shot of the calm coast.
2. Distant impact and first explosion.
3. Wider shot showing the shockwave affecting the environment.
4. Closer dramatic shot with debris, smoke, water spray and falling rock fragments.
5. Final wide shot showing the same coastline covered in smoke and aftermath.

Preserve the spatial layout of the bay, beach, dirt path, pier, shoreline and rock wall across every shot.

The explosions must interact physically with the environment through realistic debris trajectories, water displacement, smoke expansion and changing light.

Keep the scene readable rather than abstract or chaotic.

Sound: distant impact, deep explosions, rock debris, water displacement, wind and waves.
No background music.
No captions.
```

<a id="dialogue"></a>
## 💬 대화와 드라마

> 사람이 말하는 장면: 따옴표 대사, 억양, 멈춤, 립싱크. · 16개

<a id="dialogue-01"></a>
### 61. 카페에서 빵집 이야기를 나누는 두 친구

작성자 [@tanabe_fragm](https://x.com/tanabe_fragm) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-01#dialogue-01)** · [원본 게시물](https://x.com/tanabe_fragm/status/2110887676832543125)

https://github.com/user-attachments/assets/7e0fdbec-197d-46b3-a457-73a63464b2ae

**프롬프트:**

```text
A fixed, locked-off medium two-shot in a bright café at midday, horizontal 16:9 cinematic framing. Two young Japanese women in their early twenties sit facing each other across a small wooden table. The camera is at table height beside the table, so both women are seen in three-quarter view from the waist up — Misaki on the left of frame, Yui on the right — with their faces large and clearly lit. A large window runs along the background; soft natural daylight falls on their faces from the side, not from behind. Two iced lattes sit on the table between them. Photorealistic, natural skin texture, gentle background blur.

Misaki (left): 22, cheerful and talkative, black chin-length bob, white knit sweater, expressive hand gestures.
Yui (right): 23, gentle and easygoing, long brown hair, beige cardigan, laughs easily.

The camera does not move or cut. Exactly four lines of dialogue, in natural Tokyo-standard Japanese, in this order. While one speaks, the other listens with her mouth closed, reacting only with nods and smiles.

0–4s: Misaki leans forward toward Yui, eyes bright, excited:「ねえ聞いて！ 昨日ね、駅前のパン屋さん、やっと行けたの」
4–7s: Yui's eyes widen, surprised, quick:「え、まって、あの毎朝並んでるとこ？」
7–11s: Misaki nods hard, hands miming something crispy, delighted:「そうそう！ メロンパン、ぱりっぱりで…もう最高だった」
11–15s: Yui bursts out laughing and speaks through the laugh, playfully envious:「ずるい！ 今度ぜったい一緒に行こうね」

Precise lip sync: lips fully close on ま, ぱ, め, ば sounds; mouth shapes follow each vowel. No extra lines, no ad-libs, no narration. Audio is only the two voices and soft café ambience — no background music. No subtitles, no on-screen text. Single continuous horizontal shot, same framing from start to end.
```

<a id="dialogue-02"></a>
### 62. 스토리보드로 만든 사교클럽의 밤

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-02#dialogue-02)** · [원본 게시물](https://x.com/EndFolding79421/status/2111091805928186144)

https://github.com/user-attachments/assets/77131769-cb3d-4e3c-90bc-6631fd65e419

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
integrated_multimodal_description: <image 0> = STORYBOARD / VISUAL SEQUENCE REFERENCE. Follow its shot progression, camera positions, fraternity-house exterior, nighttime lighting, crowd placement and staging. <image 1> = GRACE CHARACTER REFERENCE. Preserve her exact identity, face, hair, wardrobe and proportions. <image 2> = ZACK CHARACTER REFERENCE. Preserve his exact identity, face, hair, clothing, build and proportions. CRITICAL: There is EXACTLY ONE Grace. Never duplicate her or create another woman resembling her. Multiple storyboard panels represent sequential shots, NOT multiple Graces. Realistic cinematic live-action feature film, 16:9. Natural skin texture, pores and imperfections. NO glossy/plastic AI skin. Restrained realistic acting. LOCATION: Night outside the Southern fraternity house from the storyboard: red brick, white columns, ivy, porch, central doorway, steps, lawn and trees. Warm exterior lighting with subtle blue/purple party light through windows. AUDIO THROUGHOUT: Active college party ambience: indistinct drunken conversation, occasional laughter and muffled music from inside. NO understandable background dialogue. NO cinematic/dramatic/horror score. GRACE NEVER SPEAKS. [00:00–00:04] Start immediately CLOSE SIDE PROFILE beside Grace as EXACTLY ONE Grace exits through the CENTRAL FRONT DOOR. Camera moves closely alongside her face. She is deeply upset but angry rather than helpless: wet red eyes, fresh tears, tense jaw and brow, uneven breathing, occasional small sniffle. She is fighting to maintain control. Grace pushes through several drunk partygoers near the doorway/porch. They casually move aside. She ignores everyone, never apologizes and NEVER looks back. She moves quickly with angry determination. [00:04–00:07] CUT to cinematic detail shot of Grace's legs and WHITE SNEAKERS rapidly descending the front steps. Floral dress moves naturally. She is walking FAST, almost storming, but NOT running. Brief moving side shot as she reaches the bottom and continues immediately across the lawn. One quiet sniffle. NO dialogue. [00:07–00:11] Camera dramatically PULLS BACK into the storyboard's WIDE ESTABLISHING SHOT, revealing the full house, porch, columns, lawn, partygoers and night environment. Grace moves diagonally across the foreground toward BOTTOM-LEFT, quickly leaving the house behind. Body language conveys hurt, humiliation, anger and determination. She NEVER stops and NEVER turns around. After completing the pullback, CAMERA BECOMES COMPLETELY STATIC. [00:11–00:15] Grace approaches the bottom-left edge, nearly leaving frame. KEEP CAMERA STATIC. ONLY NOW the central front door opens and Zack appears for the FIRST TIME. Zack RUNS outside, pushes urgently through partygoers and descends the SAME steps Grace used. ZACK yells across the lawn: “GRACE!” Natural contemporary North Georgia/Southern American accent, subtle and authentic, never exaggerated. Grace hears him but DOES NOT react visibly. She NEVER stops, NEVER turns around, NEVER answers and continues storming toward bottom-left. Zack runs after her as the clip ends. ABSOLUTE RULES: Exactly ONE Grace throughout. Grace exits FIRST; Zack follows several seconds later. Zack must NOT appear before 00:11. Grace has ZERO dialogue. Grace only makes subtle breathing/sniffling sounds. Zack says ONLY “GRACE!” No invented dialogue. No car. No one grabs, blocks or follows Grace except Zack. Keep crowd secondary. Preserve storyboard geography and house. Emotional focus remains on Grace.
```

<a id="dialogue-03"></a>
### 63. 막배 위의 사랑 고백

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-03#dialogue-03)** · [원본 게시물](https://x.com/minchoi/status/2104742167629435105)

https://github.com/user-attachments/assets/08f02253-f4bf-4f25-8052-58dbb34de6a1

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
"A cinematic, aching love scene on the last ferry of the night, crossing a dark sea in the rain. [Jules], the red-haired woman in the rust-orange wool coat with a single gold hexagon earring in her left ear, and [Harry]
, the clean-cut man in his late 20s with neat side-parted light-brown hair and an olive work jacket, sit side by side on a bench seat by a rain-streaked window in the quiet ferry café. Harbour lights shrink into the dark behind the glass. Intimate romantic drama, six shots. 0s–5s: Wide two-shot from across the empty café. Jules watches the harbour lights recede; Harry watches only her. [Jules: warm quick Glaswegian voice, quiet and wistful]: "This is the last ferry, you know." A beat. [Harry: slow Central Texas drawl, soft and low]: "I know." 5s–10s: Close-up on Jules in profile against the window, rain shadows sliding down her face. She keeps her eyes on the lights and forces a small smile that doesn't reach her eyes. [Jules, trying to sound light]: "Tomorrow you're on a plane, and I'm back to talking to the gulls." 10s–14s: Close-up on Harry. He turns fully toward her, earnest, his voice barely above the engine hum, and his hand finds hers on the bench. [Harry, tender, hopeful]: "Then come with me." 14s–19s: Close-up on Jules. Her composure cracks; her eyes fill, a small broken laugh escapes, and she shakes her head without looking at him. [Jules, voice trembling]: "Don't. Don't make it sound easy." 19s–25s: Tight two-shot. He lifts her hand and holds it against his chest; she finally turns to meet his eyes. [Harry, hoarse, full of feeling]: "Nothing about you's been easy, darlin'. That's why I keep coming back." 25s–30s: Extreme close-up of the two of them, foreheads touching, eyes closed, the harbour lights a soft blur behind them. [Jules, a whisper]: "Then keep coming back." [Harry, a whisper, smiling through it]: "Every time. Every single time." The ferry horn sounds low in the distance.Warm tungsten café lamps against cold blue storm light from the window, shallow depth of field, natural skin texture, glistening eyes, subtle film grain. Sound: rain on glass, the engine hum, the creak of the hull, a soft piano note under the final line."
```

<a id="dialogue-04"></a>
### 64. 머그컵이 끝까지 남는 부엌 대화

작성자 [@sebatheepan](https://x.com/sebatheepan) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-04#dialogue-04)** · [원본 게시물](https://x.com/sebatheepan/status/2104706256963244436)

https://github.com/user-attachments/assets/784f9704-5981-456e-9b0c-d666c5ec088a

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
20s, 16:9, 6 cuts, photoreal live-action, native audio with synced dialogue, British English accents. No on-screen text, subtitles, captions, watermarks or logos.

STYLE: intimate chamber drama, 35mm grain, shallow focus, understated performances.

CAST: NORA - woman, 45, auburn hair in a loose knot, black reading glasses pushed up on top of her head, grey cardigan over a faded T-shirt, tired eyes. ELLIE - her younger sister, 32, black curly shoulder-length hair soaked from rain, oversized denim jacket, jeans, silver hoop earrings.

PROPS: two identical mustard mugs. Nora holds one. A second, empty mug stands clearly visible at the empty chair opposite her.

PALETTE: amber pendant lamp vs cold teal under-cabinet light, deep shadows, natural skin.
STORY: At 3 a.m. Ellie comes home to admit she sold their late mother's house. Nora already knows.

BEATS:
0.0-3.5s | CUT 1, wide, static, eye level: heavy rain on the kitchen window. Ellie stands frozen in the doorway on the left, dripping. Nora sits at the table on the right, hands round her mug; the empty mug waits opposite. Stillness.

3.5-7.5s | CUT 2, clean medium close-up on Nora, nothing in the foreground, 50mm, slow push-in. Eyes down. NORA (flat, quiet, exhausted): "You sold it. Mum's house. Without asking me."

7.5-12.0s | CUT 3, close-up on Ellie in the doorway, 85mm, subtle handheld. Her eyes fill with tears; she swallows before speaking. ELLIE (defensive, voice cracking on the last word): "I was drowning, Nora. You weren't answering."

12.0-15.5s | CUT 4, same clean medium close-up on Nora, eyes dry at first. She looks up, pulls the glasses down off her head and sets them on the table. Only then does one tear run down her cheek. She says nothing. Only rain.

15.5-18.0s | CUT 5, low profile shot along the tabletop: Nora's hand slides the empty second mug across the wood to the empty chair. NORA (whisper, barely voiced): "Sit down."

18.0-20.0s | CUT 6, medium close-up on Ellie, already seated at the table, both hands round the second mug. One shaky breath, half laugh, half sob, then stillness. Hold.

AUDIO: dialogue close and dry. Steady rain on glass audible from the first frame, fridge hum, room tone. Mug scrape on wood at 16s. Ellie's half-laugh sob at 18.5s. No music.

NEGATIVE: no text, no extra people, no foreground shoulders in Nora's shots, no repeat of the CUT 1 wide, no props appearing or vanishing, no melodramatic sobbing, no face morphing, no lip-sync drift.
```

<a id="dialogue-05"></a>
### 65. 우연히 미슐랭이 된 요리 시험

작성자 [@yourPlugAI](https://x.com/yourPlugAI) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-05#dialogue-05)** · [원본 게시물](https://x.com/yourPlugAI/status/2112030985751756819)

https://github.com/user-attachments/assets/90eb9acf-8d2d-4c16-a086-52261c04e0cb

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
[ENGINE DIRECTIVE]

Generate a continuous 30-second hyper-realistic live-action office/academic comedy sequence using Kling 4.0 at 120fps ultra-realism in 16:9 widescreen format. Maintain 100% strict visual consistency with provided asset sheets: "Director Kang-jun" (master chef in navy coat) and "Hye-soo" (clumsy student in flour-dusted apron). Setting strictly follows "High-End Culinary Art Academy Lab". Style: High-tension K-drama comedy, sharp whip-pans, snap-zooms, exaggerated physical freezes, dramatic shadow drops, synced comedic audio hits, dynamic subtitle overlays.

[AUDIO DIRECTIVE]

MUSIC: High-energy K-drama comedic track featuring rapid orchestral pizzicato strings, sudden brass drops, and frantic pots-and-pans percussion syncs.

SOUND DESIGN: Loud metallic pots clanking, high-pitched sneaker slide screech, chef's clipboard SLAP, dramatic gong hit, liquid splash, sharp whip-pan WHOOSH, comedic record scratch.

[TIMELINE BREAKDOWN]

00:00 - 00:03 | EXTREME CLOSE-UP HOOK & FLYING SPICES (SCROLL-STOPPING HOOK)
VISUAL: Extreme macro snap-zoom onto Director Kang-jun’s twitching eye and twitching jaw. Sudden whip-pan 180 degrees to Hye-soo slipping on a stray piece of butter on the floor in slow motion.

ACTION: Kang-jun stands rigidly with his clipboard, inspecting. Hye-soo trips over her own feet; her tray of spices and a squeeze bottle of dark reduction go flying into the air in hyper-slow motion toward an expensive, unfinished plating dish.

DIALOGUE (HYE-SOO): Ah! Director!! Watch out!!

SOUND: Comedic high-pitched screech, slow-motion bass drop, frantic brass swell, metallic clang.

00:03 - 00:07 | SLIDING CATCH & CRASH ON MARBLE

VISUAL: Fast tracking camera following Hye-soo sliding across the stainless-steel prep table.
ACTION: Hye-soo executes a desperate, clumsy slide across the counter, catching the falling sauce bottle mid-air, but landing face-first on a pastry board, sending a huge cloud of flour into the air. A spray of dark reduction splatters directly onto the center of Kang-jun’s pristine clipboard and sleeve.

DIALOGUE (KANG-JUN): What... are you doing in my exam room?

SOUND: Sliding THUD, loud flour POOF, sharp record scratch, dead silence beat.

00:07 - 00:12 | SNAP-ZOOM REACTION & SHADOW DROP

VISUAL: Rapid three-stage snap-zoom on Kang-jun’s deadpan, unblinking face under a sudden dramatic shadow drop as he looks down at his splattered sleeve.

ACTION: Kang-jun slowly adjusts his glasses with one finger, maintaining total silence. He reaches down, dips his finger into the chaotic splash of sauce that accidentally landed on his tasting spoon, and slowly tastes it. His eyes widen by a millimeter—the mistake created a spectacular, unplanned savory-sweet infusion.
DIALOGUE (HYE-SOO - WHISPERING): Please, just don't fail me...

SOUND: Sharp camera shutter CLICK-CLICK-CLICK, dramatic choir chant hit, sizzle of a pan.

00:12 - 00:18 | THE WHIP-PAN INTERROGATION

VISUAL: Whip-pan camera movement back and forth between Kang-jun leaning down over the table and Hye-soo lying flat on her belly, clutching the squeeze bottle.

ACTION: Kang-jun slams his hands on the counter, leaning inches from her flour-sputtered face. His expression is terrifyingly intense, but his eyes are fixed purely on the sauce.

DIALOGUE (KANG-JUN): This sauce ratio... how did you think of this?
DIALOGUE (HYE-SOO): Huh? It just... mixed when I fell...

SOUND: Heavy counter SLAM, low bass rumble, high pizzicato tension strings.

00:18 - 00:24 | EXAGGERATED FREEZE & CLASS STUN

VISUAL: Dynamic low-angle wide shot. High-contrast lighting flashes as the entire background student team in the kitchen freezes in over-the-top shock.

ACTION: Kang-jun suddenly lifts the spoon and his clipboard into the air, turning sharply toward the evaluation board with an epic, serious posture, pointing dramatically at Hye-soo.

DIALOGUE (KANG-JUN): She’s a genius. This student gets the highest score in history!

SOUND: Triumphant K-drama orchestra hit, audience gasps, thunderous comedic sting.
00:24 - 00:30 | ABSURD RESOLUTION & CHAOTIC FINISH

VISUAL: Tracking hero shot moving backward as Kang-jun vigorously shakes Hye-soo's hand while she is still half-sprawled on the marble pastry table.

ACTION: Kang-jun aggressively shakes her flour-coated hand with a deadpan, intense expression. Hye-soo, still on her belly holding the bottle, nods along in complete confusion as a rain of flour dust falls around them.

DIALOGUE (KANG-JUN): Starting tomorrow, you are my head research assistant.

DIALOGUE (HYE-SOO): What?! I just got here yesterday!!

SOUND: High-energy comedic K-drama theme song playout, party horn sound, fast fade to black.
```

<a id="dialogue-06"></a>
### 66. 남편의 늦은 밤 부엌 고백

작성자 [@MayorKingAI](https://x.com/MayorKingAI) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-06#dialogue-06)** · [원본 게시물](https://x.com/MayorKingAI/status/2111427314248774100)

https://github.com/user-attachments/assets/813ea7c1-51c7-4c90-ac03-19969935344c

**프롬프트:**

```text
SCENE CONTEXT
EXACTLY 2 HUMAN CHARACTERS — NO DUPLICATES, NO EXTRAS. Interior, a small lived-in apartment kitchen, late at night. A husband confesses to his wife that he was fired in June and has been pretending to go to work every day. She did not know; her disbelief turns to hurt, then to unconditional support. Intimate two-person drama, real time. The emotion lives equally in their faces, their words and their voices.

CHARACTERS
DANIEL: lean man, short dark hair greying at the temples, two days of stubble, deep shadows under the eyes, a small healed nick on his chin. Pale blue cotton office shirt, top button undone, sleeves rolled to the forearm, a loosened dark navy tie, a faint coffee stain on the left cuff. Plain gold wedding ring on his left hand. 180 cm.
LUCÍA: shoulder-length chestnut hair loosely tied, strands falling over her face, natural skin with faint freckles and slight redness around the nose, no makeup. Oversized oatmeal wool cardigan with a pulled thread at one cuff, over a grey cotton t-shirt. Plain gold wedding ring on her left hand. 165 cm.

LOCATION MAP
A small square kitchen table with a worn wooden top sits at the center. Daniel sits on the right side of the table (screen-right), facing left. The doorway to a dark hallway is screen-left. On the table: a half-full glass of water between Daniel's hands and a folded, unopened envelope. His laptop bag rests on the chair beside him. The window blind is fully closed. Behind Daniel: a kitchen counter and an old wall clock. The eyeline axis runs left–right across the table; the camera always stays on the same side of it.

FORMAT
One scene, 8 shots joined by clean hard cuts, classic shot–reverse-shot coverage. Cuts follow the dialogue and also land on the listener's reaction. No fades, no dissolves, no split screens.

SHOTS
Shot 1 — Wide shot, locked-off, from the corner behind the counter, 63° FOV. Daniel sits alone in the pool of lamplight, both hands around the glass, not drinking, staring at nothing. Lucía walks in through the dark doorway, relaxed and unaware, about to cross the kitchen.

Shot 2 — Medium close-up on Daniel, 47° FOV, eye level, very slow push-in ending on his face. He lifts his eyes to her; his jaw tightens, his nostrils flare with one deep breath, his lips part twice before any sound comes out. Low, slow and hesitant, with a heavy pause before the last three words: "Lucía… I need to tell you something. I got fired. In June."

Shot 3 — Reverse: medium shot of Lucía over Daniel's out-of-focus right shoulder, 47° FOV. She freezes mid-step. Her brow furrows, her mouth falls slightly open, a short incredulous breath escapes her. Quick and confused, almost a half-laugh of disbelief: "What? What do you mean, you got fired?" She walks to the table and grips the back of the chair opposite him, standing, looking down at him, knuckles whitening. Her voice rises with hurt, sharp but never shouting, stressing "hiding" and "nothing": "And you've been hiding it from me this whole time, like nothing happened?"

Shot 4 — Close-up on Daniel, 29° FOV, slightly high angle matching her standing eyeline, handheld with an extremely subtle breath-like float. He looks up at her, then his eyes drop to the glass; his thumb rubs its rim; his eyes turn glassy. Quiet, ashamed, his voice thinning, with a long pause in the middle and a crack on the last word: "I wasn't trying to hide it. Every morning I pretended I was going to work… and I spent the whole day looking for a job."

Shot 5 — Reverse close-up on Lucía, 29° FOV, slightly low angle. No words. Her grip on the chair loosens; her furrowed brow slowly relaxes; her lips press together and tremble; her eyes fill with water. The anger drains from her face and becomes pain. The clock ticks.

Shot 6 — Medium shot of Lucía, 47° FOV. She pulls out the chair and sits down opposite him, now at his eye level, leaning slightly toward him. Softer and wounded, her voice breaking on "trust": "Why didn't you tell me? Don't you trust me?"

Shot 7 — Close-up on Daniel, static, eye level. He opens his mouth to answer but no words come. His chin trembles, his eyes go red, a tear gathers on his lower lid, he swallows hard and gives one small shake of the head. Silence.

Shot 8 — Two-shot in profile across the table, 47° FOV, slow lateral drift of less than half a meter to the right, ending with both faces and the table between them in frame. Lucía reaches across and places her hand over his. A single tear runs down her cheek; she does not wipe it. Quiet, warm and absolutely firm, each word deliberate, stressing "always": "I'm always going to be there for you." Daniel turns his hand over and holds hers tightly, closes his eyes, and lets out a long, shaking exhale. Hold on the two of them in silence.

CHARACTER ACTING
Restrained, naturalistic film acting; every emotion is visible on the face in close-up. Daniel: guilt and shame — avoids her eyes, then forces himself to hold them; jaw clenched, breath short through the nose, hands restless on the glass; relief only arrives in the final exhale. Lucía: disbelief (frozen, brow furrowed, mouth open) → hurt (knuckles white on the chair, voice rising) → softening (grip loosens, eyes fill) → steady support (still, firm gaze, gentle half-smile through tears in the final shot). Faces show living micro-expressions: trembling chins, glistening eyes, swallowing, natural irregular blinks.

LIGHTING
One warm 3200K pendant lamp hanging low over the table is the key source: light from above-front, fast falloff, deep shadows in the corners of the room, catchlights visible in both characters' eyes. A faint cold 5600K spill from the hallway behind Lucía outlines her hair. Light direction and color stay identical after every cut.

AUDIO
All dialogue in natural, clear English with a neutral American accent. Daniel: low, tired baritone, slow, hesitant, with long pauses and an audible tremor when emotion rises. Lucía: warm mid-range voice that moves from confused and fast, to sharp and hurt, to soft and breaking, to quiet and firm. Each has a distinct voice. Only one person speaks at a time, no interruptions or overlapping, about one second of silence between lines. Breaths, swallows and small catches in the voice are audible. Lip movements synchronized with the English dialogue. Ambience: wall clock ticking, refrigerator hum, chair legs scraping on floor tiles, glass touching wood, cardigan rustle. Ambience stays below the dialogue. No background music. No subtitles.

STYLE
Intimate auteur drama. 35mm film texture with organic grain, shallow depth of field, soft halation around the lamp, no digital sharpening. Palette: 60% warm amber and wood brown, 30% deep shadow, 10% cold blue spill from the hallway.

POSITIVE CONSTRAINTS
Exactly two people for the entire scene. Same faces, hair, clothing and wedding rings in every shot. Daniel always screen-right looking left; Lucía always screen-left looking right. Exactly 4 dialogue turns: 2 by Daniel, 2 by Lucía. Lucía stands in Shots 3–5 and sits from Shot 6 onward. Hands and fingers anatomically correct when they hold hands. Faces stable. The scene ends in silence with their hands joined on the table; they stay seated.
```

<a id="dialogue-07"></a>
### 67. 겨울 강변길의 이별

작성자 [@tanabe_fragm](https://x.com/tanabe_fragm) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-07#dialogue-07)** · [원본 게시물](https://x.com/tanabe_fragm/status/2110893614671040886)

https://github.com/user-attachments/assets/acc8db31-3d9a-470f-bb0a-8ada78fdc0ae

**프롬프트:**

```text
A vertical 9:16 Japanese short drama scene, cinematic and photorealistic, shot at night on a riverside walking path in early winter. Streetlights stand at even intervals along the path, their warm light reflected on the dark river. Cool night air, breath faintly visible. Shallow depth of field, soft bokeh from the streetlights, muted teal-and-amber color grade, subtle film grain.

Haruka: Japanese woman, 24, shoulder-length black hair, long beige coat. Quiet voice, but firm.
Souta: Japanese man, 25, short black hair, navy duffle coat. Usually gentle; now shaken.

Four shots, in this order. Exactly four lines of dialogue in natural Tokyo-standard Japanese, spoken softly and slowly, with real pauses. No other lines.

Shot 1 (0–4s) — Frontal tracking shot, the camera moving backward ahead of them, bust shot of both. Haruka and Souta walk side by side toward the camera, a small gap between their shoulders. Haruka keeps looking straight ahead and says quietly:「ねえ…来月から、大阪なんだ」

Shot 2 (4–7s) — Tracking from behind at waist height, focus on the space between their two hands. Their hands swing as they walk, almost touching but never touching. Souta's voice, after a pause, low:「…なんで、今言うの」

Shot 3 (7–11s) — Side tracking shot, moving alongside them. Haruka stops walking. The camera keeps moving with Souta for two more steps, then stops. Focus racks from Souta in the foreground to Haruka standing behind, now one streetlight's distance away. Haruka, still and steady:「言ったら…止められると思ったから」

Shot 4 (11–15s) — Souta turns back toward her. Slow push-in on his face; streetlight falls across only half of it. He starts to speak, swallows it, then says in a hoarse voice:「…止めたら、いてくれんの？」 Hold on his face to the end.

Audio is only their voices, footsteps, the river, and distant traffic — no background music. No subtitles, no on-screen text. Same two people, same clothes, same night riverside path in every shot.
```

<a id="dialogue-08"></a>
### 68. 다섯 장면 30초 일본 로맨스

작성자 [@agi_aibusi](https://x.com/agi_aibusi) · 29초 · 3:4 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-08#dialogue-08)** · [원본 게시물](https://x.com/agi_aibusi/status/2111462820349124692)

https://github.com/user-attachments/assets/f6c45243-42e4-4139-b6d2-b20ebb52a66c

**프롬프트:**

```text
Create one complete 30-second, ultra-realistic Japanese romantic drama. Follow the five timed scenes below within a single finished film. The emotion comes from a woman who tries to say goodbye, then finds the courage to admit she wants to meet again.

MAIN SUBJECT
Ella is the sole visible character: a beautiful adult Japanese woman with straight dark hair and bangs, natural skin texture, subtle everyday makeup, and believable expressions.

Her wardrobe for this film is a white blouse, a pale blue cardigan, simple neutral trousers, and ordinary low shoes. Keep the same facial identity, facial proportions, apparent adult age, eyes, skin tone, hair, clothes, and body proportions throughout every shot. Use small changes around her eyes and mouth to convey emotion; avoid exaggerated crying.

LOCATION
A quiet fork in a Japanese residential lane at sunset. Modest houses, concrete-block garden walls, plants at entrances, overhead utility wires, and a distant railway crossing establish a lived-in Japanese neighborhood. Keep the street layout and sunset direction coherent. No landmark, crowds, prominent brands, or readable advertisements.

CAMERA / VISUAL STYLE
Naturalistic live-action romance, intimate eye-level framing, soft warm sunset, realistic depth of field, restrained contrast. The camera occupies the emotional position of the unseen person saying goodbye to her. No visible male actor. Begin in a medium shot, hold the physical distance as she leaves, and let her approach create the final close-up. Subtle human handheld movement, clean motivated edits, no orbiting, drone shots, artificial beauty filters, or slow motion. This is a dramatic scene, not a fashion montage.

00:00–00:05 — A POLITE GOODBYE
Ella stands at the fork facing the unseen person near the camera. She makes a slightly forced but gentle smile and gives one small wave. In natural Japanese, with synchronized lips, she says: 「じゃあね。……元気でね」. She lowers her hand and begins to turn away.

00:05–00:11 — THE SMILE DISAPPEARS
She walks several normal steps away. The camera stays at the original position and does not chase her. A restrained three-quarter view reveals that her social smile has faded. She looks down very briefly, trying to maintain composure. Only ordinary footsteps and neighborhood ambience.

00:11–00:17 — SHE CHANGES HER MIND
Her feet stop naturally. A small breath moves her shoulders. She hesitates, turns her head and then her body back toward the camera, and softly calls: 「……ねえ」. Leave silence around the word. No tears falling, no melodramatic gesture.

00:17–00:24 — RETURNING
She walks back toward the same camera along the same path, stopping at a comfortable conversational distance. Her expression combines shyness and resolve. Looking toward the unseen person's eyes beside the lens, she says: 「さっきの、言い直してもいい？」. Do not rush her approach or dialogue.

00:24–00:30 — THE HONEST WORDS
An intimate close-up as she stays still. Her eyes become slightly moist, and a vulnerable smile appears. At approximately 00:25–00:27, she says quietly: 「また、会いたい」. Hold her face and the silence through the final seconds as she waits for a reply. End on this living expression without a title card or a fade to black.

PHYSICAL REALISM / CONTINUITY
Realistic walking speed, grounded feet, anatomically correct hands, consistent spatial direction, and natural breathing. No extra fingers, duplicated people, facial morphing, sliding feet, teleportation, or changing clothing. Her return follows the path she just walked. One person and one continuous emotional event; no unrelated insert shots.

AUDIO
Ella speaks only the four specified Japanese lines, in one consistent natural adult female voice. Accurate Japanese lip synchronization, quiet breaths, shoes on pavement, distant traffic, and a faint railway crossing. No male reply, narrator, music, subtitles, or added text. Preserve roughly two seconds of emotional breathing space after the final line.

FINAL FEEL
A small, believable romantic turning point. Her beauty is visible in her face and presence, while her uncertainty makes the scene human. The final result should feel like thirty seconds extracted from a convincing Japanese live-action drama.
```

<a id="dialogue-10"></a>
### 69. 바로크 홀에서의 입맞춤

작성자 [@Kiber_Alla](https://x.com/Kiber_Alla) · 37초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-10#dialogue-10)** · [원본 게시물](https://x.com/Kiber_Alla/status/2114039733688946759)

https://github.com/user-attachments/assets/0986ce77-fea6-46d4-9229-17a6d6bbfd56

**프롬프트:**

```text
lady is Character A, Lady Marian. Use this image for her face, hair, makeup and black gown.
count is Character B, the Count. Use this image for his face, wig and ivory-and-gold brocade coat.
hall is the location: the candlelit baroque throne hall with the black marble mirror floor.
goblet is the crystal wine goblet.

Cinematic live-action gothic romance, photorealistic, the look of a late-1980s dark fantasy film shot on 35mm with fine film grain. Rows of lit candelabras glow along the walls of the throne hall, a shaft of cold blue moonlight falls from the tall window, deep black shadows fill the corners, and the black marble floor reflects everything like a mirror. The throne stands raised on black marble steps under a black-and-gold canopy with gold fringe; a small round black marble side table stands beside it. Stereo sound: the deep quiet of a huge stone hall, candle flames crackling softly, faint wind at the window. No subtitles. No background music.

Character A: Lady Marian, a lady with a towering powdered blonde updo with black ostrich feathers, blue eyes, winged liner and deep red lips, in a black off-the-shoulder corseted gown with black lace ruffles and a long black train. Her neck and collarbones are completely bare: no necklace, no choker, no pearls, no jewelry at her throat in any shot.
Character B: the Count, a young pale man with cool gray eyes in a white powdered wig with rolled side curls and a black ribbon, an ivory-and-gold brocade coat, a lace jabot with a diamond brooch, a pink silk sash with a single jeweled star, rings on his fingers, seated on the throne. His mouth is clean throughout.

0–2.5s: Medium close-up of Lady Marian standing in the hall, candelabras soft behind her and a shaft of moonlight from the window. She lifts the crystal goblet of red wine and takes a slow sip, her eyes fixed ahead on the Count. Her bare neck and collarbones are visible above the black gown.
2.5–4.5s: Medium shot of the Count seated on the throne, seen through the soft out-of-focus gold fringe of the canopy in the foreground. Slow dolly-in. He looks down at her, still and unreadable.
4.5–6s: Extreme close-up of Lady Marian's face over the rim of the goblet, candle bokeh behind her. She sips the wine and lifts her eyes to him.
6–8.5s: Medium shot of the Count on the throne, front-on, slow push-in. His gaze drops to her lips and stays there. His ringed fingers tighten on the armrest.
8.5–10s: Low close-up at table height. Lady Marian's hand sets the goblet down on the round black marble side table. Crystal clinks softly on stone.
10–11s: Macro close-up of her deep red lips. Her fingertip slowly traces her lower lip.
11–14s: Over-the-shoulder shot from behind the Count on the throne, the back of his white wig and black ribbon soft in the foreground, looking down the marble steps at Lady Marian as she crosses the mirror floor and slowly climbs toward him, her black train gliding behind her.
[Character B: the Count, low and calm, not moving]: "Lady Marian. You're in the wrong wing of the castle."
14–17s: Close-up of Lady Marian from a slightly low angle as she stops on the step just below him and tilts her head with a slow smile. Her neck is bare, no necklace.
[Character A: Lady Marian, soft, amused voice]: "Am I?" A beat. "Then why haven't you called the guards?"
17–18.5s: Medium close-up of the Count from a low angle, looking down at her. His gaze slips to her lips.
[Character B: the Count, quietly, a little hoarse]: "...I'm still thinking about it."
18.5–19.5s: Extreme close-up of the Count's eyes, flicking from her eyes to her lips and back.
19.5–23s: Medium two-shot from a low angle on the steps, slight Dutch tilt. Lady Marian sits sideways on the Count's lap and leans in until her lips almost touch his.
[Character A: Lady Marian, a low whisper against his lips]: "Think faster."
23–25.5s: Close two-shot. Lady Marian twists the lace of his jabot around her fingers and tugs him toward her, gives him a quick, light kiss, then pulls back an inch with a teasing smile.
25.5–30s: Close two-shot, slow orbit around them. The Count catches her by the waist and cups the back of her head, pulls her back in and kisses her deeply and passionately. Her fingers slide into the curls of his wig, his hand presses into the small of her back, both eyes closed.

Pacing: slow, sensual and teasing through the approach, a quiet tense exchange of lines with real pauses, then a quick playful kiss turning into a deep, slow one at the very end.
```

<a id="dialogue-11"></a>
### 70. 크리스마스 파티 드레스코드 소동

작성자 [@bmx_ai13](https://x.com/bmx_ai13) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-11#dialogue-11)** · [원본 게시물](https://x.com/bmx_ai13/status/2115657377542521030)

https://github.com/user-attachments/assets/4cbfbc5e-be16-4b3d-81d3-87487e13f1dc

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
SCENE CONTEXT
30 second widescreen 1990s Christmas romcom comedy. Christmas Eve daytime, a cream and gold mansion foyer. A gorgeous woman in an inflatable dinosaur costume opens the door for her boyfriend and finds his gorgeous parents in equally absurd costumes. The boyfriend arrives last in a tuxedo. He gave everyone a different dress code.

ACTIVE REFERENCES
CLAIRE: mid 20s, strikingly beautiful supermodel face, glossy brunette blowout, glam makeup with red lips, wearing a full body green inflatable T-rex costume with tiny arms and a Santa hat on the dinosaur head, her face visible through the open neck. Bright voice.
MARGARET: 50s, stunning 90s supermodel glamour, sculpted cheekbones, voluminous blonde blowout, wearing a full body green Christmas tree costume covered in blinking multicolor bulbs and baubles, a gold star on her head. Silky voice.
HAROLD: 50s, chiseled silver fox, sharp jaw, styled silver hair, wearing a full body red lobster costume with giant padded claws and a black satin bow tie at the neck. Deep dry voice.
JAKE: late 20s, handsome, swept back blond 90s hair, sharp black tuxedo, holding red roses. Cheerful voice.

LOCATION MAP
Foreground: marble floor.
Midground: tall white double doors with a wreath, garland pillars with warm fairy lights, poinsettias, lit candles.
Background through the doors: snowy courtyard, snow falling at 3 km/h.

FORMAT MODE
Timed multishot, cuts only at the specified points, the camera does not cut on its own.

OPTICS
Each segment holds its stated FOV, no drift mid-segment. Soft vintage prime look, creamy fairy light bokeh.

CAMERA
Eye level operator inside the foyer facing the doors, locked off comic framing, quick reaction cuts.

ACTION
0.0s to 3.0s, WS 63 degrees: Claire waddles toward the doors in the swaying T-rex costume, practicing a roar with her tiny arms up. Doorbell chimes.
3.0s HARD CUT

3.0s to 5.0s, MS 47 degrees from behind Claire: she flings the doors open and shouts "RAWR! Merry Christmas, baby!"
5.0s HARD CUT

5.0s to 8.0s, WS 47 degrees reverse: Margaret the Christmas tree and Harold the lobster stand side by side on the snowy step, perfectly calm, bulbs blinking.
8.0s HARD CUT

8.0s to 10.0s, CU 29 degrees: Claire's smile freezes, her tiny T-rex arms stuck mid wave.
10.0s HARD CUT

10.0s to 13.0s, MCU 29 degrees: Margaret smiles elegantly, says "You must be Claire." Claire off screen: "And you must be a tree."
13.0s HARD CUT

13.0s to 16.0s, MS 47 degrees: Harold extends a giant lobster claw for a handshake. Claire strains her tiny T-rex arms forward. They fall short by a hand's width. Both keep straining in silence.
16.0s HARD CUT

16.0s to 19.0s, MCU 29 degrees: Harold taps his bow tie with his claw, says "Jake said black tie." Margaret: "He told me costume party." Claire: "He told me dress fun."
19.0s HARD CUT

19.0s to 22.0s, WS 63 degrees: Jake steps up behind his parents in the sharp tuxedo with roses, stops dead, says "Why is everyone dressed like that? I said formal dinner."
22.0s HARD CUT

22.0s to 25.0s, MS 47 degrees from behind Jake: the dinosaur, the tree and the lobster turn their heads toward him in perfect unison. All of Margaret's bulbs switch to solid red.
25.0s HARD CUT

25.0s to 27.0s, CU 29 degrees: Claire stares at Jake, says flatly "Rawr." Her costume slowly deflates with a long wheeze around her.
27.0s HARD CUT

27.0s to 30.0s, WS 63 degrees: Harold pinches Jake's ear with his lobster claw and drags him inside past Claire. Jake yelps "Ow ow ow!" Margaret follows, bulbs blinking happily again.

PERFORMANCE
Comedy through total seriousness: the parents treat their costumes as completely normal. Glamorous faces stay perfectly composed while the costumes are ridiculous. Claire's eyes widen in small steps, lips pressed together. Real skin texture, wet catch lights.

PHYSICS
Inflatable costume sways and bounces with each step and sags softly when deflating. Lobster claws are heavy and padded. Snowflakes land and melt on hair and costumes.

LIGHTING
Warm 3200K tungsten interior from lamps, candles and fairy lights. Cool 5600K snow daylight through the doors as rim light. Margaret's costume bulbs cast colored light on nearby faces.

AUDIO
Diegetic only: doorbell chime, costume fan motor hum, plastic squeak, wind and snow hiss at the open door, bulbs clicking, deflating wheeze, spoken dialogue. No music.

STYLE
Photoreal 1990s holiday romcom on 35mm film, fine grain, soft halation.

OUTPUT SETTINGS
16:9 widescreen, real time, 24fps.

POSITIVE LOCKS
Same four people, same costumes and same foyer in every cut. Faces stay beautiful and fully visible. Clean frames with no on-screen text, no subtitles, no captions, no logos, no watermarks.
```

<a id="dialogue-12"></a>
### 71. 1950년대 가족과 업데이트 중인 로봇

작성자 [@obi_ai6193](https://x.com/obi_ai6193) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-12#dialogue-12)** · [원본 게시물](https://x.com/obi_ai6193/status/2110855814005342673)

https://github.com/user-attachments/assets/aac6e41a-3868-4e48-adb7-f3837d11c0bb

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
[Shot1, 3s ]
水色のワンピースを着た女の子が、ロビンの隣にしゃがんで両手で優しく肩を支えている。心配そうに父親を見上げて話す。カメラはリリーの不安げな顔へゆっくりドリーイン。ロビンは静止したまま、光る目がわずかに点滅する。静かなサスペンス調のBGM。セリフ：「Daddy, something's wrong with Robin!」

[Shot2, 3s ]
黄色い花柄のワンピースを着た母親が、心配そうにロビンを見下ろしながら身を乗り出す。突然何かを思い出したように眉を上げ、考え込むように話す。カメラは母親の顔のクローズアップへゆっくりプッシュイン。背景のキッチンには暖かい照明が灯っている。不穏なストリングスが静かに流れる。セリフ：「He's been acting strange lately.」

[Shot3, 3s ]
ベージュのスーツを着た父親が突然目を大きく見開く。慌てて上半身を起こし、信じられないという表情でロビンを凝視する。カメラは父親の驚いた顔へ素早くドリーインし、タイトなクローズアップ。表情はますます緊迫していく。鋭いオーケストラの効果音が鳴り、その後一瞬の静寂が訪れる。セリフ：「Oh, no! It can't be!」

[Shot4, 3s ]
小さく光沢のあるオレンジ色のレトロロボット、ロビンが突然起動する。丸い目が明るく輝く。頭部を2回ぎこちなく機械的に動かし、非常に短い腕がわずかに震える。カメラはローアングルから光る目へゆっくりドリーイン。ロビンの元のデザイン、体の比率、アンテナ、腹部前面のパネル、極端に短い脚を完全に維持する。柔らかな電子音と陽気な完了チャイムが響く。セリフ：「Don't worry! Kling four point oh update complete!」

[Shot5, 3s ]
家族全員が突然喜びの笑い声を上げる。父親と母親が勢いよくハイタッチし、水色のワンピースを着たリリーとピンクのワンピースを着た妹も楽しそうにハイタッチする。ロビンは非常に短い機械の両腕を上げて喜び、丸い目が明るく輝く。カメラはワイドショットから緩やかにクレーンアップしながら後退。美しいレトロフューチャーなキッチンと夜の街並みを映し出す。1950年代の陽気なスウィングジャズが始まる。セリフ：「Hooray!」
```

<a id="dialogue-13"></a>
### 72. 도서관에서 대화하는 여우와 부엉이

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-13#dialogue-13)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2105981906869199107)

https://github.com/user-attachments/assets/4ebb552e-2dac-4eb1-87d4-5e65589ccd00

**프롬프트:**

```text
A photorealistic cinematic scene in a grand walnut-panelled library, late afternoon. An anthropomorphic red fox aristocrat wears a forest-green frock coat, a cream waistcoat and a carefully tied silk cravat. An elderly barn owl scholar stands beside a writing desk in a dark plum velvet jacket, with tiny spectacles resting above his beak. Warm window light catches individual strands of fur and delicate facial feathers. Begin in a medium two-shot as the fox confidently straightens his cuffs. He asks, “Would you describe me as a man of considerable intellect?” Cut to the owl’s close-up. After a thoughtful pause, the owl replies, “I would describe you as considerably well dressed.” The fox’s proud smile slowly fades in the blurred background. Understated British delivery, subtle expressions, believable animal anatomy, polished period-drama cinematography, gentle clock ticking, no subtitles.
```

<a id="dialogue-14"></a>
### 73. 미래 토크쇼의 안드로이드 게스트

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-14#dialogue-14)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2112833689889521932)

https://github.com/user-attachments/assets/f7bc3b1b-e976-4d83-9095-237b0488177b

**프롬프트:**

```text
A cinematic futuristic talk show filmed inside a polished science-fiction broadcast studio. A serious male interviewer dressed entirely in black speaks calmly while sitting in a modern chair. Opposite him sits a beautiful red-haired female android with intricate silver-black mechanical plating and highly realistic synthetic skin. Begin with a stable waist-up shot of the man speaking naturally and gesturing with both hands. Seamless cut to a close-up of the android answering him, moving her hands naturally while her mechanical fingers articulate precisely. Background screens display abstract futuristic imagery. Transition to a wide establishing shot showing the circular stage, overhead lights, glass architecture and both guests. Cut back to their faces during the conversation. At the end, the center of the stage suddenly detonates in a powerful explosion, sparks and fragments burst outward, both characters react instantly, thick smoke rapidly consumes the entire frame. Hyperrealistic live-action aesthetic, realistic explosion physics, subtle handheld reaction during blast, professional studio cameras, dramatic but believable
```

<a id="dialogue-15"></a>
### 74. 브르타뉴 절벽길 산책 대화

작성자 [@EricKerArt](https://x.com/EricKerArt) · 28초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-15#dialogue-15)** · [원본 게시물](https://x.com/EricKerArt/status/2111110194516095384)

https://github.com/user-attachments/assets/2f236590-fba9-415b-bf72-c8e0c24ef576

**프롬프트:**

```text
Sunny late summer afternoon on a narrow coastal footpath in Brittany, France, winding along the top of a cliff through bright yellow blooming gorse and heather. Deep blue sky with a few white clouds, sparkling turquoise sea below, pink granite rocks, warm golden natural light, gentle sea breeze moving the gorse. Shot on 16mm film with natural grain, warm natural colors, 1990s French auteur cinema style, no music.

Camera:
handheld throughout, operated by a single camera operator walking with the actors, slight natural sway and small breathing movements, loose documentary framing, never stabilized. Multiple cuts between angles: walking shots from the front and from behind on the path, two-shots, over-the-shoulder shots, and closer shots on their faces, edited with the rhythm of the conversation.All dialogue is spoken in French, with natural native French pronunciation, a relaxed conversational rhythm and clear diction.

Characters:
MARGOT, a 25-year-old French woman with shoulder-length chestnut hair blowing in the wind, wearing a navy and white striped sailor sweater and light beige trousers, canvas espadrilles.
LÉO, a 23-year-old French man with short dark tousled hair, wearing a loose white linen shirt with rolled sleeves and grey trousers, hands in his pockets, canvas espadrilles.Margot and Léo walk one behind the other along the narrow path between the gorse bushes, then side by side when the path widens.
MARGOT (curious, teasing, in French): "Alors, Solène ? Tu l'as rappelée ?"LÉO (evasive, in French): "Non. Elle voulait aller à Bréhat samedi. Mais samedi, Claire arrive par le train de quatorze heures."MARGOT (amused, precise, in French): "Donc tu vas chercher Claire à la gare, et tu penses à Solène tout l'après-midi."LÉO (defensive, in French): "Je n'ai pas dit ça."MARGOT (casually, without looking at him, in French): "Et si Claire ne venait pas ?"Léo stops walking on the path.LÉO (in French): "Pourquoi tu dis ça ?"MARGOT (turning back to him, calm, in French): "Elle m'a appelée hier soir." Silence.
Léo stands still among the yellow gorse, stunned, the wind in his hair. Margot gives him a small enigmatic smile, turns and keeps walking ahead along the cliff path. Léo watches her go, then slowly follows. The final image lingers on the two figures on the winding path above the sea.Natural acting, realistic gestures and subtle facial expressions, spontaneous and talkative mood. Live direct sound: sea breeze in the microphone, distant waves crashing below, seagulls, insects buzzing in the gorse, footsteps on the dry path.
```

<a id="dialogue-16"></a>
### 75. 조용한 해변의 절제된 대화

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-16#dialogue-16)** · [원본 게시물](https://x.com/shikoba_86/status/2107845428284715318)

https://github.com/user-attachments/assets/d799e31c-8972-4e11-99db-999adc069959

**프롬프트:**

```text
Use the start image as the opening frame and preserve the same coastal location: the rocky shoreline, small beach, calm bay, dirt path on the right, distant pier, and the rock wall across the cove.

Create a grounded multi-shot dialogue scene at dusk.

Two people enter from the dirt path on the right and walk toward the beach. They stop near the shoreline and have a tense, restrained conversation.

Use exactly the following dialogue and do not add, replace, paraphrase, or improvise any other spoken words:

Character A: “You said no one would be here.”
Character B: “I was wrong.”
Character A: “Then why did you bring me?”
Character B: “Because you needed to see this.”

Each line must be spoken only by the assigned character.
Do not overlap dialogue.
Leave a short natural pause between each line.

Character A is suspicious and increasingly uneasy.
Character B stays calm, controlled and slightly evasive.

Structure the scene as:
1. Wide establishing shot of the empty shoreline.
2. Wide shot as both characters enter from the path.
3. Medium two-shot as they stop.
4. Over-the-shoulder on Character A.
5. Over-the-shoulder on Character B.
6. Close reaction on Character A.
7. Close or medium close-up on Character B.
8. Final wider shot holding both characters near the shoreline.

Maintain character identity, clothing, screen direction, eyelines and beach geography across every shot.

No additional voices.
No additional dialogue.
No background music.
No captions.
```

<a id="dialogue-17"></a>
### 76. 왕자와 숲 마녀의 저주받은 종

작성자 [@airina_xyz](https://x.com/airina_xyz) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=dialogue-17#dialogue-17)** · [원본 게시물](https://x.com/airina_xyz/status/2117270321573277946)

https://github.com/user-attachments/assets/487f8321-233e-4a71-8f93-65471595c419

**프롬프트:**

```text
KLING 4.0 — 20-SECOND ROMANIAN FOLKLORE DARK COMEDY, 16:9, FIVE SHOTS.

VISUAL STYLE: Authentic 1977 Romanian-Czechoslovak live-action fairy-tale movie, imaginative handmade costumes, grotesque practical prosthetic makeup, soft 35mm film grain, faded analog color, atmospheric Carpathian woodland.

CHARACTERS:
BABA CLOANȚA: An ancient, hunched Romanian witch with a gigantic hooked nose, warts, enormous pointed ears, almost toothless mouth and glittering mischievous eyes. Multiple layers of ragged wool, old beads, dried herbs and tiny copper bells. Irritable, cunning, unexpectedly affectionate.

THE PRINCE: A handsome but painfully nervous young man, age 25, wearing a faded blue medieval doublet, a velvet cap and an oversized sword. Frightened of practically everything.

SETTING: Outside a ramshackle wooden witch's cottage deep in a misty Romanian forest. Twisted roots, mossy stones, bundles of dried herbs, a rough wooden counter.

DIALOGUE: Romanian only, naturally spoken with authentic Romanian pronunciation.

0:00–0:03 — MEDIUM CLOSE-UP: The prince rushes toward Baba Cloanța, breathless. He cries, "Mă urmărește un blestem!" His eyes dart around the trees.

0:03–0:07 — CLOSE-UP: The witch grins and holds up a tiny antique brass bell on a red string. She says mysteriously, "Sună când ești în primejdie."

0:07–0:11 — DETAIL SHOT: The prince takes the bell. Instantly it begins ringing violently in his hand. He looks at it, terrified.

0:11–0:15 — MEDIUM TWO-SHOT: The prince frantically shakes the bell and asks, "E stricat?" Baba Cloanța tilts her enormous head and studies him.

0:15–0:20 — EXTREME CLOSE-UP: The witch leans toward the prince until her grotesque face nearly fills the frame. She smiles with all three remaining teeth and whispers tenderly, "Nu, dragule. Sunt chiar aici." The prince slowly realizes what she means. His eyes widen. The bell rings faster. Cut to black at 20 seconds.

PERFORMANCE: Distinctive practical-makeup facial expressions, convincing frightened reactions, excellent timing. The witch is genuinely amused, never cartoonishly frantic.

CAMERA: Natural 1970s film coverage, restrained movements, expressive close-ups, clear continuity.

AUDIO: Romanian dialogue, creaking woodland branches, distant crows, wind, footsteps, increasingly frantic small brass bell. No music, no narrator, no subtitles.
```

<a id="fantasy-scifi"></a>
## 🐉 판타지와 SF

> 외계 행성, 괴수, 신, 드래곤이 등장하는 큰 스케일 장면. · 21개

<a id="fantasy-scifi-01"></a>
### 77. 시골 침실의 작은 구름 요정

작성자 [@Strength04_X](https://x.com/Strength04_X) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-01#fantasy-scifi-01)** · [원본 게시물](https://x.com/Strength04_X/status/2114623188202402063)

https://github.com/user-attachments/assets/720a77d9-22d6-4186-bc64-05797facb310

**프롬프트:**

```text
Create a 30-second ultra-realistic cinematic fantasy video featuring a completely original miniature cloud creature in a charming countryside bedroom.

Scene 1 (0–7 seconds): A tiny floating cloud creature with fluffy white fur, pale blue eyes, tiny dangling feet, and miniature translucent wings drifts above a wooden bedside table. Soft morning sunlight enters through linen curtains while dust particles shimmer in the air.

Scene 2 (7–14 seconds): A young woman wearing a peach-colored cardigan and a cream skirt enters the room. The little cloud follows her curiously, hovering above her head. Suddenly, it sneezes and releases a tiny shower of sparkling raindrops onto her hair.

Scene 3 (14–23 seconds): The woman looks surprised before smiling and holding out her hands. The cloud becomes excited and accidentally creates a miniature rainbow inside the room. Tiny floating droplets turn into glowing bubbles that gently drift around the furniture.

Scene 4 (23–30 seconds): The cloud settles onto the woman's head like a fluffy hat. It produces one final tiny raindrop that lands on its own nose. The creature crosses its eyes trying to look at the drop, then giggles silently as a miniature rainbow appears above it.

Visual style: Original imaginary creature, realistic fluffy cloud texture, expressive blue eyes, physically believable water droplets, soft volumetric sunlight, realistic reflections, pastel color palette, detailed fabric textures, cinematic close-ups, natural character animation, smooth camera movements.

Duration: 30 seconds. Aspect ratio: 16:9. 4K cinematic quality. Preserve the same creature and woman across all scenes. No text, subtitles, logos, or watermark. Use original designs only.
```

<a id="fantasy-scifi-02"></a>
### 78. 전장에서 깨어나는 뇌제

작성자 [@RizwanAly07](https://x.com/RizwanAly07) · 29초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-02#fantasy-scifi-02)** · [원본 게시물](https://x.com/RizwanAly07/status/2112516449080348958)

https://github.com/user-attachments/assets/38f593ff-ac42-4471-9b48-41393839cbf4

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
DURATION: 30 seconds | FORMAT: horizontal 16:9
STYLE: Ultra-photorealistic dark fantasy combat, 8K HDR, 24fps.

CHARACTER LOCK — ABSOLUTE PRIORITY
image1 = Only reference for the adult MALE Jiangshi protagonist. Preserve his exact male face, hairstyle, outfit, physique, and accessories. Never change his gender, face, or identity.
image2 = Only reference for consistent enemy monsters.

ENVIRONMENT
Vast stormy green battlefield, thousands of monsters, gigantic demons, ruined Taoist temples, shattered altars, navy storm clouds, cyan-white lightning, golden talismans, and black demonic energy. Never show an empty battlefield.

0–5s — LIGHTNING DASH
The male Jiangshi dodges monster claws, slides across grass, and throws explosive golden talismans. Lightning-powered punches and kicks destroy enemies. He says: "비켜라."

5–10s — THUNDERBLADE TORNADO
TECHNIQUE 1: 뇌부천쇄 · 천뢰풍폭
Thousands of lightning blades form a gigantic golden-cyan tornado, tearing through monster armies and destroying stone altars. He charges forward, shouting: "천뢰를 받아라!"

10–15s — THUNDERSTORM
TECHNIQUE 2: 구천뇌우 · 만뢰천폭
He slams a golden talisman into the ground. A colossal Bagua formation appears overhead, unleashing thousands of lightning bolts and three interconnected thunder tornadoes. He shouts: "하늘이여, 쓸어버려라!"

15–20s — LIGHTNING PRISON
TECHNIQUE 3: 팔괘천뢰진 · 팔방봉멸
Eight enormous golden sealing pillars rise, connecting sky and ground with cyan lightning. A gigantic octagonal prison traps thousands of monsters in crushing electrical chains. He shouts: "뇌문, 개방!"

20–25s — DEMON KING
The formations explode in a massive blue-white shockwave. A mountain-sized demon king emerges from black storm energy. The protagonist dodges, attacks with lightning-powered palms, and launches aerial counterattacks before being blasted backward.

25–30s — FINAL ULTIMATE
FINAL TECHNIQUE: 구천뇌제 · 만뢰천벌
He raises a golden talisman as thousands of lightning bolts converge around him. He says: "구천의 벼락이…" then shouts: "네놈을 멸하리라!"

A colossal golden-cyan Bagua formation fills the sky. Thousands of gigantic lightning bolts merge into a devastating thunder pillar, engulfing the demon king in an enormous explosion.

FINAL FRAME: The recognizable male protagonist stands in the foreground as lightning illuminates the monster army and ruined temples.

CAMERA: Dynamic tracking, aggressive whip-pans, fast combat cuts, dramatic low angles, realistic impact shake, continuous battlefield action.

NEGATIVE: No female characters, gender swapping, face morphing, identity changes, outfit changes, inconsistent monsters, cartoon CGI, teleportation, empty backgrounds, logos, subtitles, or watermarks.
```

<a id="fantasy-scifi-05"></a>
### 79. 밤 옥상 위에 떠오르는 빛의 도형

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-05#fantasy-scifi-05)** · [원본 게시물](https://x.com/EndFolding79421/status/2112376857773428953)

https://github.com/user-attachments/assets/3bb6eea4-c372-4302-b149-e13726a79023

**프롬프트:**

```text
A realistic woman stands alone on a rooftop at night. The city lights below glow softly in purple and pink hues. Thin fog drifts across the rooftop. A massive digital moon flickers slightly in the sky. Memory fragments — soft glowing symbols and faces — float around her. Her dress shimmers, and her hair moves slowly in the wind. The camera glides left to right with no zoom. Subtle glitch pulses appear in the sky. The atmosphere is quiet, mysterious, dreamlike, surreal.
[Negative Prompt] no anime, no crowd, no facial distortion, no logos, no daytime light, no cartoon visuals, no fire or smoke, no fantasy creatures, no close-up zooms.
```

<a id="fantasy-scifi-06"></a>
### 80. 캠코더로 찍은 도시 크기의 괴수

작성자 [@CaptainHaHaa](https://x.com/CaptainHaHaa) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-06#fantasy-scifi-06)** · [원본 게시물](https://x.com/CaptainHaHaa/status/2113996003913179501)

https://github.com/user-attachments/assets/99371ab2-08a2-4b01-b813-91451618f72d

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
30-second terrifying amateur camcorder recording of a colossal creature rampaging through the city district in the supplied reference. Preserve the dusty brick main street, vintage parked cars, blue pickup truck, storefronts and water tower.Match the creature exactly: enormous ridged head, gaping toothed mouth, hanging facial tentacles, hooked claws and vast ragged wings. Maintain its immense scale relative to the buildings. One continuous handheld recording from street level. The unseen camera operator is frightened but keeps trying to capture what’s happening. No additional visible people or creatures.

CAMCORDER LOOK:
Weathered consumer videotape footage: muted brown colours, blown-out dusty skies, colour bleed, interlacing, mild tracking distortion and imperfect autofocus. Sudden zooms amplify hand tremor. Exposure struggles when dust fills the frame. Keep the monster readable between disturbances.

[00:00–00:06]
Begin with the reference street composition, already trembling slightly in the operator’s hands.The creature takes an immense step towards the street, shoulders rolling and facial tentacles swinging with its momentum. Dust erupts around its feet. The operator hurriedly zooms towards its face, overshoots, then widens enough to recover its head and wings.The monster lifts its head and releases a deep, ragged roar. The recording microphone distorts at the peak.

[00:06–00:13]
The creature drives one clawed forelimb through the corner of a brick building. The wall buckles at the impact point, then masonry and roof timbers tumble into the street.The operator flinches, briefly pointing at the road before snapping back towards the destruction. Autofocus catches airborne dust, then finds the creature again.Its torn wings begin opening, scraping roof edges and pulling loose signs from their brackets.

[00:13–00:20]
A massive wingbeat sends a pressure wave down the street. Dust, paper and loose debris race towards the camera. Shop awnings thrash, parked vehicles rock on their suspensions and a storefront window shatters.The operator retreats towards the blue pickup, camera bouncing with hurried backward steps. The truck’s bonnet enters the foreground as the operator crouches behind it.Peer over the bonnet to reveal the monster still advancing through the haze, each footfall shaking the image.[

00:20–00:26]
From behind the pickup, the operator attempts another shaky zoom. The creature turns its head towards the camera’s position. Its tentacles curl and spread around its open mouth. 

It shoves against the nearby water tower. Metal supports bend, the tank tilts and a torrent of water pours across the rooftops as the structure collapses behind it.The camera jerks sideways at the crash, then finds the monster’s silhouette looming through water spray and dust.

[00:26–00:30]
The creature surges forward, lowering its head into the street.The operator abandons the shot and runs. The camera whips towards the pavement, catching blurred glimpses of kerb, truck tyres and shopfronts. Heavy footsteps and panicked breathing dominate the recording.
One final involuntary glance backwards catches its enormous wing sweeping across the dusty sky. Abrupt tape breakup, then cut to black.

MOVEMENT AND PHYSICS:
Give the creature tremendous weight: deliberate foot placement, shifting shoulders, heavy wing membranes and tentacles that lag behind head movements. Buildings break only where struck, with debris falling naturally. Maintain the street layout and accumulating damage throughout the continuous take.

SOUND:
Full camcorder audio: deep ground-shaking footsteps, layered animalistic roars, tearing metal, cracking masonry, falling bricks, shattering glass, wing buffets, rushing water and distant emergency sirens.Include microphone wind distortion during the pressure wave, handling bumps, the operator’s breathing and shoes scraping the pavement. Loud impacts briefly overload the microphone. 

No intelligible dialogue.
No music
The raw recorded destruction carries the entire scene.
```

<a id="fantasy-scifi-07"></a>
### 81. 작은 불의 정령을 부르는 연금술사

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-07#fantasy-scifi-07)** · [원본 게시물](https://x.com/shikoba_86/status/2111101132223205663)

https://github.com/user-attachments/assets/261c0811-e0f0-4a97-856f-6935c49f204a

**프롬프트:**

```text
A cramped alchemist's workshop at night, inside an old stone tower, lit only by candles. Rain on a small window.
Shot 1, wide: the alchemist stands at a cluttered wooden table full of glass jars and an open book.
Shot 2, medium: she slowly pours a glowing green liquid into a round glass vial.
Shot 3, close-up on the vial: the liquid flashes into golden light and a tiny fire spirit made of living flame rises out of it.
Shot 4, medium close-up: the spirit lands on her open palm, lighting her face orange. She whispers: "Finally. After a hundred tries."

CHARACTER LOCK: Alchemist: woman in her late 30s, long dark red hair tied back, ink-stained fingers, dark green apron over a cream linen shirt. Fire spirit: hand-sized figure of orange and gold flame with two bright white eyes. Same faces and outfits in every shot.
LOCATION: worn stone walls, melted candle wax, scattered parchment, deep shadows in the corners. 
AUDIO: rain, crackling candles, glass clinking, a soft whoosh when the spirit appears, her whisper. No music.
AVOID: no subtitles or on-screen text, no extra characters, no warped hands or glass.
```

<a id="fantasy-scifi-08"></a>
### 82. 공성 전의 성문 파괴자

작성자 [@itsPixieVerse](https://x.com/itsPixieVerse) · 30초 · 4:5 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-08#fantasy-scifi-08)** · [원본 게시물](https://x.com/itsPixieVerse/status/2112554401747578929)

https://github.com/user-attachments/assets/d8341755-26ad-459e-bdbf-1c54967298f5

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Photorealistic live-action cinema, shot on a digital cinema camera with real prime/anamorphic lens characteristics, authentic lens flares, subtle chromatic aberration, natural film grain, true cinema color grading. Real human anatomy at natural adult proportions, real skin with visible pores and natural imperfections, real fabric with visible weave and natural physics, real hair with natural flow and flyaways. Real practical and digital VFX blended seamlessly with live-action photography --- physically accurate particles, pyrotechnics, water, dust, and debris, real motion blur matching a natural shutter angle. Soft cinematic lighting with motivated shadows and a subtle rim light, shallow depth of field. 

NOT flat 2D, NO cel-shading, NO anime style, NO painterly brushwork, NO cartoon outlines. Also NOT a CGI render, NOT computer-generated-looking, NOT a 3D animated character, NOT a video-game character, NOT a toy or collectible figurine, NOT a statue, NOT stylized. Also NOT video game footage, NOT an in-game cutscene, NOT third-person action-game camera, NOT a boss-fight arena, NO HUD, NO health bars, NOT real-time game-engine rendering. This is indistinguishable from a real filmed movie. 

CUT DISCIPLINE: 7 distinct hard cuts timed explicitly below — do not render as one continuous take. Character maintains physical momentum and heavy exertion; no idle or showing-off poses until the final 2 seconds. 

WORLD: Narrow collapsed stone fortress gatehouse under nighttime siege bombardment. Smoldering timber, mud, flying cinders, burning background barricades, palette of charcoal iron, olive canvas, raw linen with burning amber and red accents. 

CHARACTER : A heavily muscled veteran sapper in his late 50s, weathered scarred face, short grey hair and beard, wearing a massive domed cast-iron right pauldron, torn cream canvas cowl, exposed right arm with linen wraps, spiked gauntlet, baggy frayed olive trousers, dented iron greaves, holding a giant notched iron slab shield and red-hilted broadsword. 

CINEMATIC FIGHT DESIGN (7 Trailer Cuts, 30s Total):
• HARD CUT at 0:00 (Shot 1 | 3s | Establishing Wide): Low-angle slow track through burning stone gatehouse; embers drift through falling dust as distant siege horns blare, 24mm lens.
• HARD CUT at 0:03 (Shot 2 | 3s | Macro Detail): Macro insert on his right hand clenching the red leather sword wrap, leather creaking, sparks bouncing off his spiked gauntlet, 85mm lens.
• HARD CUT at 0:06 (Shot 3 | 4s | Low Close-up): Low push-in on Torstein’s scarred face; cold grey eyes lock onto incoming threat, heavy breath condensing in freezing air as ash falls on his white hair.
• HARD CUT at 0:10 (Shot 4 | 4s | Planting Shield): Ground-level tracking shot; Torstein slams the base of the massive iron slab shield into mud and broken stone, locking his iron sabatons into position.
• HARD CUT at 0:14 (Shot 5 | 5s | Shockwave Impact): Tight OTS shot; catapult projectile slams directly into his shield in a blinding explosion of sparks and splintering wood, forcing him to slide back two feet through deep mud under raw physical strain.
• HARD CUT at 0:19 (Shot 6 | 6s | Scale Reveal): Extreme wide low-angle crane reveal; the smoke clears to show the lone armored veteran holding the narrow chokepoint breach against thousands of torchlit siege infantry charging down the ridge.
• HARD CUT at 0:25 (Shot 7 | 5s | Counter-Cleave & Resolve): Medium-wide hero shot; Torstein surges forward with a ferocious two-handed horizontal greatsword swing through the smoke, then drives the blade down into an immovable low guard. Dust settles around his silhouette in silence until 0:30.physically accurate volumetric god rays through mist, real dust particles catching the light, drifting smoke/embers with natural falloff, atmospheric haze separating foreground and background with realistic depth.

Weighty natural human movement, physically simulated cloth and hair reacting to wind and momentum, follow-through and overlapping action, realistic secondary motion, real motion blur matching a natural shutter angle, 24fps filmic motion.NOT flat 2D, no cel-shading, no anime style, no painterly brushwork, no cartoon outlines. Also NOT a CGI render, not computer-generated-looking, not a toy or figurine. Also not video game footage, not an in-game cutscene, no HUD, no health bars.
```

<a id="fantasy-scifi-09"></a>
### 83. 창백한 용의 무덤에 들어선 기사

작성자 [@itsPixieVerse](https://x.com/itsPixieVerse) · 30초 · 21:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-09#fantasy-scifi-09)** · [원본 게시물](https://x.com/itsPixieVerse/status/2112260520502005807)

https://github.com/user-attachments/assets/862f26d9-fa76-4a57-81c3-7f2d79d14f3a

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
[Shot 1 - 4.0s] Low tracking shot pushing forward behind the knight. Foreground: petrified kneeling statues half-buried in ash. Subject: The knight walks forward through deep gray ash, battered cape swaying in cold drafts. Background: the colossal slumped silhouette of the four-winged dragon. Pale, cold moonlight cuts downward through a fractured dome fissure on the right, casting sharp chiaroscuro edges across ash-dusted stone and dark rusted iron. The camera tracks forward at hip level with subtle handheld micro-shake. Cut on the knight halting.

[Shot 2 - 3.0s] Low-angle close-up. Foreground: cracked flagstones buried in fine ash. Subject: The dragon’s stony jaw pinned to the floor by a thick black-iron spear; the knight enters the frame and grips the rusted shaft with both gauntlets. Background: towering petrified scales looming in darkness. Pale, cold moonlight cuts downward through a fractured dome fissure on the right, casting sharp chiaroscuro edges across ash-dusted stone and dark rusted iron. The camera pushes in tight on the spearhead. Cut on gauntlets locking onto the iron.

[Shot 3 - 2.5s] Medium close-up, Dutch angle. Foreground: the knight's pitted visor. Subject: The knight wrenches the heavy spear upward; bright sparks shower outward as the iron blade grinds free of stone and bone, spraying ancient ash. Background: the dragon's flared nostril twitching. Pale, cold moonlight cuts downward through a fractured dome fissure on the right, casting sharp chiaroscuro edges across ash-dusted stone and dark rusted iron. The camera jolts backward in sudden recoil. Cut on the spear wrenching free.

[Shot 4 - 4.5s] Medium profile tracking upward. Foreground: the heavy spear clattering into the ash. Subject: The archdragon’s golden slit eye snaps open; its jaw unhinges with a grinding crack, venting plumes of pale soul-smoke as its neck arches up. Background: crumbling vaulted arches trembling in shadow. Pale, cold moonlight cuts downward through a fractured dome fissure on the right, casting sharp chiaroscuro edges across ash-dusted stone and dark rusted iron. The camera pans upward following the rising horned skull. Cut on the jaw snapping fully open.

[Shot 5 - 7.0s] Wide tracking arc moving right. Foreground: stone statues toppling and shattering on the floor. Subject: The dragon heaves onto its front talons; its four ragged stone wings snap open, smashing flanking gothic pillars into flying rubble. Background: the collapsing dome shaking violently. Pale, cold moonlight cuts downward through a fractured dome fissure on the right, casting sharp chiaroscuro edges across ash-dusted stone and dark rusted iron. The camera sweeps laterally through falling ash clouds. Cut on a massive wingbeat shockwave.

[Shot 6 - 9.0s] Ultra-wide hero shot (The Withheld Reveal). Foreground: the knight stands minute at screen center, drawing a greatsword in a two-handed guard. Subject: The ancient dragon rears to full height; revealed chained to its neck collar is the veiled, petrified corpse of a queen, whose skeletal hand sparks with pale blue soul-fire, igniting the dragon's throat into a blinding white-blue firestorm that illuminates the entire mausoleum. Background: the ruined dome raining ash and moonlight. Pale, cold moonlight cuts downward through a fractured dome fissure on the right, casting sharp chiaroscuro edges across ash-dusted stone and dark rusted iron. The camera cranes slowly backward and upward, holding the iconic boss title-card confrontation.
```

<a id="fantasy-scifi-10"></a>
### 84. 살아 있는 외계 터미널 1인칭 산책

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 12초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-10#fantasy-scifi-10)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2110755047910900091)

https://github.com/user-attachments/assets/a1146e32-73b6-4142-a312-30928b96a9d4

**프롬프트:**

```text
First-person cinematic POV inside a living extraterrestrial transit terminal grown from pale coral and translucent membranes. An original humanoid alien with opalescent skin, narrow amber eyes, and delicate crystalline ridges sits beside a basin of luminous drinking water. Its anatomy remains consistent throughout. As the viewer approaches, it covers the basin with one trembling hand. In a soft, precise English voice, it says: “Don't drink the water. It carries the colony's memories. Drink enough... and there won't be any room left for yours.” Moving shadows inside the water briefly resemble thousands of crowded faces. The alien struggles to recall a word, then falls silent. One continuous take, intimate framing, photoreal creature effects, organic architecture, cold bioluminescent lighting, subtle breathing and distant biological pulses, clear lip sync, no captions. 😉
```

<a id="fantasy-scifi-11"></a>
### 85. 실험실에서 깨어나는 안드로이드

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 22초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-11#fantasy-scifi-11)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2112388230582579245)

https://github.com/user-attachments/assets/8cfb1171-906f-48dd-b983-e53746a0db1c

**프롬프트:**

```text
Ultra-realistic cinematic close-up of an elegant female android awakening inside a sterile futuristic laboratory, intricate chrome machinery unfolding around her skull like mechanical petals, dozens of articulated robotic arms reconnecting cables and neural interfaces, tiny red status lights pulsing beneath translucent skin, her glowing crimson eyes slowly focusing on the camera, subtle breathing motion, micro facial expressions, hydraulic pistons moving naturally, camera slowly dollies forward while orbiting around her face, shallow depth of field, realistic reflections on polished metal, volumetric laboratory haze, physically accurate motion, seamless mechanical animation, high-end sci-fi film realism 😉
```

<a id="fantasy-scifi-12"></a>
### 86. 거대한 손이 마을로 던지는 바위

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 25초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-12#fantasy-scifi-12)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2112122589845790790)

https://github.com/user-attachments/assets/0105b9a8-df13-4436-9188-d951697da314

**프롬프트:**

```text
A god hand grabs a huge boulder from a mountain and throws it toward an enemy settlement, the camera follows the rock through the air before it crashes outside the city walls, villagers running in panic, dramatic but playful god-simulation presentation.
```

<a id="fantasy-scifi-13"></a>
### 87. 폭풍 만에서 솟아오르는 괴물

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-13#fantasy-scifi-13)** · [원본 게시물](https://x.com/shikoba_86/status/2107845423276634467)

https://github.com/user-attachments/assets/df2a1a3d-1b3d-4c91-a20e-99cf1346bb6f

**프롬프트:**

```text
Use the start image as the exact opening frame and preserve the identity of the coastal location: the rocky shoreline, narrow sandy beach, curved dirt path on the right, calm bay, wooden posts in the foreground water, small pier in the distance, and the large rock wall on the far side of the cove.

Build a multi-shot scene that begins in quiet stillness and then pushes the same location into its opposite extreme.

Opening: the sea is calm, the air is still, and the scene feels cold and quiet at dusk.

Then the weather begins to shift. Wind rises across the shoreline. The water becomes rougher. Dark storm clouds roll in over the bay. Rain begins falling and waves crash harder against the rocks and beach.

From the sea, a monstrous humanoid figure slowly emerges from the stormy water. It first appears at a distance, partially obscured by rain, sea spray and waves, then continues walking toward the shore with heavy deliberate steps.

Structure the scene as a multishot sequence:
1. Wide establishing shot of the calm coast.
2. Environmental shot as the storm takes over.
3. Medium-long shot of the figure appearing from the sea.
4. Closer dramatic shot as the creature walks through the waves.
5. Final wide or medium-wide shot as it approaches the beach.

Keep the geography of the original location coherent throughout the sequence.

Sound: rising wind, distant thunder, rain, crashing waves and heavy water movement around the creature.
No background music.
No captions.
```

<a id="fantasy-scifi-14"></a>
### 88. 빙원을 건너 외계 유적으로 가는 탐사대

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-14#fantasy-scifi-14)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2109581274755027228)

https://github.com/user-attachments/assets/c91984fc-ed66-46de-8b2e-9884f92bba73

**프롬프트:**

```text
A small expedition team crosses a frozen plain toward colossal alien ruins beneath flowing green and violet auroras. Black geometric towers rise from the snow, their surfaces interrupted by narrow cyan energy seams. The closest explorer carries a compact scanning device projecting a soft orange glow onto armored gloves. Windblown snow partially obscures the distant structures, emphasizing their immense scale. Mass Effect-inspired ancient civilization mystery, grounded military equipment, cinematic wide shot, deep blue night palette, realistic snow and metal textures
```

<a id="fantasy-scifi-15"></a>
### 89. 거대한 외계 고리 아래의 전투

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-15#fantasy-scifi-15)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2114331350807302426)

https://github.com/user-attachments/assets/267b26f9-1df3-4dc6-947a-0a87f9d92c06

**프롬프트:**

```text
Dozens of armored soldiers fight across an enormous desert battlefield beneath a gigantic alien ring megastructure. Every visible character is moving: infantry sprint between craters, two soldiers drag a wounded teammate toward cover, another group fires toward airborne enemies while robed figures run through the chaos. Suddenly the massive blue vortex beneath the megastructure activates and begins pulling soldiers, vehicles, sand and debris upward. Several characters struggle against the force, grabbing each other and nearby rocks. One soldier loses his footing and another catches his arm before he is pulled away. The camera moves rapidly through the battlefield between running characters, then rotates upward following debris toward the gigantic structure. Huge scale, continuous background action, realistic physical reactions, moving clothing and armor, explosions, atmospheric distortion, epic cinematic sci-fi warfare.
```

<a id="fantasy-scifi-16"></a>
### 90. 정글을 누비는 기계 포식자

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 22초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-16#fantasy-scifi-16)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2110996674558530007)

https://github.com/user-attachments/assets/67e18b80-d19c-42f5-b92a-93d3dcaae537

**프롬프트:**

```text
A living mechanical predator with a glowing orange central eye moves through dense alien jungle vegetation, using long metallic limbs wrapped in pulsing flesh to pull itself between trees, organic tendrils grabbing branches while hydraulic joints extend and retract, the creature suddenly notices the camera and rapidly charges forward, handheld tracking camera retreats through foliage, branches break naturally, mud splashes, vines react realistically, intense acceleration, realistic weight and momentum, dark cinematic lighting, high-end creature VFX.
```

<a id="fantasy-scifi-17"></a>
### 91. 해 뜰 무렵 깨어나는 구형 외계 마을

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 22초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-17#fantasy-scifi-17)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2110997691274580344)

https://github.com/user-attachments/assets/f0f1e1ce-2d2b-4aa3-879e-7c3fd62bde5b

**프롬프트:**

```text
A colorful alien settlement filled with enormous spherical buildings and bizarre organic machines comes alive at sunrise, round red mechanical houses rotate their giant lens-like windows, pipes expand and contract like breathing organs, small robotic creatures run through shallow water, flying vehicles weave between towers, camera glides smoothly through the town at ground level before rising above the rooftops, puddles reflecting neon lights and clouds, natural vegetation moving in the wind, playful but believable extraterrestrial world, cinematic photorealism.
```

<a id="fantasy-scifi-18"></a>
### 92. 소환된 괴수를 향해 달리는 거대 사자

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 25초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-18#fantasy-scifi-18)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2111372306761290098)

https://github.com/user-attachments/assets/912f7efc-60c9-416b-8685-546f86d73d43

**프롬프트:**

```text
A gigantic lion stands on a hill overlooking several ancient villages when a dark god summons an enormous enemy creature in the distance, thunderclouds spiral overhead, the lion roars and sprints downhill toward the coming battle.
```

<a id="fantasy-scifi-19"></a>
### 93. 대전된 성운을 통과하는 우주선

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 25초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-19#fantasy-scifi-19)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2115004381942718696)

https://github.com/user-attachments/assets/d4a09013-993f-40ad-aa49-458f919278be

**프롬프트:**

```text
An exploration ship maneuvers through a vast cloud of charged gas and floating debris. Inside the cockpit, the pilot moves the controls while the captain braces against the console and an alien crew member monitors the storm. The camera moves from the crew toward the forward window, cinematic tension, realistic motion.
```

<a id="fantasy-scifi-20"></a>
### 94. 육족 짐승 무리 곁을 걷는 탐험가

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 25초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-20#fantasy-scifi-20)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2115723998700949688)

https://github.com/user-attachments/assets/81becd60-d70b-458d-90d2-b49ed07e8641

**프롬프트:**

```text
Three explorers walk through tall grass on an alien plain as a herd of enormous six-legged creatures passes nearby. The animals lower their long necks to feed while smaller creatures fly around them. One explorer raises a scanner and another follows the herd. Cinematic tracking shot, realistic creature animation, sense of wonder.
```

<a id="fantasy-scifi-21"></a>
### 95. 석호를 건너는 긴 목의 외계 거수

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-21#fantasy-scifi-21)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2110982744247353611)

https://github.com/user-attachments/assets/ee920547-9d24-41c8-bd2e-10e69ba2c40f

**프롬프트:**

```text
Two enormous long-necked alien animals slowly walk through a shallow turquoise lagoon surrounded by bright red grass and exotic palm forests. Their massive bodies create realistic waves and splashes with every step while smaller creatures flee along the shoreline. The camera begins low near the water and smoothly cranes upward, revealing the gigantic animals against a glowing yellow-green sky and distant mountains. Realistic weight and inertia, detailed skin movement, volumetric mist, natural vegetation motion, cinematic alien wildlife documentary, smooth continuous camera movement, highly coherent anatomy.
```

<a id="fantasy-scifi-22"></a>
### 96. 붐비는 외계 시장 산책

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 25초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-22#fantasy-scifi-22)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2116029599104561566)

https://github.com/user-attachments/assets/b2d56337-eb33-4328-8b88-2a42d83d1025

**프롬프트:**

```text
A human traveler walks through a crowded alien marketplace filled with species of different shapes and sizes. A six-limbed merchant unfolds colorful fabrics, a robotic vendor prepares food and small creatures scurry between the stalls. The camera weaves through the moving crowd, cinematic space opera, rich realistic detail.
```

<a id="fantasy-scifi-23"></a>
### 97. 두 개의 태양 아래 첫 접촉

작성자 [@Alin_Reaper05](https://x.com/Alin_Reaper05) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=fantasy-scifi-23#fantasy-scifi-23)** · [원본 게시물](https://x.com/Alin_Reaper05/status/2114038906366693737)

https://github.com/user-attachments/assets/6e7534e8-7853-426b-ad46-4c59a67e101b

**프롬프트:**

```text
On a mysterious alien planet beneath two enormous glowing suns, a female astronaut cautiously approaches a tall biomechanical alien being. The alien slowly raises one hand toward her helmet, but suddenly both characters react as the ground violently trembles. The astronaut loses balance and catches herself while the alien turns rapidly toward the horizon. Strange flying creatures burst from the distant valley. The alien grabs the astronaut and pulls her behind a rock formation as energy projectiles streak overhead. She draws a compact futuristic weapon while the alien extends its arms and generates a shimmering defensive field. The camera circles around both characters continuously, switching from intimate close-ups to fast tracking shots, realistic body reactions, moving helmet reflections, atmospheric particles, strong wind, fluid character interaction, cinematic first-contact action.
```

<a id="animation"></a>
## 🧸 애니메이션

> 3D 카툰, 애니, 클레이, 페인터리 2.5D, 키네틱 타이포. · 14개

<a id="animation-01"></a>
### 98. 엄마를 위해 생일 케이크를 굽는 아들

작성자 [@aiwithaly](https://x.com/aiwithaly) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-01#animation-01)** · [원본 게시물](https://x.com/aiwithaly/status/2115085490475217187)

https://github.com/user-attachments/assets/ab4d18e0-7ef7-44e4-8e5a-a08d79cbee34

**프롬프트:**

```text
10 seconds | 16:9 | Cinematic 3D Anime | High-Quality Animation | Heartwarming Family Story.

A young East Asian man named Ming tries to bake a birthday cake for his beloved mother, but everything goes hilariously wrong. Flour explodes across his face, his mixer breaks, and his cake burns in the oven. Disappointed but determined, he buys a simple cupcake and visits his mother. When she notices the flour smudge on his nose, she smiles with pure affection and embraces him warmly. He hugs her back, realizing that love matters more than a perfect gift.

Visual Style: Beautiful cinematic 3D anime, expressive facial animation, warm golden lighting, detailed environments, smooth camera movements, realistic object physics, soft depth of field, and consistent character designs.

Audio: Playful piano, comedic kitchen sound effects, gentle orchestral strings, a joyful laugh, and an emotional musical ending. No dialogue, narration, subtitles, or on-screen text.

Negative Prompt: No character redesign, inconsistent clothing, distorted hands, extra fingers, duplicated characters, unnatural movement, flickering, random cuts, unwanted text, logos, or watermarks.
```

<a id="animation-02"></a>
### 99. 셰이커 네 개를 다루는 문어 바텐더

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 5초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-02#animation-02)** · [원본 게시물](https://x.com/EndFolding79421/status/2112371662452601207)

https://github.com/user-attachments/assets/209744a4-2514-4899-bb8e-3939a8425828

**프롬프트:**

```text
An octopus expertly shakes four cocktail shakers at once behind a neon bar [wide shot]. He tosses them all in the air and catches three—then realizes one’s missing just as a customer gets splashed in the face [camera tilt-up, splash freeze-frame].
```

<a id="animation-03"></a>
### 100. 두 애니 캐릭터의 옥상 파쿠르

작성자 [@Ayu_AI_0912](https://x.com/Ayu_AI_0912) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-03#animation-03)** · [원본 게시물](https://x.com/Ayu_AI_0912/status/2112801128442425495)

https://github.com/user-attachments/assets/b358935c-5fce-417d-9b2b-0f3d938e7b8c

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
15秒、16:9、1080p、8カット構成の、
高予算の2Dアニメ映画品質で描く
シネマティックな超上級パルクール映像。登場人物は2人。

主人公は添付画像の1人目、もう1人は添付画像
の2人目のキャラクター。添付画像を2人それぞれのキャラクターデザインの参照として使用し、顔立ち、髪型、髪色、服装、配色、年齢感、体格、全体の雰囲気を忠実に踏襲し、全カットで一貫して維持すること。2人の特徴や衣装を混同せず、それぞれを明確に描き分ける。以下の主人公のアクションとカット構成は維持し、もう1人は主人公と並走、または少し前後した位置で同じルートを進む。2人の動作には自然な時間差をつけ、互いに接触せず、それぞれの身体と動きが明確に見えるようにする。舞台は快晴の現代日本の都市。東京、渋谷、横浜を思わせる屋上、路地、階段、手すり、配管、コンクリート壁を舞台に、主人公が世界トップレベルのフリーランニングを披露する。

【カット1｜00:00〜00:01.60】
ローアングル後方追従。主人公が一気に加速し、腰ほどの高さの障害物をコングヴォルトで飛び越える。

【カット2｜00:01.60〜00:03.40】
正面ローアングル。ウォールランからティックタックを決め、向かいの屋上へジャンプして着地する。

【カット3｜00:03.40〜00:05.20】
横方向トラッキング。プレシジョンジャンプで細い足場へ着地し、そのままキャットリープで高い壁へ飛びついて登る。

【カット4｜00:05.20〜00:07.20】
屋上追従ショット。ダッシュヴォルトで障害物を越え、そのままウェブスターで屋上の隙間を飛び越える。

【カット5｜00:07.20〜00:09.20】
俯瞰移動カメラ。ダイブロールで着地の衝撃を吸収し、そのまま長い手すりをスピードヴォルトで攻略する。
【カット6｜00:09.20〜00:11.30】
正面から後退するハンドヘルド撮影。アンダーバーで低い障害物を通過し、その直後にサイドフリップで次の障害物を越える。
【カット7｜00:11.30〜00:13.20】
後方斜め上からのドローン撮影。パームスピンからコングヴォルトへ滑らかにつなぎ、最後のジャンプへ向けて全力で加速する。
【カット8｜00:13.20〜00:15.00】
クライマックス。大きな屋上の隙間へ向かって跳躍し、高く美しいコークスクリューを決める。カメラは空中で主人公の周囲を回り込む。正確に着地した後、そのままスピードを落とさず画面奥へ走り去る。

【映像スタイル】
高予算の劇場用2Dアニメ映画品質。全編を、緻密な手描き作画と美しい背景美術による2Dアニメーションで統一する。添付キャラクターのデザインを維持した、精密で安定した線画と豊かなセル調の陰影。快晴の強い日差し、都市の奥行き、光と影を映画的に描く。世界大会レベルのフリーランニング。リアルな重心移動。自然な筋肉の動き。リアルな着地衝撃。髪や衣装が風や動きに合わせて自然に揺れる。躍動感のある作画と滑らかな動きで、踏み切り、空中姿勢、着地の連続性を明確に表現する。背景は鮮明に保ち、高速移動中のみ自然なモーションブラーを使用する。ハンドヘルド撮影やドローン撮影などの指定は、2Dアニメーション上のカメラワークとして表現する。

【禁止】人物の雰囲気や服装が大きく変化すること。添付キャラクターから顔立ちや体格が大きく逸脱すること。2人の顔、髪型、衣装、配色が入れ替わること。指定した2人以外の人物が登場すること。髪型や配色の不自然な変化。顔や身体の崩れ。手足の増殖。分身。身体の融合。貫通。電線を通過すること。ワープ。浮遊。不自然な着地。実写調。3DCG調。
```

<a id="animation-04"></a>
### 101. 「절대 누르지 마」 3D 키네틱 타이포

작성자 [@su_nagomi](https://x.com/su_nagomi) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-04#animation-04)** · [원본 게시물](https://x.com/su_nagomi/status/2110877883128574135)

https://github.com/user-attachments/assets/fd600e54-83f8-4c18-ba33-93429e48a4f9

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
【30秒｜16:9｜3Dキネティックタイポグラフィ×ポップアート｜テーマ：絶対に押すな！｜BGM無し／SEあり／日本語文字を正確に表示】 【全体仕様】1920×1080、30fps、極太3Dゴシック体、赤・黄・ピンク・青・白の鮮やかな配色。文字は光沢のある立体樹脂素材。文字そのものが意思を持って動き、伸縮・衝突・回転・飛散・再結合する。カメラは高速ドリー、ウィップパン、マクロ、ローアングルを使い分ける。スタジオ照明と漫画的な集中線を組み合わせる。画面転換は文字の衝突や動きと同期。主役の赤いボタンは1個だけで、黒と黄色の警告ストライプ付き台座に固定。文字の形状・赤ボタンの構造・奥行き関係を全カットで統一。背景色は切り替えても空間配置の矛盾を起こさない。日本語は文字化け・不要文字・複製を禁止。音楽なし、コミカルなSEをアクションに完全同期。 CUT1【0:00–0:03】Visuals：真っ白なスタジオ空間。中央奥に巨大な赤い立体文字「絶対に押すな！」。中央手前に赤いボタン。Camera：50mm/f4、ゆっくりドリーイン。Lighting：白いソフトボックス光、床に柔らかな影。Motion：文字は静止。ただし「押」だけが一瞬小さく震える。SE：静寂→「ピッ」。Emotion：禁止されたものへの好奇心。Transition：ボタンへマッチカット。 CUT2【0:03–0:06】Visuals：ボタンのマクロショット。赤い表面に光が走る。奥の巨大文字「押」が左右を見回すように傾く。Camera：85mm Macro/f2.8、低い視点からボタンへ接近。Lighting：艶やかな白いハイライト。Motion：「押」の文字が元の配置からわずかに前へ傾く。SE：「ピッ、ピッ」、小さなゴムの軋み音。Transition：文字「押」へウィップパン。 CUT3【0:06–0:09】Visuals：「押」が文字列から抜け出し、ボタンへ向かって少しずつ前進。残った文字「す」「な」「！」が慌てたように震える。Camera：35mm/f4、斜め45度の立体構図、横方向トラッキング。Lighting：黄色のアクセント光。Motion：「押」が小さくジャンプしながらボタンへ近づき、「す」が横から阻止しようと傾く。SE：「ピョコ、ピョコ」「キュッ！」。Transition：「押」がジャンプした頂点で切り替え。 CUT4【0:09–0:12】Visuals：「押」がボタンの真上に浮く。一瞬、時間が止まる。次の瞬間、真下へ落下してボタンを押す。Camera：最初は真横のクローズアップ、押下時に広角28mmへ衝撃カット。Lighting：押下の瞬間に強烈な黄色の発光。Motion：「押」の着地→ボタン沈下→床面から衝撃波が広がる。SE：直前0.4秒無音→「ポチッ！」「ドカーン！」。Transition：衝撃波が画面を覆う。 CUT5【0:12–0:15】Visuals：背景が鮮烈な黄色へ変化。巨大な「えっ!?」が画面奥から飛び出し、周囲の文字を弾き飛ばす。Camera：24mm/f5.6、急激なドリーズーム。Lighting：明るいスタジオ光、文字の縁に白いリムライト。Motion：「えっ!?」が激しくバウンドし、スクワッシュ＆ストレッチで伸び縮み。SE：「バイーン！」「ポヨン！」。Transition：巨大文字がカメラ前を横切ってワイプ。 CUT6【0:15–0:19】Visuals：背景がビビッドピンクへ。文字たちがピンボールのように飛び回る。赤いボタンは床中央に固定されたまま。文字「押」が再びボタンへ突進して周囲の文字がパニックになる。Camera：35mm/f5.6、左右ウィップパンと素早い引き。Lighting：白いキーライト＋マゼンタのリムライト。Motion：文字が衝突・反発・回転。動く文字は手前と奥の2群に分け、視認性を保つ。SE：「ドン！」「バン！」「ビヨーン！」「カン！」。Transition：「押」がボタンに再衝突した衝撃で次へ。 CUT7【0:19–0:22】Visuals：背景が赤い警告空間へ。巨大な白い3D文字「押した…」が画面いっぱいに迫る。周囲を赤い警告灯が回る。Camera：45mm/f4、高速ドリーインから急停止。Lighting：赤い警告光と白い正面光。Motion：「押した…」が膨張し、重さに耐えられず下方向へ潰れる。SE：短いサイレン「ウーウー！」→重低音「ズシン！」。Transition：文字が画面を押し潰して青背景へ切り替え。 CUT8【0:22–0:25】Visuals：一転して静かな青背景。巨大な白い文字「だから言ったのに」が整列。床には疲れたように転がる「押」。Camera：50mm/f4、正面固定から軽いプッシュイン。Lighting：明るいクールホワイト。Motion：「だから言ったのに」が呆れたように左右へゆっくりウェーブ。「押」が小さく震える。SE：「ハァ〜……」「コロン」。Emotion：笑えるツッコミ。Transition：床から文字の破片が吸い上がる。 CUT9【0:25–0:28】Visuals：散らばった文字が渦を巻き、吸い寄せられて元の「絶対に押すな！」へ再結合。背景は白に戻る。Camera：35mm/f4、周囲をわずかに回り込みながら正面位置へ復帰。Lighting：清潔な白いスタジオ光。Motion：文字が一個ずつ元の場所に戻り、最後に「押」がはまる。SE：「シュルルル！」「カチカチカチ！」「ポン！」。Transition：完成と同時に静止。 CUT10【0:28–0:30】Visuals：CUT1と完全に同じ構図。元通りの「絶対に押すな！」と赤ボタン。安心した直後、「押」の文字だけが再びボタンに向かってわずかに傾く。Camera：50mm/f4、正面固定。Lighting：CUT1と一致。Motion：「押」の小さな傾き→ボタンが一度点滅。SE：短い沈黙→「ピッ」。Emotion：また押すのか！という予感。Transition：暗転なしでCUT1へ自然にループ。 【最重要の破綻防止】「押」は文字列から抜け出した同一個体として扱う。文字が増殖しない。ボタンは1個で位置固定。ボタンを押す瞬間は接触・沈下・反発の順序を守る。背景色変更は編集上のカット切り替えで行い、物理空間を不自然に変形させない。文字の輪郭・書体・厚みを統一。動きのピークは15〜22秒、ラストは静かに締める。最後の構図を冒頭と一致させる。。
```

<a id="animation-05"></a>
### 102. 햇살 가득한 만화 숲의 요정

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-05#animation-05)** · [원본 게시물](https://x.com/EndFolding79421/status/2110796791100711098)

https://github.com/user-attachments/assets/3772351f-0c6b-47f7-a361-299594a48787

**프롬프트:**

```text
Environment (Enchanted Forest): A vibrant, magical forest bathed in soft daylight. The trees are lush with bright green leaves, and beams of sunlight filter through the canopy, casting soft, dappled light on the forest floor. The scene feels peaceful, with sparkling particles floating in the air, enhancing the magical atmosphere.
Fairies: Small, ethereal fairies with glowing wings flutter gracefully around the forest. They leave shimmering trails of light as they move, adding to the enchanting and whimsical feel of the scene. The fairies’ glow contrasts with the natural sunlight, making them stand out in the serene forest setting.
Lighting: The scene is lit by warm sunlight filtering through the trees, creating soft patches of light and shadow on the forest floor. The fairies’ glowing wings add a magical touch of light that contrasts with the warm, natural tones of the sunlight. The lighting enhances the otherworldly feel of the scene.
Camera Movement: The camera moves slowly and steadily through the forest, capturing the beauty of the trees, the light filtering through them, and the fairies flying around. The movement should be smooth, as if gliding through the forest, giving the viewer a sense of exploration and wonder.
Atmosphere: Peaceful, magical, and whimsical, with a strong sense of enchantment. The fairies and the glowing forest add to the serene, otherworldly feel, making the forest seem alive with magic.
[Negative Prompt] Fairies: No overly bright or cartoonish fairies. Their glow should be soft and ethereal, not blinding. Avoid erratic or fast movements; fairies should fly gracefully and smoothly. Do not overcrowd the scene with too many fairies.
Lighting: Avoid harsh or artificial lighting. The sunlight should be natural and warm, with no excessive glare. Avoid overly bright spots that disrupt the magical atmosphere.
Camera Movement: No fast, jerky, or shaky camera movements. The camera should not zoom in or out abruptly. It must move steadily and smoothly through the scene.
Atmosphere: No dark, tense, or chaotic vibes. The scene should remain peaceful and whimsical. Avoid elements that feel foreboding or unsettling.
Environment: No lifeless or dull surroundings. The forest should remain lush, vibrant, and magical. Avoid modern or urban elements.
```

<a id="animation-06"></a>
### 103. 코드 같은 프롬프트로 만든 추상 영상

작성자 [@0thernes_ai](https://x.com/0thernes_ai) · 30초 · 21:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-06#animation-06)** · [원본 게시물](https://x.com/0thernes_ai/status/2116566254740029832)

https://github.com/user-attachments/assets/fab40254-15b6-425c-9dfe-d8fe11d7e243

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
fn fib(n) { if (n < 2) { return n; } return fib(n - 1) + fib(n - 2); } let primes = []; let n = 2; while (len(primes) < 10) { let is_prime = 1; let d = 2; while (d * d <= n && is_prime) { if (n % d == 0) { is_prime = 0; } d += 1; } if (is_prime) { push(primes, n); } n += 1;
```

<a id="animation-07"></a>
### 104. 백발 여전사의 하늘 전투

작성자 [@itsPixieVerse](https://x.com/itsPixieVerse) · 19초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-07#animation-07)** · [원본 게시물](https://x.com/itsPixieVerse/status/2105697908624617880)

https://github.com/user-attachments/assets/903fb24c-d0ec-4da2-a96a-4fc83e544267

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
STYLE: Cinematic 2.5D animation in the style of fully painterly rendering, characters and environments look like gouache concept-art paintings in motion, visible brush texture on skin, cloth and buildings, flat posterized color blocks with hard-edged light shapes, matte finish, soft filmic volumetric lighting, shallow depth of field. NOT flat 2D cartoon, NO bold black outlines, NO cel-shading, NOT glossy CGI, NOT Unreal Engine, NO photorealism, no plastic skin. 

WORLD & ENVIRONMENT: The Stratos Basin of Sol-Vara. Monumental cantilevered brass runways and suspension pylons floating at 15,000 feet above an endless boiling sea of thunderheads. Heavy wind gusts, rain squalls, and blinding sun shafts breaking through dark storm clouds. 

CHARACTER : Astra from the Stratos Basin of Sol-Vara. An athletic adult woman with long windswept silver-white hair, glowing emerald-green eyes, confident smirk, wearing a cropped white athletic top, billowing slate-blue hooded mantle with a circular eclipse crest, dark slate-blue short bottoms, tan utility pouch belt, forest-green gauntlets with brass cuffs, and black thigh-high boots, with a vertical beam of white-gold light blazing from her fist, elongated stylized tall proportions (10 heads tall), painterly matte skin with chunky brush-stroke shading. 

CINEMATIC TIMELINE (20 SECONDS / 6 DYNAMIC CUTS):
- 00:00 to 00:03 (Cut 1 | In Medias Res Hook - Macro Threat): Extreme macro close-up on Astra's clenched forest-green gauntlet; a blinding pillar of white-gold celestial energy erupts vertically from her knuckles with a deafening sonic crack. Sparks of raw light scatter outward, reflecting violently in her vibrant emerald-green eyes.
- 00:03 to 00:06 (Cut 2 | Evasion & Kinetic Slide): Low-angle tracking shot; Astra executes a high-speed knee slide along the rain-slick brass platform edge at mach speed. An incoming cluster of heavy artillery shells demolishes the catwalk inches behind her; her slate-blue capelet and silver hair whip violently through smoke and flying debris.
- 00:06 to 00:09 (Cut 3 | Smirk & Leap): Fast push-in on Astra's face as she vaults off the destroyed platform into empty space; unblinking emerald eyes, cocky grin, zero hesitation. She dives headfirst into the open sky between colossal floating battle-cruisers.
- 00:09 to 00:13 (Cut 4 | FPV Freefall Pursuit): Fast FPV drone chase diving at supersonic terminal velocity directly behind Astra as she freefalls through swirling storm clouds. She cocks her right arm back, pulling loose lightning and sunbeams directly into her fist, turning it into a miniature sun.
- 00:13 to 00:17 (Cut 5 | Celestial Strike & Hull Detonation): Low-angle wide clash; Astra slams her charged fist directly into the armored bridge of a colossal iron sky-dreadnought. An immense flat-painted shockwave of pure white-gold light explodes in a 360-degree ring, shearing the dreadnought's hull in two and parting the storm clouds across the entire horizon.
- 00:17 to 00:20 (Cut 6 | Climax Hero Poster Frame): Low-angle three-quarter hero shot; Astra lands gracefully in a three-point stance on a narrow suspension cable, rising tall with effortless swagger. Her slate-blue cloak billows against the newly opened golden sky; her gauntlet smokes with fading amber sparks as she looks dead into the camera with a lethal smirk. Hold static hero frame to freeze.

LIGHTING, DEPTH & PHYSICS: High-altitude stormy rim light, blinding vertical white-gold key flashes from her fist, cool slate shadow fill; strict three-layer depth separation in every frame; 

weighty natural character animation, cloth and hair reacting to high-speed wind shears, follow-through and explosive momentum recoil.
```

<a id="animation-08"></a>
### 105. 사무실에서 커피 마시려는 뱀

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-08#animation-08)** · [원본 게시물](https://x.com/EndFolding79421/status/2112367087242891434)

https://github.com/user-attachments/assets/1a7192a0-f5a5-406e-bcef-66d8f8f2a948

**프롬프트:**

```text
“Snake Coffee Break”A snake wearing a tiny office badge tries to sip coffee through a straw [close-up]. It slurps loudly, tongue flicking, then realizes it has no hands to hold the mug. The mug tips, spills everywhere, and the snake sighs like an exhausted intern.
```

<a id="animation-09"></a>
### 106. 90년대 애니 풍 거리의 만남

작성자 [@ShamiWeb3](https://x.com/ShamiWeb3) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-09#animation-09)** · [원본 게시물](https://x.com/ShamiWeb3/status/2112363210393436602)

https://github.com/user-attachments/assets/a13a8166-ee36-4a18-a498-fd01043c802d

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
MASTER PROMPT (paste first)

Format: 16:9, 30 seconds, 24fps, 1080p. Cinematic 90s anime film look, hand-painted backgrounds, warm golden sunlight, saturated blue sky with cumulus clouds, soft film grain, gentle lens flare.

Setting: A seaside sidewalk in the afternoon. A tall chain-link fence runs along the right side, with the ocean behind it, palm trees, and an orange-lined road on the left.

Characters (use the attached sheets as strict references):

Mei Aihara (@Image1): wavy purple-black hair, round glasses, pink hoop earrings, pink and blue oversized sweater, green high-waist pants, white-pink-blue sneakers, black spiral notebook with stickers. Shy and bubbly.
Yuki Kageyama (@Image2): long white double braids, black blazer, turtleneck, slim pants, boots. Calm, observant, protective.
Luca Moretti (@Image3): messy blonde hair with a faded undercut, star face tattoos, neck and sleeve tattoos, ear piercings, white tank top, black trousers, leather shoes, cigarette in hand.

Sound style: Anime audio. Exaggerated sparkle chimes, soft “doki-doki” heartbeats, cute kyahaha laughs, wind and wave ambience, light lo-fi guitar under the first half, and a low tense string drone from 19s.

TIMELINE

0:00–3:00 | Luca, profile close-up
Camera: tight side-profile close-up on Luca, fence in sharp focus beside him, deep-focus background.

Action: He leans on the fence with the cigarette in his lips. Smoke drifts up toward the sky. In the soft-focus background, Mei and Yuki walk small and distant down the sidewalk. At 2:00 his eyes slide toward them and the frame blurs as the focus pulls away.
Sound: waves, seagulls, soft inhale and exhale, faint lo-fi guitar.
3:00–7:00 | The girls chatting (medium two-shot, eye level)

Camera: Front-facing two-shot at the same angle as the reference, with the fence and ocean at right, as they walk toward the camera.
Action: Mei gestures excitedly with one hand, clutching her notebook to her chest. Yuki listens with a small smile.

Mei (excited): “Gojo Satoru is so handsome, I could kiss and marry him!”
At 5:00 both burst out laughing. Mei closes her eyes and laughs wide-mouthed (her “cheerful laugh” expression). Yuki covers her mouth and laughs with a quiet “pfft”, shoulders shaking.
Sound: kyahaha! giggles, a cute sparkle “ting” on the punchline, and bouncy footsteps.
7:00–10:00 | The collision
Camera: Low ground-level shot of Luca’s black leather shoe stepping into frame while Mei’s sneakers drift past, slightly out of focus. Cut to a wide shot at the fence with the ocean behind them: Luca walks left to right, Mei walks right to left, looking at her phone-free hands, and they bump.

Mei (voice-over, still rambling, cut off): “I have his wallpapers plastered all over my room—”
Her notebook and books fly out of her arms.

Sound: shoe clack, quick “whoosh”, soft thump, “Eh?!” gasp, books slapping the pavement.
10:00–12:00 | Kneeling to pick up
Camera: Wide high-angle shot looking down at both of them crouching, books scattered on the sidewalk. Luca bends low and Mei crouches beside him, flustered.
Mei (flustered, soft): “A-ah, sorry!”

Sound: fabric rustle, shy breathing.
12:00–16:00 | Hands and eyes (the key shot)

12:00: Extreme close-up on the blue book. Her hand and his tattooed hand land on it at the same time.
Sound: all ambient sound drops out, one soft heartbeat “doki.”
13:00: Low-angle close two-shot over the book. Mei on the left with sunlit hair and glasses, Luca on the right looking down at her. Their eyes meet slowly. Her cheeks flush.

14:00: Extreme close-up on Mei’s eye. The pupil dilates and the glasses reflect sky and sparkle highlights.
14:45: Extreme close-up on Luca’s eye with the pierced eyebrow, face tattoos and a slight softening in his stare.

15:30: Return to the two-shot, slow push-in. Her lips part slightly.
Luca (low, calm): “...Here.”
Sound: double heartbeat “doki-doki”, a sparkle chime, soft strings. (Luca’s line is my addition, since the reference has no dialogue here. Remove it if you want it silent.)
16:00–19:00 | Yuki calls, Mei snubs him
Camera: Wide shot from behind Yuki’s position. Yuki stands on the sidewalk on the left, waving. Mei and Luca are kneeling at center-right with the fence behind them.
Yuki (calling out): “Meimei!”
Mei jolts, grabs her notebook and stands up fast. She does not look at Luca. She turns her head away, bows slightly without a word, and hurries toward Yuki with her head down. Luca stays crouched and watches her go.
Sound: gasp, quick footsteps, a “pip-pip” panicked blip.

19:00–22:30 | Yuki’s warning
Camera: Medium shot, low angle, over Yuki’s shoulder. Yuki grabs Mei by the arm, and both glance back toward the fence. Sun flare glints off Mei’s glasses.

Yuki (hushed, serious): “Meimei, that guy is with the Mafia. Be careful!”
Sound: the tense string drone rises, and the ambience gets muffled.
22:30–26:00 | Luca stares
Camera: Over-the-shoulder shot from behind Mei and Yuki (their heads blurred in the foreground). Rack focus onto Luca, who is now standing, hands at his sides, staring after them. A new cigarette smoulders and smoke drifts across the sky.

Sound: wind, a single low taiko or bass hit.
26:00–30:00 | Final beat

26:00: Close-up on Mei’s profile as she looks back over her shoulder. Their eyes meet one more time across the distance. She blushes and snaps her head away (the snub).
28:00: Cut to Luca. A slow, small smirk. He looks down at his tattooed hand that touched hers, then back at her fading figure.
29:00: Final wide shot. The fence, the ocean, smoke curling up, the two girls walking away small in the distance. Fade out.

Sound: a last “doki” heartbeat, a sparkle chime, then the music fades into waves.
Negative prompt

Realistic or 3D look, character design drift (wrong hair colour, missing glasses, missing face tattoos), extra fingers, text watermarks, camera shake, fast cuts during the eye-contact shots, western cartoon style.
```

<a id="animation-10"></a>
### 107. 페인터리 2.5D 드래곤과 기수

작성자 [@itsPixieVerse](https://x.com/itsPixieVerse) · 19초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-10#animation-10)** · [원본 게시물](https://x.com/itsPixieVerse/status/2105140025784738231)

https://github.com/user-attachments/assets/ebba669b-63d7-4730-a0e5-99edbac6d354

**프롬프트:**

```text
Cinematic 2.5D animation in the style of fully painterly rendering, characters and environments look like gouache concept-art paintings in motion, visible brush texture on skin, cloth and buildings, flat posterized color blocks with hard-edged light shapes, matte finish, soft filmic volumetric lighting, shallow depth of field. NOT flat 2D cartoon, NO bold black outlines, NO cel-shading, NOT glossy CGI, NOT Unreal Engine, NO photorealism, no plastic skin.

ENVIRONMENT / WORLD :Ash-rift volcanic canyon with cracked white salt-rime ground, towering dark basalt pinnacles, glowing molten fissure seams, ancient ruined stone viaduct arches in midground, and a smoldering amber caldera sky dissolved in heat mist. 
CHARACTERS: 
Kip : Slender scout, rust-orange hair, freckles, draped charcoal mantle, olive vest, burnt-sienna trousers, heavy chestnut mechanical gauntlet. 

Ignis-Vael : Colossal obsidian dragon, faceted black scales, crimson wing membranes, swept-back horns, amber eyes. Bonded allies.

MULTI-CUT SEQUENCE (20 SECONDS TOTAL):[CUT 1 | 00:00–04:00 | WIDE TRACKING]: Low tracking move along the salt-rime canyon floor. Kip strides past dark basalt crags, ruined stone arches in distant haze. He stops and looks to the sky.[CUT 2 | 04:00–08:50 | IMPACT WIDE]: Hard cut to low angle. Ignis-Vael drops through orange smoke, slamming talons into frozen earth, scattering ash. Kip turns smoothly with a calm smirk, mantle flaring.[CUT 3 | 08:50–14:50 | MEDIUM CLOSE-UP]: Hard cut. Kip extends his mechanical gauntlet; the giant dragon lowers its horned head and presses its snout into his palm. Amber throat-glow lights Kip's face as steam vents from nostrils.[CUT 4 | 14:50–20:00 | HERO POSTER FRAME]: Hard cut to low-angle tableau. Kip stands beside the towering beast as it spreads massive crimson wings against the burning caldera sky, venting smoke upward. Hold frame. 
LIGHTING & ATMOSPHERE:Low amber magma under-glow, rear caldera rim-light, cool slate shadow fill. Volumetric heat haze and drifting ash flakes.

NEGATIVE:photorealism, glossy CGI, 3D render, plastic textures, anime, flat cartoon lineart, cel-shaded outlines, fighting each other, fear, weapons drawn, text, watermark
```

<a id="animation-11"></a>
### 108. 핼러윈 밤에 열리는 그림 같은 문

작성자 [@HBCoop_](https://x.com/HBCoop_) · 24초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-11#animation-11)** · [원본 게시물](https://x.com/HBCoop_/status/2116621038180339741)

https://github.com/user-attachments/assets/a3772305-35cf-4653-9d6c-84ceda196574

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Locked-off camera, no camera movement at all. Hand-painted 2.5D animation, visible brushwork held in every frame.

From inside a dark hallway, the heavy panelled door swings open on its hinges on the left of the doorway. Its free edge with the brass handle travels toward us and round to the left, in the first second and a half, until the door stands wide open at the left of the frame. The hinges stay fixed and the door stays rigid. The blade of moonlight on the floor widens as the door opens.

As the door clears, a woman in a long oxblood leather coat and a wide-brimmed black hat steps up from the wet cobbled street onto the doorstep, into the doorway, the orange jack-o'-lantern pail swinging by its black handle in the hand on the right of the frame. She stops, facing us, with a soft closed-mouth smile. A black raven flies in from the left, lands on the stone gatepost and folds its wings.

Normal real-time speed, no slow motion.

Sound: old door hinges creak, boots on wet cobbles, one raven caw, distant wind. No speech, no music.
```

<a id="animation-12"></a>
### 109. 「부」를 배우는 점토 유령

작성자 [@JasonHeatony7](https://x.com/JasonHeatony7) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-12#animation-12)** · [원본 게시물](https://x.com/JasonHeatony7/status/2115812533533581757)

https://github.com/user-attachments/assets/e6070066-7856-4e96-a308-8ac1540ed9e1

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

<a id="animation-13"></a>
### 110. 분홍 머리 꼬마 마녀와 불꽃 정령

작성자 [@imhealmachine](https://x.com/imhealmachine) · 20초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-13#animation-13)** · [원본 게시물](https://x.com/imhealmachine/status/2105659020359184617)

https://github.com/user-attachments/assets/20a2b7a4-b5e1-4322-8746-972581ac103f

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
20-second cinematic animated short, 16:9 widescreen.

Use the provided reference image as the strict character and visual style reference.
Maintain the exact same young female wizard character throughout the entire video: long pastel pink hair, huge blue eyes, freckles, oversized pointed blue-and-yellow wizard hat, bright blue and yellow wizard outfit, oversized blue boots, golden crescent-shaped magic staff, and the distinctive floating cyan-and-coral magical flame.

Preserve the original stylized cute 3D character proportions, smooth toy-like materials, soft rounded shapes, colorful pastel palette, clean high-quality 3D animation aesthetic.

SETTING:
A whimsical open meadow at golden hour, covered with tiny colorful flowers, soft rolling hills in the distance, dreamy clouds, gentle warm sunlight. Magical fantasy atmosphere.

SHOT 01 [0-3s]
Medium low-angle shot.
The little wizard stands alone in the meadow, looking extremely serious and determined.
She grips her tall staff with both hands and carefully raises it.
A tiny cyan magical flame flickers into existence above the golden crescent tip.
Her eyes widen.
She looks surprised, then gives a tiny proud smile as if thinking, “I did it!”

Slow cinematic push-in toward her face and the flame.
Hair and cape gently move in the breeze.

SHOT 02 [3-6s]
Close-up on the magical flame.
The flame suddenly develops two tiny glowing eyes.

It looks at the wizard.

The wizard freezes.

The little flame mischievously hops out of the staff and flies away.

Quick whip pan following the escaping flame.

The wizard's expression changes from pride to complete confusion.
She immediately runs after it, awkwardly carrying the oversized staff.

SHOT 03 [6-11s]
Fast comedic tracking shot across the meadow.

The tiny flame spirit zigzags rapidly between flowers while the wizard chases it.

Her oversized hat bounces wildly.
Her cape flaps behind her.
She almost trips over her own large boots, regains balance, then continues running.

The flame repeatedly grows slightly larger each time it jumps.

Dynamic side tracking camera, energetic but readable movement, playful physical comedy.

SHOT 04 [11-16s]
The wizard suddenly stops.

Camera swings around her to reveal that the tiny flame has transformed into an enormous floating magical fire spirit towering above her.

Huge swirling cyan core surrounded by coral-orange flames.

The wizard slowly looks upward.

Her eyes become huge.

One beat of silence.

She nervously raises her staff.

The giant flame rushes toward her.

She closes her eyes and desperately swings the staff forward.

A brilliant magical collision erupts.

Strong cinematic camera push, magical particles, wind pushing her hair and cape backward.

SHOT 05 [16-20s]
Instead of an explosion, the enormous flame bursts into hundreds of glowing pastel stars, sparkling petals, and tiny magical flowers.

Wide cinematic shot.

The entire meadow instantly blooms with colorful flowers.

The wizard is sitting on the ground in the middle of the flowers, slightly dazed, her oversized hat tilted sideways.

A tiny version of the flame spirit floats back toward her.

It gently lands on the tip of her staff.

She stares at it suspiciously for a moment.

The flame makes one tiny playful bounce.

The wizard sighs, then gives a small amused smile.

Slow camera pull-back revealing the magical flower-covered meadow.

End on a warm whimsical fantasy tableau.

ANIMATION:
High-quality expressive stylized 3D character animation.
Clear facial acting and readable poses.
Cute exaggerated physical comedy.
Smooth character motion with subtle squash and stretch.
Strong anticipation and reaction poses.
Natural secondary motion in long hair, cape, sleeves and oversized hat.
Keep the character's face, costume, colors, proportions and staff design consistent in every shot.

CAMERA:
cinematic animated-film camera language,
clear shot transitions,
smooth dolly and tracking movement,
brief whip pan during the chase,
dynamic perspective during the magical climax,
no excessive camera shake.

LIGHTING:
soft golden-hour sunlight,
pastel fantasy lighting,
soft volumetric glow from magic,
cyan magical light illuminating the character's face,
warm rim light,
clean colorful highlights.

IMPORTANT:
No dialogue.
No text.
No subtitles.
No additional human characters.
Do not redesign the wizard.
Do not change her outfit or hairstyle.
Do not change the staff design.
Keep the same stylized 3D rendering style as the reference image.
Avoid realistic human proportions.
Avoid photorealism.
Avoid horror imagery.
Avoid distorted hands or facial features.
```

<a id="animation-14"></a>
### 111. 한 문장으로 만든 소녀의 핼러윈 비밀

작성자 [@toku8ai](https://x.com/toku8ai) · 15초 · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=animation-14#animation-14)** · [원본 게시물](https://x.com/toku8ai/status/2116545073878061420)

https://github.com/user-attachments/assets/fe9ee33a-2a85-45a0-bbac-56b2e836e2ae

**프롬프트:**

```text
女の子がモンスターと出会うが、最終的に彼女自身も可愛いドラキュラのモンスターだったというストーリー。最後は「ハッピーハロウィン」というロゴとともに、ハロウィンを祝ってほしい。
```

<a id="vlog-ugc"></a>
## 🤳 브이로그와 UGC

> 실제 촬영처럼 보이도록 만든 휴대폰 셀카와 일상 클립. · 8개

<a id="vlog-ugc-01"></a>
### 112. 브런치 셀카 영상, 원테이크

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=vlog-ugc-01#vlog-ugc-01)** · [원본 게시물](https://x.com/minchoi/status/2111471573395755295)

https://github.com/user-attachments/assets/27503fa0-194a-48dd-830d-98270e65b2c1

**프롬프트:**

```text
Raw vertical 9:16 video recorded on a phone's front camera (not on screen), one continuous 30-second take with no cuts. It looks like an ordinary unedited phone clip, not a film: slightly soft image, a little digital noise and compression, deep focus with the café behind her as sharp as her face, auto-exposure brightening and dimming as people pass the sunny window behind her, no colour grading. The phone sits close and a little low, looking slightly up at her; around 9 s a waiter's arm bumps the table, the phone slides and tilts, and she catches it and props it back up. Sadie, a young woman in her early 20s with long honey-blonde waves, light natural makeup, small gold hoop earrings and a cropped cream knit top, sits at a small marble table by a big sunny window in a busy brunch café. Her sister sits across from her, out of frame except for her arm and a hand with a silver ring. Behind Sadie: other tables of people talking, a counter with a glass pastry case, plants, staff moving about, chalkboards too far away to read. Around 9 s a waiter sets down two plates, a lemon ricotta pancakes and a plate of eggs on toast, plus two iced coffees in plain glasses. Around 15 s she turns the pancake plate toward the camera; around 20 s she cuts a bite, eats it and closes her eyes; around 26 s her sister's hand reaches in with a fork and steals a piece of pancake, and Sadie swats at it, laughing. [Sadie: casual young woman's voice, warm and a bit giggly, recorded on the phone's built-in mic from half a metre away]: "Okay, I promised I'd show you what we get. ... We get the same thing every single time. ... Oh, here it is! Thank you! ... Look at this. Lemon ricotta pancakes. ... Mmm. Okay. Yeah. Still the best. ... Hey! Get your own!" [Her sister, off camera: a young woman's voice, dry and amused]: "That's the tax." [Sadie, laughing]: "She does this every time." Audio as captured by the phone mic in a busy café, not studio clean: her voice close but with the room around it, the hiss and grind of an espresso machine, cups and cutlery clinking, overlapping chatter and laughter from other tables, a door bell jingling, a chair scraping, faint music in the background. No subtitles, no captions, no on-screen text.
```

<a id="vlog-ugc-02"></a>
### 113. 노을 해변 셀카 브이로그

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=vlog-ugc-02#vlog-ugc-02)** · [원본 게시물](https://x.com/minchoi/status/2111471595755647205)

https://github.com/user-attachments/assets/c729b343-4a66-49ce-859f-51c4a15039fa

**프롬프트:**

```text
Raw vertical 9:16 selfie video shot on a phone's front camera held at arm's length while she sits on the sand, one continuous 30-second take with no cuts. It looks like an ordinary unedited phone clip, not a film: slightly soft, a little digital noise and compression, deep focus so the sea behind her is as sharp as her face, a low golden sun to one side with lens flare drifting across the frame, auto-exposure dimming and brightening as her head blocks and reveals the sun, no colour grading. Handheld and relaxed: the phone sways gently and tilts as she leans back on her other hand. Sadie, a young woman in her early 20s with long honey-blonde waves blowing across her face in the wind, light natural makeup, small gold hoop earrings and an oversized white knit sweater with no print, sits on cool sand on a wide, quiet beach at sunset, knees pulled up. Behind her: low waves rolling in and spreading foam up the sand, the sun sinking toward the horizon, a couple walking a dog along the waterline in the distance, a few gulls. Around 8 s she tucks her hair behind her ear and the wind blows it straight back. Around 16 s a bigger wave runs further up the sand behind her and she glances back at it. Around 24 s she turns her face into the sun for a moment, eyes closed, then smiles back at the camera. [Sadie: casual young woman's voice, soft and unhurried, a little buffeted by the wind, recorded on the phone's built-in mic]: "Okay. Long week. ... I just needed to sit somewhere and not look at my phone. ... Which, yeah, I'm on my phone. I know. ... But look at this. ... I'm staying till it's gone. ... Okay. Bye." Audio as captured by the phone mic outdoors on an open beach, not studio clean: waves rolling in and breaking softly, the long hiss of foam sliding up the sand and pulling back, wind buffeting the mic in gusts, gulls calling overhead, a dog barking far down the beach, faint voices from people far away, the sand crunching as she shifts. Her voice close on top with no echo at all, sometimes partly swallowed by a gust. No subtitles, no captions, no on-screen text.
```

<a id="vlog-ugc-04"></a>
### 114. 남자친구 시점의 여름 산책

작성자 [@agi_aibusi](https://x.com/agi_aibusi) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=vlog-ugc-04#vlog-ugc-04)** · [원본 게시물](https://x.com/agi_aibusi/status/2110924176890757483)

https://github.com/user-attachments/assets/095734dd-0a85-4705-ac24-5f58f60af580

**프롬프트:**

```text
Create a 30-second video in 1920×1080, with the realism of an ordinary recording a boyfriend made of his girlfriend during a summer walk in Japan.

The small story:
They have no particular destination. She has just opened a can of fruit juice, and he starts recording without announcing it. Over the next half-minute, she gradually notices the camera, gets a little embarrassed, and begins including him in the moment. Their familiarity should come through in how she waits for him, looks at him, and closes the distance between them.

The woman:
A beautiful Japanese woman around 24 years old, with an approachable, individual face rather than a polished model appearance. Dark brown eyes, natural skin texture, light everyday makeup, and straight black hair loosely gathered in a low ponytail. A few short strands around her temples have escaped in the summer humidity.

She wears a faded navy cotton T-shirt, loose ivory trousers, comfortable gray sneakers, and a small rust-colored crossbody bag. A plain elastic hair tie is around one wrist. Keep her facial features, hair, outfit, bag, and proportions consistent in every shot.

Her expressions are understated and responsive. Sometimes she looks distracted or squints in the light. Her smile develops because of something between them, rather than appearing on cue.

The place:
A residential neighborhood in a regional Japanese city, near a narrow canal. Late afternoon in midsummer, with warm sunlight still reaching the upper parts of the houses.

Use ordinary local details: patched asphalt, short concrete bridges over the canal, metal railings warm from the sun, compact houses with tiled roofs, frosted entrance windows, outdoor air-conditioning units, bicycles tucked beside gates, and plants growing in mismatched pots. Utility wires cross the sky. A striped fabric awning hangs outside a closed shop farther down the street.

Avoid famous landmarks and postcard compositions. The location should feel like somewhere the couple already knows.

How the camera behaves:
The boyfriend holds a small consumer camera at his own eye or chest level. Most of the time he is beside her or only a step behind. The viewpoint should feel like her companion's attention, with no third-person shots of the couple.

Let framing respond to their interaction. When she suddenly looks at him, he may take a fraction of a second to correct the composition. When he laughs, the camera moves slightly. When they walk, his footsteps create a gentle, uneven rhythm.

Use ordinary consumer-camera rendering: restrained detail, modest dynamic range, occasional clipped highlights, a little shadow noise, and slight focus hesitation when she moves closer. Preserve natural skin color.

Keep the camera's attention on her face, gestures, and shared surroundings. Avoid fashion poses, body-scanning shots, elaborate camera moves, slow motion, or a glossy advertising finish.

Suggested edit — six short memories from the same walk:

0:00–0:05
She stands beside a low canal railing with a small, unbranded can of mandarin orange juice. The recording begins just as she finishes lifting the pull tab. She takes a sip, lowers the can, and notices that he is filming.

She looks directly at him with a briefly puzzled expression, then gives a small, amused smile, as though silently asking, “Really, you're filming this?”

Begin with a slightly loose frame that includes her hands and the canal, then let the boyfriend adjust it toward her face.

0:05–0:10
A cut to the two of them walking side by side along the narrow lane. She carries the can naturally in one hand.

She gets half a step ahead, realizes he has slowed down while filming, and turns back. Instead of posing, she waits with a mildly impatient but affectionate look. Once he catches up, she resumes walking beside him.

Her gaze should meet the person holding the camera, not an imaginary audience.

0:10–0:15
They pause near a house entrance where a small glass wind chime hangs beneath the eaves.

A breeze makes it ring. She glances upward and listens for a moment. Loose strands of hair move against her cheek; she brushes them aside with her free hand.

She notices him still watching her through the camera and suppresses a smile before looking back toward the wind chime.

Keep this moment quiet and unhurried.

0:15–0:20
On a short concrete bridge, she stops to look down at the canal. The camera first catches the rippling water, then tilts back toward her after she has already turned around.

She leans slightly toward him to see what he is recording. Her face briefly comes too close for the camera's focus, making her laugh softly and step back.

The laugh should feel like a shared interruption, with a small answering movement from the camera.

0:20–0:25
They rest beside the bridge in the shade. She is closer to the camera now, relaxed enough to stop paying attention to being filmed.

She takes another small sip of juice, then holds the can toward him as an offer. Leave the can clearly visible in the foreground, separate from her face.

He does not take it during the shot. She gives a tiny questioning lift of her eyebrows, then draws it back with an affectionate smile.

0:25–0:30
She steps toward him and gently touches his free forearm, inviting him to keep walking. Only a small, natural part of his arm may enter the lower edge of the frame.

As they start moving together, he lowers the camera. The view drifts from her smiling face to her bag, their moving shadows, and the sunlit pavement.

Let the last second settle on the overlapping shadows of two people walking close together. End with an ordinary recording stop, without a dramatic transition or title.

Sound:
Use the sound that would actually reach the camera microphone: cicadas, the juice can opening, a few footsteps, a wind chime, faint canal water, distant tires on the road, and their quiet laughter.

A single softly spoken Japanese remark such as “撮ってたの？” may occur when she first notices the camera, but speech is optional. Do not add explanatory dialogue.

No music, voiceover, or added dramatic sound effects.

Continuity and physical detail:
There is one juice can, carried by her throughout the sequence. Its color, size, opening, and remaining shape stay consistent. The crossbody strap stays on the same shoulder. Her ponytail remains tied.

Hands should hold objects with believable contact and weight. Walking speed, foot placement, shadows, and reflections must agree with the surroundings. Keep the canal, bridge, houses, sunlight direction, and summer weather coherent between cuts.

Emotional direction:
The viewer should feel that she knows and trusts the person behind the camera. Build that feeling through small changes in distance and attention: noticing him, waiting for him, leaning in, offering a drink, and asking him to walk beside her.

Let ordinary pauses remain. Her beauty is something her boyfriend happens to notice during their time together.

The finished video should feel like a personal memory he would keep because of the way she looked at him that afternoon.
```

<a id="vlog-ugc-05"></a>
### 115. 도시를 걷는 고양이 브이로거

작성자 [@AIwithSarah_](https://x.com/AIwithSarah_) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=vlog-ugc-05#vlog-ugc-05)** · [원본 게시물](https://x.com/AIwithSarah_/status/2107724687984013347)

https://github.com/user-attachments/assets/030f8c84-b903-4724-bc92-ecbf40411f8e

**프롬프트:**

```text
A 15-second continuous cinematic selfie-style video of an anthropomorphic tabby cat vlogger walking down a modern city street while holding a front-facing camera. The cat is wearing black headphones and a blue plaid shirt, speaking directly to the camera in a casual, confident tone like a daily street vlogger. Mouth movement synced to speech throughout.
The camera remains in selfie mode the entire time with slight handheld shake for realism. Natural daylight lighting. Background includes passing cars, pedestrians, and tall buildings softly blurred with shallow depth of field.
As the cat walks forward, it talks continuously, occasionally nodding, blinking, and slightly adjusting its headphones mid-sentence. Subtle fabric movement from wind. Natural whisker and ear motion. The cat briefly laughs near the end while still speaking, then gives a friendly wink at the camera.
Ultra-realistic fur detail, natural lip sync, vlog aesthetic, cinematic color grading, 4K, 24fps, realistic motion blur.
```

<a id="vlog-ugc-06"></a>
### 116. 주차된 차 안에서 찍은 고백

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=vlog-ugc-06#vlog-ugc-06)** · [원본 게시물](https://x.com/minchoi/status/2111471592601534511)

https://github.com/user-attachments/assets/fda16860-4b69-4102-b34d-44e53e8733d6

**프롬프트:**

```text
Raw vertical 9:16 video recorded on a phone's front camera, one continuous 30-second take with no cuts. It looks like an ordinary unedited phone clip, not a film: slightly soft image, digital noise and compression, flat grey daylight through rain-streaked windows, no colour grading. the picture wobbles whenever she moves and jolts when she pulls the door shut. Sadie, a young woman in her early 20s with long honey-blonde hair in a messy bun with loose strands, no makeup, small gold hoop earrings and an oversized sage-green hoodie with no print, sits in the driver's seat of a small, slightly messy hatchback parked in a supermarket car park on a rainy afternoon. Rain streaks every window; through the rear window, blurred parked cars and a trolley bay. At the start she drops into the seat and pulls the door shut. She tells the story with her hands. Around 18 s she covers her face with both hands. Around 26 s a trolley rattles past her window and she slides down low in the seat as if hiding, laughing. [Sadie: casual young woman's voice, a bit breathless and mortified, recorded on the phone's built-in mic in a small car]: "Okay. I need to tell someone this immediately. ... So I'm in the cereal aisle, and this guy waves at me. Like, a big wave. So I wave back. Big wave. ... He was waving at his wife. Who was right behind me. ... And then I saw them again at the checkout. ... I'm never going back in there. I live in the car now. This is my home." Audio as captured by the phone mic inside a closed car, not studio clean: rain drumming on the roof and windscreen, her voice close and boxy in the small space, the door's heavy thud, fabric rustling against the seat, and outside, muffled through the glass, a trolley rattling past, a car door slamming and an engine starting. No subtitles, no captions, no on-screen text.
```

<a id="vlog-ugc-07"></a>
### 117. 공항 게이트 셀카 영상

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=vlog-ugc-07#vlog-ugc-07)** · [원본 게시물](https://x.com/minchoi/status/2111471585001390367)

https://github.com/user-attachments/assets/a91941d8-1924-4fd0-bcc8-f4bf34c570a4

**프롬프트:**

```text
Raw vertical 9:16 selfie video shot on a phone's front camera held low at chest height while she sits, one continuous 30-second take with no cuts. It looks like an ordinary unedited phone clip, not a film: slightly soft image, a little digital noise and compression, deep focus so the gate area behind her is as sharp as her face, flat white overhead light mixed with pale daylight from the big windows, no colour grading. The phone rests in her hand near her knee, so the angle is a little low and drifts as she shifts in her seat. Sadie, a young woman in her early 20s with long honey-blonde waves in a loose low ponytail, no makeup, small gold hoop earrings, an oversized grey crew-neck sweatshirt with no print and black leggings, sits in a row of connected grey seats at an airport gate early in the morning, a small carry-on suitcase beside her knee and a paper coffee cup with no logo in her free hand. Behind her: a wall of tall windows with a parked plane on the tarmac in pale morning light, other travellers sitting with bags, a man on a phone call pacing slowly, someone asleep with their hood up, a gate desk far off with screens too small and distant to read. Around 9 s she sips her coffee. Around 15 s she glances over her shoulder toward the gate desk as an announcement plays, listens, then turns back. Around 23 s she yawns behind her hand mid-sentence and laughs at herself. [Sadie: casual young woman's voice, quiet and a little croaky from the early start, keeping it down because she's in a public place, recorded on the phone's built-in mic]: "Okay, it is way too early. ... I've been up since four. ... But I'm surprising my best friend for the weekend, and she has no idea, so... worth it. ... Wait, is that us? ... No. Not us. ... Okay. Forty minutes. I'm getting another coffee. Don't judge me." Audio as captured by the phone mic in a huge, hard-surfaced airport terminal, not studio clean: her voice soft and close on top, with the wide, echoey hum of the terminal all around it; at around 15 s a two-tone chime and then a boarding announcement over the PA, distant, echoing and unintelligible; suitcase wheels rolling past on the hard floor; a coffee machine hissing at a kiosk; low murmured conversations from nearby seats; a child chattering a few rows away; a jet engine whining faintly through the glass; her sweatshirt rustling when she moves. No subtitles, no captions, no on-screen text.
```

<a id="vlog-ugc-08"></a>
### 118. 길을 걸으며 찍는 셀카 브이로그

작성자 [@minchoi](https://x.com/minchoi) · 30초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=vlog-ugc-08#vlog-ugc-08)** · [원본 게시물](https://x.com/minchoi/status/2104742701073564121)

https://github.com/user-attachments/assets/376a6559-cdae-44f7-a2a7-2802d194f54a

**프롬프트:**

```text
"Raw vertical 9:16 selfie video shot on a phone's front camera held at arm's length, one continuous 30-second take with no cuts. It looks like an ordinary unedited phone clip, not a film: slightly soft image, a little digital noise and compression, deep focus with the background as sharp as her face, auto-exposure brightening and dimming as she walks between sun and tree shade, no colour grading. Handheld and imperfect: the phone bobs and sways with each step, tilts off level, drifts until the top of her head is cut off, and she re-centres it. [Sadie], a young woman in her early 20s with long honey-blonde waves blowing across her face, light natural makeup, small gold hoop earrings, a cropped cream knit top and light-wash jeans, walks forward along one long, straight, tree-lined downtown street in bright late-morning sun, a plain iced coffee cup with no logo in her free hand. She never stops, turns around or turns a corner; behind her is the same street she has already walked, with a few passers-by, parked cars and shopfronts with unreadable signs. Around 12 s a flower stall slides past beside her and she glances at it; around 17 s she passes a bakery window, glances at it and laughs.[Sadie: casual young woman's voice, a little breathless from walking, recorded on the phone's built-in mic]: "Okay, walk with me. I'm meeting my sister for brunch and I'm, like, ten minutes early for once. ... I love this street in the morning, before all the people. ... Oh, the flower stall's out again, so pretty. ... And that bakery... no. Be strong. ... Okay, it's just up here. I'll show you what we get. Bye!"Audio as captured by the phone mic, not studio clean: her voice close and slightly compressed, light wind buffeting the mic, traffic passing, a bus pulling away, footsteps, snippets of passer-by chatter, all mixed under and around her voice."
```

<a id="vlog-ugc-09"></a>
### 119. 2010년대 감성 옷가게 라이브

작성자 [@bmx_ai13](https://x.com/bmx_ai13) · 30초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=vlog-ugc-09#vlog-ugc-09)** · [원본 게시물](https://x.com/bmx_ai13/status/2111824850222452968)

https://github.com/user-attachments/assets/415dbfe5-3407-4d15-8069-2413f0477869

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Create a 30second ultra realistic video featuring the character from @.jpg (maintaining her exact pinkish purple bob hair, heterochromia eyes one green and one amber, face markings, and facial features) hosting a live shopping session inside a trendy boutique in 2010. The video is captured entirely through an early smartphone front-facing camera (like iPhone 4 era), featuring authentic 2010 mobile livestream aesthetics: heavy pixelation, low resolution, digital compression artifacts, grainy texture, and slightly shaky handheld movements.

Scene 1 — Welcome to the Live (0–5 seconds)
Choi Yu-na stands inside a 2010 style women's boutique with neon signage and racks filled with early 2010s fashion trends, wearing her signature black bomber jacket over a black top and gray pleated skirt. She holds her early smartphone at arm's length, smiling into the low res pixelated camera and greeting her viewers.

Dialogue: “Hey guys! Welcome to my mobile live stream! I'm here at the boutique today, and you guys have to see these new arrivals!”
She briefly pans the pixelated camera toward the clothing racks, then returns it to her face.

Scene 2 — Show the First Dress (5–10 seconds)

She picks up a trendy 2010 color-block party dress from the rack, holding it up close to the low res camera lens to show its fabric and design.

Dialogue: “Look at this color block dress! It's so hot right now, and the fabric is super cute for a night out!”
She squints slightly at the screen as if reading early mobile chat comments.

Scene 3 — First Outfit Try On (10–16 seconds)

A pixelated, glitchy transition shows her wearing the same color-block dress, standing in front of a full-length boutique mirror while maintaining her exact face, hair, and unique eye colors. She poses and takes a few steps for the camera.

Dialogue: “Okay everyone, here it is on! How does it look? I'm totally loving this style!”
She smiles and waves at the viewer names popping up on her phone screen.

Scene 4 — Second Outfit Reveal (16–23 seconds)

A quick, low-res transition brings her back wearing a classic 2010 sequin top and skinny jeans set. She adjusts her hair, steps forward, and shows off the outfit.

Dialogue: “And check out this sequin top and denim combo! Perfect for weekend hangs with friends!”
Her delivery feels spontaneous, casual, and true to early social media video creators.

Scene 5 — Final Sales Pitch (23–30 seconds)

She stands near the boutique display wearing the second outfit while holding the color-block dress on a hanger beside her, smiling brightly into the phone.

Dialogue: “Alright guys, let me know in the comments which one you like best! Send a text message or leave a comment to grab yours before they sell out. Bye!”
```

<a id="product"></a>
## 👟 제품과 광고

> 제품이나 공간이 그대로 유지돼야 하는 광고. · 8개

<a id="product-01"></a>
### 120. 로켓처럼 루프를 도는 향수병

작성자 [@AIWithRay](https://x.com/AIWithRay) · 10초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=product-01#product-01)** · [원본 게시물](https://x.com/AIWithRay/status/2114672427964010805)

https://github.com/user-attachments/assets/79f0bb6e-dfe7-463c-a674-d9f67081f365

**프롬프트:**

```text
Cinematic, photoreal night scene on a black stage inside a giant hangar. A towering concrete loop ramp/road with glowing red edge lights and a white center stripe dominates the background. In front of it stands a premium transparent glass perfume bottle, unlabeled, no logo, filled with pale golden fragrance, featuring elegant beveled edges, a polished metallic cap, realistic glass refraction, crisp reflections, and subtle condensation droplets. The bottle engages four small rocket nozzles under its base; soft white exhaust with bright orange cores appears. The bottle glides forward, then blasts up the glowing ramp, hugging the curve, leaving faint light trails and red neon reflections across its glass surface. At the apex it shoots off the ramp and transitions to a sleek electric-thruster flight, like a futuristic luxury flying car, then ends in a close hero shot of the perfume bottle hovering and roaring upward vertically with four bright jets, volumetric spotlights and fog below, sparks and vapor interaction, dramatic rim light, golden highlights, crisp reflections, shallow depth of field, 4K, high-end luxury perfume and car commercial look. No text, no brand, no label. Duration 9–10 seconds. Aspect ratio 9:16. Negative cues: no logos, no text, no labels, no hands, no spillage, no deformation, no duplicate bottles, no cartoon look, no melting glass, no detached cap, no liquid leakage, no extreme motion-blur smears. Beat sheet (timing guide) 0–2s: Low-angle push-in on the massive loop ramp; perfume bottle centered, engines arming beneath the base with subtle heat shimmer and glowing orange cores. 2–6s: Dynamic follow-cam as the bottle rockets up the ramp; speed ramping, neon edge lights streaking, dramatic red reflections sliding across the glass. 6–8s: Bottle leaves the ramp, switches to electric thrusters; quick cinematic orbit as it hovers midair, revealing the golden fragrance and metallic cap. 8–10s: Tight hero shot of the perfume bottle ascending vertically with four bright jets, swirling fog, volumetric spotlights, realistic vapor, and luxurious golden reflections. End with the bottle sharply focused and centered against the dark hangar.
```

<a id="product-02"></a>
### 121. 럭셔리 나이트 크림 ASMR 광고

작성자 [@yourPlugAI](https://x.com/yourPlugAI) · 30초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=product-02#product-02)** · [원본 게시물](https://x.com/yourPlugAI/status/2114574940166840517)

https://github.com/user-attachments/assets/b65023de-d937-48c9-ad26-86b99b48836c

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
[ENGINE DIRECTIVE]
Generate a continuous 30-second hyper-realistic luxury beauty ASMR sequence at 60fps in 16:9 widescreen format using Kling 4.0. Style: High-end commercial macro video, 8K resolution, photorealistic, pristine studio lighting, crisp micro-depth of field. Maintain 100% strict visual consistency across the entire shot with provided reference sheets: "Elena", "L'ÉLIXIR NUIT", and "Minimalist Marble Spa Suite". Zero motion blur artifacts, high tactile accuracy, smooth camera transitions, seamless timeline execution without cuts.

[AUDIO DIRECTIVE]
- MUSIC: None. Pure organic binaural ASMR soundscape.
- SOUND DESIGN: Heavy glass-on-marble placement, sharp fingernail glass taps, magnetic lid snap, foil seal peel-pop, soft creamy spatula glide, skin-on-skin massage swipes, skin press suction-pat, final magnetic closure snap.

[TIMELINE BREAKDOWN]

00:00 - 00:04 | MARBLE PLACEMENT & GLASS TAPPING
- VISUAL: Extreme close-up 45-degree macro shot on the Carrara marble counter. Elena’s manicured hand smoothly sets the heavy "L'ÉLIXIR NUIT" frosted glass jar down, then gently taps her index nail three times on the glass side.
- ACTION: Crisp placement, followed by precise rhythmic nail taps against the cold frosted glass surface.
- SOUND: Heavy glass-on-marble THUD, followed by three ultra-sharp, resonant fingernail GLASS TAPS.

00:04 - 00:08 | MAGNETIC LID SNAP & ELEVATION
- VISUAL: Smooth camera glide into a tight macro eye-level shot focused on the silver metallic lid interface.
- ACTION: Elena lifts the square magnetic lid slightly, letting the magnetic pull snap it back down once before fully twisting and lifting the polished chrome lid straight up out of frame.
- SOUND: Crisp metallic magnetic SNAP-CLICK, smooth threads twisting sound, soft air release.

00:08 - 00:12 | HERMETIC FOIL PEEL
- VISUAL: Camera pans smoothly upward to an overhead 45-degree top-down macro shot centered on the inner pull-tab.
- ACTION: Elena’s thumb and index finger grip the foil seal tab, slowly peeling back the silver protective foil seal in one continuous smooth motion, exposing the whipped ivory cream surface.
- SOUND: High-pitch foil seal BREAK-CRINKLE, followed by a soft pneumatic vacuum POP.

00:12 - 00:16 | SPATULA SCOOP & TEXTURE LIFT
- VISUAL: Macro tracking camera glides horizontally across the open jar mouth.
- ACTION: Elena glides the sleek metallic spatula through the top layer of cream, lifting a thick, velvety dollop of whipped cream and holding it steady under warm key light.
- SOUND: Soft creamy glide audio, subtle metallic spatula chime.

00:16 - 00:20 | DIRECT CHEEK PLACEMENT
- VISUAL: Camera smoothly tracks upward and tilts into a medium close-up macro framing Elena’s right cheekbone and glowing skin texture.
- ACTION: Elena uses her fingertip to transfer the rich cream dollop directly onto her high cheekbone.
- SOUND: Soft, subtle skin contact PAT sound, creamy texture placement.

00:20 - 00:24 | GLIDING MELT & TACTILE PRESS
- VISUAL: Tight tracking shot following the circular motion of her fingers across her cheek, transitioning to a palm press.
- ACTION: Elena massages the cream into her skin using upward circular motions as it melts into a dewy barrier layer. She then gently presses the palm of her hand against her cheek and pulls back slowly to showcase elasticity.
- SOUND: Deep skin-on-skin gliding SWIPE audio, wet hydration texture sound, skin suction-pat, quiet relaxing breath exhale.

00:24 - 00:30 | MAGNETIC CLOSURE & HERO VANITY POSE
- VISUAL: Smooth camera pull-back into a wide hero shot framing Elena setting the jar on the marble counter, looking into the vanity mirror with a subtle, serene smile.
- ACTION: Elena brings the magnetic silver lid back over the glass jar, letting it snap firmly closed, and rests her hands on the counter beside the product. FADE TO BLACK at 00:30.
- SOUND: Satisfying metallic magnetic lid SNAP, soft marble contact, ambient studio silence.
```

<a id="product-03"></a>
### 122. 럭셔리 거실 멀티샷 광고

작성자 [@WorldEverett](https://x.com/WorldEverett) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=product-03#product-03)** · [원본 게시물](https://x.com/WorldEverett/status/2105275472552542625)

https://github.com/user-attachments/assets/54af9bcb-2e3d-4d98-ae10-446479978dbd

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
A cinematic luxury interior advertisement showcasing the living room in the reference image. No people, no typography. Preserve the furniture, layout, and cream, black, and gold palette. Gentle orchestral music blended with atmospheric alternative rock.

First 3 seconds: rapid 0.5–1-second cuts between floor-level chair details, an overhead view of the seating, and a dramatic low-angle wide shot.

Shot 1: Low-angle orbit around the cream armchair, emphasizing its sculptural black-and-gold shell. Push close to the upholstery, then transition behind the chair into the next shot.

Shot 2: High-angle sweeping view of the living room, descending toward the marble coffee table. Window shadows stretch across the wooden floor; sunlight glints on gold surfaces.

Shot 3: Fast lateral glide past the black chairs, close to floor level. Tilt upward from their gold bases toward the windows and circular ceiling lights. Whip-pan into the next shot.

Shot 4: Rapid extreme close-ups of fabric, marble veins, gold textures, and delicate plant shadows. Dynamic match cuts between curved chair edges, the round table, and glowing ceiling rings.

Shot 5: Start low behind the cream armchair, then rise in a sweeping arc to reveal the entire room from a high angle. Ease into a striking final wide shot.

Alternate dramatic high and low angles, fluid camera movements, foreground wipes, and sharp rhythmic cuts. Emphasize shadow play, dappled sunlight, rich contrast, reflections, and shifting focus. Keep furniture stationary and geometry consistent.
```

<a id="product-04"></a>
### 123. 애니 풍 프렌치토스트 광고

작성자 [@ryosuke_journey](https://x.com/ryosuke_journey) · 30초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=product-04#product-04)** · [원본 게시물](https://x.com/ryosuke_journey/status/2111366523369701863)

https://github.com/user-attachments/assets/014e5d9c-2d98-4709-b8df-8ba87df92e71

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
MAISON DORÉ — SIZZLE
30秒・9:16 縦型アニメーションCM
日本の最先端フルカラーアニメーションによる、シネマティックでクールな飲食CM。
動画尺30秒、アスペクト比9:16の縦型。
全編アニメーション。
実写ではなく、繊細で洗練された現代日本アニメ映画の画風で描く。
空気感としては、ハイエンドな劇場アニメと、少しインディー感のある映像作品の中間。
線は細く美しく、色彩は落ち着きつつ、光のにじみや空気の揺れが印象的。
食べ物はアニメ表現でありながら、熱・泡・バター・シロップ・焼き色の物理描写は非常にリアル。
BGMなし。
セリフなし。
字幕なし。
テロップなし。
ナレーションなし。
環境音のみ。
最終3秒は、アップロードされたフレンチトーストのポスター画像をそのまま使用する。
画像の再生成は禁止。
最後の画面はアップロード画像と完全一致。

1. 全体トーン / 映像コンセプト
映像の方向性は、
“寝起きの静けさ” × “フレンチトーストの熱” × “クールなテンポ感”。
可愛すぎる萌え系ではなく、
少しアンニュイで、今っぽくて、洒落ているアニメーション。
映像前半は静かで気だるい寝起きのムード。
中盤から調理のテンポが上がり、
後半はバターとメープルシロップのシズル感で一気に高揚する。
全カットで画角・アングルを変える。
単調な構図は禁止。
編集テンポは良く、リズム感のあるカット割り。
ただし落ち着いた高級感は失わない。
色調は以下を基調にする。
アイボリー
アンバー
柔らかなベージュ
キャラメルブラウン
ダークグレー
スモーキーなブルーグレー

2. キャラクターデザイン（変更後）
女性
成人女性。20代半ば。
ちょいロックで綺麗、でも寝起きの自然なラフさがある女性。
画風
キャラクター作画は、
細くやわらかな線、少しラフでエモーショナルな現代アニメ映画風。
シャープすぎるモード系ではなく、
自然な髪のハネ、眠そうなまぶた、生活感のある柔らかな表情を含んだ、
スタイリッシュだけど少し人間味のある画風。
肌はなめらかだが、つるつるすぎるCG感は禁止。
髪の動きは繊細。
ライティングに合わせて髪先に柔らかなハイライトが入る。
顔・髪
大人っぽく整った顔立ち
少し眠たげな目元
無表情寄りだが、静かな色気とクールさがある
髪は肩につくくらいのラフなボブ〜ミディアム
少し寝ぐせが残っている
ベースはダークカラー（ダークブラウン〜ダークネイビー）
毛先や一部に控えめな明るいニュアンス
派手すぎない小さなピアス
黒いネイル
服装（寝起き感）
“起きてそのままキッチンに来た”感じの服装。
少し大きめの白〜オフホワイトのTシャツ
または、くたっとした薄手のロングTシャツ
首元は少しゆるい
袖も少しルーズ
下は、ゆるいスウェットショートパンツ
裸足
全体にラフで生活感があり、気取っていない
ただしだらしなすぎず、絵として美しいバランス
見せるための服ではなく、寝起きの日常着。
過度に露出を強調しない。
自然でおしゃれな「部屋着感」を重視。

3. 背景 / 空間設定
深夜から明け方前くらいの、静かなモダンキッチン。
大きな窓の外には、まだ夜の名残がある都会の景色。
室内は暖かなアンバーの間接照明。
冷蔵庫を開けた時だけ、青白い光が差し込む。
静かで、少しひんやりした空気。
調理が始まるにつれて、湯気と熱気で空間が少しずつ温まる。
ステンレス、木のまな板、ガラスボウル、黒いフライパン、アイボリーの皿。
光の反射や素材感は美しく、上質に描く。

4. 30秒のカット構成

CUT 01｜0.0–1.5秒
WAKE UP KITCHEN
ワイドショット、斜め後方。
静かなキッチンに、寝起きの女性がゆっくり入ってくる。
少し眠そうな姿勢。
オーバーサイズTシャツの裾が自然に揺れる。
裸足で床を歩く。
冷蔵庫を開けると、青白い光が彼女の横顔とTシャツを照らす。
環境音：足音、冷蔵庫の開く音、夜明け前の静けさ。

CUT 02｜1.5–3.0秒
INSIDE THE FRIDGE
冷蔵庫内側からのローアングル。
少し前屈みになった彼女が、ぼんやりした寝起きの目で中を探す。
ラフな髪が少し頬にかかる。
黒いネイルの指が、発酵バター、卵、牛乳を取り出す。
環境音：パッケージが擦れる音、冷蔵庫のモーター音。

CUT 03｜3.0–4.5秒
BRIOCHE
超クローズアップ、真横。
厚切りブリオッシュを包丁で切る。
柔らかい断面がゆっくり戻る。
パンくずが小さく落ちる。
起き抜けの静けさの中で、切る音だけが心地よく響く。
環境音：パンを切る繊細な音。

CUT 04｜4.5–6.0秒
EGG DROP
極端なローアングル、ボウルの縁から。
卵が割られ、卵黄が落ちる。
一瞬だけなめらかなスローモーション。
彼女の袖口が少し落ちて、ラフな部屋着感が見える。
環境音：卵の殻が割れる音。

CUT 05｜6.0–7.5秒
MIX
真俯瞰。
卵、牛乳、バニラを泡立て器で混ぜる。
寝起きの少し気だるいテンポから、調理に入るにつれ手元が少しずつシャープになる。
液体が美しい渦を描く。
環境音：泡立て器とガラスの音。

CUT 06｜7.5–9.0秒
SOAK
超マクロ、液面と同じ高さ。
ブリオッシュを卵液に沈める。
パンが静かに液を吸う。
彼女の指先が軽くパンを押さえる。
液面の揺れが美しい。
環境音：液体の揺れる音。

CUT 07｜9.0–10.5秒
BAREFOOT STEP
床スレスレの超低空ショット。
裸足が床を一歩踏む。
眠気の残るゆっくりした動き。
床に柔らかいアンバーの光が反射する。
環境音：裸足の小さな足音。

CUT 08｜10.5–12.0秒
BUTTER IGNITION
超ローアングル、フライパン表面すれすれ。
発酵バターが熱いフライパンに落ちる。
黄金色に溶け、白い泡が一斉に立ち上がる。
ここから映像のテンポが一段上がる。
環境音：鋭い「ジュッ」という音。

CUT 09｜12.0–14.0秒
SIZZLE STARTS
超クローズアップ、斜め45度。
卵液を吸ったブリオッシュをフライパンに置く。
周囲のバターが激しく泡立ち、湯気が立ち上る。
フレンチトーストの縁が少しずつ色づく。
環境音：力強い焼き音。

CUT 10｜14.0–15.5秒
HAIR / MORNING FACE
クローズアップ、斜め後方。
彼女が片手で髪を耳にかける。
少し寝ぐせの残る髪。
眠たげな横顔。
でも目は料理に集中していてクール。
Tシャツの肩が少し落ちるラフなシルエット。
環境音：遠くの焼き音、衣擦れ。

CUT 11｜15.5–17.0秒
THE FLIP
ダイナミックなローアングル。
フレンチトーストを返す。
一瞬宙に浮き、次の瞬間、美しいキャラメルブラウンの焼き色が現れる。
テンポ良く、かっこよく。
ここは映像のビート感が出る重要カット。
環境音：金属音、焼き音。

CUT 12｜17.0–18.5秒
HEAT
顔のクローズアップ。
熱気で前髪が少し揺れる。
彼女が静かに息を吐く。
寝起きのぼんやり感は消え、料理モードに入っている。
表情はクールで静か。
環境音：小さな吐息、遠くのバターの音。

CUT 13｜18.5–20.5秒
GOLDEN SURFACE
フレンチトースト表面の超マクロ。
焼き目、焦がしバターの艶、きめ細かな表面。
カメラが表面を滑るように動く。
アニメならではの美しい線と、現実的な質感表現を両立。
環境音：小さな泡が弾ける音。

CUT 14｜20.5–22.0秒
PLATING
真俯瞰からやや下降。
アイボリーの皿にフレンチトーストを盛る。
置かれた瞬間に、柔らかさが伝わる微妙な沈み。
彼女の黒いネイルの手がフレームから離れる。
環境音：皿と器具が触れる音。

CUT 15｜22.0–24.0秒
MELTING BUTTER
超クローズアップ、真横から。
中央に四角い発酵バターを置く。
角がゆっくり丸くなり、底から溶け始める。
このあたりから、最終ポスターの色調・構図に自然に寄せていく。
環境音：細かな泡の音。

CUT 16｜24.0–26.5秒
LIQUID GOLD
極端な超マクロ、斜め上から。
琥珀色のメープルシロップが落ちる。
溶けたバターと混ざり、焼き目の上を流れ、縁から厚く滴る。
泡、艶、粘度、表面張力を美しく描写。
ラストに向けて料理の見た目を、アップロード画像に近づける。
環境音：液体が流れる微かな音。

CUT 17｜26.5–27.0秒
MATCH TO POSTER
エクストリームクローズアップ。
フレンチトーストの表面、バターの位置、シロップの流れ、焼き色を、
アップロード画像と一致するように構図を整える。
最後の一瞬で、アニメの料理描写から、完成ポスターへ視覚的につながる。
環境音：小さなジュワッという音。

CUT 18｜27.0–30.0秒
FINAL POSTER
27秒で、アップロードされた画像そのものに直接切り替える。
新規生成はしない。
画像の文字、レイアウト、料理、余白、ロゴ、すべて完全維持。
Maison Doré
CAFÉ & BREAKFAST
SIZZLE
French Toast
香ばしさが、とろける。
原材料
営業時間
住所
GOOD FOOD BRIGHTER DAYS
すべてそのまま。
9:16で画面いっぱいに表示。
完全静止。
ズーム、パン、文字変形、追加エフェクト禁止。
環境音は自然に静寂へフェード。
30秒で終了。

5. 追加の演出指定
カット割りはテンポ良く
ただし過剰に忙しすぎず、上質さを保つ
マッチオンアクションを多用する
包丁、卵、泡立て器、フライパン、バター、シロップの動きで編集リズムを作る
女性は過剰にポーズを取らない
「寝起きのラフさ」と「料理の美しさ」のコントラストを重視
キャラの魅力は、表情の押し出しではなく、仕草・空気感・手元の所作で見せる

6. ネガティブ指定
実写禁止
3Dゲーム風の質感禁止
萌えアニメ化禁止
子どもっぽい顔立ち禁止
過剰なセクシー演出禁止
不自然な露出強調禁止
指の破綻禁止
髪型・服装のカットごとの変化禁止
調理手順の破綻禁止
不自然な液体挙動禁止
テロップ・字幕・ロゴ追加禁止
最終ポスターの再生成禁止
9:16以外禁止
```

<a id="product-05"></a>
### 124. 자작나무 탄산수 광고

작성자 [@minchoi](https://x.com/minchoi) · 15초 · 9:16 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=product-05#product-05)** · [원본 게시물](https://x.com/minchoi/status/2104742449562136796)

https://github.com/user-attachments/assets/4c191103-92c3-4938-8efc-4f340fbfd109

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
"A premium product ad for [Fernloch]
sparkling birch water: a clear glass bottle of crystal-clear sparkling water with fine bubbles, its dark-green label reading "FERNLOCH" and "SPARKLING BIRCH WATER". Clean, bright commercial style, four shots. 0s–3s: Macro close-up sliding slowly along the bottle; the label fills the frame, fine bubbles rising inside, condensation beading on the glass. 3s–7s: Side angle at counter height. [Jules]'s hand in a rust-orange coat sleeve lifts the bottle by its shoulder and pours crystal-clear sparkling water into a heavy glass tumbler as fine bubbles race up. 7s–11s: Front angle, label facing the camera. She sets the bottle down upright beside the full glass. 11s–15s: Medium shot across the counter. [Harry]'s hand in an olive jacket sleeve takes the bottle by the neck and lifts it toward the lens, label facing the camera.Soft window light from the left, pale oak counter, warm-white wall, the label crisp and readable in every shot, gentle fizz and a soft glass clink."
```

<a id="product-06"></a>
### 125. 냉장고에서 파티까지 원테이크

작성자 [@shikoba_86](https://x.com/shikoba_86) · 21초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=product-06#product-06)** · [원본 게시물](https://x.com/shikoba_86/status/2113047628271198538)

https://github.com/user-attachments/assets/9e832264-7265-4e5e-adec-125b83d93f3e

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
One continuous shot, no cuts. The camera starts inside the closed dark fridge, on the middle shelf. At 2 seconds the door opens, the light switches on, and the smiling young man reaches in and takes the can. Then the camera moves forward, never backward: it glides out through the open fridge door, passes over his shoulder as he turns away, and continues forward behind his back, following the can in his hand as he walks out of the quiet, dim kitchen, down a short hallway, the party music getting louder, and through a doorway into a different room: the crowded living room party with string lights. There he opens the can with a hiss, takes a sip and talks and laughs with the young woman. He sets the can down on the table; the camera pushes in to a close-up of the can as the party blurs behind it. The background darkens and glowing blue and violet light streaks sweep in with motion-design graphics, revealing "With you, frame by frame." and "KLING 4.0" around the can.
CAMERA: one forward-moving tracking shot from inside the fridge to the table. The camera never pulls back and never stays inside the fridge after he takes the can.
Sound: silence and fridge hum, the door opening, muffled party music growing through the hallway, full music in the living room, the can hissing open, laughter, then the music drops to a single deep bass hit as the graphic appears.
```

<a id="product-08"></a>
### 126. 제품은 고정, 배경만 휩팬

작성자 [@shikoba_86](https://x.com/shikoba_86) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=product-08#product-08)** · [원본 게시물](https://x.com/shikoba_86/status/2112959711385391271)

https://github.com/user-attachments/assets/3cf01a99-4631-411b-a4f1-d234e404e1fe

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
The can stays perfectly still in the center of the frame for the whole video, same position, same size, label facing the camera. Only the background moves: between each keyframe, a fast horizontal whip pan with strong motion blur sweeps the background from right to left and reveals the next location, while the can stays sharp and locked in place.
```

<a id="product-09"></a>
### 127. 손이 캔을 들고 장면을 넘나들기

작성자 [@shikoba_86](https://x.com/shikoba_86) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=product-09#product-09)** · [원본 게시물](https://x.com/shikoba_86/status/2112959715185725562)

https://github.com/user-attachments/assets/ed182435-4247-4d95-a1a4-8b203e6798b2

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Between each keyframe, a hand enters the frame, picks up the can, and the camera follows it in one continuous movement into the next location, where the hand sets the can down in the center of the frame, in the same position and size, label facing the camera, and leaves the frame. The can is always the same can.
```

<a id="reference-edit"></a>
## 🔁 참고 영상 편집

> 기본 클립 하나를 후속 프롬프트로 바꿉니다: 동물, 계절, 인물 추가. · 6개

<a id="reference-edit-01"></a>
### 128. 참고 영상 음악에 맞춰 춤추게 하기

작성자 [@EndFolding79421](https://x.com/EndFolding79421) · 10초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=reference-edit-01#reference-edit-01)** · [원본 게시물](https://x.com/EndFolding79421/status/2111477898611659214)

https://github.com/user-attachments/assets/f2cbcab4-1b70-4d1a-b7d2-b6abd712886d

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Ruth (image1) dancing to the music in (video1).
```

<a id="reference-edit-02"></a>
### 129. 기본 클립: 두 친구, 개, 공

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=reference-edit-02#reference-edit-02)** · [원본 게시물](https://x.com/shikoba_86/status/2111760138214293935)

https://github.com/user-attachments/assets/d33349f5-f8d4-498d-8d9e-3af89987ce12

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
A city park on a sunny late-summer afternoon: a wooden bench beside a gravel path, tall green trees, a few people walking in the background.
CHARACTER LOCK: Friend A: man in his late 20s, short curly black hair, light stubble, white t-shirt, faded blue denim jacket, beige chinos, white sneakers. Friend B: man in his late 20s, short straight blond hair, clean-shaven, dark green hoodie, black jeans, grey sneakers. Dog: medium-sized golden retriever with a red collar. Same faces, clothes and dog in every frame.
PHOTOGRAPHY LOCK: 35mm and 50mm lenses, shallow depth of field, warm afternoon sunlight through the leaves, soft dappled shadows on the gravel, natural skin texture. Consistent color and exposure throughout.
LIGHT AND COLOR: lit only by the sun filtering through the trees. Warm highlights, soft green shadows. Muted, natural colors, no commercial color grade.
CAMERA LOCK: handheld, calm, slightly off-center compositions. No drone shots, no orbits, no crash zooms.
SHOT 1 — Wide shot. The two friends sit on the bench. Friend A throws a yellow tennis ball down the gravel path and the dog runs after it. Audio: the dog's paws on gravel, birds, distant voices.
SHOT 2 — Medium shot on the path. The dog catches the ball and runs back toward the bench with the ball in its mouth. Audio: paws on gravel, panting.
SHOT 3 — Medium shot on the bench. The dog drops the ball at Friend B's feet instead of Friend A's. Friend B picks it up and laughs. Audio: laughter.
SHOT 4 — Close-up on Friend A, half smiling, shaking his head.
FRIEND A (amused, mock-offended): "He always brings it back to you. Never to me."
Friend B pats the dog on the head. Audio: dog panting, birds.
AVOID: no music, no subtitles or on-screen text, the ball stays yellow, the dog keeps its red collar, no warped hands, no CGI or AI-generated look.
```

<a id="reference-edit-03"></a>
### 130. 편집: 여우, 가을, 플란넬 셔츠

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=reference-edit-03#reference-edit-03)** · [원본 게시물](https://x.com/shikoba_86/status/2111760149379461180)

https://github.com/user-attachments/assets/4d39ef19-c145-4152-9821-b8609234785d

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Replace the dog with a red fox, change the season to late autumn, and change Friend A's denim jacket to a red flannel shirt. Keep all actions and the dialogue unchanged.
```

<a id="reference-edit-04"></a>
### 131. 편집: 개를 공룡으로

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=reference-edit-04#reference-edit-04)** · [원본 게시물](https://x.com/shikoba_86/status/2111760141640949817)

https://github.com/user-attachments/assets/6b54f0ce-af0c-4203-82eb-cc22923ce508

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Replace the dog with the small dinosaur from the reference image. It runs, catches the yellow ball in its mouth and drops it at Friend B's feet, with the same path, timing and actions as the dog. Friend B pets it in the last shot. Keep everything else unchanged.
```

<a id="reference-edit-05"></a>
### 132. 편집: 벤치에 친구 한 명 추가

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=reference-edit-05#reference-edit-05)** · [원본 게시물](https://x.com/shikoba_86/status/2111760154135777331)

https://github.com/user-attachments/assets/e75419f1-cd43-4c9c-b234-d3b993c5792e

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Add a third friend sitting in the empty space in the middle of the bench, between Friend A (curly black hair, denim jacket) and Friend B (blond, green hoodie): a woman in her late 20s with a long dark braid and a yellow raincoat. She sits in this same spot, between the two friends, in every shot. Keep the bench, its length and its armrests exactly as they are. She watches the dog and laughs with the others. Keep everything else unchanged.
```

<a id="reference-edit-06"></a>
### 133. 편집: 여름을 가을로

작성자 [@shikoba_86](https://x.com/shikoba_86) · 15초 · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/kling-4-0-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-kling-4.0-prompts&utm_content=reference-edit-06#reference-edit-06)** · [원본 게시물](https://x.com/shikoba_86/status/2111760145063559511)

https://github.com/user-attachments/assets/71a39711-2aeb-4150-94e7-df5508a29972

> 📎 이 예시는 참조 이미지나 영상을 직접 올려야 합니다.

**프롬프트:**

```text
Change the season from late summer to late autumn: orange and red leaves on the trees and on the gravel, cooler softer light. Keep the people, the dog and all actions unchanged.
```

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
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_ko.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_ko.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_ko.md)
- [Awesome Claude Fable 5.2 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-fable-5.2-video-prompts/blob/main/README_ko.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_ko.md)

<a id="license"></a>
## 📄 라이선스와 출처

프롬프트와 결과 영상은 각 카드에 표시된 크리에이터의 것이며, 카드는 X 원문으로 연결됩니다. 제목, 설명, 번역, 빌드 스크립트는 [CC BY 4.0](LICENSE)으로 배포합니다.

이 목록이 도움이 됐다면 ⭐ 를 눌러 다른 사람도 찾을 수 있게 해 주세요.
