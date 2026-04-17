# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page, zero-dependency HTML study tool for USMLE Step 3 biostatistics. It is deployed via GitHub Pages at `step-3-biostats.robbiemed.org` (CNAME configured).

The entire app lives in `index.html` — there is no build step, no package manager, no framework.

## Development

Open `index.html` directly in a browser. No server required.

To preview with a local server (avoids any cross-origin quirks):
```bash
python3 -m http.server 8080
```

## Architecture

Everything is in a single `index.html`:

- **CSS** (lines 7–513): Custom properties via `:root` CSS variables (`--bg`, `--accent`, etc.). No external CSS framework.
- **HTML sections** (lines 537–1096): Six `<div class="section">` blocks (`s1`–`s6`), only one visible at a time via `.active` class toggling.
- **JavaScript** (lines 1100–1188): Three functions:
  - `show(id, btn)` — tab navigation, swaps `.active` on sections and nav buttons
  - `calculate()` — reads the four 2×2 inputs (`#ca`–`#cd`), computes all risk measures and diagnostic stats, writes results to DOM
  - `answer(qnum, chosen, correct)` — handles drill question scoring, disables buttons after answer, reveals explanation

## Content sections

| Nav label | Section ID | Topic |
|-----------|-----------|-------|
| 1. THE 2x2 | `s1` | 2×2 table explanation |
| 2. RISK MATH | `s2` | AR, RR, OR, ARR, RRR, NNT/NNH formulas |
| 3. CALCULATOR | `s3` | Live 2×2 calculator (risk + diagnostic stats) |
| 4. DX TESTS | `s4` | Sensitivity, specificity, PPV, NPV, LR+/− |
| 5. DRILL | `s5` | 6 board-format practice questions with scoring |
| 6. CHEATSHEET | `s6` | Condensed formula reference |

## Fonts

Loaded from Google Fonts: `JetBrains Mono` (monospace formulas/labels) and `Syne` (UI body text).

## Deployment

Push to `main` — GitHub Pages serves `index.html` automatically. The `CNAME` file maps the custom domain.
