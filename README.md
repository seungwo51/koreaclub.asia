# KOREACLUB · koreaclub.asia

> 강남·홍대·압구정·청담 클럽 게스트 입장 & 테이블 예약 다국어 포털
> Multilingual nightlife portal for Seoul clubs — Gangnam · Hongdae · Apgujeong · Cheongdam

🔗 **Live:** https://koreaclub.asia

---

## 소개

정적(static) 단일 페이지 기반의 다국어 클럽 안내·예약 문의 포털입니다.
지역별 내부 전경, 가격대, 이용 안내를 한 화면에서 제공하고 카카오톡·문자로 문의를 받습니다.

## 지원 언어 (hreflang)

| 언어 | 경로 |
|---|---|
| 한국어 (기본) | `/` |
| English | `/en` |
| 日本語 | `/jp` |
| 中文 | `/ch` |

## 기술 스택

- **프론트엔드:** HTML + CSS + JavaScript (단일 파일 인라인 구조)
- **폰트:** Google Fonts (Outfit)
- **미디어:** WebP 이미지 · MP4 영상(desktop/mobile 분리) · MP3 BGM
- **호스팅:** GitHub Pages
- **도메인/DNS:** 커스텀 도메인 `koreaclub.asia` (CNAME) + Cloudflare
- **SEO:** `sitemap.xml` · `robots.txt` · `rss.xml` · hreflang · Open Graph / Twitter Card

## 폴더 구조

```
.
├── index.html          # 한국어 (메인)
├── en/index.html       # English
├── jp/index.html       # 日本語
├── ch/index.html       # 中文
├── assets/             # ⚠️ 현재 'asstes'(오타) — 'assets'로 변경 필요
│   ├── hero/           # 지역별 히어로 이미지 (webp)
│   ├── video/
│   │   ├── desktop/    # 데스크톱 배경 영상 (mp4)
│   │   └── mobile/     # 모바일 배경 영상 (mp4)
│   ├── gangnam/        # interior/ (내부 전경) · price/ (가격표)
│   ├── hongdae/
│   ├── apgujeong/
│   ├── cheongdam/
│   ├── flags/          # 언어 국기 아이콘 (webp)
│   └── audio/bgm.mp3   # 배경 음악
├── favicon.ico
├── CNAME               # koreaclub.asia
├── robots.txt
├── sitemap.xml
└── rss.xml
```

> ⚠️ **알려진 이슈 (배포 시 미디어 전부 안 보임):**
> 에셋 폴더명이 `asstes`(오타)인데 HTML은 전부 `/assets/...`(루트 절대경로)로 참조합니다.
> 그 결과 모든 이미지·동영상·국기·BGM이 **404**가 됩니다.
> **해결:** 폴더명을 `asstes` → `assets`로 변경 (`git mv asstes assets` 후 push). 한 번이면 root·en·jp·ch 전부 정상화됩니다.

## 로컬 실행

```bash
# 정적 사이트라 별도 빌드 없이 로컬 서버만 띄우면 됨
python3 -m http.server 8000
# http://localhost:8000 접속
```

## 배포 (GitHub Pages)

1. `main` 브랜치에 push
2. **Settings → Pages → Source:** `main` / `root`
3. 커스텀 도메인: `CNAME` 파일(`koreaclub.asia`) + Cloudflare DNS (GitHub Pages 대상 레코드)
4. push 시 자동 재배포

---

## 🔍 검색엔진 노출 체크리스트 (Baidu · Google · Yahoo! Japan · Naver)

> **중요 — 먼저 알아둘 것:** 이 `README.md`는 **GitHub 저장소 페이지에만** 표시되며,
> 웹사이트(koreaclub.asia)의 검색 순위에는 영향을 주지 않습니다.
> 실제 검색 노출은 다음 두 가지로 이뤄집니다 →
> ① HTML에 이미 들어있는 on-page SEO (meta · OG · hreflang · sitemap)
> ② 아래 각 검색엔진 **웹마스터 도구에 직접 등록 + 사이트맵 제출**

### 이미 적용된 on-page SEO

- `<title>` · `<meta name="description">` · `<link rel="canonical">`
- Open Graph / Twitter Card *(주의: `og:image`가 `/assets/...` 경로 → 폴더명 수정 후에 정상 동작)*
- hreflang (ko · zh · ja · en · x-default)
- `sitemap.xml` · `robots.txt`(Yeti·Daumoa·Baiduspider·Googlebot·Bingbot·Slurp 허용) · `rss.xml`

### 검색엔진별 등록 — 여기서 실제 노출이 시작됨

| 시장 | 검색엔진 | 등록 도구 | 비고 |
|---|---|---|---|
| 미국/글로벌 | **Google** | Google Search Console — `search.google.com/search-console` | sitemap.xml 제출 |
| **일본** | **Yahoo! JAPAN** | (별도 도구 없음) | 2010년부터 **Google 검색 기반** → Search Console 등록으로 함께 커버 |
| 일본/글로벌 | **Bing** (+ 글로벌 Yahoo) | Bing Webmaster Tools — `bing.com/webmasters` | 글로벌 Yahoo 검색은 Bing 기반 |
| **중국** | **Baidu** | Baidu 搜索资源平台 — `ziyuan.baidu.com` | 해외 호스팅은 색인 제한적 ↓ 아래 주의 |
| **한국** | **Naver** | Naver 서치어드바이저 — `searchadvisor.naver.com` | robots.txt에 Yeti 이미 허용 |
| 한국 | **Daum (Kakao)** | 'Daum 검색 등록'으로 검색해 신청 | |

**공통 절차:** 각 도구에서 → ① 사이트 소유 확인(HTML 메타태그 삽입 또는 인증 파일 업로드) → ② `https://koreaclub.asia/sitemap.xml` 제출 → ③ 색인(크롤링) 요청.

> ⚠️ **Baidu 주의 (사실 그대로):** 바이두는 중국 외 호스팅(GitHub Pages·Cloudflare) 사이트의 색인이 느리거나 제한적일 수 있습니다.
> 중국 시장 노출이 핵심이라면 **중국 내 호스팅 + ICP 비안(备案) 취득**이 색인·속도에 유리합니다.
> 현재 구성(GitHub Pages)만으로는 바이두 완전 색인을 보장할 수 없습니다.

### 노출을 더 끌어올리려면 (선택)

- **JSON-LD 구조화 데이터** 추가: `schema.org/LocalBusiness` 또는 `NightClub` 타입 (영업시간·지역·연락처) → 리치 결과 노출에 유리 *(현재 HTML에는 미적용)*
- 지역 키워드를 각 언어 페이지의 `<title>`·`<h1>`·`description`에 자연스럽게 반영
- 외부 백링크(블로그·SNS·지도 등록) 확보

---

*Static site · GitHub Pages + Cloudflare · © KOREACLUB*
