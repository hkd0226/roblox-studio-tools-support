# Roblox Studio Tools — Support / 사용 안내 및 문의

Customer documentation for the two Roblox Studio plugins by **hkd0226**.
These instructions apply to **version 0.1.0**. Version 0.2.0 is an unreleased candidate;
its new features are not available in the current store plugins.

**[English](#english) · [한국어](#한국어)**

## English

### Contact

[✉ Email support — primary](mailto:hkd0226@gmail.com?subject=Roblox%20Studio%20tools%20support)
&nbsp; · &nbsp;
[✉ Email support — backup](mailto:hkd0226@hanmail.net?subject=Roblox%20Studio%20tools%20support)

If your email application does not open, copy **hkd0226@gmail.com** into your preferred
email service. The backup address is **hkd0226@hanmail.net**. These are the seller's
confirmed contact addresses. No fixed response time is promised.

For a public bug report, open this repository's **Issues** tab and choose **New issue →
Bug report / 오류 제보**. A GitHub account is needed to open an issue; email is also available.
Public issues can be read by anyone. Send account or billing questions privately, and
contact Roblox Support for Roblox checkout or payment problems.

Include the product and version, Studio version, operating system, steps to reproduce,
expected result, actual result, and exact error text. Never include passwords, API keys,
cookies, authentication tokens, payment information, or private project files.

### Products

| Product | Store page | What it does |
| --- | --- | --- |
| Clearance Check — Door and Passage | [Open the Roblox Creator Store page](https://create.roblox.com/store/asset/132141689341950/Clearance-Check-Door-and-Passage) | Finds bounding-box overlap suspects in rectangular passage volumes and sampled door sweeps. |
| Viewport Batch Builder | [Open the Roblox Creator Store page](https://create.roblox.com/store/asset/71263242408985/Viewport-Batch-Builder) | Builds static native ViewportFrames from selected Models or BaseParts for inventory and shop UI. |

Use the current price and availability shown on Roblox. Install the purchased plugin
through Roblox Studio, then open its button in the **Plugins** tab. Make a separate
place backup before trying a new workflow and stop Play before using these edit tools.

### Clearance Check 0.1.0 — quick start

1. Open the **Clearance** toolbar button. Choose **Create 2-zone example (Undo supported)**
   in a test place. This creates two selected passage guide Parts and one obstacle.
2. Keep those Parts selected, choose **Mode: Passage**, and click **Inspect selection**.
   Compare the two results. A red bound has overlap suspects; a green bound has no
   suspects found by this query. Use **Select suspect parts** to inspect the reported objects.
3. For your own scene, select **1–50 rectangular block Parts in Workspace**.
   In Passage mode the selected Parts are test volumes, and are excluded as obstacles.
4. For a door, choose **Door swing**, set the angle and margin, and choose the left or
   right **local X edge** hinge. The sweep rotates around the Part's **local Y axis**.
   Orient and size the Part to match the intended rectangular door.
5. Inspect the report text as well as the colored bounds. Select the report text and
   copy it if needed. **Clear / Cancel** removes the visualization or requests cancellation.
   Rerun after changing the scene or reopening the place; previous results are snapshots.

**Limits and interpretation**

- Inputs are rectangular block `Part` objects, not Models or MeshParts. Each dimension
  must be at most **500 studs**. Door angles are **−180 to −1 or 1 to 180 degrees**;
  margin is **0–10 studs**.
- The query uses **Default collision-group interactions** and `CanQuery`. Terrain,
  `CanQuery=false` objects, non-collidable obstacles, selected guide Parts, and objects
  with `ClearanceIgnore=true` on themselves or an ancestor below Workspace
  (excluding Workspace itself) are excluded.
- Door sweeps use samples at intervals of at most 5 degrees with conservative padding.
  A suspect can therefore be a bounding-box false positive. Check the object in Studio.
- Results are not exact mesh/union collision, avatar walkability, pathfinding, or a
  constraint/physics simulation. A green result does not guarantee player passage.
- Version 0.1.0 uses edge hinges and Default-group queries. Edited-pivot hinges and a
  collision-group selector are not in the current released version.
- The plugin does not move or delete your original scene geometry. Example creation
  adds example objects and is intended to be removable with Studio Undo.

### Viewport Batch Builder 0.1.0 — quick start

1. Open **Viewport Batch** from the Plugins tab. Select the source **Models or BaseParts**
   in Explorer. Nested selections are deduplicated; separately selected roots are the batch items.
2. Choose frame width and height, yaw, pitch, field of view, and margin. Choose the
   **Studio / Soft / Contrast** lighting and **Transparent / Dark / Light** background.
3. Click **Preview first selected model** to inspect the first source, then **Generate batch**.
4. Find the generated folder under **ReplicatedStorage → ViewportBatch** (or a numbered
   variant if that name already exists). Each generated ViewportFrame has its own
   WorldModel and CurrentCamera.
5. Copy or move the generated ViewportFrames into your **ScreenGui / Frame** UI,
   for example under StarterGui. ReplicatedStorage alone does not display a game UI.
   Test the size, layout, and appearance in your actual interface.
6. If a source changes, generate a new batch and replace the appropriate output yourself.
   Version 0.1.0 does not have saved named presets or single-frame regeneration.

**Limits and interpretation**

- At most **100 roots**, **5,000 BaseParts per root**, and **20,000 BaseParts per batch**.
  Every source needs visible BasePart geometry. Source and geometry descendants must
  have `Archivable=true`; the plugin reports a problem rather than changing that setting.
- Width/height: whole numbers **64–1,024**; aspect ratio **1:4–4:1**; yaw **−180–180°**;
  pitch **−80–80°**; field of view **10–90°**; margin **0–40% per edge**.
- The generated result is a static clone in a native ViewportFrame. It does not export
  PNGs, animate models, rotate them at runtime, or synchronize source changes.
- The original source is not edited. Scripts and package links are removed from output
  clones; cloned parts are anchored and their collision, touch and query flags are disabled.
- Legacy SpecialMesh bounds can require additional margin. ViewportFrame rendering
  can differ from Workspace rendering; check the final result in your own UI.
- A generated batch is intended to use one Studio Undo operation. Keep a place backup
  for recovery rather than relying on Undo as the only copy of your work.

### Troubleshooting

| Symptom | Check or next step |
| --- | --- |
| The plugin button is missing | Confirm the product is installed and enabled in Studio's plugin management. Reopen Studio if needed. |
| The tool asks you to stop Play | Stop the test session and use the plugin in edit mode. |
| Clearance reports an unsupported selection | Select rectangular block Parts in Workspace, within the selection and size limits. Do not select a Model or MeshPart as the test volume. |
| Clearance misses an obstacle you expected | Check `CanCollide`, `CanQuery`, Default-group interaction, `ClearanceIgnore`, and whether the object is a selected guide. Terrain is outside the supported query. |
| Clearance reports a suspect that looks clear | Inspect the reported part and its bounds. Conservative door sweep padding and bounding boxes can produce false positives. Reduce margin only if that matches your intended clearance. |
| Viewport output is empty or invisible in the game | Ensure the source has visible geometry; place the output under a visible ScreenGui/Frame and check its parent, size, position and Visible state. Output in ReplicatedStorage is not displayed automatically. |
| Viewport generation reports Archivable or size limits | Review the reported source. Enable Archivable yourself only if appropriate, or split a large batch. Original settings are not changed automatically. |
| A preview is cropped | Increase margin or adjust view/FOV; inspect legacy SpecialMesh and unusual geometry. |
| Output did not change after editing a source | Version 0.1.0 uses static clones. Generate another batch; there is no automatic refresh. |
| Undo is busy or a run fails/cancels | Let the current Studio operation finish. Read the report, correct the input and retry. A cancelled scan is not a completed inspection. Restore your place backup if recovery is needed. |

For an unresolved problem, contact support or file an issue using the details above.
Share only a minimal example you have permission to share; a redacted screenshot and
error text are often enough. This repository contains documentation only, not plugin
source code or downloadable plugin releases.

## 한국어

### 문의

[✉ 기본 이메일로 문의](mailto:hkd0226@gmail.com?subject=Roblox%20Studio%20tools%20support)
&nbsp; · &nbsp;
[✉ 예비 이메일로 문의](mailto:hkd0226@hanmail.net?subject=Roblox%20Studio%20tools%20support)

메일 앱이 열리지 않으면 **hkd0226@gmail.com**을 복사해 사용하는 메일 서비스에서
작성해 주세요. 예비 주소는 **hkd0226@hanmail.net**입니다. 판매자가 확인한 연락처이며,
정해진 응답 시간은 약속하지 않습니다.

공개 오류 제보는 이 저장소의 **Issues → New issue → Bug report / 오류 제보**를
사용할 수 있습니다. GitHub 계정이 필요하며, 이메일로도 문의할 수 있습니다.
공개 제보 내용은 누구나 읽을 수 있습니다. 계정·결제 관련 개인 문의는 이메일을
사용하고, Roblox 결제 자체의 문제는 Roblox 고객지원에 문의해 주세요.

제품명과 버전, Studio 버전, 운영체제, 재현 순서, 예상 결과, 실제 결과, 정확한
오류 문구를 적어 주세요. 비밀번호, API 키, 쿠키, 인증 토큰, 결제 정보나 비공개
프로젝트 파일을 포함하지 마세요.

### 판매 제품

- [Clearance Check — Door and Passage](https://create.roblox.com/store/asset/132141689341950/Clearance-Check-Door-and-Passage):
  직사각형 통로 검사 공간과 문 회전 경로에서 경계 상자가 겹치는 의심 대상을 찾습니다.
- [Viewport Batch Builder](https://create.roblox.com/store/asset/71263242408985/Viewport-Batch-Builder):
  선택한 Model 또는 BasePart로 인벤토리·상점 UI용 정적 ViewportFrame을 일괄 생성합니다.

현재 가격과 판매 가능 여부는 Roblox 상품 페이지에서 확인해 주세요. 구매한 플러그인을
Studio에서 설치하고 **Plugins** 탭의 제품 버튼으로 엽니다. 작업 파일을 별도로 백업하고
Play를 중지한 편집 모드에서 사용해 주세요. 이 문서는 현재 **0.1.0**용입니다.
**0.2.0은 아직 출시하지 않은 후보 버전**이며 아래 사용법에 새 기능을 포함하지 않았습니다.

### Clearance Check 0.1.0 — 처음 사용

1. **Clearance** 버튼으로 패널을 열고 테스트 place에서 **Create 2-zone example
   (Undo supported)**을 누릅니다. 통로 가이드 Part 두 개와 장애물 하나가 생성됩니다.
2. 선택된 두 Part를 유지하고 **Mode: Passage → Inspect selection**을 실행합니다.
   빨간 경계는 의심 대상이 있으며, 초록 경계는 이 쿼리에서 찾은 의심 대상이 없습니다.
   **Select suspect parts**로 보고된 대상을 선택해 확인합니다.
3. 실제 검사에는 **Workspace의 직사각형 block Part 1–50개**를 선택합니다.
   Passage 모드에서 이 Part는 검사 공간이며, 선택한 가이드 자체는 장애물에서 제외됩니다.
4. 문 검사는 **Door swing**을 선택하고 각도·여유 값을 입력합니다. 경첩은 Part의
   **로컬 X축 왼쪽/오른쪽 가장자리**, 회전 축은 **로컬 Y축**입니다. 실제 문 방향과
   크기에 맞는 직사각형 Part를 사용하세요.
5. 색상뿐 아니라 보고서도 읽어 주세요. 보고서 텍스트를 선택해 복사할 수 있습니다.
   **Clear / Cancel**로 시각화를 지우거나 중단을 요청합니다. 장면을 변경하거나 다시
   열었으면 재검사하세요. 이전 결과는 당시 장면의 검사 결과입니다.

**범위와 제한**

- 입력은 Model/MeshPart가 아닌 직사각형 block `Part`입니다. 각 크기는 최대
  **500 studs**, 문 각도는 **−180~−1 또는 1~180도**, 여유는 **0~10 studs**입니다.
- **Default 충돌 그룹 관계**와 `CanQuery`를 사용합니다. Terrain, `CanQuery=false`,
  비충돌 장애물, 선택한 가이드, 자신이나 Workspace 아래 조상에 `ClearanceIgnore=true`가
  있는 대상은 제외합니다. Workspace 자체의 이 속성은 검사하지 않습니다.
- 문 회전은 최대 5도 간격으로 표본 검사하고 보수적으로 경계를 넓힙니다. 경계 상자
  때문에 실제로는 부딪히지 않는 대상도 보고될 수 있으므로 Studio에서 확인하세요.
- 정밀 mesh/union 충돌, 아바타 통과, pathfinding, constraint/물리 시뮬레이션 검사가
  아닙니다. 초록 결과가 플레이어 통과를 보장하지는 않습니다.
- 현재 0.1.0에는 편집한 pivot을 쓰는 경첩과 충돌 그룹 선택 기능이 없습니다.
- 원본 장면의 형상을 이동하거나 삭제하지 않습니다. 예제 생성은 새 예제 객체를
  추가하며 Studio Undo로 제거하도록 구성되어 있습니다.

### Viewport Batch Builder 0.1.0 — 처음 사용

1. **Viewport Batch** 버튼으로 패널을 열고 Explorer에서 원본 **Model 또는 BasePart**를
   선택합니다. 부모와 자식을 함께 선택한 경우 중복을 제거해 최상위 선택 단위로 처리합니다.
2. 프레임 너비·높이, yaw, pitch, FOV와 margin을 설정합니다. 조명은
   **Studio / Soft / Contrast**, 배경은 **Transparent / Dark / Light** 중 선택합니다.
3. **Preview first selected model**로 첫 대상을 확인하고 **Generate batch**를 누릅니다.
4. **ReplicatedStorage → ViewportBatch**에서 결과를 찾습니다. 같은 이름이 이미 있으면
   번호가 붙습니다. 각 ViewportFrame 안에는 WorldModel과 CurrentCamera가 들어 있습니다.
5. 결과 프레임을 **ScreenGui / Frame** 안으로 복사하거나 이동합니다. 예를 들어
   StarterGui의 인벤토리 UI에 넣습니다. ReplicatedStorage에 있는 결과는 게임 UI에
   자동 표시되지 않습니다. 실제 UI에서 배치·크기·표시 상태를 확인하세요.
6. 원본을 수정했다면 새 배치를 생성해 필요한 출력을 직접 교체합니다. 현재 0.1.0에는
   이름을 붙여 저장하는 프리셋이나 프레임 한 개만 다시 생성하는 기능이 없습니다.

**범위와 제한**

- 배치 최대 **100개 선택 단위**, 단위당 **BasePart 5,000개**, 배치 전체 **20,000개**입니다.
  보이는 BasePart가 있어야 합니다. 원본과 형상 자손의 `Archivable=true`가 필요하며,
  꺼져 있으면 오류를 알리고 원본 설정을 자동 변경하지 않습니다.
- 너비·높이는 정수 **64–1,024**, 비율 **1:4–4:1**, yaw **−180–180도**, pitch
  **−80–80도**, FOV **10–90도**, margin은 각 가장자리 **0–40%**입니다.
- 결과는 ViewportFrame 안의 정적 복사본입니다. PNG 내보내기, 애니메이션,
  실행 중 자동 회전이나 원본 변경 자동 동기화 기능은 없습니다.
- 원본은 수정하지 않습니다. 결과 복사본에서 스크립트와 package link를 제거하고,
  복사된 Part를 고정하며 충돌·touch·query를 끕니다.
- 오래된 SpecialMesh는 여유가 더 필요할 수 있습니다. ViewportFrame과 Workspace의
  렌더링은 다를 수 있으므로 최종 UI에서 확인해 주세요.
- 배치 생성은 Studio Undo 한 번으로 되돌리도록 구성되어 있습니다. 작업 복구를
  Undo에만 의존하지 말고 별도 place 백업을 보관해 주세요.

### 자주 겪는 문제

| 증상 | 확인할 항목 |
| --- | --- |
| 제품 버튼이 보이지 않음 | Studio 플러그인 관리에서 설치·활성화를 확인하고 필요하면 Studio를 다시 엽니다. |
| Play 중지 안내 | 테스트 실행을 중지한 뒤 편집 모드에서 사용합니다. |
| Clearance 선택 오류 | Workspace의 직사각형 block Part를 선택하고 개수·크기 제한을 확인합니다. Model/MeshPart를 검사 공간으로 선택하지 않습니다. |
| Clearance에서 예상 장애물이 안 잡힘 | CanCollide, CanQuery, Default 그룹 관계, ClearanceIgnore 및 선택한 가이드인지 확인합니다. Terrain은 지원하지 않습니다. |
| Clearance 의심 대상이 실제로는 안 겹침 | 보고된 대상의 경계를 확인합니다. 회전 경로 여유와 경계 상자 때문에 추가 대상이 나올 수 있습니다. 의도한 검사 여유에 맞을 때만 margin을 줄입니다. |
| Viewport 결과가 게임에서 안 보임 | 원본에 보이는 형상이 있는지, 결과가 표시되는 ScreenGui/Frame 아래인지, 부모·크기·위치·Visible 상태를 확인합니다. ReplicatedStorage는 자동 표시 위치가 아닙니다. |
| Archivable 또는 배치 제한 오류 | 오류 대상의 설정을 검토합니다. 적절한 경우 직접 Archivable을 켜거나 배치를 나눕니다. 원본 설정은 자동 변경되지 않습니다. |
| 형상이 잘려 보임 | margin을 늘리거나 시점/FOV를 조절하고 SpecialMesh 등 특수 형상을 확인합니다. |
| 원본을 수정해도 결과가 그대로임 | 0.1.0은 정적 복사본입니다. 새 배치를 생성하세요. 자동 갱신 기능은 없습니다. |
| Undo가 바쁘거나 작업 오류·중단 | Studio의 기존 작업이 끝난 뒤 보고서를 읽고 입력을 고쳐 재시도합니다. 중단한 검사는 완료 검사로 사용하지 않습니다. 복구가 필요하면 place 백업을 사용합니다. |

해결되지 않으면 위 연락처 또는 오류 제보 양식으로 문의해 주세요. 공유 권한이 있는
최소 예제만 제공하고, 가능하면 민감한 내용을 가린 화면과 오류 문구부터 보내 주세요.
이 저장소는 고객 문서 전용이며 플러그인 소스나 설치 파일을 배포하지 않습니다.
