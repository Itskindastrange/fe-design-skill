# Landing / brand register (taste-frontend v2 + impeccable brand, merged)

Design IS the product here: landing pages, marketing, portfolios, campaigns, brand surfaces. The bar is distinctiveness; a visitor should ask "how was this made?", not "which AI made this?" Restraint without intent now reads as mediocre. Name the aesthetic lane before committing ("Klim specimen", "Stripe-minimal", "acid-maximalism"); then describe what you're about to build the way a competitor would describe theirs. If that sentence fits the category's modal landing page, restart.

## Dials

Set three dials from the design read; they gate every layout/motion/density decision below.

- `DESIGN_VARIANCE` (1 symmetric → 10 artsy chaos)
- `MOTION_INTENSITY` (1 static → 10 cinematic)
- `VISUAL_DENSITY` (1 gallery-airy → 10 cockpit)

| Use case | V / M / D |
|---|---|
| SaaS landing (mainstream) | 7 / 6 / 4 |
| Agency / creative landing | 9 / 8 / 3 |
| Premium consumer | 7 / 6 / 3 |
| Designer/studio portfolio | 8 / 7 / 3 |
| Developer portfolio | 6 / 5 / 4 |
| Editorial / blog | 6 / 4 / 3 |
| Public-sector / trust-first | 3 / 2 / 5 |
| Redesign | match existing (+2 V/M if overhaul) |

Variance 1-3: symmetric grids, centered OK. 4-7: offsets, mixed aspect ratios, left-aligned headers. 8-10: masonry, fractional grids (`2fr 1fr 1fr`), big empty zones. Motion 8-10 means real scroll choreography (see motion.md), never `window.addEventListener('scroll')`. Density 8-10: no card boxes, 1px separators, `font-mono` numbers. All asymmetry collapses to strict single column < 768px.

"Motion claimed, motion shown": a static page claiming intensity 7 is broken; if you can't ship working motion in scope, drop the dial to 3 and ship clean static.

## Design system honesty

If the brief reads as one of these, install the OFFICIAL package; don't hand-recreate its CSS, don't override 90% of its tokens, one system per project:

| Brief | Reach for |
|---|---|
| Microsoft/enterprise | `@fluentui/react-components` |
| Material-flavored | `@material/web` + M3 tokens |
| IBM-style B2B analytics | `@carbon/react` |
| Shopify admin | Polaris |
| Atlassian-style | `@atlaskit/*` |
| GitHub-style devtool | `@primer/css` / `@primer/react-brand` |
| UK public sector | `govuk-frontend` |
| US public sector | `uswds` |
| Accessible React foundation | `@radix-ui/themes` |
| Modern SaaS, owned components | shadcn/ui (never default state: customize radii, colors, shadows) |
| Indie/Tailwind default | Tailwind v4 utilities |

Aesthetics without an official package (glassmorphism, bento, brutalism, editorial, dark-tech, aurora, kinetic type): build honestly with native CSS + Tailwind, label approximations (there is no official Apple `liquid-glass.css`; web versions are `backdrop-filter` approximations with a `prefers-reduced-transparency` solid fallback).

## Stack defaults

React/Next.js, Server Components by default; anything using Motion/scroll/pointer physics is an isolated `'use client'` leaf. Tailwind v4 (check version before config edits; v4 uses `@tailwindcss/postcss`, not the `tailwindcss` postcss plugin). Animation: Motion via `import { motion } from "motion/react"`. Fonts via `next/font` or self-hosted `@font-face` + `font-display: swap`, never a Google Fonts `<link>` in production. Icons: one family per project from `@phosphor-icons/react`, `hugeicons-react`, `@radix-ui/react-icons`, or `@tabler/icons-react`; lucide only on explicit request; never hand-roll icon SVG paths; standardize strokeWidth globally.

## Typography (on top of SKILL.md font bans)

- Display default `text-4xl md:text-6xl tracking-tighter leading-none`; body `text-base leading-relaxed max-w-[65ch]` at full AA contrast.
- Hero headline ≤ 2 lines desktop (3 max). A 4-line hero headline is a font-size error: widen the container (`max-w-5xl/6xl`) and/or use `clamp(3rem, 5vw, 5.5rem)`.
- Italic display words containing `y g j p q`: `leading-[1.1]` minimum + bottom padding reserve, or descenders clip.
- Light text on dark: add 0.05-0.1 line-height.
- Modular scale, fluid `clamp()` headings, ≥1.25 step ratio.

## Hero discipline (hard rules)

- Fits the initial viewport: headline ≤ 2 lines, subtext ≤ 20 words and ≤ 4 lines, CTA visible without scroll. Top padding ≤ 6rem desktop.
- Max 4 text elements: (eyebrow OR brand strip OR neither) + headline + subtext + CTAs (1 primary + ≤1 secondary). Banned inside the hero: tagline under CTAs, trust micro-strip, pricing teaser, feature bullets, avatar rows, raw stats, floating stamp badges, pill tags.
- Logo wall ("Trusted by") lives in its own section UNDER the hero. Real SVG logos (Simple Icons CDN / devicon), or invented monogram SVG for invented brands; never styled-text wordmarks; logos only, no category captions.
- Hero needs a real visual. Text + gradient blob is a placeholder, not a hero.
- Centered hero allowed only at variance ≤ 4 or for manifesto/launch briefs where the message is the design; otherwise split, offset, or asymmetric.

## Section and page structure

- Section-layout-repetition: a layout family appears at most once more per page; ≥4 distinct families across 8 sections. Max 2 consecutive image/text zigzags.
- Split-header ban: no "giant left headline + small floating right paragraph" as a section header; stack vertically, 65ch body.
- Bento grids: exactly as many cells as content (no blank tiles), rhythm not repetition, `grid-flow-dense` thinking, 3-5 intentional cards beat 8 messy ones, 2-3 cells minimum carry real visual variation (image/pattern/tint), labels can sit outside cards.
- Navigation: one line at desktop, height ≤ 80px.
- Shape consistency lock: one corner-radius system page-wide, or a documented rule (buttons pill, cards 16px, inputs 8px) followed everywhere.
- Page theme lock: one theme. Section tints within the family fine; mode flips mid-page are broken (one deliberate full theme-switch device allowed only when the brief calls for it).

## Imagery (landing pages are visual products)

Priority: (1) image-generation tool if available in the environment, right aspect ratio per section; (2) real photography: verified Unsplash URLs when you can verify they resolve (web fetch/browser), otherwise `https://picsum.photos/seed/{descriptive-seed}/{w}/{h}`; (3) clearly-labeled placeholder slots + tell the user what's needed. Never fill pages with hand-rolled decorative SVGs or div-built fake screenshots. Even minimalist briefs ship 2-3 real images; pure-text pages are incomplete work, not restraint. Search for the brand's physical object ("hand-cut pasta on a scratched wooden table"), not the category ("Italian food"). One decisive photo beats five mediocre ones. Alt text carries voice.

## Content density

- Default section shape: headline ≤ 8 words + sub ≤ 25 words + one visual or CTA.
- No data dumps: top 3-5 highlights + "view all" link; >5 items need a real component (grouped 2-col, card grid, tabs, scroll-snap pills, marquee), never a `divide-y` wall. Spec sheets: grouped chunks, 2-col spec cards, or featured-vs-rest disclosure; never 10 hairline rows.
- Quotes ≤ 3 lines, real typographic quotes, attribution name + role (+company); never name-only.
- Fake-precise numbers (5.8mm, 4.1×) only from real data or explicitly marked mock.
- One copy register per page.
- Marquee max one per page. Middle-dot `·` max one per metadata line, never the default separator for everything.

## Color (on top of SKILL.md)

**Brand-archetype probe (run before choosing any palette):** Ask: what is the physical world of this brand? A software tool lives in a glowing screen. A cookware brand lives in a cast-iron surface, a flame, a scarred cutting board. A fashion brand lives in fabric, light, negative space. If your palette would fit a SaaS dashboard brief equally well, it is wrong for a craft/consumer/editorial brand. Dark palettes are not inherently premium — they are correct for brands whose physical world is dark (spirits, cinema, hardware), and wrong for brands whose world is daylit, material, or craft-forward. Run the scene sentence (SKILL.md) and let the physical environment force the answer before any color token is written.

Brand surfaces have permission for Committed, Full-palette, and Drenched strategies; use them. A single saturated hero color is voice, not excess; beige-and-muted-slate ignores the register. Tinted neutrals: 0.005-0.015 chroma toward the brand's own hue, not generic warmth. When a cultural-symbol palette is the obvious pull, reach past it.

## Landing-specific tells (banned)

Section-number eyebrows (`001 · Capabilities`), pagination labels on tiles (`01 / 4`), "Brand · No. 01" micro-meta, `<br>`-split italicized headlines as default, vertical rotated text, crosshair/hairline grid decoration, pills overlaid on photos, photo-credit-as-decoration captions, version footers (`v1.4.2`, `Build 0048`), live-stock counters, hero-bottom mono strips (`DESIGN · BUILD · SHIP`), "Quietly in use at", micro-meta sentences under eyebrows, generic step labels ("Step 1/2/3"; the verb-noun is the label), filled-track progress bars as comparison visuals, monospace as costume for "technical" when the brand isn't, large rounded icon above every heading, all-caps body copy.

## Brand permissions

Take what product can't afford: ambitious first-load choreography (one well-orchestrated entrance beats scattered micro-interactions), single-purpose viewports with deliberate pacing, unexpected color strategies, art direction that shifts per section when the narrative demands it. Some brands skip entrance motion entirely; restraint can be the voice.

## Performance & dark mode

LCP < 2.5s (hero image priority/preloaded), INP < 200ms, CLS < 0.1. Bundle awareness: Motion isn't tiny, Three.js is large, lazy-load below the fold. Theme: decide deliberately via the scene sentence (SKILL.md); when shipping dual-mode, pick ONE token strategy (Tailwind `dark:` or CSS variables), keep hierarchy and brand fidelity in both, test both before declaring done.
