# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A single-page HTML pitch deck for **Klydo** — a fashion quick-commerce startup. No build step, no framework, no dependencies. Open `h&m.html` in a browser to preview.

## Structure

- `h&m.html` — the pitch deck markup and scroll-tracking JS
- `style.css` — all styling (extracted from HTML, not inline)
- Images are named descriptively:
  - `klydo-logo.png` — logo
  - `ankit-agarwal.png`, `pradeep-yadav.png` — founder headshots
  - `sabina-nazneen.png`, `manikanta-kondeti.png`, `chandnni-nain.png`, `divya-tak.png`, `kahran-singh.png` — extended team
  - `brand-universe.png` — brand collage
  - `hmnow-screen-1.png` through `hmnow-screen-5.png` — HM NOW app screenshots
  - `bangalore-zones.jpeg` — delivery zones map

## Design System

- **Font:** Raleway (Google Fonts CDN)
- **Primary color:** `#FF2D8A` (Klydo pink — from logo)
- **Secondary color:** `#8B45D6` (purple — from logo)
- **Tertiary color:** `#00D4DC` (cyan — from logo)
- **Background:** white (`#fff`), text is `#1a1a2e`
- **Shape language:** Rounded rectangles — `border-radius: 16px` on cards, `10px` on tags/pills/bars. NOT fully rounded (no `999px`).
- **Gradients:** Pink-to-purple (`linear-gradient(135deg, #FF2D8A, #8B45D6)`) used on accent text, dividers, bar fills, and check icons

## Architecture Notes

- **Navigation:** Fixed top nav with pill buttons that smooth-scroll to section IDs (`why`, `pmf`, `team`, `growth`, `scale`, `brands`, `hm`). A scroll listener highlights the active pill.
- **Slides:** Each `<section class="slide sN">` is a full-viewport slide. Decorative gradient blurs via `::before` pseudo-elements per slide class (`s1`–`s10`).
- **Reusable CSS patterns:** `.card-grid` with `.g2`/`.g3`/`.g4` for column layouts, `.stat-card` for metric callouts, `.highlight` for emphasis blocks, `.checklist` for feature lists, `.phones-row > .phone` for device mockups, `.tag` / `.tag.teal` / `.tag.dark` for badges.
- When adding new slides, add a `<section class="slide sN">` and a matching `::before` rule in `style.css`. Add a nav pill if the section should be navigable.
