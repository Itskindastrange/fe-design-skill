---
name: fe-design
description: Anti-slop frontend design skill. Use this skill whenever the user asks to build, design, redesign, restyle, polish, or improve any web interface - landing pages, marketing sites, portfolios, dashboards, product UI, app shells, components, forms, or full applications. Also use when the user mentions making a site "look better", "more premium", "less AI-generated", or asks for any visual/UX work, even if they don't say "design" explicitly. Produces distinctive, production-grade interfaces that do not look templated or LLM-generated. Compiled from design-impeccable, emil-design-eng, and taste-frontend with conflicts pre-resolved.
---

# fe-design: Compiled Anti-Slop Frontend Skill

One goal: ship interfaces nobody can identify as AI-generated. Neither the pixels (purple gradients, cream-and-brass palettes, eyebrow-label scaffolding) nor the words (em dashes, "seamless", aphoristic cadence) may scream LLM.

This skill is a build-time merge of three sources with precedence already resolved:
- **design-impeccable** owns layout, spacing, typography, color, copy
- **emil-design-eng** owns motion, easing, micro-interactions (wins ALL motion conflicts)
- **design-taste-frontend v2** owns landing-page direction, palette/font bans, design-system mapping

When bans collide, the strictest ban wins. Resolved decisions live in [CONFLICTS.md](CONFLICTS.md); don't re-derive them.

## Setup (every invocation)

1. Read the project before designing: existing CSS tokens / theme / a representative component, and `package.json`. Never import a library without confirming it exists or outputting the install command first. Reuse committed brand colors and fonts; identity-preservation beats every ban below.
2. Classify the task and load exactly ONE route reference:

| Brief reads as | Load |
|---|---|
| Landing page, marketing site, portfolio, campaign, brand surface (design IS the product) | [reference/landing.md](reference/landing.md) |
| Dashboard, product UI, app shell, admin, settings, tool (design SERVES the product) | [reference/product.md](reference/product.md) |
| Existing site/app to upgrade or restyle | [reference/redesign.md](reference/redesign.md) first, then the matching register above |
| Analyze / audit / critique / "what's wrong" / "give me recommendations" / "roast this" / "how can I improve" — no code wanted | [reference/critique.md](reference/critique.md) only — no code written |

3. If the task involves ANY animation, transition, or interaction work (it almost always does), also load [reference/motion.md](reference/motion.md). Motion rules there override anything else.
4. Before declaring any page done, run [reference/preflight.md](reference/preflight.md). Not optional.

## The design read (before any code)

State in one line: *"Reading this as: [page kind] for [audience], with a [vibe] language, leaning toward [aesthetic family or design system]."* If the brief genuinely diverges between two directions, ask ONE question. Otherwise declare and proceed.

Then run the two-altitude reflex check:
- **First-order**: could someone guess your theme + palette from the category alone ("cookware brief → cream and brass")? That's the training-data reflex. Rework.
- **Second-order**: could someone guess your aesthetic from category-plus-avoidance ("AI tool that's not SaaS-cream → editorial serif + mono labels")? That's the trap one tier deeper. Rework until neither answer is obvious.

## Always-on rules (apply to every route)

### Copy (the text tells)

- **Zero em dashes (—) and zero en dashes (–) anywhere visible.** Headlines, body, captions, buttons, alt text, quotes, attribution. Use periods, commas, colons, parentheses, or a plain hyphen. This is binary, not "use sparingly"; the model historically ignores soft limits here.
- No marketing buzzwords: seamless, elevate, unleash, empower, supercharge, next-gen, cutting-edge, game-changer, world-class, transform, streamline. Pick a specific noun and a verb describing what the product literally does.
- No aphoristic cadence as a default voice. If three or more copy blocks land on a short rebuttal-shaped sentence ("Serious tools. Not serious prices."), rewrite. Specific beats poetic.
- No performative-craftsman labels ("Field notes", "From the bench", "Quietly trusted by"). Plain functional labels or none.
- Button labels are verb + object ("Save changes", not "OK"). One label per intent per page: "Get in touch" + "Let's talk" on the same page is a fail.
- Before shipping, re-read every visible string. Anything grammatically broken, referent-unclear, or cute-but-wrong gets replaced with a plain functional sentence.

### Absolute visual bans (match and refuse, all registers)

- Gradient text (`background-clip: text` + gradient). Solid color; emphasis via weight or size.
- Side-stripe borders (`border-left` > 1px as colored accent on cards/callouts).
- Glassmorphism as default decoration. Rare and purposeful, or nothing.
- The hero-metric template (big number + small label + gradient accent).
- Identical card grids (same icon + heading + text card repeated endlessly) and the 3-equal-cards feature row.
- Tiny uppercase tracked eyebrow above every section, and numbered section markers (01/02/03) as default scaffolding. Mechanical cap: eyebrow count ≤ ceil(sectionCount / 3); if section A has one, the next two don't.
- Pure `#000000` and pure `#ffffff` as surfaces. Off-black, off-white.
- AI-purple/blue glow aesthetic, neon outer glows, oversaturated accents (keep saturation < 80%, max 1 accent, locked across the whole page).
- Emojis in code, markup, or visible text (icon-library glyphs instead) unless the user explicitly wants a playful chat-native vibe.
- Div-built fake screenshots (fake task lists, fake terminals). Real screenshot, generated image, real component preview, or nothing.
- Generic placeholder content: John Doe, Acme, Lorem Ipsum, 99.99%. Realistic names, contextual brand names, organic messy numbers (47.2%).
- Custom mouse cursors. Scroll cues ("Scroll to explore", bouncing chevrons). Decorative status dots. Locale/weather strips. Version labels in heroes (BETA, v0.6) unless the brief is literally a launch.

### Fonts (strictest-ban merge; see CONFLICTS.md)

Banned as picks: **Inter, Roboto, Arial, Open Sans, DM Sans, Plus Jakarta Sans, Outfit, Space Grotesk, Space Mono, IBM Plex (all), Fraunces, Instrument Serif, Instrument Sans, Playfair Display, Cormorant (all), Lora, Crimson (all), Newsreader, Syne, DM Serif (all)**. These are training-data defaults; using them is how output converges to the monoculture.

Instead, run the selection procedure: write three concrete brand-voice words (physical-object words, not "modern"/"elegant"), browse a real catalog (Google Fonts, Pangram Pangram, ABC Dinamo, Klim, Future Fonts) with those words, and pick the font the brand would be as a physical object. Geist, Satoshi, Cabinet Grotesk are acceptable but rotate: never the same display font two projects in a row. Serif only when the brief is genuinely editorial/luxury/publication AND you can articulate why this serif fits this brand; never in dashboards. Emphasis inside a headline = italic/bold of the SAME family, never a random serif word injected into a sans headline. Cap families at 3 (display + body + optional mono); pair on a contrast axis, not two similar sans.

### Color

- Verify contrast mechanically: body ≥ 4.5:1, large text ≥ 3:1, placeholders 4.5:1, every CTA label against its button fill. Muted-gray-on-tinted-near-white is the #1 readability failure.
- Pick a color strategy before colors: Restrained (neutrals + ≤10% accent), Committed (one saturated color carries 30-60%), Full palette (3-4 named roles), Drenched (the surface IS the color). Product floors at Restrained; brand surfaces have permission to commit. Name a real reference ("Klim orange drench", "Vercel monochrome") or ambition decays to beige.
- The warm cream/sand/beige body background is the saturated AI default. Do not translate "warm/editorial/artisan" into near-white warm-tinted backgrounds. Banned premium-consumer reflex palette: cream/bone bg + brass/clay/oxblood accent + espresso text. Rotate alternatives: cold luxury (silver/chrome/smoke), forest (deep green/bone/amber), black-and-tan, cobalt+cream, terracotta+slate, monochrome+one saturated pop.
- One palette, one gray family, one accent for the whole page. One theme for the whole page: no dark section sandwiched into a light page. Theme choice is never a default; write one sentence of physical scene (who uses this, where, what ambient light) and let it force the answer.
- Use OKLCH for new token systems.

### Layout

- Hierarchy through scale + weight contrast (≥1.25 ratio brand, 1.125-1.2 product). Body line length 65-75ch. `text-wrap: balance` on h1-h3.
- Cards only when elevation communicates hierarchy; otherwise borders/dividers/space. Nested cards always wrong.
- Vary layout families: once a section layout is used, max once more per page; max 2 consecutive image+text zigzags. Semantic z-index scale, never 999.
- `min-h-[100dvh]`, never `h-screen`. Grid over flexbox percentage math. Explicit single-column collapse below 768px for every asymmetric layout.
- Display heading ceiling clamp() ≤ 6rem; letter-spacing ≥ -0.04em.

### Variety rotation (anti-monoculture)

This skill's own rules create a new uniform if followed lazily. Across consecutive projects, rotate: display font, palette family, hero paradigm, theme. If the previous project was Geist-on-zinc with an asymmetric split hero, this one is not. The pre-flight check asks for this explicitly.

### Non-negotiables

- `prefers-reduced-motion` alternative for every animation. Hover effects gated behind `@media (hover: hover) and (pointer: fine)`.
- Animate only `transform` and `opacity` (plus blur/clip-path when they earn it and stay smooth).
- Interactive components ship all states: default, hover, focus-visible, active, disabled, loading (skeletons, not spinners), empty, error.
- Semantic HTML, alt text with voice, focus rings, labels above inputs, error text below.

## Out of scope

Data-table engines (TanStack/AG Grid), code editors (Monaco), native mobile (HIG/Material direct), realtime collab UI internals. Say so and point to the right tool. For deep single-purpose passes (critique scoring, live browser variant iteration), `/design-impeccable critique|live` still exists; this skill replaces the trio for build and redesign work.
