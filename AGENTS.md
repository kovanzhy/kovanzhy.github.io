# AGENTS.md

This file provides guidance to Codex and other coding agents when working with this repository.

## Project Overview

Static portfolio website for Yurii Kovanzhy (`kovanzhy.github.io`), built as a single-page site using vanilla HTML, CSS, and JavaScript. Hosted on GitHub Pages.

## Versioning

Previous versions are archived in `/_versions/` and kept in git. The directory is hidden from GitHub Pages because Jekyll excludes `_`-prefixed directories by default.

| Version | Path | Notes |
|---|---|---|
| v1 | `_versions/v1/index.html` | Original gradient/glassmorphism design |
| v2 | `_versions/v2/index.html` | Brittany Chiang sidebar layout (discarded) |
| v3 | `index.html` | Current — top-nav, original design |

## Architecture

Everything lives in `index.html`: embedded CSS and embedded JavaScript. This is intentional: zero build dependencies, zero npm.

External dependencies are CDN-only:
- Google Fonts: Inter (300-700) and JetBrains Mono (400-500)

Layout:
- Fixed top nav (`#nav`) with `YK` logo, numbered section links, and `Contact me` mailto CTA
- Full-width hero section with typewriter effect on subtitle
- Scrollable content sections inside `.content`, max-width 1100px
- No sidebar; single-column page structure

Sections, in order:
1. `#about` — two-column text grid and stats bar
2. `#experience` — `.exp-card` list with left-border hover accent
3. `#skills` — grouped tag lists by category
4. `#education` — `.edu-card` list
5. `#contact` — intro text, contact card links, and footer

## Design System

Color palette is defined with CSS variables:

```css
--navy:         #09172b;
--navy-mid:     #0f2342;
--navy-card:    #111f38;
--green:        #64ffda;
--green-dim:    rgba(100, 255, 218, 0.08);
--green-border: rgba(100, 255, 218, 0.18);
--slate:        #8892b0;
--slate-light:  #a8b2d8;
--slate-lighter:#ccd6f6;
--white:        #e6f1ff;
```

Typography:
- `--sans`: Inter — body, headings, cards
- `--mono`: JetBrains Mono — nav links, dates, tags, labels, code-style elements

Background:
- Subtle dot grid via `radial-gradient` on `body`, using a 32px grid

Responsive breakpoints:
- `<= 900px`: about grid collapses to one column
- `<= 768px`: nav padding reduced, experience and education cards become single-column
- `<= 520px`: nav links hidden, hero buttons stack vertically, contact cards stack

## JavaScript Features

- Scroll progress bar (`#progress`) — thin green line at top of viewport
- Nav shadow — added after scrolling past 20px
- Typewriter effect — cycles through four phrases on the hero subtitle
- Smooth scroll — all `a[href^="#"]` links
- Reveal on scroll — `IntersectionObserver` adds `.visible` to `.reveal` elements
- Experience cards — click anywhere on a card to open LinkedIn, except nested anchor clicks
- Education cards — click to open `https://usv.ro/`

## Key Links

- LinkedIn: `https://www.linkedin.com/in/yurii-kovanzhy/`
- Contact email: `kovanzhy.yurii@gmail.com`
- University: `https://usv.ro/`
- Company links in experience cards currently point to LinkedIn as placeholders; update per-card `.exp-at a` `href` values when real URLs are available.

## Common Tasks

Update an experience company URL:
1. Find the relevant `.exp-at a` in `#experience`.
2. Replace `href="https://www.linkedin.com/in/yurii-kovanzhy/"` with the company URL.

Add a new experience entry:
1. Copy a `.exp-card` block inside `.exp-list`.
2. Update role, company, period, description, and tags.
3. The JavaScript click handler applies automatically to all `.exp-card` elements.

Add a new section:
1. Add `<section class="section reveal" id="newid">` inside `.content`.
2. Add a matching `<li><a href="#newid">` item to `.nav-links`.
3. The existing `IntersectionObserver` will pick up `.reveal` automatically.

Local development:

```bash
python -m http.server 8000
```

or:

```bash
npx serve .
```

Deployment:
- Push to `main`; GitHub Pages serves `index.html` automatically.

## Constraints

- Maintain the single-file architecture unless explicitly asked to split files.
- Do not add npm, bundlers, package manifests, or a build process unless explicitly requested.
- Preserve mobile responsiveness for all changes.
- Keep the dark-only theme; do not add a light mode unless explicitly requested.
- Favicon is an inline SVG data URI in `<head>` with navy background and green `YK` monospace text.
- Keep changes scoped to the requested task. Do not rewrite archived versions unless asked.
