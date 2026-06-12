# Critique mode (analyze without touching code)

Read the site, run every rule against it, output a ranked findings report. No code written. One actionable fix per finding.

## Step 1 — Read before judging

Read all files: CSS/tokens, representative components, `package.json`, any existing design system. Never critique from assumptions — quote the actual line when citing a problem.

## Step 2 — Run the two-altitude reflex check first

- **First-order:** could someone guess the theme + palette from the category alone? ("cookware → cream and brass", "SaaS → purple gradient + Inter")
- **Second-order:** could someone guess the aesthetic from category-plus-avoidance? ("AI tool that avoids SaaS-cream → editorial serif + mono labels")

If either answer is yes, that's a CRITICAL finding regardless of execution quality.

## Step 3 — Brand-archetype probe

What is the physical world of this brand? Does the palette match that world, or does it match a different category's default? (A craft brand in cobalt = wrong. A spirits brand in cream = wrong.) Mismatch = HIGH finding.

## Step 4 — Run all preflight categories as findings

For each category below, list every failure as a finding. Skip passing items — report only problems.

### Copy
- Em dashes / en dashes present (CRITICAL — binary fail)
- Buzzwords: seamless, elevate, unleash, empower, supercharge, next-gen, cutting-edge, game-changer, world-class, revolutionize (HIGH per instance)
- Aphoristic cadence: 3+ short rebuttal-shaped sentences in a row (MEDIUM)
- Performative-craftsman labels: "Field notes", "From the bench", "Quietly trusted by" (MEDIUM)
- CTA labels not verb+object, or duplicate intent labels on same page (MEDIUM)
- Grammatically broken, referent-unclear, or cute-but-wrong copy (HIGH)

### Typography
- Banned font in use: Inter, Roboto, Arial, Open Sans, DM Sans, DM Serif, Plus Jakarta Sans, Outfit, Space Grotesk, Space Mono, IBM Plex (all), Fraunces, Instrument Serif, Instrument Sans, Playfair Display, Cormorant (all), Lora, Crimson (all), Newsreader, Syne (CRITICAL per font)
- Serif without register justification, or serif in a dashboard (HIGH)
- Random serif word injected into a sans headline for "emphasis" (HIGH)
- More than 3 font families (HIGH)
- Two similar sans paired instead of contrast-axis pairing (MEDIUM)
- Body line length > 75ch or < 55ch (MEDIUM)
- Heading clamp > 6rem or tracking > -0.02em on display (MEDIUM)
- Missing `text-wrap: balance` on h1–h3 (LOW)

### Color & theme
- Contrast fail: body < 4.5:1, large text < 3:1, CTA label vs button fill < 4.5:1 (CRITICAL per instance)
- Cream/bone/beige bg + brass/clay/oxblood accent + espresso text on a premium-consumer brief (CRITICAL)
- AI-purple/blue gradient or neon glow (CRITICAL)
- Gradient text (`bg-clip-text` / `background-clip: text`) (HIGH)
- More than 1 accent color, or accent shifts mid-page (HIGH)
- Pure `#000000` or `#ffffff` as a surface (HIGH)
- Mixed warm + cool grays (MEDIUM)
- Saturation > 80% on any non-accent surface (MEDIUM)
- Dark section sandwiched into a light page (or vice versa) without deliberate intent (MEDIUM)
- Theme choice appears to be a default, not a deliberate scene-sentence decision (MEDIUM)

### Layout
- Hero doesn't fit initial viewport without scroll (CRITICAL)
- Hero headline > 2 lines at desktop (HIGH)
- Hero subtext > 20 words (MEDIUM)
- More than 4 text elements in the hero (MEDIUM)
- Top padding > 6rem on hero (MEDIUM)
- Eyebrow count > ceil(sections / 3) — count `uppercase tracking` labels mechanically (HIGH)
- Numbered section eyebrows (01/02/03) (HIGH)
- Identical 3-card feature row (HIGH)
- Hero metric template: big number + small label + gradient accent (HIGH)
- More than 2 consecutive image/text zigzags (MEDIUM)
- Same layout family used more than twice on the page (MEDIUM)
- `h-screen` instead of `min-h-[100dvh]` (MEDIUM)
- No explicit single-column collapse < 768px on asymmetric layouts (HIGH)
- Semantic z-index violations (999, 9999) (LOW)

### Motion
- Infinite animation loop on informational content (CRITICAL)
- Missing `prefers-reduced-motion` alternative (CRITICAL)
- Hover effects not gated behind `@media (hover: hover) and (pointer: fine)` (HIGH)
- `window.addEventListener('scroll')` for animation (HIGH)
- Animating `top/left/width/height` instead of `transform/opacity` (HIGH)
- Content hidden until animation plays (no default-visible fallback) (HIGH)
- More than 1 marquee (MEDIUM)
- Animation duration > 300ms on UI interactions (MEDIUM)
- Built-in easing keywords (`ease-in-out`) instead of custom cubic-bezier (LOW)

### States & semantics
- Missing loading state (skeletons, not spinners) on async data (HIGH)
- Missing empty state (HIGH)
- Missing error state (HIGH)
- No hover/active/focus-visible/disabled states on interactive elements (HIGH)
- Missing focus rings (CRITICAL — accessibility)
- Dead `#` href links (MEDIUM)
- Div soup where semantic elements belong (MEDIUM)
- Missing alt text on images (HIGH)
- Labels not above inputs (MEDIUM)

### Content & assets
- Generic placeholders: John Doe, Acme, Lorem ipsum, 99.99% (HIGH)
- Div-built fake screenshots (HIGH)
- Hand-rolled decorative SVG illustration filling a product image slot (MEDIUM)
- Scroll cues: "Scroll to explore", bouncing chevrons (MEDIUM)
- Pills overlaid on photos (MEDIUM)
- Locale/weather strips, version labels in heroes (MEDIUM)
- Quotes > 3 lines or name-only attribution (LOW)
- Emojis in copy (MEDIUM unless brief is explicitly playful)

### Code
- Import not in `package.json` (CRITICAL)
- Multiple design systems on one page (HIGH)
- shadcn in default state (un-customized radii/colors/shadows) (MEDIUM)
- `h-screen` / `height: 100vh` (already in layout but flag in code too) (MEDIUM)
- Missing title/description/og meta (MEDIUM)
- Missing favicon (LOW)

## Step 5 — Output format

Group by severity. Within each group, most impactful first.

```
## CRITICAL  (fix before anything else)
- [Copy] em dash in hero headline: "Hand-finished — ready to cook" → remove, use comma or period
- [Font] Inter used as body font (globals.css:12) → replace with non-banned sans

## HIGH
- [Palette] Cream bg (#faf5ec) + brass accent (#b08947) on premium cookware brief → reflex palette; rotate to iron/ember or cobalt/stone
- [Motion] Infinite glow animation on hero blob (globals.css:88) → remove or gate on explicit live-data signal
...

## MEDIUM
...

## LOW
...

## Reflex check result
First-order: [PASS/FAIL — explanation]
Second-order: [PASS/FAIL — explanation]
Brand-archetype: [PASS/FAIL — explanation]

## Summary
X critical, Y high, Z medium, W low findings.
Estimated impact of fixing CRITICAL+HIGH alone: [one sentence].
```

No code written in this mode. If the user says "now fix it", classify as redesign and load redesign.md.
