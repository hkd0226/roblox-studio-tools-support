# Door & Passage Check 0.1.0 — Customer guide / 사용 안내

Release status: preparation and verification are in progress. This guide is not a Roblox sale or upload receipt. The plugin installation file is not distributed by this documentation repository. Confirm availability, version and price on the Roblox product listing when it is published.

현재 상품 검수·게시 준비 중입니다. 이 문서는 Roblox 업로드·판매 완료 증빙이 아닙니다. 이 저장소에서는 플러그인 설치 파일을 배포하지 않습니다. 게시된 Roblox 상품 페이지에서 판매 여부·버전·가격을 확인하세요.

## English

### Install and open

For a supplied local review package, inspect `DoorPassageClearanceCheck-0.1.0.rbxmx` in Roblox Studio and use **Plugins → Save as Local Plugin**. Open a separate test place, stop Play, then choose **Plugins → Door & Passage Check → OpenDoorPassageCheck**. For a Store installation, use the installation offered by its Roblox listing. Back up your project before testing.

### Door swing

1. Select one door Model and position its Model pivot at the hinge.
2. Enter an angle from **−170 to −1** or **1 to 170 degrees**; zero is invalid.
3. Choose **Preview scan parameters**, then **Scan selected door swing**.
4. Click a result row to select and focus the candidate in Studio.

The sweep samples intervals no greater than 15 degrees and excludes the selected door from candidates. A BasePart uses its own center and orientation as the pivot; prefer a correctly positioned Model pivot for a hinge.

### Passage

Select one Part or Model as the passage center and orientation. Enter three positive values in **width, depth, height** order, for example **8, 10, 6** studs. Choose **Check selected passage marker**. The selected marker is excluded from candidate results.

### Limits and troubleshooting

The tool checks bounding-box overlap candidates. It does not move, rename or delete map geometry, and the numeric parameter preview creates no scene objects. Results are not exact mesh collisions or a guarantee of avatar walkability. Mesh bounds, collision settings, CanQuery and decorative objects can cause unexpected candidates or misses. Inspect the reported objects and test actual character movement yourself. Rerun after changing the scene; previous results describe the earlier input.

If the plugin button is missing, confirm that the plugin is installed and enabled in Studio. For an invalid angle or size, correct the input and scan again. For an unexpected result, check the selected object, pivot, dimensions and relevant collision settings.

## 한국어

### 설치·열기

로컬 검수 파일을 받은 경우 Studio에서 `DoorPassageClearanceCheck-0.1.0.rbxmx`의 코드를 확인하고 **Plugins → Save as Local Plugin**으로 설치합니다. 별도 테스트 place를 열고 Play를 중지한 뒤 **Plugins → Door & Passage Check → OpenDoorPassageCheck**를 선택합니다. Store 상품은 해당 Roblox 페이지의 설치 기능을 사용하세요. 테스트 전에 작업을 백업하세요.

### 문 회전 검사

1. 문 Model 하나를 선택하고 Model pivot을 경첩 위치에 맞춥니다.
2. **−170~−1도 또는 1~170도**를 입력합니다. 0도는 지원하지 않습니다.
3. **Preview scan parameters → Scan selected door swing**을 실행합니다.
4. 결과 행을 눌러 Studio에서 후보 객체를 선택·확인합니다.

최대 15도 간격으로 검사하며 선택한 문은 후보에서 제외합니다. BasePart는 자신의 중심·방향을 pivot으로 사용하므로 실제 경첩에는 pivot을 맞춘 Model을 권장합니다.

### 통로 검사

통로의 중심·방향을 나타내는 Part 또는 Model 하나를 선택합니다. **너비, 깊이, 높이** 순서로 양수 3개를 입력하고, 예를 들어 **8, 10, 6** studs로 설정합니다. **Check selected passage marker**를 누릅니다. 선택한 표식 자체는 후보에서 제외됩니다.

### 결과 해석·오류 확인

이 도구는 경계 상자의 겹침 후보를 찾습니다. 원본 형상을 이동·이름 변경·삭제하지 않으며 숫자 미리보기는 장면 객체를 생성하지 않습니다. 정밀 mesh 충돌이나 모든 아바타의 통과 가능성을 보장하지 않습니다. Mesh 경계, 충돌 설정, CanQuery, 장식물에 따라 예상과 다른 후보나 누락이 생길 수 있습니다. 실제 객체와 캐릭터 이동을 직접 확인하고, 장면을 바꿨으면 재검사하세요.

버튼이 없으면 플러그인의 설치·활성화를 확인하세요. 각도·크기 오류는 입력을 고친 후 다시 검사합니다. 결과가 예상과 다르면 선택 객체, pivot, 크기와 충돌 설정을 확인하세요.

## Tested customer example / 검수 예제

[Download or view DPC-Customer-Source0-0.1.0.rbxl](./DPC-Customer-Source0-0.1.0.rbxl). Save a copy and open it with **File → Open** in Studio after saving your current project. This place is separate from the plugin and contains no Script, LocalScript or ModuleScript instances. It does not install the plugin automatically.

SHA-256: `65f5f82ec2ccad0a46887fa54bd02a6b18b5d0cfd17930beb9539625570bdbbf`.

The exact file was reopened and checked after a full Studio restart on **2026-10-12 KST**. Select **Workspace.Part**. At **90 degrees**, the preview showed **7 samples** for bounds **4 × 1 × 2**, and the swing scan reported **Workspace.SpawnLocation** near 90 degrees. Passage input **8, 10, 6** returned **Baseplate** and **SpawnLocation** as overlap candidates. This centered-Part example demonstrates bounds queries; it is not a real hinged-door or avatar movement certification.

[고객 예제 받기](./DPC-Customer-Source0-0.1.0.rbxl). 현재 작업을 저장한 뒤 예제 사본을 내려받고 Studio의 **File → Open**으로 엽니다. 이 place는 플러그인과 별도이며 Script·LocalScript·ModuleScript 객체를 포함하지 않습니다. 플러그인이 자동 설치되지는 않습니다.

**2026-10-12 KST**에 위 해시와 같은 파일을 Studio 전체 재시작 후 열어 확인했습니다. **Workspace.Part**를 선택하고 **90도**를 입력하면 크기 **4 × 1 × 2**에 대해 미리보기 **7개 표본**, 회전 검사 후보 **SpawnLocation**이 관찰됐습니다. 통로 입력 **8, 10, 6**은 **Baseplate·SpawnLocation** 후보를 반환했습니다. 중심 pivot의 Part로 경계 쿼리를 보여 주는 예제이며 실제 경첩이나 아바타 통과 검증은 아닙니다.

## Support / 문의

Email: **hkd0226@gmail.com** (backup: **hkd0226@hanmail.net**). Public bug reports: [repository Issues](https://github.com/hkd0226/roblox-studio-tools-support/issues). Include the product/version, Studio version, reproduction steps, expected and actual results, and exact error text. Do not include passwords, tokens or private project files. No fixed response time is promised.

문의에는 제품·버전, Studio 버전, 재현 순서, 예상·실제 결과와 정확한 오류 문구를 적어 주세요. 비밀번호·인증 토큰·비공개 프로젝트는 보내지 마세요. 정해진 응답 시간은 약속하지 않습니다.
