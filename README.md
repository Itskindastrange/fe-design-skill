# fe-design

An anti-slop frontend design skill for Claude Code. Produces interfaces that do not look AI-generated — no cream-and-brass palettes, no banned fonts, no eyebrow scaffolding, no em-dash copy. Compiled from three source skills with conflicts pre-resolved at build time.

**What it owns:**
- Layout, spacing, typography, color, copy (via design-impeccable)
- Motion, easing, micro-interactions (via emil-design-eng — wins all motion conflicts)
- Landing direction, palette/font bans, design-system mapping (via design-taste-frontend v2)

**Covers:** landing pages, marketing sites, portfolios, dashboards, product UI, app shells, components, redesigns.

---

## Install

### Step 1 — Install the `superpowers` dependency

This skill requires [obra/superpowers](https://github.com/obra/superpowers). Install it first inside Claude Code.

Register the marketplace:

```
/plugin marketplace add obra/superpowers-marketplace
```

Install the plugin:

```
/plugin install superpowers@superpowers-marketplace
```

Reload plugins:

```
/reload-plugins
```

### Step 2 — Install fe-design

```bash
npx skills add github:abdullahahmaddd/fe-design-skill
```

Reload plugins:

```
/reload-plugins
```

### Step 3 — Verify

Start a new chat and ask Claude to build a landing page or dashboard. The skill should trigger automatically. You can also invoke it explicitly:

```
/fe-design
```

---

## How it works

The skill auto-triggers on any frontend design task. When invoked, it:

1. Reads existing project tokens and `package.json` before touching anything
2. Classifies the task (landing / product / redesign) and loads exactly one route reference
3. Runs a design read — states the page kind, audience, vibe, and aesthetic lane
4. Runs a two-altitude reflex check — ensures the palette and aesthetic are not guessable from the category alone
5. Builds with all always-on rules enforced
6. Runs a pre-flight checklist before declaring done

## Trigger phrases

The skill activates automatically when you ask Claude to:

- Build or design any web interface
- Make a site "look better", "more premium", or "less AI-generated"
- Create a landing page, marketing site, portfolio, dashboard, product UI, or app shell
- Redesign or restyle an existing site or component

## What it bans

**Fonts (training-data defaults):** Inter, Roboto, Arial, Open Sans, DM Sans, DM Serif, Plus Jakarta Sans, Outfit, Space Grotesk, Space Mono, IBM Plex (all), Fraunces, Instrument Serif, Instrument Sans, Playfair Display, Cormorant (all), Lora, Crimson (all), Newsreader, Syne

**Palette reflexes:** cream/bone/beige body backgrounds, brass/clay/oxblood accents on premium-consumer briefs, AI-purple/blue gradients, neon glows

**Copy tells:** em dashes, en dashes, "seamless", "elevate", "unleash", "empower", "next-gen", aphoristic three-line cadence, performative-craftsman labels

**Layout tells:** eyebrow above every section, numbered section markers (01/02/03), identical 3-card feature rows, hero metric template, gradient text, glassmorphism as default decoration

## Files

```
skills/fe-design/
├── SKILL.md           # Entry point, always-on rules, font/color/layout bans
├── CONFLICTS.md       # 15-row conflict resolution table (build-time decisions)
└── reference/
    ├── landing.md     # Landing pages, marketing, portfolios — dial system, hero discipline
    ├── product.md     # Dashboards, product UI, app shells — product register
    ├── redesign.md    # Existing sites — audit protocol, preservation rules, fix priority
    ├── motion.md      # All motion rules — easing, durations, scroll choreography (emil)
    └── preflight.md   # Pre-flight checklist — run before declaring any page done
```

## Eval results (iteration 1)

Mechanical slop checks (14 criteria: em dashes, banned fonts, buzzwords, cream/brass palette, purple gradients, gradient text, scroll listeners, generic placeholders, scroll cues, pure-black surfaces, reduced-motion, hover gating, eyebrow cap, fake numbers):

| Eval | Baseline | With skill |
|---|---|---|
| Marrow cookware landing | 9/14 (Inter+Fraunces, 10 em dashes, no reduced-motion, 6 eyebrows on 5 sections) | 14/14 |
| RAG pipeline dashboard | 11/14 (2 em dashes, no reduced-motion, no hover gate) | 14/14 |
| Motion designer portfolio | 8/14 (Inter, buzzwords, purple gradient, 11 eyebrows on 4 sections) | 14/14 |

Design choices per with-skill run (non-reflexive, distinct across all three):

| Eval | Fonts | Palette |
|---|---|---|
| Marrow cookware | Gilda Display + Geist | Iron-black OKLCH + ember orange (iron-fire) |
| RAG dashboard | System sans + tabular numerals | Deep teal (restrained, product register) |
| Motion portfolio | Clash Display + General Sans | Vermilion OKLCH (dark creative) |

---

## License

MIT
