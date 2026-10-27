# Bullet chart list

**Category:** Gauges · **Tags:** bullet graph, target vs actual, qualitative bands, Stephen Few

A stack of horizontal bullet charts — actual bar, target tick, prior-year marker and three grey performance bands — with % of target and a sort control.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Many metrics need actual vs target in little space (the dense replacement for a wall of gauges)
- Each metric has its own scale and its own 'poor / satisfactory / good' bands
- You want prior period as a secondary comparison

## Avoid it when
- There is no target or band to compare against (use a plain bar)
- The audience needs a trend (pair with a sparkline column)

## Anatomy
- Label column: metric name + unit
- Three bands in stepped neutral greys (darkest = poor) behind the bar, full row height
- Actual bar: one-third of band height, accent colour, 4px rounded end
- Target: 2px ink tick, taller than the bar
- Prior year: small hollow diamond marker
- Value + % of target on the right; % in up/down text colour

## Data shape
```
[{ name: "Revenue", unit: "$K", actual: 270, target: 250, prior: 231, zones: [150, 225, 300] }, …]
```

## Interactions
- Sort: original order, % of target, or gap to target
- Hover a row: actual, target, prior year and band reached

## Accessibility
- % of target written as text with a ▲/▼ glyph
- Each row has an aria-label summarising actual vs target

## Design tokens used
`--s1`, `--surface-2`, `--axis`, `--ink`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a list of horizontal bullet charts in one self-contained HTML file with inline SVG (no libraries). One row per metric, each with its own scale from 0 to the top of its range. In each row draw: three qualitative bands as stepped neutral greys (darkest = poor) spanning the row height; the actual value as an accent bar one-third the band height with a 4px rounded end; a 2px ink target tick taller than the bar; a small hollow diamond for the prior-year value. A left label column shows the metric name and unit; a right column shows the actual value and % of target with ▲/▼ in success/danger text colours. Add a segmented sort control (Default / % of target / Gap) and hover tooltips. Rows animate to their new positions when sorted. Include a tiny legend explaining bar, tick, diamond and bands. CSS variables for all colours, light and dark themes.
