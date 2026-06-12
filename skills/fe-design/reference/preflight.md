# Pre-flight check (run before declaring any page done)

Every box, honestly. One failed box means the page is not done.

## Copy
- [ ] ZERO em dashes (—) or en dashes (–) anywhere visible (headlines, body, captions, buttons, alt text, attribution)
- [ ] No buzzwords (seamless/elevate/unleash/next-gen family); no aphoristic-rebuttal cadence ×3; no performative-craftsman labels
- [ ] Every visible string re-read; nothing grammatically broken, referent-unclear, or cute-but-wrong
- [ ] One CTA label per intent across the page; labels are verb + object; no CTA wraps to 2 lines at desktop

## Typography
- [ ] No banned fonts (Inter, Outfit, Space Grotesk, Fraunces, Instrument Serif, Playfair, Cormorant, DM-family, Plex-family, etc. per SKILL.md)
- [ ] Display font differs from your previous project (rotation)
- [ ] Serif only with explicit register justification; never in dashboards
- [ ] Italic display words with descenders have leading ≥ 1.1 + padding reserve
- [ ] Heading clamp ≤ 6rem, tracking ≥ -0.04em, body 65-75ch

## Color & theme
- [ ] Contrast verified: body 4.5:1, large 3:1, placeholders 4.5:1, every CTA label vs button fill, every form element vs section bg
- [ ] One accent, locked page-wide; one gray family; saturation < 80%; no pure #000/#fff surfaces
- [ ] One theme page-wide (no inverted section mid-page); both modes tested if dual-mode
- [ ] Not the cream/brass/espresso reflex palette on a premium-consumer brief; palette family differs from previous project
- [ ] No AI-purple gradients, neon glows, gradient text

## Layout
- [ ] Hero: ≤ 2-line headline, ≤ 20-word subtext, CTA in first viewport, ≤ 4 text elements, top padding ≤ 6rem, real visual present
- [ ] Eyebrow count ≤ ceil(sections / 3) (count `uppercase tracking` labels mechanically; hero counts)
- [ ] No numbered-section eyebrows, no split-header pattern, ≤ 2 consecutive zigzags, ≥ 4 layout families per 8 sections
- [ ] Bento: N items → N cells, no blank tiles, 2-3 cells visually varied
- [ ] Logo wall under hero, real SVG logos, logos only
- [ ] Nav one line ≤ 80px; one radius system; semantic z-index scale
- [ ] `min-h-[100dvh]` not `h-screen`; explicit < 768px single-column collapse; no horizontal scroll at any viewport; heading copy tested at every breakpoint (no overflow)

## Motion (full pass in reference/motion.md §9)
- [ ] Every animation justified in one sentence (hierarchy/story/feedback/state); no infinite loops without explicit request
- [ ] Durations ≤ 300ms on UI; ease-out entries; custom curves not built-in keywords
- [ ] `prefers-reduced-motion` alternative everywhere; hover gated behind `(hover: hover)`
- [ ] Only transform/opacity (+earned blur/clip-path); no `window.addEventListener('scroll')`; GSAP pins use `start: "top top"` with cleanup
- [ ] Content visible by default; reveals enhance, never gate
- [ ] Marquee ≤ 1 per page; "motion claimed = motion shown"

## States & semantics
- [ ] Loading (skeletons), empty (teaching), error (inline) states present
- [ ] All interactive states: hover, focus-visible, active, disabled
- [ ] Semantic HTML, alt text with voice, labels above inputs, focus rings
- [ ] No dead `#` links; current page indicated in nav

## Content & assets
- [ ] Real images (gen tool → verified URLs → picsum seeds → labeled TODO slots); no div-fake screenshots; no hand-rolled decorative SVGs
- [ ] Realistic names/brands/numbers; no John Doe, Acme, 99.99%, Lorem
- [ ] No pills on photos, photo-credit decoration, version footers, locale/weather strips, scroll cues, decorative status dots, hero version labels
- [ ] Quotes ≤ 3 lines with clean attribution
- [ ] Icons from one allowed family; emojis absent

## Code
- [ ] Every import exists in package.json (or install command given)
- [ ] Motion isolated in `'use client'` leaf components with useEffect cleanup
- [ ] One design system per project; shadcn never in default state
- [ ] Core Web Vitals plausible: LCP < 2.5s (hero priority), INP < 200ms, CLS < 0.1
- [ ] Meta tags (title, description, og); favicon

## Final
- [ ] First-order slop test: theme+palette not guessable from category alone
- [ ] Second-order: aesthetic family not guessable from category-plus-avoidance
- [ ] The inverse test: your one-sentence description of the page would NOT fit the category's modal landing page
