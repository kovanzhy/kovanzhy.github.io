# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static portfolio website for Yurii Kovanzhy (kovanzhy.github.io), built as a single-page application using vanilla HTML, CSS, and JavaScript. Hosted on GitHub Pages.

## Versioning

Previous versions are archived in `/_versions/` — stored in git but hidden from GitHub Pages (Jekyll excludes `_`-prefixed directories automatically). Not publicly accessible.

| Version | Path | Notes |
|---|---|---|
| v1 | `_versions/v1/index.html` | Original gradient/glassmorphism design |
| v2 | `_versions/v2/index.html` | Brittany Chiang sidebar layout (discarded) |
| v3 | `index.html` | Current — top-nav, original design |

## Architecture

**Single-File Structure**: Everything lives in `index.html` — embedded CSS and JavaScript. Intentional: zero build dependencies, zero npm.

**External dependencies** (CDN only):
- Google Fonts: Inter (300–700) + JetBrains Mono (400–500)

**Layout**:
- Fixed top nav (`#nav`) with `YK` logo, numbered section links, `Contact me` CTA (mailto)
- Full-width hero section with typewriter effect on subtitle
- Scrollable content sections (`.content` wrapper, max-width 1100px)
- No sidebar — single column layout

**Sections** (in order):
1. `#about` — two-column text grid + stats bar
2. `#experience` — `.exp-card` list with left-border hover accent
3. `#skills` — grouped tag lists by category
4. `#education` — `.edu-card` list
5. `#contact` — intro text + contact card links + footer

## Design System

**Color palette (CSS variables)**:
```
--navy:         #09172b   (page background)
--navy-mid:     #0f2342
--navy-card:    #111f38   (card backgrounds)
--green:        #64ffda   (primary accent)
--green-dim:    rgba(100, 255, 218, 0.08)
--green-border: rgba(100, 255, 218, 0.18)
--slate:        #8892b0   (body text)
--slate-light:  #a8b2d8
--slate-lighter:#ccd6f6   (emphasis text)
--white:        #e6f1ff   (headings)
```

**Typography**:
- `--sans`: Inter — body, headings, cards
- `--mono`: JetBrains Mono — nav links, dates, tags, labels, code-style elements

**Background**: Dot grid via `radial-gradient` on `body` (very subtle green dots, 32px grid)

**Responsive breakpoints**:
- `≤ 900px`: About grid collapses to single column
- `≤ 768px`: Nav padding reduced, exp/edu cards go single column
- `≤ 520px`: Nav links hidden, hero buttons stack vertically, contact cards stack

## JavaScript Features

- **Scroll progress bar** (`#progress`) — thin green line at top of viewport
- **Nav shadow** — added on scroll past 20px
- **Typewriter effect** — cycles through 4 phrases on hero subtitle with blinking cursor
- **Smooth scroll** — all `a[href^="#"]` links
- **Reveal on scroll** — IntersectionObserver adds `.visible` to `.reveal` elements
- **Experience cards** — click anywhere → opens LinkedIn in new tab (skips nested `<a>` clicks)
- **Education cards** — click → opens `https://usv.ro/` in new tab

## Key Links

- LinkedIn: `https://www.linkedin.com/in/yurii-kovanzhy/`
- Contact email: `kovanzhy.yurii@gmail.com`
- University: `https://usv.ro/`
- Company links (experience cards): currently all point to LinkedIn as placeholder — update per-card `.exp-at a` href when real URLs are available

## Common Tasks

**Update experience company URL** (when real URLs are ready):
- Find the relevant `.exp-at a` in `#experience`
- Replace `href="https://www.linkedin.com/in/yurii-kovanzhy/"` with the company URL

**Add a new experience entry**:
- Copy a `.exp-card` block inside `.exp-list`
- Update role, company, period, description, tags
- The JS click handler on `.exp-card` applies automatically to all cards

**Add a new section**:
1. Add `<section class="section reveal" id="newid">` inside `.content`
2. Add `<li><a href="#newid">` to `.nav-links`
3. IntersectionObserver picks up `.reveal` automatically

**Local development**:
```bash
python -m http.server 8000
# or
npx serve .
```

**Deployment**: Push to `main` branch — GitHub Pages serves `index.html` automatically.

## Constraints

- Maintain single-file architecture unless explicitly required to split
- Zero npm / no build process
- Preserve mobile responsiveness for all changes
- Dark-only theme — no light mode toggle
- Favicon: inline SVG data URI in `<head>` (navy background, green "YK" monospace)
