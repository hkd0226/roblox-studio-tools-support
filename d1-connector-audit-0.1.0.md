# D1 Connector Audit — v0.1.0

## English

D1 Connector Audit checks the Attachment connections you declare in selected Workspace module Models. Use issue rows to select the actual endpoints, then edit with Studio's normal tools and scan again.

### What the tool checks

Audit the Attachment connections that you explicitly declare in selected module Models. Results show missing or duplicate ends, pairs inside the same selected module, positional gaps and two orientation errors. Click a result row to select its actual endpoint objects, or select and copy the text report.

It inspects a snapshot at scan time. It does not discover undeclared joints, repair placement, or check collision, mesh seams, physical joints or avatar traversal.

### Installation and opening

Check the plugin's current availability and price on Roblox before purchasing. Install through Roblox's normal plugin flow, then open **Plugins → D1 Connector Audit → Connector Audit**. The panel title is **D1 Connector Audit 0.1.0**. Work in edit mode, in a copy or backup of your place.

The plugin does not need HTTP access, an API key or external code downloads.

### Declare your own connections

1. Treat each selected Workspace Model as one module. Select Models at one hierarchy level; do not select a Model and one of its descendant Models together.
2. Put each inspected Attachment directly under a BasePart in that module.
3. In the Attachment's Attributes, add a String named `D1PairId`. Use a shared ID for the two intended endpoints in different modules. IDs are case-sensitive and contain 1–64 ASCII letters, digits, underscores, dots or hyphens. Examples: `Door_A`, `hall.03`, `socket-1`.
4. Leave `D1Open` absent or set it to Boolean `false` for a normal pair. A Boolean `true` permits a single intentionally open endpoint; it does not permit an open flag on a two-endpoint pair.
5. Set the endpoint frames to your intended connection. Their primary axes (Attachment local X / WorldAxis) must oppose each other; their secondary axes (local Y / WorldSecondaryAxis) must align. This orientation convention must suit your design.
6. Every Attachment inside the selected Models is inspected and must have a valid declaration, including helper Attachments. Exclude unrelated modules, rigs and helpers from your selection.

Two endpoints with the same ID inside one selected Model are reported as **SAME_MODULE**. More than two endpoints with one ID are **DUPLICATE**; the tool does not guess which pair you intended.

### Run and use a report

1. Select the module Models in Explorer.
2. Set **Position tolerance** and **Angle tolerance**. Defaults are `0.05` studs and `3` degrees. Allowed ranges are 0–10 studs and 0–180 degrees.
3. Click **Scan selected Models**. Read the module/connector counts and scroll the result rows.
4. A gap or angle greater than its tolerance fails that check. Equality is accepted. **PASS** means only that the declared connector contract meets these limits.
5. Click a row to select its actual Attachments. This changes selection, not the module's geometry. Edit with Studio's normal tools and scan again.
6. Click **Select report text — then Ctrl+C**, press Ctrl+C and paste into your notes. Check that the pasted report includes its header and final row.
7. Use **Clear / Cancel** to clear the current rows/report and request cancellation of pending work. Hiding the panel or unloading the plugin also invalidates pending results. If the scene changes during a scan, correct the input and rescan.

A result row is a snapshot too. Moving a module or changing IDs after a report does not update its old measurements. Removed endpoints require a new scan.

### Optional example: 10 declared connection groups

[Download the example place](./D1-10Joint-Customer-Source0.rbxlx): `D1-10Joint-Customer-Source0.rbxlx`. It contains 67 authored objects: 11 Folders, 18 Models, 19 Parts and 19 Attachments, with no Script, ModuleScript or PackageLink. The place may also contain normal Studio services, Camera and Terrain.

Download the example separately from the plugin. Buying or installing a plugin does not automatically install this example place.

1. Save any existing work. Use Studio **File → Open** (Ctrl+O) to open `D1-10Joint-Customer-Source0.rbxlx` as a separate example place.
2. Stay in edit mode and check that `D1_10Joint_Compare` is a Folder under Workspace. This route opens a place; it does not merge the example into your current project.
3. Expand that folder and its `J01`–`J10` folders.
4. Select the **18 module Models inside the J folders**, together. Do not select the root Folder, the J folders, individual Parts or Attachments.
5. Set `0.05` studs and `3` degrees, then scan.
6. The unedited example is designed for **18 Models, 19 Attachments, 10 rows: 2 PASS, 1 intentional open and 7 issues**. Compare every row with the table below.
7. Click J02's row: it should select the two Endpoint objects in J02's separate modules. Scroll to J10 and copy the full report.
8. Clear, reselect the 18 Models and scan again. Save the test place, close Studio normally, reopen it, set the tolerances and scan again. Do not rely on a report surviving restart.

| Group | Expected status | Meaning |
| --- | --- | --- |
| J01 | PASS | Coincident, correctly oriented pair |
| J02 | FAIL_POSITION | Position gap around 0.2 studs |
| J03 | FAIL_PRIMARY | Primary-axis error around 12° |
| J04 | FAIL_SECONDARY | Secondary-axis error around 12° |
| J05 | MISSING | Single end without intentional-open permission |
| J06 | DUPLICATE | Three declared ends |
| J07 | OPEN_ACCEPTED | Explicit intentional-open singleton |
| J08 | SAME_MODULE | Both ends in one selected module |
| J09 | PASS | Gap/angle just inside default limits |
| J10 | FAIL_POSITION_PRIMARY | Gap/primary angle just outside default limits |

Small displayed differences in floating-point measurements do not change the intended meaning of this example. **OPEN_ACCEPTED** is an accepted open end, not a complete joint.

### Preservation, Undo and limits

The audit does not move, resize, recolor or rewrite module geometry, Source or attributes. Selecting a row does change the current selection. Use normal Studio Undo/Redo for your own edits, then rescan; the audit does not create a geometry-repair operation to undo. Keep a place backup before editing.

The limits are **200 selected Models, 200 Attachments and 5,000 inspected instances**. Nested selected Models are rejected. Attachments directly under a Bone or other non-BasePart parent are unsupported. A connection missing both declarations cannot be discovered. A wrong authored ID or axis can produce a misleading contract result; inspect your intended design yourself.

### Troubleshooting and support

- **No declared connectors:** check that selected objects are Workspace Models containing Attachments.
- **Invalid input:** check every selected Attachment's direct parent and exact attribute types/names/ID characters.
- **Missing or duplicate:** inspect all ends that share the displayed ID.
- **Changed during scanning / removed endpoint:** reselect the current modules and rescan.
- **Old or empty report:** scan again; report data is not saved as your place's audit history.
- **Cannot open or find the example:** use File → Open for the exact `.rbxlx` filename and report the filename and Studio version; the download is not automatically included by buying a plugin.

Use [GitHub support](https://github.com/hkd0226/roblox-studio-tools-support) and [Issues](https://github.com/hkd0226/roblox-studio-tools-support/issues). Submitting an Issue requires a GitHub login. Email: [hkd0226@gmail.com](mailto:hkd0226@gmail.com), backup [hkd0226@hanmail.net](mailto:hkd0226@hanmail.net). Include product/version, Studio version/OS, reproduction steps, expected/actual result and error text. Do not attach private projects, credentials or personal data. No response-time is promised.

## 한국어

D1 Connector Audit는 선택한 Workspace 모듈 Model에서 직접 선언한 Attachment 연결점을 검사합니다. 문제 행으로 실제 연결점을 선택한 뒤 Studio 기본 도구로 편집하고 다시 검사하세요.

### 검사 범위와 설치

선택한 모듈 Model 안의 Attachment 규약을 검사합니다. 누락·중복·같은 모듈 내 쌍·위치 오차·두 축 오차를 표시하고, 결과 행을 눌러 실제 연결점을 선택하거나 보고서 전체를 복사합니다. 선언되지 않은 연결을 자동 발견하거나 배치를 고치지 않습니다. 충돌·메시 이음새·물리 Joint·아바타 통과 검사가 아닙니다.

구매 전에 Roblox에서 플러그인의 현재 공개 여부와 가격을 확인하세요. Roblox의 정상 플러그인 설치 절차로 설치한 뒤 **Plugins → D1 Connector Audit → Connector Audit** 를 엽니다. 창 제목은 **D1 Connector Audit 0.1.0** 입니다. 백업 또는 별도 시험 place의 편집 모드에서 사용하세요. HTTP·API 키·외부 코드 다운로드가 필요하지 않습니다.

### 연결점 선언

1. Workspace의 선택 Model 하나를 모듈 하나로 취급합니다. 같은 계층의 모듈만 선택하고, Model과 그 자손 Model을 함께 선택하지 마세요.
2. 검사할 Attachment를 모듈의 BasePart 직계 자식으로 둡니다.
3. Attachment의 Attributes에 String `D1PairId` 를 추가합니다. 서로 다른 모듈의 의도한 두 끝에 같은 ID를 사용합니다. 대소문자를 구분하며 ASCII 영문자·숫자·밑줄·점·하이픈만 1–64자 허용합니다. 예: `Door_A`, `hall.03`, `socket-1`.
4. 일반 쌍은 `D1Open` 을 생략하거나 Boolean `false` 로 둡니다. Boolean `true` 는 의도된 열린 끝 하나만 허용합니다. 두 끝이 있는 쌍에 open을 지정하면 허용되지 않습니다.
5. primary 축(Attachment local X / WorldAxis)은 서로 반대, secondary 축(local Y / WorldSecondaryAxis)은 같은 방향이 되도록 작성합니다. 이 규약이 자신의 설계에 맞는지 확인하세요.
6. 선택 Model 안의 **모든 Attachment** 를 검사합니다. 보조 Attachment도 올바른 규약이 필요하므로 불필요한 모듈·리그·보조 객체를 선택에서 제외하세요.

같은 선택 Model의 두 끝은 **SAME_MODULE**, 같은 ID의 세 끝 이상은 **DUPLICATE** 입니다. 도구가 의도한 쌍을 추측하지 않습니다.

### 검사·선택·복사

1. Explorer에서 모듈 Model들을 선택합니다.
2. **Position tolerance** 와 **Angle tolerance** 를 설정합니다. 기본값은 `0.05` stud / `3` 도, 허용 범위는 0–10 stud / 0–180도입니다.
3. **Scan selected Models** 를 눌러 개수와 결과 행을 확인합니다. 결과는 스크롤할 수 있습니다.
4. 허용오차를 초과하면 해당 검사 실패이며, 같은 값은 허용합니다. **PASS** 는 선언한 규약의 수치 조건만 충족했다는 뜻입니다.
5. 결과 행을 누르면 실제 Attachment가 선택됩니다. 기하는 바꾸지 않습니다. Studio 기본 도구로 편집한 뒤 다시 검사하세요.
6. **Select report text — then Ctrl+C** 를 누르고 Ctrl+C로 복사하여 메모에 붙여넣습니다. 첫 헤더와 마지막 행까지 들어갔는지 확인하세요.
7. **Clear / Cancel** 은 현재 결과를 지우고 진행 중 검사의 취소를 요청합니다. 창 숨김이나 플러그인 해제도 이전 결과를 무효화합니다. 검사 중 장면이 바뀌면 입력을 확인하고 재검사하세요.

보고서는 검사 순간의 snapshot입니다. 이후 모듈 이동·ID 변경은 기존 측정값에 자동 반영되지 않습니다. 연결점이 삭제됐을 때도 다시 검사해야 합니다.

### 선택 예제: 연결 그룹 10개

[예제 place 다운로드](./D1-10Joint-Customer-Source0.rbxlx): `D1-10Joint-Customer-Source0.rbxlx`. 작성 객체는 Folder 11개·Model 18개·Part 19개·Attachment 19개, 총 67개이며 Script·ModuleScript·PackageLink는 없습니다. place에는 정상 Studio의 기본 서비스·Camera·Terrain도 포함될 수 있습니다.

예제는 플러그인과 별도로 다운로드합니다. 플러그인 구매·설치가 예제 place 자동 설치를 뜻하지 않습니다.

1. 기존 작업을 저장합니다. Studio **File → Open** (Ctrl+O)으로 `D1-10Joint-Customer-Source0.rbxlx` 를 별도 예제 place로 엽니다.
2. 편집 모드에서 Workspace 안의 `D1_10Joint_Compare` Folder를 확인합니다. 이 경로는 place를 열며 현재 프로젝트에 예제를 합치는 기능이 아닙니다.
3. 그 안의 `J01`–`J10` 폴더를 펼칩니다.
4. **J 폴더 안의 모듈 Model 18개** 를 함께 선택합니다. 루트 Folder·J 폴더·Part·Attachment를 선택하지 마세요.
5. `0.05` stud / `3` 도로 검사합니다.
6. 원본 예제는 **Model 18개·Attachment 19개·10행: PASS 2개·의도된 OPEN 1개·문제 7개** 로 설계했습니다. 위 영문 표의 J01–J10 예상 상태를 모두 대조하세요.
7. J02 행을 누르면 서로 다른 두 모듈의 Endpoint 객체가 선택되어야 합니다. J10까지 스크롤하고 전체 보고서를 복사하세요.
8. Clear 후 모듈 18개를 다시 선택해 검사합니다. 시험 place를 저장하고 Studio를 정상 종료·재열기한 뒤 허용오차를 설정하고 재검사하세요. 보고서가 재시작 후 남을 것이라고 기대하지 마세요.

**OPEN_ACCEPTED** 는 열린 끝을 허용했다는 뜻이며 완성된 연결이 아닙니다. 부동소수점 표시의 작은 차이를 실제 설계 안전성으로 해석하지 마세요.

### 원본 보존·Undo·한도

검사는 모듈 기하를 이동·크기 변경·색 변경하거나 Source·attributes를 수정하지 않습니다. 결과 행 선택은 현재 선택을 바꿉니다. 직접 편집한 내용은 Studio의 정상 Undo/Redo로 되돌리고 다시 검사하세요. 검사는 되돌릴 기하 수리 작업을 만들지 않습니다. 편집 전 place 백업을 유지하세요.

선택 Model 최대 **200개**, Attachment 최대 **200개**, 검사 instance 최대 **5,000개** 입니다. 중첩 Model 선택은 거부합니다. Attachment는 BasePart 직계 자식이어야 하므로 Bone이나 다른 부모 아래의 Attachment는 지원하지 않습니다. 두 끝의 선언이 모두 없으면 발견할 수 없습니다. 잘못 작성한 ID·축이 오해를 부르는 결과를 만들 수 있으므로 실제 설계 의도를 직접 확인하세요.

### 문제 해결·문의

- 연결점이 없다는 안내: Workspace의 Model을 선택했고 그 안에 Attachment가 있는지 확인합니다.
- 잘못된 입력: 모든 선택 Attachment의 직계 부모·attribute 이름과 자료형·ID 문자를 확인합니다.
- 누락·중복: 표시된 ID를 공유하는 끝들을 모두 확인합니다.
- 검사 중 변경·연결점 삭제: 현재 모듈을 다시 선택해 검사합니다.
- 빈 보고서·옛 보고서: 다시 검사합니다. 보고서는 place의 저장된 검사 이력이 아닙니다.
- 예제 열기·다운로드 문제: 정확한 `.rbxlx` 파일을 File → Open으로 열고 파일명과 Studio 버전을 함께 문의합니다. 플러그인 구매가 예제 파일 자동 배송을 뜻하지 않습니다.

[GitHub 지원](https://github.com/hkd0226/roblox-studio-tools-support)과 [Issues](https://github.com/hkd0226/roblox-studio-tools-support/issues)를 사용하세요. Issue 제출에는 GitHub 로그인이 필요합니다. 기본 이메일 [hkd0226@gmail.com](mailto:hkd0226@gmail.com), 보조 [hkd0226@hanmail.net](mailto:hkd0226@hanmail.net). 상품·버전, Studio 버전/OS, 재현 순서, 예상/실제 결과, 오류 문구를 적고 개인 프로젝트·인증정보·개인정보는 첨부하지 마세요. 응답 시간을 보장하지 않습니다.
