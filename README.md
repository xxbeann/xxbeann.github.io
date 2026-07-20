# 코드 심는 콩 — Hugo 블로그

티스토리(hELLO) → **Hugo + Stack** 마크다운 블로그. 벨로그식 시리즈 · 모노크롬 디자인 · 방문자수 · 날짜 자유.

> ⚠️ 이 스캐폴드는 hugo 미설치 환경에서 만들어졌습니다. 아래대로 로컬에서 처음 돌릴 때 에러가 나면 알려주세요 — 바로 잡아드립니다.

## 로컬에서 실행

```bash
# 1) Hugo extended 설치 (0.157.0+ 필요)
brew install hugo

# 2) 테마 서브모듈 받아오기 (이미 add됨. 클론만 새로 받는 경우)
git submodule update --init --recursive

# 3) 개발 서버 (초안 포함해서 보기 → -D)
hugo server -D
#   → http://localhost:1313
```

## 글 쓰기

```bash
hugo new post/내-글-슬러그/index.md
```

- 프론트매터 `date` 를 **아무 값이나** 직접 지정 → 원하는 순서/날짜로 발행
- 미래 날짜로 예약처럼 쓰려면 `hugo.toml` 의 `buildFuture = true` 주석 해제
- 완성되면 프론트매터 `draft: false`

### 벨로그식 시리즈

1. 프론트매터에 `series: ["시리즈명"]` 과 `series_order: 1` 추가
2. 본문 맨 위에 `{{</* series */>}}` 한 줄 → 시리즈 네비 박스가 자동 렌더
   (구현: `layouts/_partials/article/series.html` + `layouts/_shortcodes/series.html`)

## 커스터마이즈 포인트

| 무엇 | 어디 |
|------|------|
| 색·폰트 (hELLO 매칭) | `assets/scss/custom.scss` |
| 사이드바·위젯·메뉴·색상테마 | `hugo.toml` |
| 방문자수(GoatCounter) | `layouts/_partials/head/custom.html` |
| 아바타/파비콘 | `assets/img/avatar.png` (직접 넣기) |

## 배포 (GitHub Pages)

1. GitHub에 이 레포 push (`main` 브랜치)
2. 레포 **Settings → Pages → Source = GitHub Actions**
3. push 하면 `.github/workflows/deploy.yml` 이 자동 빌드·배포
4. 커스텀 도메인은 `hugo.toml` 의 `baseURL` 수정 + DNS 설정

## ⚠️ 배포 전 확인 2가지

1. **SUIT CDN 경로** (`custom.scss`) — 안 되면 주석의 Pretendard로 교체
2. **GoatCounter 코드** (`head/custom.html`) — goatcounter.com 가입 후 본인 코드로 교체
   (`xxbeann` → 실제 사이트 코드)

## 방문자수 세팅 (GoatCounter)

1. [goatcounter.com](https://www.goatcounter.com) 가입 → 사이트 코드 생성
2. `layouts/_partials/head/custom.html` 의 `xxbeann` 을 본인 코드로 교체
3. 배포하면 방문 집계 시작 (대시보드에서 확인)
