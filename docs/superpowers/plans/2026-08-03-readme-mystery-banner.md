# README Mystery Banner Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the temporary vector README banner with a polished, spoiler-light cinematic banner built from real game art, and remove story-ending spoilers from the README.

**Architecture:** Produce one optimized raster banner at `docs/99knights-banner.png` using the existing title-screen artwork as the visual base. Keep the README as the only consumer of the banner and rewrite its marketing copy to reveal the premise without disclosing the household connection, protocol explanation, or ending.

**Tech Stack:** PNG image composition, GitHub Markdown, GitHub Pages static repository.

## Global Constraints

- Banner text: `99KNIGHTS`, `ROYAL EXPRESS DELIVERY`, `THREE ORDERS. ONE IMPOSSIBLE ROUTE.`
- Chinese tagline: `三个订单，一条不该存在的路线。`
- Do not show or name the family, dinner ending, household connection, or the three food items.
- Retain a clear browser-play link near the top of the README.
- Use actual game art rather than simple vector illustration.

---

### Task 1: Produce cinematic mystery banner

**Files:**
- Create: `docs/99knights-banner.png`
- Reference: local title-screen capture `v091_title_bilingual.png`

**Interfaces:**
- Produces: a 1600×700 PNG referenced by README Markdown.

- [ ] Compose the title-screen art into a wide 1600×700 crop.
- [ ] Cover old UI and spoiler copy with cinematic gradients and framing.
- [ ] Add the approved English and Chinese mystery taglines.
- [ ] Verify image dimensions, PNG readability, and absence of family/food imagery.
- [ ] Upload the resulting binary asset to the repository.

### Task 2: Rewrite README for spoiler-light presentation

**Files:**
- Modify: `README.md`

**Interfaces:**
- Consumes: `docs/99knights-banner.png`
- Produces: a README that links to the live build without revealing the narrative twist or ending.

- [ ] Change the image reference from SVG to PNG.
- [ ] Replace the family/kingdom-ending tagline with the approved mystery tagline.
- [ ] Rewrite About and Story sections to reveal only the Royal Express Protocol emergency premise.
- [ ] Remove explicit family-ending language from Highlights and Current Release.
- [ ] Preserve controls, technical notes, and feedback instructions.

### Task 3: Verify repository presentation

**Files:**
- Verify: `README.md`
- Verify: `docs/99knights-banner.png`

**Interfaces:**
- Consumes: completed banner and README.
- Produces: confirmed main-branch presentation with no broken asset reference.

- [ ] Fetch both files from the updated branch.
- [ ] Confirm README references the exact PNG path.
- [ ] Confirm the live-play URL remains `https://bigonewd.github.io/99Knights/`.
- [ ] Confirm prohibited spoilers no longer appear in the README.
