# Viewport Batch Builder 0.2.0

**Release candidate guide / 출시 전 안내**

The Creator Store currently offers **0.1.0**. Version **0.2.0 is not released yet**.
This guide describes the 0.2.0 candidate. Named presets, loading a frame's saved
settings and regenerating one frame are not features of the current 0.1.0 store
version. This candidate includes revised handling for saved frames after reopening.
Fresh native tests, full Studio restart/regeneration and final game-interface checks
remain pending for this revision. Confirm the panel shows **v0.2.0**
before following this guide.

현재 Creator Store 판매판은 **0.1.0**이며 **0.2.0은 아직 출시 전**입니다.
이 문서는 0.2.0 후보의 사용법입니다. 이름 있는 프리셋, 프레임 설정 불러오기,
프레임 한 개 갱신은 현재 0.1.0 판매판 기능이 아닙니다. 이번 후보는 재열기 후 저장된
프레임 처리를 수정했습니다. 이 수정본의 새 엔진 검수, 전체 Studio 재시작 후 갱신과
최종 게임 UI 검수는 아직 미완료입니다. 패널에 **v0.2.0**이
표시되는지 확인한 뒤 이 안내를 사용하세요.

[Creator Store product](https://create.roblox.com/store/asset/71263242408985/Viewport-Batch-Builder)
· Asset **71263242408985** · Listed price **US$4.99**
(check Roblox for the current price and availability).

**[English](#english) · [한국어](#한국어)**

## English

### What you get

Build native, static **ViewportFrames** from selected Models or BaseParts for
inventory and shop UI. The camera fits visible geometry using the selected frame
aspect ratio, view and margin. The output is a static clone: there is **no PNG export,
animation, runtime turntable or live synchronization** with the source.

### First batch

1. Save a separate place backup and stop Play. Open **Viewport Batch** in the Plugins tab.
2. Select the original **Models or BaseParts** in Explorer. Each selected root is one
   batch item; selecting both a parent and its child does not create duplicate items.
3. Set **WIDTH**, **HEIGHT**, **YAW**, **PITCH**, **FIELD OF VIEW** and **MARGIN**.
   Choose **Lighting: Studio / Soft / Contrast** and
   **Background: Transparent / Dark / Light** by cycling their buttons.
4. Click **Preview first selected model**. Check the view and increase margin if needed.
   The preview shows only the first selected source, not the whole batch.
5. Click **Generate batch**. Read the created count, skipped items and warnings.
   Invalid individual sources can be skipped; do not assume every selected item was created.
6. Find the output under **ReplicatedStorage → ViewportBatch**. A number is added if
   the folder name is occupied. Sources with the same name receive distinct output names.
7. Copy or move the ViewportFrames into your own **ScreenGui / Frame**, for example
   an inventory container under StarterGui. Keep each frame's preview WorldModel and
   Camera. ReplicatedStorage does not display a game UI automatically. Check parent,
   size, position, Visible state and layout, then test your actual interface in Play.

Generation uses cloned geometry. Original sources are not moved, resized or rewritten.
Scripts and package links are removed from the clones before they enter the place;
cloned Parts are anchored and have collision, touch and query disabled. Use Studio's
**Edit → Undo / Redo** for the generated batch. **Cancel current batch** requests a
stop after the current source; a cancelled batch does not save its new staged output.

### Save and load a named look

1. Set your camera, frame dimensions, margin, lighting and background.
2. Under **SAVED LOOKS · local Studio settings**, enter a name such as **Pilot_A**.
   Click **Save / replace named preset** and check the saved confirmation message.
3. Click **Choose saved preset** until the desired name is chosen, then click
   **Load chosen preset**. This fills the controls; it does not update existing frames.
   Preview, generate or regenerate after loading.
4. To replace a look, save using the same name. Names are matched without case.
   To remove it, choose it and click **Delete chosen preset**; generated frames are not deleted.

Presets use this plugin's **local Studio settings on the same computer**. They are
not embedded in the place or synchronized through this tool to another computer or
account. Saving and restoring `Pilot_A` after a full restart were observed with the
previous candidate. Fresh checks of this revised candidate remain pending. To try restoration,
reopen Studio and use **Choose saved preset → Load chosen preset**. Keep a written
copy of important settings when changing computers or reinstalling the plugin.

Up to **20** presets are supported. Trimmed names must use **1–80 UTF-8 bytes**,
with no control characters or backslash; Korean characters can use several bytes.
If saving cannot be confirmed, close other Studio windows and retry. Do not keep
overwriting presets while Studio reports that existing saved data is unavailable.

### Edit the source and refresh only its card

1. Make your intended edits to the **original Model or BasePart**. Existing output
   stays unchanged until you explicitly regenerate it.
2. Select **exactly one generated ViewportFrame** in Explorer. If you want its previous
   look, click **Load settings from selected frame**, then make any desired changes
   to the controls. Regeneration uses the current controls, not an automatically selected preset.
3. Click **Regenerate selected frame only**. It uses the frame's original-source
   reference and refreshes only that frame's static clone, camera and appearance.
4. Check the card in its actual UI. Use normal Studio **Edit → Undo / Redo** to compare
   the update; keep a separate place backup for recovery.

The existing ViewportFrame object, its parent, Size, Position and LayoutOrder remain
in place. Sibling cards, UI decoration children and your custom attributes are
preserved. Rendering contents, lighting/background, plugin metadata and the aspect
ratio constraint are updated for the new settings. The operation does not resize
the existing frame's UI rectangle; adjust your layout yourself if its dimensions
need to change. Avoid manually renaming, replacing or duplicating the plugin's
PreviewWorld, PreviewCamera or VBBSourceReference children.

After saving and reopening a place, Studio can display a static card with its
`CurrentCamera` reference empty. Preserve its PreviewCamera and PreviewWorld children.
This candidate accepts that normal saved state for regeneration and still rejects
a different camera reference. Actual reopened-frame regeneration, Undo/Redo and
rendering checks for this revision remain pending; an empty reference alone is not
proof that the preview structure is damaged.

An older 0.1.0 frame may not have stored settings or a source reference. Choose a
preset or set the controls yourself, and supply the original source as below.

### If the original-source reference is missing

The `VBBSourceReference` ObjectValue links a generated frame to its original source.
If that link is empty or the original is unavailable, the tool asks for an explicit
source. It does not guess from names or paths.

1. In Explorer, select **one generated ViewportFrame plus exactly one intended
   original Model or BasePart**. Do not select a clone inside that ViewportFrame.
2. Confirm this is the correct original, especially when several Models share a name.
   Load/set the desired controls, then click **Regenerate selected frame only**.
3. The existing source-reference object is retained when present, and its Value is
   rebound to your explicitly selected source. Only this card is refreshed.

A missing-source attempt reports an error before refreshing the card; correct the
selection and retry. Supplying an explicit source can also intentionally change
which item a card represents. Check the result before saving your place.

### Limits

| Setting or input | Supported range |
| --- | --- |
| Batch size | At most 100 selected roots |
| Geometry count | At most 5,000 BaseParts per root and 20,000 per batch |
| Source | Model or BasePart containing visible BasePart geometry; source and geometry descendants must be Archivable |
| Width / height | Whole numbers 64–1,024 pixels |
| Aspect ratio | 1:4–4:1 |
| Yaw / pitch | −180…180° / −80…80° |
| Field of view | 10–90° |
| Margin | 0–40% per edge |
| Lighting / background | Studio, Soft, Contrast / Transparent, Dark, Light |

Legacy SpecialMesh bounds can need extra margin. ViewportFrame rendering differs
from Workspace rendering; check unusual geometry, materials and your final UI.
The tool is an edit-time static preview builder, not a game inventory system.

### Troubleshooting and recovery

| Symptom | Next step |
| --- | --- |
| Blank preview | Select a supported source containing visible BaseParts. Completely transparent geometry is not used to fit the camera. |
| Output is invisible in game | Place it under a displayed ScreenGui/Frame, preserve its Camera/WorldModel, and check parent, size, position and Visible. |
| Cropped view | Increase margin or adjust yaw, pitch or FOV. Check SpecialMesh warnings visually. |
| Source edits are absent | Regenerate that frame explicitly; there is no live refresh. |
| Old frame has no saved settings | Use current controls or a named preset and explicitly select the original source if needed. |
| Original source unavailable | Select one generated frame and exactly one original Model/BasePart, then regenerate. |
| Rendering structure changed | Restore the frame's original preview structure or generate a fresh frame; do not guess which renamed children should be used. |
| Archivable or count error | Review the reported source; enable Archivable yourself only if appropriate, or split the batch. The plugin does not change source settings. |
| Undo is busy or regeneration fails | Let Studio finish its other operation, read the error and retry after correcting the input. Keep a place backup. |
| Saved preset unavailable | Close other Studio windows and retry; do not overwrite known presets while a read/save error is shown. |

Use normal Studio Undo and a saved place backup rather than relying on Undo alone.
To revert a candidate installation, disable/remove it in Studio's plugin management
and return to the released plugin. Local preset settings are separate from a place
backup; keep a written copy before switching machines or reinstalling.

### Support

[Email — primary](mailto:hkd0226@gmail.com?subject=Viewport%20Batch%20Builder%20support)
· [Email — backup](mailto:hkd0226@hanmail.net?subject=Viewport%20Batch%20Builder%20support)
· [Public bug report](https://github.com/hkd0226/roblox-studio-tools-support/issues/new/choose)

If a mail link does not open, use **hkd0226@gmail.com** or **hkd0226@hanmail.net** directly.
Include product/version, Studio version, operating system, reproduction steps,
expected and actual results, and exact error text. No fixed response time is promised.
Public issues are visible to everyone; omit credentials, payment details and private
project files. Share only a minimal example you have permission to share. Roblox
checkout or billing problems should also be raised with Roblox Support.

## 한국어

### 생성하는 결과

선택한 Model 또는 BasePart로 인벤토리·상점 UI용 정적 **ViewportFrame**을 만듭니다.
프레임 비율·시점·margin에 맞춰 보이는 형상을 카메라에 담습니다. 결과는 정적 복사본이며
**PNG 내보내기, 애니메이션, 실행 중 자동 회전, 원본 변경 자동 동기화는 없습니다.**

### 첫 배치 생성

1. place를 별도 파일로 백업하고 Play를 중지합니다. Plugins 탭의 **Viewport Batch**를 엽니다.
2. Explorer에서 원본 **Model 또는 BasePart**를 선택합니다. 최상위 선택 단위마다 결과
   한 개를 만듭니다. 부모와 자식을 함께 선택해도 중복 결과를 만들지 않습니다.
3. **WIDTH**, **HEIGHT**, **YAW**, **PITCH**, **FIELD OF VIEW**, **MARGIN**을 설정합니다.
   조명 버튼은 **Studio / Soft / Contrast**, 배경 버튼은 **Transparent / Dark / Light**
   순서로 바꿀 수 있습니다.
4. **Preview first selected model**로 시점과 잘림을 확인합니다. 필요하면 margin을
   늘립니다. 미리보기는 첫 번째 선택 원본만 보여주며 배치 전체를 보여주지는 않습니다.
5. **Generate batch**를 실행하고 생성 개수·건너뛴 항목·경고를 확인합니다. 사용할 수 없는
   개별 원본은 건너뛸 수 있으므로 선택한 항목이 모두 생성됐다고 가정하지 마세요.
6. **ReplicatedStorage → ViewportBatch**에서 결과를 찾습니다. 이름이 이미 있으면 번호를
   붙입니다. 원본 이름이 같아도 결과 이름을 구분합니다.
7. 프레임을 자신의 **ScreenGui / Frame**으로 복사하거나 이동합니다. 예를 들어 StarterGui의
   인벤토리 컨테이너에 넣습니다. 프레임 내부의 WorldModel과 Camera를 유지하세요.
   ReplicatedStorage 결과는 게임 UI에 자동 표시되지 않습니다. 부모·크기·위치·Visible·
   레이아웃을 확인하고 실제 게임 UI를 Play에서 확인합니다.

원본을 이동·크기 변경·수정하지 않고 복사본을 사용합니다. 복사본이 place에 들어가기
전에 스크립트와 package link를 제거하며, 복사된 Part를 고정하고 충돌·touch·query를
끕니다. 배치 생성은 Studio **Edit → Undo / Redo**를 사용합니다. **Cancel current batch**는
현재 원본 처리 후 중단을 요청하며, 취소한 배치의 새 임시 결과는 저장하지 않습니다.

### 이름 있는 프리셋 저장·불러오기

1. 카메라·프레임 크기·margin·조명·배경을 설정합니다.
2. **SAVED LOOKS · local Studio settings**에 **Pilot_A** 같은 이름을 입력하고
   **Save / replace named preset**을 누릅니다. 저장 확인 문구를 확인하세요.
3. **Choose saved preset**으로 원하는 이름을 고른 뒤 **Load chosen preset**을 누릅니다.
   설정 입력값만 불러오며 기존 프레임은 바뀌지 않습니다. 이후 미리보기·배치 생성·
   개별 프레임 갱신 중 필요한 작업을 실행합니다.
4. 같은 이름으로 저장하면 기존 프리셋을 교체하며 대소문자는 구분하지 않습니다.
   삭제는 이름을 고르고 **Delete chosen preset**을 누릅니다. 생성된 프레임은 삭제하지 않습니다.

프리셋은 **같은 컴퓨터의 플러그인용 로컬 Studio 설정**에 저장합니다. place에 포함되지
않고, 이 도구가 다른 컴퓨터나 계정으로 동기화하지 않습니다. 이전 후보에서는 `Pilot_A`
저장과 전체 Studio 재시작 후 불러오기를 확인했습니다. 이번 수정본의 새 검수는 아직 미완료입니다.
복원을 확인할 때는 다시 연 Studio에서 **Choose saved preset → Load chosen preset**을
사용하세요. 컴퓨터 변경이나 재설치 전 중요한 설정값은 따로 적어 두세요.

최대 **20개**이며, 앞뒤 공백을 뺀 이름은 **UTF-8 1–80바이트**입니다. 제어 문자와
역슬래시는 사용할 수 없고, 한글은 글자당 여러 바이트를 사용할 수 있습니다.
저장 확인 오류가 나면 다른 Studio 창을 닫고 재시도합니다. 기존 프리셋을 읽을 수 없다는
안내가 나오는 동안 계속 덮어쓰지 마세요.

### 원본을 편집한 뒤 카드 한 개만 갱신

1. 원하는 변경을 **원본 Model 또는 BasePart**에 적용합니다. 기존 결과는 직접 갱신할
   때까지 그대로 유지됩니다.
2. Explorer에서 **생성된 ViewportFrame 한 개만** 선택합니다. 이전 모양을 유지하려면
   **Load settings from selected frame**을 누른 뒤 입력값을 조정합니다. 갱신은 현재
   입력값을 사용하며 프리셋을 자동으로 골라 적용하지 않습니다.
3. **Regenerate selected frame only**를 누릅니다. 원본 참조를 사용해 해당 프레임의
   정적 복사본·카메라·표시를 갱신합니다.
4. 실제 UI에서 결과를 확인합니다. 일반 Studio **Edit → Undo / Redo**로 변경을 비교하고
   별도 place 백업을 보관합니다.

기존 ViewportFrame 객체, 부모, Size, Position, LayoutOrder를 유지합니다. 옆 카드,
UI 장식 자식 객체와 사용자가 추가한 속성도 보존합니다. 표시용 내부 형상·카메라,
조명·배경, 플러그인 메타데이터와 비율 constraint는 새 설정에 맞춰 바뀝니다.
기존 프레임의 UI 사각형 크기를 자동 변경하지 않으므로 크기가 달라져야 하면 레이아웃을
직접 조정하세요. 플러그인의 PreviewWorld, PreviewCamera, VBBSourceReference를 임의로
이름 변경·교체·중복 생성하지 않는 것이 좋습니다.

place를 저장하고 다시 열면 정적 카드가 표시되더라도 `CurrentCamera` 참조가 비어 있을
수 있습니다. PreviewCamera와 PreviewWorld 자식 객체는 유지하세요. 이번 후보는 이 정상
저장 상태에서 갱신을 허용하며 관계없는 카메라 참조는 계속 거부합니다. 이 수정본의 실제
재열기 후 갱신·Undo/Redo·화면 표시 검수는 아직 미완료입니다. 참조가 비어 있다는 이유만으로
표시 구조가 손상됐다고 판단하지 마세요.

0.1.0에서 만든 프레임은 저장된 설정이나 원본 참조가 없을 수 있습니다. 프리셋 또는
직접 입력값을 사용하고 아래 방법으로 원본을 함께 선택하세요.

### 원본 참조가 비어 있거나 끊겼을 때

`VBBSourceReference` ObjectValue는 결과 프레임과 원본을 연결합니다. 참조가 비어 있거나
원본을 사용할 수 없으면 원본을 직접 선택하라는 안내를 표시합니다. 이름·경로로 추측하지 않습니다.

1. Explorer에서 **생성된 ViewportFrame 한 개 + 의도한 원본 Model 또는 BasePart 한 개**를
   함께 선택합니다. 프레임 안에 들어 있는 미리보기 복사본을 원본으로 선택하지 마세요.
2. 특히 같은 이름의 Model이 여럿이면 올바른 원본인지 확인합니다. 입력값을 불러오거나
   설정한 뒤 **Regenerate selected frame only**를 누릅니다.
3. 기존 원본 참조 객체가 있으면 그 객체를 유지하며 Value를 직접 선택한 원본에 연결합니다.
   선택한 카드만 갱신합니다.

원본이 없는 상태의 실행은 카드를 갱신하기 전에 오류를 알립니다. 선택을 고쳐 재시도하세요.
원본을 직접 선택하면 카드가 나타내는 항목을 의도적으로 바꿀 수도 있으므로 place 저장 전에
결과를 확인하세요.

### 제한

| 항목 | 지원 범위 |
| --- | --- |
| 배치 | 최상위 선택 단위 최대 100개 |
| 형상 개수 | 단위당 BasePart 최대 5,000개, 배치 전체 최대 20,000개 |
| 원본 | 보이는 BasePart 형상을 포함한 Model 또는 BasePart; 원본과 형상 자손의 Archivable 필요 |
| 너비·높이 | 정수 64–1,024픽셀 |
| 비율 | 1:4–4:1 |
| Yaw / Pitch | −180…180도 / −80…80도 |
| FOV | 10–90도 |
| Margin | 각 가장자리 0–40% |
| 조명 / 배경 | Studio, Soft, Contrast / Transparent, Dark, Light |

오래된 SpecialMesh는 여유가 더 필요할 수 있습니다. ViewportFrame과 Workspace 렌더링은
다를 수 있으므로 특수 형상·재질과 최종 UI를 확인하세요. 편집 중 정적 미리보기를 만드는
도구이며 게임 인벤토리 시스템 전체를 구성하지는 않습니다.

### 문제 해결과 복구

| 증상 | 확인할 항목 |
| --- | --- |
| 빈 미리보기 | 보이는 BasePart가 있는 지원 원본을 선택합니다. 완전히 투명한 형상은 카메라 맞춤에 쓰지 않습니다. |
| 게임에서 안 보임 | 표시되는 ScreenGui/Frame 아래에 넣고 Camera/WorldModel을 유지하며 부모·크기·위치·Visible을 확인합니다. |
| 형상이 잘림 | margin을 늘리거나 yaw·pitch·FOV를 조정하고 SpecialMesh 경고를 실제 화면에서 확인합니다. |
| 원본 변경이 안 보임 | 해당 프레임을 직접 갱신합니다. 자동 동기화 기능은 없습니다. |
| 오래된 프레임에 저장 설정 없음 | 현재 입력값 또는 프리셋을 사용하고 필요하면 원본을 직접 함께 선택합니다. |
| 원본을 사용할 수 없음 | 결과 프레임 한 개와 원본 Model/BasePart 한 개를 선택해 갱신합니다. |
| 표시 구조 변경 오류 | 기존 내부 구조를 복원하거나 새 프레임을 생성합니다. 이름이 바뀐 자식 객체를 추측해 사용하지 않습니다. |
| Archivable 또는 개수 오류 | 안내된 원본을 검토하고 적절한 경우 직접 Archivable을 켜거나 배치를 나눕니다. 원본 설정은 자동 변경하지 않습니다. |
| Undo 작업 중 또는 갱신 오류 | Studio의 다른 작업이 끝난 뒤 오류를 읽고 입력을 고쳐 재시도합니다. place 백업을 유지하세요. |
| 프리셋 읽기·저장 오류 | 다른 Studio 창을 닫고 재시도하며 오류 중에는 알고 있는 프리셋을 덮어쓰지 않습니다. |

일반 Studio Undo와 place 백업을 함께 사용하세요. 후보 설치를 되돌릴 때는 플러그인 관리에서
비활성화·제거한 뒤 출시판으로 돌아갑니다. 로컬 프리셋은 place 백업과 별개이므로 컴퓨터
변경이나 재설치 전 중요한 설정값을 따로 적어 두세요.

### 문의

[기본 이메일](mailto:hkd0226@gmail.com?subject=Viewport%20Batch%20Builder%20support)
· [예비 이메일](mailto:hkd0226@hanmail.net?subject=Viewport%20Batch%20Builder%20support)
· [공개 오류 제보](https://github.com/hkd0226/roblox-studio-tools-support/issues/new/choose)

메일 링크가 열리지 않으면 **hkd0226@gmail.com** 또는 **hkd0226@hanmail.net**으로 직접
작성하세요. 제품·버전, Studio 버전, 운영체제, 재현 순서, 예상·실제 결과와 오류 문구를
포함합니다. 정해진 응답 시간은 약속하지 않습니다. 공개 제보에 인증 정보·결제 정보·비공개
프로젝트 파일을 올리지 마세요. 공유 권한이 있는 최소 예제만 제공하고, Roblox 결제 자체의
문제는 Roblox 고객지원에도 문의해 주세요.
