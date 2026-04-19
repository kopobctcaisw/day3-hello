# AI 코드어시스턴스 교육 프로그램 판매 랜딩페이지 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 40대 이상 비전공 성인을 대상으로 한 단일 정적 랜딩페이지를 구축해 카카오톡 무료 상담 전환을 유도한다.

**Architecture:** 기존 `index.html` 단일 파일 구조를 유지하고, 섹션 단위 마크업(히어로/성과/소개/가격/FAQ/CTA)과 내부 CSS, 최소 JS를 함께 배치한다. 모든 CTA는 동일한 카카오 오픈채팅 링크로 연결하고, CTA 위치 구분용 데이터 속성으로 클릭 이벤트 추적 기반을 만든다.

**Tech Stack:** HTML5, CSS3, Vanilla JavaScript

---

## 파일 구조 및 책임

- Modify: `index.html`
  - 책임: 단일 랜딩페이지의 전체 마크업, 스타일, CTA 링크, 최소 상호작용(부드러운 스크롤/클릭 추적 로그)
- Reference: `docs/superpowers/specs/2026-04-19-ai-code-assistance-education-sales-design.md`
  - 책임: 구현 기준 스펙

---

### Task 1: 기존 플레이스홀더 제거 및 페이지 골격 구성

**Files:**
- Modify: `index.html`
- Test: `index.html` (브라우저 수동 확인)

- [ ] **Step 1: 골격 검증용 실패 기준 정의**

```html
<!-- 현재 상태(실패 기준): hello world 1 텍스트만 존재 -->
hello world 1
```

검증 기준: 아래 요소가 없으면 실패로 간주
- `<header>` 히어로 섹션
- `<main>` 내부 섹션 구획
- 최소 5개 섹션 앵커 ID

- [ ] **Step 2: 골격 부재 확인**

Run: `python - <<'PY'\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\nchecks=['<header','<main','id="proof"','id="program"','id="pricing"','id="faq"','id="cta"']\nmissing=[c for c in checks if c not in html]\nprint('MISSING', missing)\nassert missing\nPY`
Expected: `MISSING [...]` 출력 및 assert 통과(즉, 현재는 골격이 없음)

- [ ] **Step 3: 최소 구현으로 페이지 골격 작성**

```html
<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>AI 코드어시스턴스 교육 | 40대 비전공 실무 전환</title>
  </head>
  <body>
    <header id="hero"></header>
    <main>
      <section id="proof"></section>
      <section id="program"></section>
      <section id="pricing"></section>
      <section id="faq"></section>
      <section id="cta"></section>
    </main>
  </body>
</html>
```

- [ ] **Step 4: 골격 검증 통과 확인**

Run: `python - <<'PY'\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\nchecks=['<header','<main','id="proof"','id="program"','id="pricing"','id="faq"','id="cta"']\nmissing=[c for c in checks if c not in html]\nprint('MISSING', missing)\nassert not missing\nPY`
Expected: `MISSING []`

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: scaffold single-page landing structure"
```

---

### Task 2: 히어로/성과/프로그램/가격/CTA 콘텐츠 구현

**Files:**
- Modify: `index.html`
- Test: `index.html` (브라우저 수동 확인)

- [ ] **Step 1: 콘텐츠 존재 실패 기준 정의**

```text
필수 문구:
- 비전공 40대도 AI 코딩으로 실무 전환 가능
- 카톡으로 무료 상담 받기
- 수강생 성과 사례
- 수강 방식 · 기간 · 비용
```

- [ ] **Step 2: 현재 문구 누락 확인**

Run: `python - <<'PY'\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\nphrases=['비전공 40대도 AI 코딩으로 실무 전환 가능','카톡으로 무료 상담 받기','수강생 성과 사례','수강 방식 · 기간 · 비용']\nmissing=[p for p in phrases if p not in html]\nprint('MISSING', missing)\nassert missing\nPY`
Expected: 하나 이상 누락

- [ ] **Step 3: 스펙 기준 콘텐츠 삽입**

```html
<header id="hero">
  <h1>비전공 40대도 AI 코딩으로 실무 전환 가능</h1>
  <p>나이와 전공 제약 없이, 실무 중심 프로젝트로 빠르게 전환하세요.</p>
  <a class="cta-button" data-cta-position="hero" href="https://open.kakao.com/o/REPLACE_ME" target="_blank" rel="noopener noreferrer">카톡으로 무료 상담 받기</a>
</header>

<section id="proof" aria-labelledby="proof-title">
  <h2 id="proof-title">수강생 성과 사례</h2>
  <article>
    <h3>업무 자동화 도입</h3>
    <p>6주 학습 후 반복 보고서 작성 시간을 주당 6시간 절감.</p>
  </article>
  <article>
    <h3>실무 산출물 완성</h3>
    <p>8주 내 사내 도구 프로토타입 1건 배포.</p>
  </article>
</section>

<section id="program" aria-labelledby="program-title">
  <h2 id="program-title">프로그램 소개</h2>
  <p>AI 코드어시스턴스를 활용해 기획-구현-검증 흐름을 실무형으로 익힙니다.</p>
</section>

<section id="pricing" aria-labelledby="pricing-title">
  <h2 id="pricing-title">수강 방식 · 기간 · 비용</h2>
  <ul>
    <li>방식: 온라인 라이브 + 과제 피드백</li>
    <li>기간: 8주</li>
    <li>비용: 990,000원 (부가세 포함)</li>
  </ul>
</section>

<section id="cta" aria-labelledby="cta-title">
  <h2 id="cta-title">지금 시작해보세요</h2>
  <a class="cta-button" data-cta-position="bottom" href="https://open.kakao.com/o/REPLACE_ME" target="_blank" rel="noopener noreferrer">카톡으로 무료 상담 받기</a>
</section>
```

- [ ] **Step 4: 필수 문구 검증 통과 확인**

Run: `python - <<'PY'\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\nphrases=['비전공 40대도 AI 코딩으로 실무 전환 가능','카톡으로 무료 상담 받기','수강생 성과 사례','수강 방식 · 기간 · 비용']\nmissing=[p for p in phrases if p not in html]\nprint('MISSING', missing)\nassert not missing\nPY`
Expected: `MISSING []`

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add conversion-focused landing content sections"
```

---

### Task 3: 가독성 중심 스타일 및 반응형 구현

**Files:**
- Modify: `index.html`
- Test: `index.html` (브라우저 수동 확인)

- [ ] **Step 1: 스타일 실패 기준 정의**

```text
필수 스타일 기준:
- 기본 본문 폰트 크기 18px 이상
- CTA 버튼 터치 영역 높이 44px 이상
- 모바일 우선 컨테이너 여백
```

- [ ] **Step 2: 스타일 기준 미충족 확인**

Run: `python - <<'PY'\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\nchecks=['font-size: 18px','min-height: 44px','padding: 0 1rem']\nmissing=[c for c in checks if c not in html]\nprint('MISSING', missing)\nassert missing\nPY`
Expected: 하나 이상 누락

- [ ] **Step 3: 접근성/가독성 중심 CSS 추가**

```html
<style>
  :root {
    --bg: #f7f8fb;
    --surface: #ffffff;
    --text: #111827;
    --muted: #4b5563;
    --primary: #0f766e;
    --primary-dark: #115e59;
    --max-width: 960px;
  }

  * { box-sizing: border-box; }

  body {
    margin: 0;
    font-family: "Pretendard", "Noto Sans KR", system-ui, -apple-system, sans-serif;
    font-size: 18px;
    line-height: 1.6;
    color: var(--text);
    background: var(--bg);
  }

  .container {
    width: min(100%, var(--max-width));
    margin: 0 auto;
    padding: 0 1rem;
  }

  section, header {
    padding: 3rem 0;
  }

  h1 { font-size: clamp(2rem, 5vw, 3rem); line-height: 1.25; margin: 0 0 1rem; }
  h2 { font-size: clamp(1.5rem, 4vw, 2rem); margin: 0 0 1rem; }

  .cta-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-height: 44px;
    padding: 0.75rem 1.25rem;
    border-radius: 0.75rem;
    background: var(--primary);
    color: #fff;
    text-decoration: none;
    font-weight: 700;
  }

  .cta-button:hover { background: var(--primary-dark); }

  .card-grid {
    display: grid;
    gap: 1rem;
  }

  .card {
    background: var(--surface);
    border-radius: 0.75rem;
    padding: 1.25rem;
    box-shadow: 0 6px 20px rgba(15, 23, 42, 0.08);
  }

  @media (min-width: 768px) {
    .card-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  }
</style>
```

- [ ] **Step 4: 스타일 기준 검증 통과 확인**

Run: `python - <<'PY'\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\nchecks=['font-size: 18px','min-height: 44px','padding: 0 1rem']\nmissing=[c for c in checks if c not in html]\nprint('MISSING', missing)\nassert not missing\nPY`
Expected: `MISSING []`

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add readable responsive styles for adult learners"
```

---

### Task 4: 중간 CTA/FAQ 및 링크 일관성 검증 추가

**Files:**
- Modify: `index.html`
- Test: `index.html` (정적 검증 + 브라우저 수동 확인)

- [ ] **Step 1: CTA 일관성 실패 기준 정의**

```text
검증 기준:
- data-cta-position 값이 hero/mid/bottom 3개 존재
- 모든 .cta-button href 값 동일
- FAQ 섹션 존재
```

- [ ] **Step 2: 현재 기준 미달 확인**

Run: `python - <<'PY'\nimport re\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\npositions=re.findall(r'data-cta-position="([^"]+)"', html)\nhrefs=re.findall(r'class="cta-button"[^>]*href="([^"]+)"', html)\nprint('POSITIONS', positions)\nprint('UNIQUE_HREFS', sorted(set(hrefs)))\nassert set(positions)!={'hero','mid','bottom'} or len(set(hrefs))!=1 or 'id="faq"' not in html\nPY`
Expected: assert 통과(현재 미달)

- [ ] **Step 3: 중간 CTA 및 FAQ 추가, 링크 동일화**

```html
<section id="program" aria-labelledby="program-title">
  <div class="container">
    <h2 id="program-title">프로그램 소개</h2>
    <p>AI 코드어시스턴스를 활용해 기획-구현-검증 흐름을 실무형으로 익힙니다.</p>
    <a class="cta-button" data-cta-position="mid" href="https://open.kakao.com/o/REPLACE_ME" target="_blank" rel="noopener noreferrer">카톡으로 무료 상담 받기</a>
  </div>
</section>

<section id="faq" aria-labelledby="faq-title">
  <div class="container">
    <h2 id="faq-title">자주 묻는 질문</h2>
    <details>
      <summary>비전공자도 수강 가능한가요?</summary>
      <p>가능합니다. 기초부터 실습 중심으로 진행합니다.</p>
    </details>
    <details>
      <summary>직장인도 병행 가능한가요?</summary>
      <p>주중/주말 학습 시간을 분산할 수 있는 구조로 운영합니다.</p>
    </details>
  </div>
</section>
```

- [ ] **Step 4: CTA/FAQ 검증 통과 확인**

Run: `python - <<'PY'\nimport re\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\npositions=set(re.findall(r'data-cta-position="([^"]+)"', html))\nhrefs=re.findall(r'class="cta-button"[^>]*href="([^"]+)"', html)\nprint('POSITIONS', sorted(positions))\nprint('UNIQUE_HREFS', sorted(set(hrefs)))\nassert positions=={'hero','mid','bottom'}\nassert len(set(hrefs))==1\nassert 'id="faq"' in html\nPY`
Expected:
- `POSITIONS ['bottom', 'hero', 'mid']`
- `UNIQUE_HREFS ['https://open.kakao.com/o/REPLACE_ME']`

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add mid-cta faq and enforce single kakao consultation link"
```

---

### Task 5: 최소 상호작용 및 최종 검증

**Files:**
- Modify: `index.html`
- Test: `index.html` (브라우저 수동 확인)

- [ ] **Step 1: 상호작용 실패 기준 정의**

```text
검증 기준:
- html 요소에 smooth scroll 설정
- CTA 클릭 로그 스크립트 존재
- 콘솔 에러 없이 페이지 로드
```

- [ ] **Step 2: 상호작용 기준 미충족 확인**

Run: `python - <<'PY'\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\nchecks=['scroll-behavior: smooth','querySelectorAll(\'.cta-button\')','console.log(\'[CTA_CLICK]\'']\nmissing=[c for c in checks if c not in html]\nprint('MISSING', missing)\nassert missing\nPY`
Expected: 하나 이상 누락

- [ ] **Step 3: 최소 JS 상호작용 추가**

```html
<style>
  html { scroll-behavior: smooth; }
</style>

<script>
  document.querySelectorAll('.cta-button').forEach((button) => {
    button.addEventListener('click', () => {
      const position = button.dataset.ctaPosition || 'unknown';
      console.log('[CTA_CLICK]', position);
    });
  });
</script>
```

- [ ] **Step 4: 검증 및 수동 테스트 실행**

Run: `python - <<'PY'\nfrom pathlib import Path\nhtml=Path('index.html').read_text(encoding='utf-8')\nchecks=['scroll-behavior: smooth','querySelectorAll(\'.cta-button\')','console.log(\'[CTA_CLICK]\'']\nmissing=[c for c in checks if c not in html]\nprint('MISSING', missing)\nassert not missing\nPY`
Expected: `MISSING []`

Run: `python -m http.server 4173`
Expected: `Serving HTTP on ... 4173`

수동 확인 체크리스트:
- `http://localhost:4173` 접속
- 모바일 뷰(360px)에서 텍스트 가독성 확인
- hero/mid/bottom CTA 클릭 시 모두 동일 링크로 이동하는지 확인
- 콘솔에 `[CTA_CLICK] hero|mid|bottom` 로그 출력 확인

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: finalize landing interactions and verification-ready setup"
```

---

## 스펙 커버리지 점검

- 핵심 메시지/타깃 반영: Task 2
- 성과 증명형 정보 구조: Task 2
- 단일 페이지/정적 기술 스택: Task 1, Task 3
- 가격 즉시 공개: Task 2
- CTA 반복 노출 및 카카오 링크 통일: Task 4
- 가독성/접근성(큰 글자, 터치영역): Task 3
- 최소 상호작용: Task 5
- 테스트 범위(레이아웃/링크/기본 품질): Task 5

누락 없음.

## Placeholder/일관성 점검

- TBD/TODO/추후 구현 문구 없음
- 함수/선택자/속성명 일관성 확인: `.cta-button`, `data-cta-position`
- 링크 값 일관성: `https://open.kakao.com/o/REPLACE_ME`로 통일

