---
name: apply-design-system
description: Use when generating a design system, auditing visual consistency, or checking for generic AI-design patterns. Three modes (generate tokens, UI scoring 0-10, slop detection). Triggers on "design system", "visual audit", "slop check".
---

# Apply Design System

Pick a side. These are the rulings, not a tutorial. Framework-agnostic — the visual half that `frontend-patterns` (Svelte specifics) leaves open. Three jobs: generate a token set, audit a UI, or catch AI slop.

## Generate

| Rule | Why |
|------|-----|
| Extract before you invent | Read existing CSS/Tailwind/styled-components first; the codebase is the source of truth, not your taste. |
| One scale per axis | Spacing on a 4px/8px step, type on a modular scale. No arbitrary values. |
| Name by role, not value | `--color-surface`, not `--color-gray-100`. Values change; roles don't. |
| Ship three artifacts | `design-tokens.json`, CSS custom properties, and a `DESIGN.md` stating the rationale for each decision. |

Competitor research is optional, not a gate. Use a browser MCP if one is present; when none is available, work from the codebase and the brief alone — never block on a tool that isn't there.

## Audit

Score each axis 0-10. Every score cites a `file:line` example as evidence; a score without one is an opinion, not an audit. Anything below 8 also ships an exact fix.

The axes that earn their keep:

- **Token adherence** — your palette and scale, or scattered hex and magic numbers?
- **Type hierarchy** — clear h1 > h2 > body > caption, or flat?
- **Spacing rhythm** — one scale, or arbitrary gaps?
- **Component consistency** — do similar elements look similar?
- **Responsive integrity** — fluid, or broken at breakpoints?
- **State coverage** — hover, focus, loading, empty, error all handled?
- **Accessibility** — contrast ratios, focus rings, touch targets.

## Slop check

Flag and kill the generic AI-design tells:

- Purple-to-blue gradient as the default on everything.
- Glassmorphism cards with no depth purpose.
- Rounded corners on elements that read as flat (tables, code blocks).
- Scroll-triggered animation that delays the content.
- Centered hero text over a stock gradient.
- A personality-free sans stack picked by default.
