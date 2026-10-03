# Clearance Check — Door and Passage 0.2.0

**Current release guide / 현재 출시판 안내 — 0.2.0**

This guide is for **0.2.0**. Confirm your installed plugin shows
**DOOR + PASSAGE / 0.2.0** before following it. New in 0.2.0: **edited Part-pivot
hinges** and **selection of existing collision groups**. Edge hinges, Clear/Cancel
and the built-in 2-zone example remain available from the earlier version.

이 문서는 **0.2.0** 사용법입니다. 설치한 패널에 **DOOR + PASSAGE / 0.2.0**이
표시되는지 먼저 확인하세요. 0.2.0의 새 기능은 **편집한 Part pivot 경첩**과
**기존 충돌 그룹 선택**입니다. 가장자리 경첩, Clear/Cancel과 내장 2구역 예제는
이전 버전부터 제공하던 기능입니다.

[Creator Store product](https://create.roblox.com/store/asset/132141689341950/Clearance-Check-Door-and-Passage)
· Asset **132141689341950** · Listed price **US$4.99**
(check Roblox for the current price and availability).

**[English](#english) · [한국어](#한국어)**

## English

### What the tool checks

Clearance Check finds **bounding-box overlap suspects** in rectangular passage
volumes and sampled door swings. Use it to find objects worth inspecting while
editing a place. It does not repair obstacles or move your original geometry.
A green result means this query found no suspects; it is not a guarantee that an
avatar can pass or that a physical door will work.

### First passage inspection

1. Save a separate place backup and stop Play. Open **Clearance** in the Plugins tab.
2. In a scratch place, click **Create 2-zone example (Undo supported)**. It adds two
   selected passage guide Parts and one obstacle. Keep the two guide Parts selected.
3. Use **Mode: Passage**, set **Margin** to `0`, and click **Inspect selection**.
   One example zone contains an obstacle; the other has no suspects for this query.
4. Read the report as well as the colors. **Select suspect parts** selects the reported
   obstacles. Select text in the report and copy it if you need a record.
5. For your own scene, select **1–50 rectangular block Parts in Workspace**. Their
   position, orientation and size define the passage test volumes. The selected
   guide Parts are excluded as obstacles. Margin expands each side by that many studs.
6. Use **Clear / Cancel** to remove the visualization or request cancellation.
   A cancelled inspection is not a completed result. Run again after changing the
   scene, controls, collision rules or reopening the place.

The example adds new objects; use Studio's **Edit → Undo** to remove them. Inspection
does not modify the original Parts, so clearing a report does not undo scene edits.

### Door swing with an edge or edited pivot

1. Select a rectangular block Part sized and oriented like your door. Click the mode
   button until it shows **Mode: Door swing**.
2. Set **Door angle** from **−180 to −1** or **1 to 180 degrees**. Positive and negative
   values sweep in opposite directions around the chosen pivot. Zero and angles
   with an absolute value below 1 are rejected. Set **Margin** from **0–10 studs**.
3. Click the hinge button to cycle through **Left local X edge**, **Right local X edge**
   and **Edited Part pivot**. Left and right refer to the Part's local X axis, not the
   camera's left and right.
4. For **Edited Part pivot**, first use Studio's **Edit Pivot** tool to position and
   orient that Part's pivot. The sweep rotates around the **pivot's local Y axis**.
   The pivot must be within **500 studs of the Part's center**. For an edge hinge,
   rotation follows the Part's local Y axis at the selected local X edge.
5. Choose the query collision group as described below, then click **Inspect selection**.
   Inspect each suspect in Studio before deciding whether to change the door or obstacle.

This models a rectangular door volume, not a hinge constraint or a moving assembly.
Changing the pivot changes the inspection path; the plugin does not set up a physical door.

### Collision groups and exclusions

Click **Collision group: … (click to change)** to cycle through groups already
registered in the place. The chosen group represents the **query's group**, and
its collision relationships filter potential obstacles. It does not assign that
group to your Parts or create new groups. Add or configure groups in Studio's
Collision Groups editor first. If a group is removed, select a valid group and rerun.

The inspection excludes Terrain, selected guide Parts, non-collidable obstacles,
objects excluded by `CanQuery` or the chosen group's collision rules, and objects
with `ClearanceIgnore=true` on themselves or an ancestor below Workspace. Setting
that attribute on Workspace itself does not exclude the whole scene.

### Limits and result interpretation

| Setting or input | Supported range |
| --- | --- |
| Test volumes | 1–50 rectangular block `Part` objects in Workspace; not Models, MeshParts, balls or cylinders |
| Part dimensions | Each dimension at most 500 studs |
| Door angle | −180…−1 or 1…180 degrees; fractional values within these ranges are accepted |
| Margin | 0–10 studs on each side |
| Edited pivot distance | At most 500 studs from the Part center |
| Inspection mode | Studio edit mode; stop Play first |

Passages use bounding-box overlap. Door sweeps sample the path at intervals of at
most 5 degrees and conservatively expand the sampled bounds to cover intermediate
poses. This can report objects that do not actually intersect the geometry. Numerical
padding can add suspects, especially far from the world origin.

This is not exact mesh/union collision, avatar walkability, pathfinding, Terrain
clearance, or a physics/constraint simulation. Results are a snapshot: changing an
obstacle or collision rule afterwards does not update the report automatically.
Changes to selected Parts during inspection can stop the scan; stabilize the scene and rerun.

### Troubleshooting and recovery

| Symptom | Next step |
| --- | --- |
| Selection error | Select only supported block Parts in Workspace and check the count and dimensions. |
| Expected obstacle is missing | Check `CanCollide`, `CanQuery`, group interaction, `ClearanceIgnore`, and whether it is one of the selected guides. Terrain is outside the supported query. |
| A reported object appears clear | Check its bounds, door orientation, hinge, angle and margin. Conservative sampling can produce false positives. |
| Door swings around the wrong point or axis | Verify local X edge choice, or reposition and orient the Part's edited pivot before inspecting again. |
| Group is missing | Register/configure it in Studio, then cycle the group button. The plugin does not create groups. |
| Inspection stopped, cancelled or scene changed | Treat it as incomplete. Read the message, correct the input and inspect again. |
| Error needs more detail | Read Studio Output and include the error text when contacting support. Do not use an old report as a successful new scan. |

Use normal Studio Undo for scene edits and example creation. Keep a separate place
backup for recovery. If you need to disable an installation, use Studio's plugin
management. Restore from your place backup if needed, and verify the displayed
plugin version before continuing.

### Support

[Email — primary](mailto:hkd0226@gmail.com?subject=Clearance%20Check%20support)
· [Email — backup](mailto:hkd0226@hanmail.net?subject=Clearance%20Check%20support)
· [Public bug report](https://github.com/hkd0226/roblox-studio-tools-support/issues/new/choose)

If a mail link does not open, use **hkd0226@gmail.com** or **hkd0226@hanmail.net** directly.
Include the product/version, Studio version, operating system, reproduction steps,
expected and actual results, and exact error text. No fixed response time is promised.
Public issues are visible to everyone; omit credentials, payment details and private
project files. Share only a minimal example you have permission to share. Roblox
checkout or billing problems should also be raised with Roblox Support.

## 한국어

### 무엇을 검사하나요?

직사각형 통로 공간과 문 회전 경로에서 **경계 상자가 겹치는 의심 대상**을 찾습니다.
편집 중 확인할 장애물을 찾는 도구이며, 원본 형상을 이동하거나 장애물을 자동 수정하지
않습니다. 초록색은 이 검사에서 의심 대상을 찾지 못했다는 뜻입니다. 아바타 통과나
물리적으로 작동하는 문을 보장하는 결과는 아닙니다.

### 통로 검사 처음 사용

1. place를 별도 파일로 백업하고 Play를 중지합니다. Plugins 탭의 **Clearance**를 엽니다.
2. 테스트 place에서 **Create 2-zone example (Undo supported)**을 누릅니다.
   통로 가이드 Part 두 개와 장애물 하나가 추가됩니다. 선택된 가이드 두 개를 유지합니다.
3. **Mode: Passage**, **Margin `0`**으로 **Inspect selection**을 실행합니다.
   예제 한 구역에는 장애물이 있고, 다른 구역은 이 검사에서 의심 대상이 없습니다.
4. 색상과 보고서를 함께 읽습니다. **Select suspect parts**로 보고된 장애물을 선택할
   수 있고, 보고서 텍스트를 선택해 복사할 수 있습니다.
5. 실제 장면에는 **Workspace의 직사각형 block Part 1–50개**를 선택합니다.
   위치·방향·크기가 검사 공간을 정하며, 선택한 가이드 자체는 장애물에서 제외됩니다.
   Margin 값만큼 검사 공간의 각 면을 바깥으로 넓힙니다.
6. **Clear / Cancel**로 시각화를 지우거나 중단을 요청합니다. 중단한 검사는 완료된
   결과로 사용하지 않습니다. 장면·설정·충돌 규칙을 바꾸거나 place를 다시 열면 재검사합니다.

예제는 새 객체를 추가하므로 Studio **Edit → Undo**로 제거할 수 있습니다. 검사는
원본 Part를 수정하지 않으며, 결과를 지우는 동작은 장면 편집을 되돌리는 동작이 아닙니다.

### 가장자리 경첩과 편집한 pivot으로 문 검사

1. 문 크기와 방향에 맞는 직사각형 block Part를 선택하고 모드 버튼을 눌러
   **Mode: Door swing**으로 바꿉니다.
2. **Door angle**은 **−180도부터 −1도 또는 1도부터 180도**, **Margin**은
   **0–10 studs**로 설정합니다. 각도 부호에 따라 반대 방향으로 회전합니다.
   0도와 절댓값 1도 미만은 허용하지 않습니다.
3. 경첩 버튼은 **Left local X edge → Right local X edge → Edited Part pivot**
   순서로 바뀝니다. 왼쪽·오른쪽은 화면 방향이 아닌 **Part의 로컬 X축** 기준입니다.
4. **Edited Part pivot**을 쓰려면 먼저 Studio **Edit Pivot**으로 해당 Part의 pivot
   위치와 방향을 편집합니다. 회전 축은 **pivot의 로컬 Y축**이며, pivot은 Part 중심에서
   **500 studs 이내**여야 합니다. 가장자리 경첩은 해당 로컬 X축 가장자리에서 Part의
   로컬 Y축을 기준으로 회전합니다.
5. 아래 충돌 그룹을 선택하고 **Inspect selection**을 누릅니다. 보고된 대상을 Studio에서
   확인한 다음 문 또는 장애물을 수정할지 결정합니다.

직사각형 문 공간을 검사할 뿐, 경첩 constraint나 움직이는 assembly를 시뮬레이션하지
않습니다. pivot 편집은 검사 경로를 바꾸며, 플러그인이 실제 물리 문을 구성하지는 않습니다.

### 충돌 그룹과 제외 대상

**Collision group: … (click to change)**를 눌러 place에 이미 등록된 그룹을 선택합니다.
선택한 그룹은 **검사 쿼리의 그룹**이며, 그 그룹의 충돌 관계로 장애물을 걸러냅니다.
원본 Part의 그룹을 바꾸거나 새 그룹을 만들지 않습니다. Studio의 Collision Groups
편집기에서 그룹과 관계를 먼저 설정하세요. 그룹이 삭제됐으면 유효한 그룹을 선택해 다시 검사합니다.

Terrain, 선택한 가이드, 비충돌 장애물, `CanQuery` 또는 선택 그룹의 충돌 규칙으로
제외되는 대상은 검사하지 않습니다. 자신이나 Workspace 아래 조상에
`ClearanceIgnore=true` 속성이 있는 대상도 제외합니다. Workspace 자체에 이 속성을
설정해도 장면 전체가 제외되지는 않습니다.

### 범위와 결과 해석

| 항목 | 지원 범위 |
| --- | --- |
| 검사 공간 | Workspace의 직사각형 block `Part` 1–50개; Model, MeshPart, 공·원기둥은 입력 불가 |
| Part 크기 | 각 크기 최대 500 studs |
| 문 각도 | −180…−1 또는 1…180도; 이 범위 안의 소수 각도도 가능 |
| Margin | 각 면 0–10 studs |
| 편집 pivot 거리 | Part 중심에서 최대 500 studs |
| 사용 모드 | Studio 편집 모드; Play 중지 필요 |

통로는 경계 상자 겹침을 검사합니다. 문 회전은 최대 5도 간격으로 표본을 만들고,
사이 경로를 포함하도록 경계를 보수적으로 넓힙니다. 실제 형상끼리 겹치지 않아도
의심 대상으로 보고할 수 있습니다. 특히 월드 원점에서 먼 곳은 계산 여유로 의심 대상이
추가될 수 있습니다.

정밀 mesh/union 충돌, 아바타 통과, pathfinding, Terrain 여유 또는 물리·constraint
검사는 지원 범위가 아닙니다. 결과는 검사 당시의 상태입니다. 이후 장애물이나 충돌
규칙을 바꿔도 자동 갱신되지 않습니다. 검사 중 선택한 Part가 바뀌면 중단될 수 있으니
장면을 안정시킨 뒤 다시 실행하세요.

### 문제 해결과 복구

| 증상 | 확인할 항목 |
| --- | --- |
| 선택 오류 | Workspace의 지원하는 block Part만 선택하고 개수·크기를 확인합니다. |
| 예상 장애물이 안 나옴 | CanCollide, CanQuery, 그룹 관계, ClearanceIgnore 및 선택한 가이드인지 확인합니다. Terrain은 지원하지 않습니다. |
| 실제로는 안 겹쳐 보이는 대상이 나옴 | 대상 경계와 문 방향·경첩·각도·margin을 확인합니다. 보수적 표본 검사로 추가 의심 대상이 나올 수 있습니다. |
| 잘못된 위치나 축으로 문이 회전함 | 로컬 X축 가장자리 선택 또는 편집한 Part pivot의 위치·방향을 고쳐 재검사합니다. |
| 그룹이 안 보임 | Studio에서 그룹을 등록·설정한 뒤 그룹 버튼을 누릅니다. 플러그인은 그룹을 생성하지 않습니다. |
| 중단·취소 또는 장면 변경 안내 | 미완료 검사로 취급하고 안내를 읽어 입력을 고친 뒤 다시 실행합니다. |
| 오류의 추가 정보가 필요함 | Studio Output의 문구를 확인해 문의에 포함합니다. 예전 보고서를 새 검사의 성공 결과로 사용하지 않습니다. |

장면 편집과 예제 생성은 일반 Studio Undo로 되돌리고, 별도 place 백업을 보관하세요.
설치를 비활성화·제거해야 하면 Studio 플러그인 관리를 이용하세요. 필요하면 place
백업으로 복구하고 표시된 플러그인 버전을 확인한 뒤 작업을 계속하세요.

### 문의

[기본 이메일](mailto:hkd0226@gmail.com?subject=Clearance%20Check%20support)
· [예비 이메일](mailto:hkd0226@hanmail.net?subject=Clearance%20Check%20support)
· [공개 오류 제보](https://github.com/hkd0226/roblox-studio-tools-support/issues/new/choose)

메일 링크가 열리지 않으면 **hkd0226@gmail.com** 또는 **hkd0226@hanmail.net**으로
직접 작성해 주세요. 제품·버전, Studio 버전, 운영체제, 재현 순서, 예상·실제 결과와
정확한 오류 문구를 포함합니다. 정해진 응답 시간은 약속하지 않습니다. 공개 제보는
누구나 볼 수 있으므로 인증 정보·결제 정보·비공개 프로젝트 파일은 올리지 마세요.
공유 권한이 있는 최소 예제만 제공하고, Roblox 결제 자체의 문제는 Roblox 고객지원에도
문의해 주세요.
