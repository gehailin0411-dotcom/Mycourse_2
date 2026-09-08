# Mycourse_2 — Agentic Workflows Mini-Course

## Stack & Conventions

- **Stack:** Plain static site — HTML + CSS + vanilla JS only. No build step, no framework, no bundler, no package.json. Must run by opening files directly / via GitHub Pages with zero setup.
- **Hosting:** GitHub Pages, served from the repo root (or `/docs` — decide once we set up Pages, then keep it consistent).
- **Audience & tone:** Students with no prior AI/LLM background. Lesson prose must explain foundational concepts as they come up, not assume familiarity. Written like normal course lessons (explanatory paragraphs, examples), never a slide-by-slide bullet dump.
- **Content is one-time and hand-authored:** built once from 5 specific source slide images shared in-session. This is not a feature where visitors upload their own files — no upload UI, no dynamic content ingestion.
- **Folder structure:**
  ```
  /index.html          — landing page: course title + TOC linking to all 5 sections
  /sections/section-1.html ... section-5.html — one page per lesson section
  /styles.css          — shared stylesheet (single file, no preprocessor)
  /script.js           — shared JS (nav highlighting, prev/next wiring)
  /assets/             — any images/diagrams used in lesson content
  ```
- **Naming:** section files as `section-N.html` (1-indexed, matches slide order). Keep section titles in sync between `index.html`'s TOC and each section page's `<title>`/heading.
- **Navigation (every section page must have both):**
  1. A persistent sidebar/TOC listing all 5 sections, current one highlighted.
  2. Previous/Next buttons at the bottom, linear through the 5 sections.
- **Design:** clean, readable default — good typography, light theme, minimal chrome, no client branding beyond the course title. No color/style requests on file; keep it simple unless told otherwise.
- **No extras:** no quizzes, no exercises, no code-example sections — just the written lesson per section, unless this changes later.
- **Testing approach:** no automated tests (static content site). Verify manually by opening pages in a browser and checking nav links resolve and render correctly before pushing.
- **Git:** develop on `claude/mini-course-from-slides-49evpl`; commit with descriptive messages; don't push until content/nav is verified.

## Feature Plan

### Phase 1 — Ingest slides
Receive the 5 slide images from the user (one at a time or all at once). For each, read the slide content and note the core concept(s) it covers, so section order and scope stay faithful to the original slide sequence.

### Phase 2 — Draft lesson sections
For each of the 5 slides, write one `section-N.html` with full lesson prose derived from that slide's content — not a transcription, an actual explanation aimed at a beginner audience. Plain HTML structure, styled via shared `styles.css`.

**Data model (conceptual):** each section is a static page with:
- `title` (heading + `<title>`)
- `order` (N, 1–5, fixed by slide order)
- `content` (hand-written HTML prose body)

No database, no JSON data files — content lives directly in each HTML page.

### Phase 3 — Build navigation & landing page
- `index.html`: course title, short intro, TOC list linking to all 5 sections in order.
- Shared sidebar (or nav include via JS) on every section page listing all 5 sections, highlighting the current one.
- Prev/Next buttons on each section page, wired linearly (section 1 → 2 → 3 → 4 → 5), disabled/hidden appropriately at the first and last section.
- Shared `styles.css` applied consistently across landing + all sections.

**Key flow:** user lands on `index.html` → clicks a section (or "Start") → reads lesson → uses Prev/Next or sidebar to move between sections → can jump back to `index.html` via TOC/logo at any time.

### Phase 4 — Verify & deploy
- Manually click through every nav path (TOC links, Prev/Next chain, first/last section edge cases) in a browser.
- Confirm GitHub Pages is enabled and serving from the correct branch/folder.
- Commit and push final content to `claude/mini-course-from-slides-49evpl`.
