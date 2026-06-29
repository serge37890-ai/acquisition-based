# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the "Acquisition Based" marketing site — a static one-page sales site for a client-acquisition agency targeting home service businesses (HVAC, plumbing, electrical, etc.). It is plain HTML/CSS/JS with no build system, package manager, or framework. Open `index.html` directly in a browser, or use a Live Server–style auto-reload extension for iteration.

## Files

- `index.html` — the entire site, one page, sections identified by id (`#problem`, `#solution`, `#services`, `#guarantee`, `#team`, `#contact`) that double as nav anchors.
- `style.css` — all styling. CSS variables for the color palette and typography live in `:root` at the top.
- `script.js` — mobile nav toggle (hamburger) and an `IntersectionObserver`-driven scroll-reveal effect (elements with class `.reveal` fade/slide in once visible).
- `Article1.png`–`Article4.png` — unused source images (AI-generated dashboard mockups) kept for reference only; deliberately not used in the page because their glossy/glow style conflicts with the site's monochrome design language. Don't wire these into the page without checking with the user first.

## Design constraints (locked — do not deviate without explicit user approval)

- **Color palette**: only `#222222` (dark), `#7B7B7B` (gray), `#F8F8F8` (light), `#FFFFFF` (white), plus green reserved exclusively for CTAs (`--green: #146B3F`, hover `--green-hover: #1B8A52` in `style.css`). No other colors.
- **No AI-slop aesthetic**: no stock gradients, glow/neon effects, generic stock photography, or cliché SaaS-dashboard imagery. Keep the editorial, typography-driven, high-whitespace look modeled on the Wolfpixel "Personal Portfolio Website Design" Dribbble shot.
- **Mobile-first**: base CSS in `style.css` targets mobile; tablet rules are behind `@media (min-width: 700px)`, desktop behind `@media (min-width: 960px)`. Always check both breakpoints after changes (hamburger nav becomes inline nav, hero switches from stacked to a 3-column grid with rotated side label).
- **Fonts**: General Sans via Fontshare CDN (linked in `<head>`), with system sans-serif fallback. No other font families.
- **Icons**: hand-rolled inline SVG (stroke, `currentColor`, no fill, 24x24 viewbox) — not an icon library, not raster images. Follow this pattern for any new icons.

## Known gotcha

`.nav` uses `backdrop-filter: blur(8px)` for the frosted header effect. That property creates a new containing block for `position: fixed` descendants — `#nav-links` (the mobile menu panel) is one such descendant. It must use an explicit `height` (currently `calc(100vh - var(--nav-height))`) rather than `bottom: 0`, because `bottom: 0` resolves against `.nav`'s own (76px-tall) box instead of the viewport once the containing block is hijacked, collapsing the panel to zero height. If you touch `.nav__links` positioning, keep the explicit height — don't switch back to `top`+`bottom`.

## Content status

Hero photo and the three Team photos are placeholders (CSS box + person-outline SVG icon) — real photos haven't been provided yet. Hero stat counters from the original design reference were intentionally dropped since no real metrics were available yet (don't fabricate numbers on a live sales page). Team member names/roles beyond "Founder" are placeholders. The Contact section CTA link is a dead `href="#"` pending a real booking link (Calendly, phone, mailto).
