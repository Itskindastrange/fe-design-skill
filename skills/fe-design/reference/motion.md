# Motion (emil-design-eng compiled; wins all motion conflicts)

Precedence: these rules override anything in landing.md, product.md, or upstream skills. Perpetual/infinite micro-animations (pulse loops, typewriters, infinite carousels on every card) are NOT a default at any motion intensity; they appear only when the user explicitly asks for an "alive"/showcase feel, and even then only on sections that semantically benefit (live status, feeds).

## 1. Should this animate at all?

Decide by frequency of exposure:

| Frequency | Decision |
|---|---|
| 100+ times/day (keyboard shortcuts, command palette) | No animation. Ever. |
| Tens of times/day (hover, list navigation) | Remove or drastically reduce |
| Occasional (modals, drawers, toasts) | Standard animation |
| Rare/first-time (onboarding, celebrations) | Can add delight |

Never animate keyboard-initiated actions. Every animation needs a one-sentence purpose: hierarchy, storytelling, feedback, or state transition. "It looked cool" is not a purpose; GSAP-because-GSAP-is-installed is amateur.

## 2. Easing

- Entering or exiting → **ease-out** (starts fast, feels responsive)
- Moving/morphing on screen → ease-in-out
- Hover/color change → ease
- Constant motion (marquee, progress) → linear
- **Never ease-in on UI** (delays the moment the user watches most closely). No bounce, no elastic, except subtle bounce (0.1-0.3) for drag-to-dismiss and playful gestures.

Built-in CSS easings are too weak. Use custom curves:

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);      /* strong ease-out for UI */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);  /* on-screen movement */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);   /* iOS-like drawers */
```

## 3. Duration

| Element | Duration |
|---|---|
| Button press feedback | 100-160ms |
| Tooltips, small popovers | 125-200ms |
| Dropdowns, selects | 150-250ms |
| Modals, drawers | 200-500ms |
| Marketing/explanatory | Can be longer |

UI animations stay under 300ms. Perceived speed compounds: a 180ms ease-out select feels faster than a 400ms one; a fast spinner makes loading feel shorter. Asymmetric timing: slow where the user is deciding (hold-to-delete 2s linear), fast where the system responds (release 200ms ease-out). Exit slightly faster than enter.

## 4. Springs

Use for: drag with momentum, interruptible gestures, decorative mouse-tracking, "alive" elements. Apple-style config is easiest to reason about: `{ type: "spring", duration: 0.5, bounce: 0.2 }`. Springs maintain velocity when interrupted; CSS keyframes restart from zero, so prefer transitions/springs for anything rapidly re-triggered.

Never drive continuous values (mouse position, scroll) through React `useState`; use `useMotionValue` / `useTransform` / `useScroll` outside the render cycle.

## 5. Component micro-rules

- Pressables: `transform: scale(0.97)` on `:active`, transition 160ms ease-out. Subtle range 0.95-0.98.
- Never enter from `scale(0)`. Start `scale(0.95)` + `opacity: 0`.
- Popovers scale from their trigger: `transform-origin: var(--radix-popover-content-transform-origin)` (or Base UI `--transform-origin`). Modals stay centered.
- Tooltips: delay the first, open adjacent ones instantly with no animation (`transition-duration: 0ms` on `[data-instant]`).
- CSS transitions over keyframes for anything interruptible (toasts, toggles).
- Crossfade looks like two overlapping objects? Add `filter: blur(2px)` during the transition to bridge it. Keep blur < 20px (Safari cost).
- Modern entry: `@starting-style` block instead of the `useEffect`-mounted-class pattern, with the data-attribute fallback where support demands.
- Stagger entering groups 30-80ms apart; stagger is decorative, never blocks interaction. Parent `variants` and children must share one client component tree.

## 6. Scroll choreography (canonical skeletons)

Library choice: **Motion (`motion/react`)** for UI/state/reveal work. **GSAP + ScrollTrigger** only for real pin/scrub scrolltelling, isolated in leaf client components with cleanup. Three.js for canvas scenes only. Never mix GSAP/Three with Motion in one component tree.

For simple "appear on scroll", prefer Motion `whileInView`:

```tsx
<motion.li
  initial={reduce ? false : { opacity: 0, y: 24 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true, amount: 0.3 }}
  transition={{ duration: 0.6, delay: i * 0.06, ease: [0.16, 1, 0.3, 1] }}
/>
```

Sticky-stack and horizontal-pan sections must pin correctly: `start: "top top"` (not `"top center"`), `pin: true`, `scrub`, distance computed from track width, `invalidateOnRefresh: true`, `gsap.context` + `ctx.revert()` cleanup, `useReducedMotion` bail-out. The common failure is the trigger firing mid-viewport so the user sees half a slide.

Reveal animations enhance an already-visible default; never gate content visibility on a class-triggered transition (headless renderers and hidden tabs never fire it, section ships blank).

### Forbidden

- `window.addEventListener("scroll", ...)` in any form. Use `useScroll()`, ScrollTrigger, IntersectionObserver, or CSS `animation-timeline: view()`.
- `requestAnimationFrame` loops touching React state.
- One identical entrance reflexively applied to every section. Each reveal should fit what it reveals; suppressing the reflex is never a reason to ship a page with zero motion.

## 7. Performance

- Animate only `transform` and `opacity` (premium materials like blur/clip-path/mask allowed when they materially improve the effect and stay smooth). Never `top/left/width/height/padding`.
- Framer Motion shorthand props (`x`, `y`, `scale`) run on the main thread. Under load (page hydration, busy main thread) use the full string: `animate={{ transform: "translateX(100px)" }}`, or plain CSS animations, which run off-thread.
- WAAPI (`element.animate(...)`) gives JS control with CSS performance for programmatic one-shots.
- Don't update inheritable CSS variables on a parent per-frame (style recalc on all children); set `transform` directly on the element.
- Grain/noise overlays only on `fixed inset-0 pointer-events-none` layers, never scrolling containers. `backdrop-filter` only on fixed/sticky elements. `will-change: transform` sparingly.

## 8. Accessibility

- `prefers-reduced-motion: reduce` is mandatory for everything beyond hover states: keep opacity/color crossfades that aid comprehension, remove positional movement, collapse infinite loops/parallax/scroll-hijack/magnetic physics to static.
- Hover animations behind `@media (hover: hover) and (pointer: fine)` (touch devices fire hover on tap).
- Gestures: momentum-based dismissal (velocity > ~0.11 dismisses regardless of distance), damping past boundaries instead of hard stops, pointer capture during drag, ignore extra touch points mid-drag.

## 9. Review checklist (motion pass)

| Issue | Fix |
|---|---|
| `transition: all` | Name exact properties |
| `scale(0)` entry | `scale(0.95)` + `opacity: 0` |
| `ease-in` on UI | `ease-out` or custom curve |
| Center-origin popover | Trigger-anchored origin (modals exempt) |
| Animation on keyboard action | Remove |
| Duration > 300ms on UI element | 150-250ms |
| Hover without media query | Gate it |
| Keyframes on rapidly-triggered element | CSS transitions |
| Same enter/exit speed | Exit faster |
| Everything mounts at once | 30-80ms stagger |
| Infinite loop on informational section | Remove (loops need explicit request + semantic benefit) |

Review animations the next day or in slow motion (DevTools animations panel); timing issues are invisible at full speed. Test gestures on real devices.
