# CLAUDE.md — 쓰임장부 법적 문서 페이지

Claude Code가 이 저장소에서 작업할 때 참고하는 프로젝트 가이드.

## 프로젝트 개요

- **목적**: Google Play Console 등록용 외부 URL(개인정보처리방침·이용약관)을 제공하는 정적 HTML 사이트.
- **배포**: GitHub Pages, `main` 브랜치 루트에서 서빙.
  - 홈: https://loverjwc-eng.github.io/sseumjangbu/
  - 개인정보처리방침: https://loverjwc-eng.github.io/sseumjangbu/privacy.html
  - 이용약관: https://loverjwc-eng.github.io/sseumjangbu/terms.html
- **빌드 없음**: 번들러·패키지 매니저·테스트 러너 없음. 파일 수정 → 커밋 → 푸시가 전체 워크플로.

## 파일 구조

| 파일 | 역할 |
|---|---|
| `index.html` | 진입 페이지. 앱 소개 + 문서 링크 카드 |
| `privacy.html` | 개인정보처리방침 (9개 조항, `<h2>1. …</h2>` 형식) |
| `terms.html` | 이용약관 (12개 조항, `<h2>제N조 (…)</h2>` 형식) |
| `README.md` | 배포 절차 안내 |

## 코딩 규약

- **언어**: 문서 본문·주석·커밋 메시지 모두 한국어.
- **self-contained**: 각 HTML은 `<style>` 인라인. 외부 리소스는 Pretendard 폰트 CDN(jsdelivr) 하나만 허용. 새 JS·CSS 파일을 추가하지 않는다.
- **테마**: 색상은 `:root` CSS 변수(`--color-bg`, `--color-fg`, `--color-secondary`, `--color-tertiary`, `--color-border`, `--color-brand`, `--color-brand-subtle`)로만 정의. 다크모드는 `@media (prefers-color-scheme: dark)`에서 같은 변수를 재정의. 하드코딩 색상 금지.
- **반응형**: 모바일 우선. 좌우 여백 24px, 가로 스크롤 없어야 함.
- **메타 정보 동기화**: 문서 내용이 바뀌면 다음을 함께 갱신한다.
  - `.meta`의 `시행일자` 및 `버전`
  - `<footer>`의 `최종 수정일`
  - `index.html` 푸터의 버전 표기
- **조항 번호**: 조항을 추가·삭제하면 이후 번호를 모두 다시 맞춘다. 상호 참조(예: "제N조 참조")도 확인.

## 앱 코드와의 동기화 (중요)

같은 문서가 앱 저장소에도 존재한다.

- `frontend/src/pages/Privacy.jsx`
- `frontend/src/pages/Terms.jsx`

이 저장소의 `privacy.html` / `terms.html`을 수정하면 앱 쪽 JSX도 동일하게 바꿔야 한다. 이 저장소만 고쳤을 경우 작업 결과 보고에 "앱 쪽 미반영"을 명시한다.

## 검증 방법

자동 테스트는 없다. 변경 후 최소 확인:

1. 로컬에서 HTML 열기(`python3 -m http.server` 등)로 라이트/다크 모드 렌더링 확인.
2. 세 페이지 간 상대 링크(`./privacy.html`, `./terms.html`, `./index.html`) 깨짐 없는지 확인.
3. 모바일 폭(375px)에서 가로 스크롤이 생기지 않는지 확인.

## 하지 말 것

- `main`에 직접 푸시하지 않는다. 작업 브랜치에서 커밋 후 PR.
- 법적 문서의 실질 내용(수집 항목, 보유 기간, 제3자 제공, 관할 법원 등)을 임의로 바꾸지 않는다. 문구 다듬기·오타 수정은 가능하되, 조항의 의미가 바뀌는 변경은 사용자에게 먼저 확인.
- 연락처(`loverjwc@gmail.com`)·사업자 정보를 추측해서 채우지 않는다.
