# PRR Role Audit v0.1.0 — customer guide

English / 한국어

Use the [Roblox product page](https://create.roblox.com/store/asset/135277121017733/PRR-Role-Audit) to check the current price, availability and installed version. This guide describes the scoped audit; it does not promise correct physics or automatic repairs.

## English

### What it checks

PRR Role Audit compares four current Part properties with role rules you explicitly write: **Anchored, CanCollide, CanTouch, CanQuery**, in that order. Use it to review mixed static props, intended triggers, details and moving objects without guessing their purpose.

A PASS means these four stored properties match your declared rule. It does not establish correct physical behavior, collisions, touch events, queries, assemblies, avatars, performance, or game logic. You remain responsible for choosing the right expectations.

### Installation and example

Follow the current Roblox product listing's installation instructions and open **Role Audit** from Studio's Plugins toolbar. Confirm the installed panel displays v0.1.0.

The separate, script-free example is [PRR-12Case-Customer-Source0.rbxl](./PRR-12Case-Customer-Source0.rbxl). Download that file separately, save your current project, then use **File → Open / Ctrl+O** to open that exact file. Select the `PRRRoleAudit_12Case_PRIVATE` Model in Workspace and scan with the four default rules below. The Model name is retained from the tested example. This opens a separate place; it does not merge it into your project. The plugin must be installed separately and does not install the example automatically.

### 1. Define the role rules

The initial rules are examples of an author's chosen intentions, not recommended settings for every game:

```text
Solid=true,true,false,true
Trigger=true,false,true,true
Detail=true,false,false,false
Moving=false,true,true,true
```

| Role | Anchored | CanCollide | CanTouch | CanQuery |
| --- | --- | --- | --- | --- |
| Solid | true | true | false | true |
| Trigger | true | false | true | true |
| Detail | true | false | false | false |
| Moving | false | true | true | true |

Write one rule per line as `Role=true,false,false,true`. A role name is 1–32 ASCII characters, starts with a letter, and then uses letters, digits or underscores: `[A-Za-z][A-Za-z0-9_]*`. Names and tags are case-sensitive. Use exactly four lowercase `true` / `false` values. Spaces around names and values are accepted. Blank lines and lines beginning with `#` are ignored.

You can define up to **16 roles** and **4,000 characters** of rule text. Use the rule input area's vertical and horizontal scrollbars to reach longer text. Unicode can be used in comments; role names remain ASCII. A duplicate role, invalid name/value, missing field or empty rule set is rejected; the plugin does not silently invent a rule.

### 2. Tag the actual Parts

Use Studio's Properties tags to put a tag such as `PRR_Solid` directly on each Part you want to check. Each Part should have one intended `PRR_<Role>` tag.

Tagging a Model does not tag its children or supply their role. Tags without the `PRR_` prefix do not define a role for this audit. The plugin does not add or change tags.

### 3. Select and scan

In Edit mode, select Models or BaseParts **inside Workspace**, then click **Scan selected**. Folder roots and a root outside Workspace are not accepted. A selected Model includes its descendant BaseParts. Repeated or overlapping selections are deduplicated so an actual Part is checked once.

The scope is at most **200 BaseParts** and **5,000 distinct selected-scope objects**, including selected roots. Reduce the selection if it exceeds a limit or contains no BaseParts.

The scan reads the four raw properties and tags. It does not change Parts, materials, transforms, scripts, tags or geometry.

### 4. Read the result

| Status | Meaning | Next step |
| --- | --- | --- |
| PASS | All four properties match the one declared role. | Confirm that your rule expresses the intended design. |
| FLAG_MISMATCH | At least one expected flag differs from the actual flag. | Read the expected/actual field values; inspect the Part. |
| MISSING_ROLE | The Part has no direct `PRR_` tag. | Add a role yourself if this Part belongs in the audit. |
| MULTIPLE_ROLES | The Part has more than one `PRR_` tag. Unknown tags also count. | Resolve the role declaration; no priority is chosen automatically. |
| UNKNOWN_ROLE | Its single `PRR_` tag has no matching rule. | Correct the tag or add the intended rule. |

Click a result row to select its **actual Part**. Duplicate names can produce repeated paths in a text report; UI rows retain their individual object reference. If an object was moved, renamed or removed, scan again rather than relying on its old row.

### 5. Copy and keep the complete report

Scroll to **Complete report**, click inside it, then press **Ctrl+A / Ctrl+C**. The complete report includes the declared rules and every result row with expected and actual values.

Results are snapshots. Part/tag edits are not live synchronization: scan again after a change. Editing the rule text or using **Clear results** clears the previous result.

Custom rules are not automatically saved as plugin presets in this version. Keep a copy of the report or your rule text separately, then paste the rules back when you reopen the plugin. Save the place normally to retain your own Part tags and properties.

### 6. Fix deliberately and rescan

The audit has no auto-repair button. Decide whether the rule or the Part should change, make that edit normally in Studio, and scan again. Use Studio Undo/Redo for your own edits and save a place backup before bulk changes. Clearing results only clears plugin results; it is not an Undo operation and it does not change the scene.

### Example result and limits

With the unchanged 12-Part example and the four default rules, the expected result is 5 matching Parts, 5 flag mismatches, 1 missing role and 1 multiple-role Part. An unknown role and invalid rule text are separate cases; the example's counts do not cover every possible input.

The audit cannot infer whether an invisible Part is unnecessary or whether an unanchored Part is wrong. Intentional markers, triggers and moving props may be valid. It does not inspect collision-group matrices, weld behavior, contact events, raycast behavior, traversal, checkpoint rules or avatar access. Its values describe the scan moment.

### Free Studio alternative

Studio Explorer's tag/property filters, grouped AND/OR queries and Ctrl+A selection can find the same declared-tag and raw-flag cases without buying a plugin. PRR Role Audit packages the editable rules, all statuses, expected/actual report and individual Part-row selection into one GUI workflow. No measured speed or accuracy advantage is promised.

### Troubleshooting and support

- No results: select a Model or BasePart in Workspace, check the scope limits, and return to Edit mode.
- Wrong role: check exact case, the `PRR_` prefix, and that the tag is on the Part itself.
- Old result: rescan after a Part/tag change; rule edits clear the old report.
- Invalid rules: check the line number, four lowercase bool values, name syntax and duplicate role names.
- Cannot see the last row: scroll the results and complete-report areas; resize the plugin window if needed.
- Wrong expected values: correct your declared rule. PASS certifies agreement with that rule only.

Support: [hkd0226@gmail.com](mailto:hkd0226@gmail.com), backup [hkd0226@hanmail.net](mailto:hkd0226@hanmail.net). Existing support repository: https://github.com/hkd0226/roblox-studio-tools-support

Include the product/version, Studio and OS version, selected object types, the rule text, steps, expected/actual result and any Output error. Do not send credentials, private project files or unrelated personal data. Confirm current price and availability on the actual Roblox product listing.

## 한국어

현재 가격·판매 여부와 설치 버전은 [Roblox 상품페이지](https://create.roblox.com/store/asset/135277121017733/PRR-Role-Audit)에서 확인하세요. 선언한 규칙의 제한된 검사 안내이며, 물리 안전이나 자동 수정을 약속하지 않습니다.

### 검사하는 내용

PRR Role Audit는 제작자가 직접 정한 역할 규칙과 Part의 현재 네 속성 **Anchored, CanCollide, CanTouch, CanQuery** 를 같은 순서로 비교합니다. 정적 소품·트리거·장식·움직이는 물체가 섞인 장면을 제작 의도에 맞춰 확인하는 도구입니다.

PASS는 네 속성이 선언한 규칙과 일치한다는 뜻입니다. 실제 물리·충돌·접촉 이벤트·쿼리·조립체·아바타·성능·게임 로직이 올바르다는 판정은 아닙니다. 적절한 기대값은 제작자가 정해야 합니다.

### 설치와 예제

실제 Roblox 상품페이지의 설치 안내를 따르고 Studio Plugins 도구 모음의 **Role Audit** 를 여세요. 설치된 패널에 v0.1.0이 표시되는지 확인하세요.

별도 스크립트 없는 예제는 [PRR-12Case-Customer-Source0.rbxl](./PRR-12Case-Customer-Source0.rbxl) 입니다. 파일을 따로 다운로드하고 현재 작업을 저장한 뒤 **File → Open / Ctrl+O** 로 해당 파일을 여세요. Workspace의 `PRRRoleAudit_12Case_PRIVATE` Model을 선택하고 아래 기본 규칙 네 개로 검사하세요. Model 이름은 실제 검수 예제와 동일하게 유지했습니다. 다른 place가 열리며 현재 프로젝트에 예제를 합치지 않습니다. 플러그인은 별도로 설치해야 하고 예제를 자동 설치하지 않습니다.

### 1. 역할 규칙 입력

위 영문 규칙과 표의 Solid·Trigger·Detail·Moving은 특정 제작 의도의 예시입니다. 모든 게임에 권장하는 설정이 아닙니다.

한 줄에 `Role=true,false,false,true`를 입력합니다. 값 순서는 Anchored → CanCollide → CanTouch → CanQuery입니다. 역할 이름은 1–32자의 ASCII 문자이고, 영문자로 시작한 뒤 영문자·숫자·밑줄만 사용합니다. 역할과 태그의 대소문자는 구분됩니다. 값은 소문자 `true` 또는 `false` 네 개입니다. 이름과 값 주변 공백은 허용하며 빈 줄과 `#`로 시작하는 줄은 무시합니다.

최대 **16개 역할 / 4,000자** 입니다. 긴 입력은 규칙 입력 영역의 세로·가로 스크롤바로 확인하세요. 주석에는 유니코드 문자를 쓸 수 있지만 역할 이름은 ASCII 형식을 지켜야 합니다. 역할 중복·잘못된 이름이나 값·누락 값·빈 규칙은 오류로 안내합니다. 도구가 임의의 역할이나 기대값을 정하지 않습니다.

### 2. 실제 Part에 태그 지정

Studio Properties의 태그에서 각 Part에 `PRR_Solid`처럼 직접 `PRR_<Role>` 태그를 붙이세요. 검사할 Part마다 의도한 역할 하나를 지정합니다.

Model에 붙인 태그는 자식 Part에 상속되지 않습니다. `PRR_` 접두사가 없는 태그는 이 검사에서 역할로 사용하지 않습니다. 도구가 태그를 추가하거나 변경하지 않습니다.

### 3. 선택 후 검사

Edit 모드에서 **Workspace 안의 Model 또는 BasePart** 를 선택하고 **Scan selected** 를 누르세요. Folder를 선택 루트로 쓰거나 Workspace 밖의 루트를 선택하면 거부됩니다. Model을 선택하면 그 아래 BasePart를 확인하며, 중복·중첩 선택에 포함된 같은 Part는 한 번만 검사합니다.

최대 **200 BasePart / 5,000개의 서로 다른 선택 범위 객체** 이며 선택한 루트도 객체 수에 포함됩니다. 한도를 넘거나 BasePart가 없으면 선택 범위를 줄이거나 바꾸세요.

도구는 네 속성과 태그를 읽습니다. Part·재질·위치·스크립트·태그·기하를 변경하지 않습니다.

### 4. 결과 확인

- **PASS**: 선언한 역할의 네 기대값과 실제값이 모두 일치합니다.
- **FLAG_MISMATCH**: 적어도 한 속성이 다릅니다. 표시된 기대값과 실제값을 보고 Part를 확인하세요.
- **MISSING_ROLE**: Part 자체에 `PRR_` 태그가 없습니다.
- **MULTIPLE_ROLES**: `PRR_` 태그가 둘 이상입니다. 미등록 역할도 중복으로 셉니다. 임의의 우선순위는 적용하지 않습니다.
- **UNKNOWN_ROLE**: 역할 태그 하나는 있지만 그 이름의 규칙이 없습니다.

결과행을 누르면 그 행의 **실제 Part** 가 선택됩니다. 같은 이름의 객체는 보고서 경로가 같을 수 있지만 UI 행은 각각의 객체 참조를 보관합니다. 객체를 이동·이름 변경·삭제했다면 이전 행에 의존하지 말고 다시 검사하세요.

### 5. 전체 보고서 복사와 규칙 보관

**Complete report** 영역으로 내려가 안을 누른 뒤 **Ctrl+A / Ctrl+C** 로 복사하세요. 선언한 규칙과 모든 결과행의 기대값·실제값이 포함됩니다.

결과는 검사 시점의 스냅샷입니다. Part나 태그를 바꾼 뒤 다시 검사하세요. 규칙 입력을 수정하거나 **Clear results** 를 누르면 이전 결과가 지워집니다.

이 버전은 사용자 규칙을 플러그인 프리셋으로 자동 저장하지 않습니다. 규칙이나 전체 보고서를 따로 복사해 보관하고 플러그인을 다시 열 때 입력하세요. 직접 지정한 태그와 Part 속성은 place를 정상 저장해 보관하세요.

### 6. 의도에 맞춰 수정 후 재검사

자동 수정 기능은 없습니다. 규칙과 Part 중 무엇을 고쳐야 하는지 결정해 Studio에서 직접 수정한 뒤 다시 검사하세요. 직접 한 수정에는 Studio Undo/Redo를 사용하고 대량 변경 전에는 place 백업을 저장하세요. 결과 지우기는 장면 수정이나 Undo 작업이 아닙니다.

### 예제 결과와 한계

변경하지 않은 12-Part 예제에 기본 규칙 네 개를 적용한 기대 결과는 일치 5개·속성 불일치 5개·역할 누락 1개·복수 역할 1개입니다. 미등록 역할과 잘못된 규칙은 별도 사례이며, 이 예제 수량이 모든 입력을 검증하는 것은 아닙니다.

보이지 않는 Part가 불필요한지, Anchored가 꺼진 Part가 잘못됐는지 도구가 추론하지 않습니다. 의도한 데이터 마커·트리거·움직이는 소품은 정상일 수 있습니다. 충돌 그룹 행렬·용접 동작·접촉 이벤트·Raycast 결과·통행·체크포인트·아바타 접근을 검사하지 않습니다.

### 무료 기본 도구로 확인

Studio Explorer의 태그·속성 필터, AND/OR 조합과 Ctrl+A 선택으로 같은 역할 태그·raw 속성 사례를 플러그인 구매 없이 찾을 수 있습니다. PRR Role Audit는 편집 가능한 규칙·전체 상태·기대/실제 보고서·개별 Part 행 선택을 하나의 GUI 동선으로 제공합니다. 실측된 속도나 정확도 우위는 약속하지 않습니다.

### 문제 해결과 지원

결과가 없으면 Workspace의 Model/BasePart 선택, 수량 한도와 Edit 모드를 확인하세요. 역할이 이상하면 대소문자·`PRR_` 접두사·Part 자체의 태그를 확인하세요. 오래된 결과는 다시 검사하고, 규칙 오류는 줄 번호·네 bool 값·이름 형식·역할 중복을 확인하세요. 끝 행이 보이지 않으면 결과/보고서 영역을 스크롤하고 창 크기를 조정하세요. 기대값 자체가 틀렸다면 규칙을 수정하세요.

지원: [hkd0226@gmail.com](mailto:hkd0226@gmail.com), 보조 [hkd0226@hanmail.net](mailto:hkd0226@hanmail.net). 기존 지원 저장소: https://github.com/hkd0226/roblox-studio-tools-support

문의에 상품/버전·Studio/OS 버전·선택 객체 유형·규칙·재현 순서·기대/실제 결과·Output 오류를 적어주세요. 인증정보·비공개 프로젝트 원본·불필요한 개인정보는 보내지 마세요. 현재 가격과 판매 여부는 실제 Roblox 상품페이지에서 확인하세요.
