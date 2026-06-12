# Product register (impeccable product, merged)

Design SERVES the product: app UIs, dashboards, admin, settings, data views, tools, authenticated surfaces. The slop test flips here: not "would someone say AI made this" but "would a user fluent in Linear/Figma/Notion/Raycast/Stripe sit down and trust this, or pause at every subtly-off component?" The failure mode is strangeness without purpose: over-decorated buttons, mismatched form controls, gratuitous motion, display fonts in labels, invented affordances for standard tasks. The bar is earned familiarity; the tool disappears into the task.

## Typography

- One well-tuned family is often right; product UI doesn't need display/body pairing. (Font bans from SKILL.md still apply: not Inter; a system-ui stack or Geist/Satoshi-class sans is the equivalent move. See CONFLICTS.md.)
- Fixed rem scale, not fluid clamp; users view at consistent DPI and a fluid h1 shrinking in a sidebar looks worse.
- Tighter step ratio: 1.125-1.2. Prose still 65-75ch; data tables can run dense, 120ch+ fine.
- Serif never in dashboards. Mono for code, timestamps, and (at high density) all numbers, with `font-variant-numeric: tabular-nums`.

## Color

Restrained is the floor: tinted neutrals + one accent ≤ 10% of surface. A single surface can earn Committed (a category color carrying a report, a drenched welcome screen).

- Standardize a state vocabulary: hover, focus, active, disabled, selected, loading, error, warning, success, info.
- Accent marks primary actions, current selection, state. Never decoration. No heavy saturation on inactive states.
- A second neutral layer for sidebars/toolbars/panels, slightly warmer or cooler than the content surface.

## Layout

- Responsive behavior is structural (collapsing sidebar, responsive table, breakpoint columns), not fluid typography.
- Density is a permission here: many rows, many labels, when users need it. Cards still earn elevation or don't exist; high-density surfaces group with `border-t` / `divide-y` / space, not boxes.
- Standard navigation patterns are a virtue: top bar + side nav, breadcrumbs, tabs, command palettes. Don't reinvent affordances for flavor (custom scrollbars, weird form controls, non-standard modals).
- Dropdowns inside `overflow: hidden|auto` containers get clipped: use native `<dialog>`/popover API, `position: fixed`, or a portal.

## Components

Every interactive component ships default, hover, focus, active, disabled, loading, error. Half-stated components are unfinished.

- Skeletons matching layout shape, not spinners in content.
- Empty states that teach the interface, not "No data".
- Inline form errors below the input; labels above; no placeholder-as-label; no `window.alert()`.
- Same button shape, same control vocabulary, same icon family across every screen. If "save" looks different in two places, one is wrong.
- Modal is usually laziness: exhaust inline editing, slide-overs, progressive disclosure first.

## Motion

motion.md governs (and it already agrees with this register): 150-250ms on most transitions, motion conveys state and feedback only, no orchestrated page-load sequences (users load into a task), no decorative loops, no animation on keyboard-triggered actions.

## Data presentation

- Mono/tabular numbers in any column users compare.
- Loading, empty, error, and partial states for every async region.
- Realistic mock data (organic values, varied dates, distinct avatars/names per row); never identical rows of John Doe at 50%.
