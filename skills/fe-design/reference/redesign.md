# Redesign protocol (taste-v2 §11 + redesign-existing-projects, merged)

Misclassifying the mode is the biggest source of bad redesign output. After this file, load the matching register (landing.md or product.md) for the surface being redesigned.

## 1. Detect the mode (first action)

- **Greenfield**: no existing site, or full overhaul approved → registers apply directly.
- **Redesign, preserve**: modernize without breaking the brand → audit first, extract tokens, evolve.
- **Redesign, overhaul**: new visual language, existing content/IA preserved.

If ambiguous, ask once: "Preserve the existing brand, or start visually from scratch?"

## 2. Audit before touching anything

Document: brand tokens (colors, type stack, logo, radii) · information architecture (page tree, nav, conversion paths) · content blocks (what works, what's filler) · patterns to preserve (signature interactions, copy voice) · patterns to retire (slop tells, broken layouts, dead links, perf traps) · dial reading of the existing site (its variance/motion/density is your starting point, not the baseline) · SEO baseline (ranking pages, metas, structured data; SEO migration is the #1 redesign risk).

## 3. Preservation rules

- IA, slugs, anchor IDs, nav labels stay stable unless asked (SEO + muscle memory).
- Extract brand colors BEFORE applying any palette rule. A brand that is already purple stays purple; identity-preservation overrides the bans.
- Existing committed fonts override the SKILL.md font bans (the reflex-reject lists are for greenfield choices).
- Copy voice preserved unless a rewrite is requested.
- Never regress accessibility wins (focus states, alt text, contrast, keyboard nav).
- Never silently change: URL structure, nav labels, form field names/order (analytics + autofill), logo/wordmark, legal/consent copy.
- Work with the existing stack. No framework or styling-library migrations. Check Tailwind version before touching config. Test after every change; keep changes reviewable.

## 4. Diagnose (common findings checklist)

Typography: default/banned fonts everywhere · headlines without presence (size up, tighten tracking and leading) · body too wide (65ch) · only 400/700 weights (add 500/600) · proportional figures in data (tabular-nums/mono) · all-caps subheaders · orphans (`text-wrap: balance/pretty`).

Color/surfaces: pure #000 bg · oversaturated or multiple accents · mixed warm+cool grays · AI purple/blue gradient · untinted black shadows · zero texture/depth (subtle grain, ambient gradients) · inconsistent light direction · random inverted-theme section mid-page.

Layout: everything centered · 3-equal-cards row · `100vh` instead of `100dvh` · flexbox percentage math · no max-width container (1200-1440px) · uniform radius on everything · zero overlap/depth · CTAs not bottom-aligned across card groups · misaligned baselines in side-by-side columns · mathematically-centered-but-optically-off icons (1-2px nudges).

Interactivity: no hover/active states · zero-duration transitions · missing focus rings · spinner instead of skeletons · no empty/error states · dead `#` links · no current-page indicator in nav · `top/left/width/height` animations.

Content: John Doe/Acme/Lorem · round fake numbers · buzzword copy · "Oops!" errors (be direct: "Connection failed. Try again.") · passive voice · identical blog dates · shared avatars · Title Case On Everything (sentence case).

Code: div soup (use semantic elements) · inline styles mixed in · hardcoded px widths · missing alt text · z-index 9999 · dead commented code · imports not in package.json · missing title/description/og meta.

Strategic omissions: legal links, back navigation, custom 404, client-side form validation, skip-to-content link, favicon.

## 5. Fix priority (max impact, min risk)

1. **Font swap** (biggest lift, lowest risk; respect rule 3 if fonts are brand-committed)
2. **Color cleanup** (desaturate, unify neutrals, keep brand accent)
3. **Hover/active states** (page feels alive)
4. **Layout & spacing** (container, rhythm, section padding)
5. **Replace generic components** (cliché patterns → modern alternatives)
6. **Loading/empty/error states** (feels finished)
7. **Typography scale polish** (the premium final touch)

Motion layer additions follow motion.md throughout.

## 6. Evolution vs full redesign

- IA, content, SEO sound → targeted evolution (priorities 1-4): ~70% of value at ~40% of risk.
- Structural visual debt (broken IA, no system, broken mobile) → full redesign with strict content preservation.
- The brand itself is changing → treat as greenfield.
