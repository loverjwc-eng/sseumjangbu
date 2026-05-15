# 쓰임장부 법적 문서 페이지

Play Console 등록용 외부 URL을 위한 정적 HTML 페이지 모음.

## 파일

- `index.html` — 진입 페이지 (홈)
- `privacy.html` — 개인정보처리방침
- `terms.html` — 이용약관

모두 self-contained (외부 CSS는 Pretendard 폰트 CDN만). 다크모드 자동 대응. 모바일 반응형.

## GitHub Pages로 배포

### 1단계: 별도 Public 저장소 생성

GitHub Pages는 무료 계정에선 **Public 저장소만** 무료. 새 저장소를 만듭니다.

```bash
# GitHub 웹에서 새 저장소 만들기:
#   https://github.com/new
#   - 이름: sseumjangbu
#   - Public 선택
#   - README 추가 X (이 폴더에 이미 있음)
```

### 2단계: 이 폴더를 새 저장소로 push

```bash
cd /Users/wonjeong/jichul2/legal-pages
git init -b main
git add .
git commit -m "쓰임장부 법적 문서 (개인정보·이용약관)"
git remote add origin git@github.com:loverjwc-eng/sseumjangbu.git
git push -u origin main
```

(만약 HTTPS 인증 쓰시면 `https://github.com/loverjwc-eng/sseumjangbu.git`)

### 3단계: GitHub Pages 활성화

1. https://github.com/loverjwc-eng/sseumjangbu/settings/pages 접속
2. **Source**: "Deploy from a branch"
3. **Branch**: `main` / `/ (root)` 선택
4. **Save** 클릭
5. 1~2분 대기 → 페이지 활성화

### 4단계: URL 확인

활성화되면 다음 URL이 작동:

```
https://loverjwc-eng.github.io/sseumjangbu/                  (홈)
https://loverjwc-eng.github.io/sseumjangbu/privacy.html      (개인정보처리방침)
https://loverjwc-eng.github.io/sseumjangbu/terms.html        (이용약관)
```

브라우저에서 위 URL 열어서 정상 작동 확인.

## Play Console에 사용

Play Console에서 요구하는 URL:

- **개인정보처리방침 URL**: `https://loverjwc-eng.github.io/sseumjangbu/privacy.html`
- **이용약관 URL**: 동일 도메인의 terms.html

## 향후 업데이트

문서 내용을 수정해야 할 때:

1. 이 폴더의 HTML 파일 직접 수정
2. `git add . && git commit -m "..."`
3. `git push`
4. 1~2분 후 GitHub Pages가 자동 재배포

## 앱 내 페이지와 동기화

같은 내용이 앱 내에도 있음 (참고용):
- `frontend/src/pages/Privacy.jsx`
- `frontend/src/pages/Terms.jsx`

내용 변경 시 둘 다 같이 수정 필요. (1.1에서 단일 source-of-truth 통합 검토 권장.)
