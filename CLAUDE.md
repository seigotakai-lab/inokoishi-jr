# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This is a small static website for 猪子石ジュニアバドミントンクラブ (Inokoishi Junior Badminton Club), used by coaches, rotation-duty parents (当番), and guardians. It is plain HTML with inline `<style>` — no build system, no JavaScript, no dependencies, no tests.

All user-facing text is in Japanese. Preserve the Japanese wording and tone when editing; do not translate content to English.

## Running / previewing

There is no build step. Open `index.html` directly in a browser, or serve the directory statically, e.g.:

```
python3 -m http.server 8000
```

Some pages (`leader/index.html`, `menu/beginner.html`) are laid out for A4 print via `@media print` and `@page { size: A4; margin: 10mm; }` — verify changes in the browser's print preview, not just on-screen.

## Site structure

`index.html` at the repo root is the hub. Each other page lives in its own top-level directory and is linked from the hub as a card:

- `menu/beginner.html` — beginner/初級 practice menu (19:00–20:15), including class definitions and promotion criteria (also duplicated on the class page).
- `footwork/index.html` — weekly A/B footwork rotation.
- `leader/index.html` — ordered list of practice-leader candidates and their roles. **Contains real children's names and school grades** — treat as personal data (see below).
- `class/index.html` — class tiers (初心者 / 初級者 / 中級者 / 上級者) and promotion criteria.
- `rules/index.html` — こころえ (code of conduct) read aloud at practice start.

Internal links are relative (`../index.html`, `menu/beginner.html`, etc.). When moving or renaming a page, update the hub cards in `index.html` and the breadcrumbs / footer back-links on the page.

## Page conventions

Each page is self-contained — CSS lives in a `<style>` block in `<head>`, there is no shared stylesheet. When adjusting visuals, copy the patterns already used on sibling pages rather than inventing new ones:

- `<meta name="robots" content="noindex, nofollow">` is present on every page and should stay (the site lists minors' names).
- Font stack: `"Meiryo", "MS Gothic", sans-serif`.
- Color palette used consistently across pages:
  - Primary dark blue `#1F4E79` (headers, footers, accent text)
  - Primary mid blue `#2E75B6` (nav, breadcrumbs, section headers)
  - Light blue background `#F0F4F8` / tint `#DEEAF1`
  - Accent orange `#ED7D31` / deep `#C55A11` (A-menu, promotion, end markers)
  - Accent green `#375623` / tint `#E2EFDA` (beginner / guide blocks)
  - Accent purple `#7030A0` (class tiers)
  - Notice yellow `#FFF2CC` with `#FFD700` left border (footnotes / 注意)
- Hub pages (with breadcrumbs) follow: `header` → `.breadcrumb` → `.container` → `.section`s → `footer` with a back-link to `../index.html`.
- Print-oriented pages (`leader`, `menu/beginner`) set `body { width: 190mm; margin: 10mm auto; }` and use `.title-sub` / `.title-main` banner blocks instead of the hub-style header.
- Class badges reuse the same class names across pages (`badge-s`/`badge-a`/`badge-b`/`badge-c` for 上級/初級/中級/初心者) — keep these in sync if the color coding changes.

## Content duplication to keep in sync

The class tier table and the 初心者 → 初級者 promotion criteria appear on **both** `class/index.html` and `menu/beginner.html`. When one is edited, update the other so they stay consistent.

Footers that self-identify as the club also appear on every page — update them together if the club name ever changes.

## Privacy

`leader/index.html` contains full names of minors and their school grade levels. The `noindex, nofollow` meta tag is the only protection in place. Do not add tracking, analytics, external fonts, or any third-party requests, and do not paste the contents of that page into external services (translation, diagramming, pastebins, etc.).

## Git workflow

The remote is `seigotakai-lab/inokoishi-jr`. The default branch is `main`; feature work happens on separate branches and is merged via PR. Existing history is mostly GitHub web-UI "Add files via upload" commits — when making real code changes, write a real commit message describing the intent (English or Japanese is fine).
