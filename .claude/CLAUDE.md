# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# PCL Website — Project Rules
# These rules apply specifically to the PurpleCactusLabs/website repo.
# Global rules in ~/.claude/CLAUDE.md and ~/.claude/rules/ also apply.

## What This Repo Is
Marketing site for Purple Cactus Labs — purplecactuslabs.com
Deployed on Vercel, auto-deploys from GitHub `main`.

## Files & Routes
- `index.html` — homepage, contains all CSS and JS inline (single file)
- `notion-gmail-sidebar/index.html` — product landing page (route: `/notion-gmail-sidebar`)
- `success/index.html` — post-purchase success page
- `privacy.html`, `terms.html` — legal pages (routes: `/privacy`, `/terms`)
- `verify.js` — Puppeteer screenshot script for visual QA (`node verify.js`)
- `vercel.json` — URL rewrites (clean routes without `.html`)

Assets in root: `PCL_neon_logo_dark.svg`, `PCL_logo_white.svg`, `favicon.svg`, `hero.png`, `og-image.png`, `og-image-sidebar.png`, `PCL_US Dot Map-reduced size.svg`

## Architecture — index.html

Three-layer z-index system that creates the "content scrolls over fixed logo" effect:

| Layer | Class | z-index | Role |
|-------|-------|---------|------|
| Fixed background | `.logo-stage` | 0 | Hero logo + tagline, fixed to viewport, never scrolls |
| Transparent spacer | `.hero-spacer` | 1 | `100vh` tall, invisible — pushes content below fold |
| Scrollable content | `.content` | 2 | Everything else; has `background: var(--deep-night)` so it covers the logo as user scrolls |

Nav (`.nav`, z-index: 10) is sticky inside `.content`. The nav logo teleports: as the user scrolls, the hero logo fades out with `neon-off`, and the nav logo fades in — creating the illusion the logo moved up into the nav.

## CSS Custom Properties
```
--deep-night:   #0D0B14   (page background)
--dark-violet:  #1A1528
--pcl-purple:   #A855F7   (brand purple — primary accent)
--neon-fuchsia: #D946EF   (secondary accent / gradients)
--deep-purple:  #7C3AED
--muted-violet: #6B6880
```

## Animation Sequence (page load)
1. Tagline lines reveal left-to-right (clip-path, 750ms each, staggered)
2. Tagline slides down to make room for logo (translateY, ~1900ms)
3. Logo neon flicker fires (`neon-on` keyframe)
4. Logo holds with slow `neon-pulse`
5. Scroll indicator ("See what we make") fades in (~3100ms)
6. Scroll-triggered `IntersectionObserver` reveals sections as user scrolls

## Preview
Max uses VS Code with Microsoft Live Preview extension.
He previews changes himself — NEVER call preview_* tools, never start a server.

## Committed & Locked — Do Not Modify
- Footer CTA tab ("Like this website?") — committed, working, do not touch

## Copy Rules
- Never remove body copy without explicit instruction
- Never rewrite or simplify existing copy without being asked
- Pillar headlines: punchy, one-line, self-evident — never academic

## Git
Never run git commands. When committing, provide two blocks for GitHub Desktop:
1. Summary — one-line title
2. Description — bullet points
Stop there.
