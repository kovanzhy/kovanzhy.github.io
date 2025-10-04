# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static portfolio website for Yurii Kovanzhy (kovanzhy.github.io), built as a single-page application using vanilla HTML, CSS, and JavaScript. The site is hosted on GitHub Pages.

## Architecture

**Single-File Structure**: The entire portfolio is contained in `index.html` with embedded CSS and JavaScript. This approach is intentional for simplicity and zero build dependencies.

**Key Components**:
- **Header/Navigation**: Fixed-position nav bar with smooth scrolling links to sections
- **Hero Section**: Full-viewport landing with gradient background
- **Content Sections**: About, Experience, Skills, Education, Contact - all using semantic HTML5
- **Animations**: Intersection Observer API for scroll-based animations on section visibility
- **Back-to-Top Button**: Fixed-position scroll button with show/hide logic

**Styling Approach**:
- System font stack (Helvetica-based) for clean typography
- Mobile-first responsive design with `@media` queries
- Flexbox and CSS Grid for layouts
- CSS transitions and transforms for interactive effects
- Consistent color scheme: primary blue (#007aff), neutral grays, gradient backgrounds

**JavaScript Features**:
- Smooth scroll navigation behavior
- Intersection Observer for progressive element reveals
- Scroll event listener for back-to-top button visibility

## Development Workflow

**No Build Process**: This is a static site with no bundler, transpiler, or package manager. Changes to `index.html` are immediately visible when served.

**Local Development**:
```bash
# Serve locally with any static server, e.g.:
python -m http.server 8000
# or
npx serve .
```

**Deployment**: Push changes to the `main` branch. GitHub Pages automatically serves the updated `index.html`.

## Common Tasks

**Editing Content**:
- Experience updates: Modify `.timeline-item` divs in the Experience section
- Skills/Certifications: Update `.grid-item` divs in Skills section
- Contact info: Update links/email in Contact section

**Styling Changes**:
- All styles are in the `<style>` block in `<head>`
- Color scheme variables are hardcoded; search for hex values to update consistently
- Responsive breakpoint is at 768px (mobile/tablet)

**Adding Sections**:
1. Add new section in HTML with unique ID
2. Add navigation link in header menu
3. Apply `.animate-on-scroll` class for reveal animation
4. Update smooth scroll event listeners if needed

## Important Constraints

- Maintain single-file architecture unless explicitly required to split
- Keep dependencies at zero (no npm, no frameworks)
- Preserve accessibility features (semantic HTML, proper heading hierarchy)
- Ensure mobile responsiveness for all changes
- LinkedIn profile link in logo: `https://www.linkedin.com/in/yurii-kovanzhy/`
