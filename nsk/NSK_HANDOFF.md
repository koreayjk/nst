# 노바스마트코리아(NSK) 웹사이트 — 작업 인수인계 문서

> 새 세션에서 이 문서를 먼저 읽으면 지금까지의 맥락을 그대로 이어서 작업할 수 있습니다.

---

## 1. 프로젝트 개요

- **목표**: 기존 **노바스타테크(NST / novastartech.kr)** 홈페이지를 복제해, **노바스마트코리아(NovaSmartKorea / NSK)** 사이트를 별도로 제작.
- **원칙**: 레이아웃·콘텐츠는 NST와 동일, **회사명·브랜드 컬러·로고·연락처만 NSK로 교체**.
- **형태**: 단일 정적 페이지 (`index.html`) + 이미지 에셋. 한국어/영어 토글 지원(`lang` ko/en, `data-i18n` 방식).
- **작업 저장 위치(현재)**: `koreayjk/nst` 저장소, 브랜치 **`claude/quirky-gauss-hg3fus`**, **`nsk/` 폴더**.
  - ⚠️ 아직 **독립 저장소 `koreayjk/nsk`는 미생성** (세션 권한 스코프로 생성 불가 → 아래 6번 참고).

---

## 2. 파일 구조 (`nsk/`)

```
nsk/
├─ index.html                    # 사이트 본문 (약 1.4MB, 이미지·폰트 base64 임베드)
├─ README.md                     # 배포 안내
├─ NSK_HANDOFF.md                # (이 문서)
└─ assets/
   ├─ nsk-logomark.png           # 공식 로고마크 (빨강 NOVA 사각형)
   ├─ nsk-logo-lockup.png        # 공식 전체 로고 락업 (마크 + 워드마크 + 태그라인)
   ├─ process-comparison.png     # 공정 비교 도식 (브랜드명 없음, 범용)
   └─ product-film-spec.png      # 제품 사양 도식 (브랜드명 없음, 범용)
```

> 헤더/푸터 로고는 `index.html` 안에 **base64로 임베드**되어 있음(별도 파일 참조 아님). `assets/`의 로고 PNG는 원본 보관용.

---

## 3. 브랜드 아이덴티티 (최종: 공식 네이비 + 빨강)

원본 로고 파일 `NSK_LOGOMARK.ai`(빨강 NOVA 로고마크 + 네이비 "NOVA SMART KOREA" + "Smart Flooring Creators")에서 추출.

| 용도 | 값 | CSS 변수 |
|---|---|---|
| 배경 | `#ffffff` (흰색) | `--bg` |
| 섹션 보조 배경 | `#f4f6f9` | `--bg-2` |
| 카드/패널 | `#ffffff` | `--panel` |
| 경계선 | `#e4e8ee` | `--line` |
| 본문·제목 (네이비) | `#1d2b53` | `--ink` |
| 보조 텍스트 | `#55607a` | `--ink-soft` |
| 흐린 텍스트 | `#8a93a6` | `--ink-faint` |
| **강조/포인트 (빨강)** | `#dd1727` | `--accent`, `--accent-warm` |
| 보조 강조 (네이비) | `#1d2b53` | `--accent-2` |

- **역할 분담**: 네이비 = 본문/제목/버튼/구조, 빨강 = 아이라벨(eyebrow)·하이라이트 키워드(`.gl`)·아이콘·`KOREA` 워드마크·링크 hover·selection.
- **버튼(`.btn-primary`)**: 네이비 배경 + 흰 글자 (`background:var(--ink);color:#fff`).
- **워드마크(HTML)**: `NOVA SMART <span class="tech">KOREA</span>` — "NOVA SMART"는 네이비(`--ink`), `.tech`(KOREA)는 빨강 `#dd1727`.
- **SPC/LVT 단면 카드**: 필름 밴드가 네이비(`#1d2b53`) + 흰 글자.

> 참고: 초기에 **그린 테마 → 흰색 배경 → 공식 네이비+빨강** 순으로 진화함(2번 히스토리). 지금은 공식 네이비+빨강이 최종.

---

## 4. 회사/연락처 정보 (명함 기준, 국·영문 모두 반영됨)

| 항목 | 내용 |
|---|---|
| 회사명 | 노바스마트코리아 / **Nova Smart Korea Ltd., Co.** (약칭 NSK) |
| 대표이사 | **백병교 (Beak, Byoung Gyo)** |
| 이메일 | **bbk2000@hanmail.net** |
| 전화(T) | **+82-42-716-7117** (042-716-7117) |
| 모바일(M) | +82-10-2464-0357 (010-2464-0357) |
| 팩스(F) | +82-42-538-2204 (042-538-2204) |
| 본사(KO) | 대전광역시 유성구 테크노1로 75 한밭대학교 대덕산학융합캠퍼스 308호 (우편번호 34014) |
| 본사(EN) | 308, 75 Techno 1-ro, Yuseong-gu, Daejeon 34014, Republic of Korea |
| 태그라인 | Smart Flooring Creators |

- 샘플요청/문의 `mailto:` 링크도 모두 `bbk2000@hanmail.net`으로 교체됨.
- **운영 거점** 문구("한국(본사·연구·생산) · 미국·중국·베트남(공급)")는 명함에 없어 **기존 유지** — 필요 시 실제 정보로 교체.

---

## 5. 편집 시 반드시 주의할 점 ⚠️

- **`index.html`에는 이미지·폰트가 base64로 임베드**되어 있음. base64 문자열 안에 우연히 `NST`, `NSK`, `#hex` 유사 문자열이 포함될 수 있음.
- 따라서 **단순 전역 치환 금지**. 반드시 **공백/괄호/태그 경계를 포함한 타깃 치환**을 사용 (예: `'NST '`, `'(NST)'`, `'vs. NST'`, `fill="#..."`, `background:var(--accent)` 등).
- 브랜드 텍스트는 대소문자 변형 존재: `노바스타테크/노바스마트코리아`, `NovaStarTech/NovaSmartKorea`, `NOVASTAR/NOVASMART`, `TECH/KOREA`, `NST/NSK`.
- 연락처 이메일 도메인에 `novastartech.kr`가 남아있지 않은지 확인(모두 `bbk2000@hanmail.net`으로 교체 완료).

---

## 6. 배포 방법 (독립 저장소 + GitHub Pages)

현재 세션 권한이 `koreayjk/nst`로 제한되어 **새 저장소를 자동 생성하지 못함**. 아래 수동 절차 필요:

1. GitHub에서 **New repository → 이름 `nsk` (Public)** 생성.
2. `nsk/` 폴더 내용 전체(`index.html`, `assets/`, `README.md`)를 새 저장소 루트에 업로드/커밋.
3. **Settings → Pages → Branch: `main` / `/(root)`** → `https://koreayjk.github.io/nsk` 로 공개.
4. (선택) 커스텀 도메인: `CNAME` 파일 추가 + DNS 설정.
   - ⚠️ `novastartech.kr`은 NST가 사용 중이라 재사용 불가. 새 도메인(예: `novasmartkorea.kr`) 필요.

> 또는 현재 브랜치 `claude/quirky-gauss-hg3fus`의 `nsk/` 폴더를 그대로 새 저장소로 복사해도 됨.

---

## 7. 로컬 미리보기(스크린샷) 방법

Playwright + 사전 설치된 Chromium 사용:

```js
// shot.cjs  (node shot.cjs 로 실행)
const { chromium } = require('/opt/node22/lib/node_modules/playwright');
(async () => {
  const b = await chromium.launch({ executablePath: '/opt/pw-browsers/chromium' });
  const p = await b.newPage({ viewport: { width: 1280, height: 900 } });
  await p.goto('file:///<경로>/nsk/index.html', { waitUntil: 'networkidle' });
  await p.screenshot({ path: 'out.png' });
  // KO 토글:  await p.click('#langToggle button');
  // 섹션:     (await p.$('.showcase')).screenshot({path:'sec.png'});
  await b.close();
})();
```

주요 섹션 셀렉터: `.hero` / `#why` / `.band` / `#tested` / `#specs` / `.showcase` / `.band-img` / `.gal3` / `.apps-grid`(SPC·LVT) / `.cta`(연락처) / `footer`.

---

## 8. 사진 위 텍스트 가독성 처리(중요 디자인 규칙)

- 사진 위 텍스트는 **전체 이미지에 흰 스크림을 크게 깔지 않음** (사진이 죽어 보임).
- 대신 **글자 주변에만 흰색 헤일로(text-shadow)** 적용 → 사진은 선명, 글자만 또렷.
  - 적용 셀렉터: `.showcase`(제목/문단), `.band-img .bi-cap`(중앙 캡션), `.gal3 .g .cap`(하단 캡션).
  - `<style>` 끝부분에 `text-shadow` 규칙 블록으로 존재. 이미지 `::after` 스크림은 매우 옅게만 유지.

---

## 9. 커밋 히스토리 (브랜치 `claude/quirky-gauss-hg3fus`)

```
b02a12c 공식 네이비+빨강 브랜드 + 실제 로고 + 명함 연락처 반영
e179990 사진 위 텍스트: 전체 스크림 대신 글자 주변 헤일로
1ac9b07 흰색 테마에서 사진 위 텍스트 가독성 수정
ffb7e7e 배경 흰색 테마로 전환
c9253a8 NSK 사이트 최초 추가 (NST 복제 + 리브랜딩, 당시 그린 테마)
```

---

## 10. 남은 작업 / 다음 세션 후보

- [ ] **독립 저장소 `koreayjk/nsk` 생성 + GitHub Pages 배포** (6번).
- [ ] (선택) 커스텀 도메인 연결 (예: `novasmartkorea.kr`) + `CNAME`.
- [ ] (선택) 헤더/푸터에 태그라인 "Smart Flooring Creators" 노출.
- [ ] (선택) 운영 거점 문구를 실제 정보로 갱신.
- [ ] (선택) 메타 태그(og:image 등)에 공식 로고 반영, favicon 교체.

---

*최종 업데이트 기준 커밋: `b02a12c` · 브랜치 `claude/quirky-gauss-hg3fus` · 저장소 `koreayjk/nst`*
