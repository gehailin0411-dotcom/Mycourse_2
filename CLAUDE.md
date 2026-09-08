# Mycourse_2 — Agentic Workflows Mini-Course

## Stack & Conventions

- **Stack:** Plain HTML + CSS + vanilla JS only. No build step, no framework, no bundler, no package.json. Must run by opening the file directly / via GitHub Pages with zero setup.
- **HARD CONSTRAINT — single file:** The entire project — every lesson section and the navigation between them — must live in one `index.html` file. All CSS and JS inlined via `<style>` and `<script>` tags; no separate `.css`/`.js` files, no additional HTML pages. Linking external images and external CSS/JS libraries (e.g. via CDN `<link>`/`<script src="https://...">`) is allowed. This is so the finished project can be copy-pasted as a single file for sharing in class and on single-file code platforms. Sections are shown/hidden via JS (e.g. toggling visibility or a simple client-side router within the one page), not separate page loads.
- **Hosting:** GitHub Pages, serving the single `index.html` from the repo root.
- **Audience & tone:** Students with no prior AI/LLM background. Lesson prose must explain foundational concepts as they come up, not assume familiarity. Written like normal course lessons (explanatory paragraphs, examples), never a slide-by-slide bullet dump.
- **Content is one-time and hand-authored:** built once from 5 specific source slide images shared in-session. This is not a feature where visitors upload their own files — no upload UI, no dynamic content ingestion.
- **File structure:**
  ```
  /index.html   — everything: course title/TOC, all 5 lesson sections, inlined <style>, inlined <script> for nav
  ```
- **Naming:** each section identified by a stable id/anchor (e.g. `section-1` ... `section-5`, 1-indexed, matching slide order) used by both the TOC links and the nav JS. Keep section titles in sync between the TOC and each section's own heading.
- **Navigation (every section page must have both):**
  1. A persistent sidebar/TOC listing all 5 sections, current one highlighted.
  2. Previous/Next buttons at the bottom, linear through the 5 sections.
- **Design:** clean, readable default — good typography, light theme, minimal chrome, no client branding beyond the course title. No color/style requests on file; keep it simple unless told otherwise.
- **No extras:** no quizzes, no exercises, no code-example sections — just the written lesson per section, unless this changes later.
- **Testing approach:** no automated tests (static content site). Verify manually by opening `index.html` in a browser and checking in-page nav (TOC + Prev/Next) shows/hides the right section correctly before pushing.
- **Git:** develop on `claude/mini-course-from-slides-49evpl`; commit with descriptive messages; don't push until content/nav is verified.

## Feature Plan

### Phase 1 — Ingest slides
Receive the 5 slide images from the user (one at a time or all at once). For each, read the slide content and note the core concept(s) it covers, so section order and scope stay faithful to the original slide sequence.

### Phase 2 — Draft lesson sections
For each of the 5 slides, write one `<section>` block (in `index.html`) with full lesson prose derived from that slide's content — not a transcription, an actual explanation aimed at a beginner audience. All sections live in the same file, styled via the single inlined `<style>` block.

**Data model (conceptual):** each section is an in-page block with:
- `title` (heading, also used as its TOC label)
- `order` (N, 1–5, fixed by slide order)
- `content` (hand-written HTML prose body)

No database, no JSON data files, no separate pages — every section's markup lives directly in `index.html`, toggled via inline `<script>`.

### Phase 3 — Build navigation within the single page
- Course title + TOC near the top of `index.html`, listing all 5 sections in order (in-page links/buttons, not separate URLs).
- Inline `<script>` shows the active section and hides the rest, highlighting the current entry in the TOC.
- Prev/Next buttons on each section, wired linearly (section 1 → 2 → 3 → 4 → 5), disabled/hidden appropriately at the first and last section.
- One inlined `<style>` block applied consistently across TOC + all sections.

**Key flow:** user opens `index.html` → sees course title + TOC → clicks a section (or "Start") → JS shows that section's content and hides others → uses Prev/Next or TOC to switch sections → can jump back to the TOC at any time, all within the same page load.

### Phase 4 — Verify & deploy
- Manually click through every nav path (TOC links, Prev/Next chain, first/last section edge cases) in a browser, confirming only one section is visible at a time and no page reload occurs.
- Confirm GitHub Pages is enabled and serving `index.html` from the repo root.
- Commit and push the final single-file `index.html` to `claude/mini-course-from-slides-49evpl`.
