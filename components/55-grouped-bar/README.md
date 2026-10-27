# Grouped bar chart

**Category:** Basic charts · **Tags:** clustered bar, side by side, comparison, orientation

Quarterly revenue for three channels as side-by-side bars within each quarter, switchable between vertical and horizontal, with legend toggles, optional value labels and per-group hover.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Comparing 2–4 series within each category and across categories at the same time
- Exact values per series matter (unlike stacked bars, every bar shares the zero baseline)
- Few categories (≤ 8)

## Avoid it when
- More than 4 series per group (use small multiples or a dot plot)
- The total per group is the main message (use stacked bars)
- Continuous time with many points (use lines)

## Anatomy
- Groups evenly spaced; bars inside a group touch with a 2px surface gap
- Each bar ≤ 24px thick, 4px rounded data end, square at the baseline
- Categorical slots in fixed order; legend toggles series without recolouring
- Hairline grid on the value axis, compact ticks
- Optional value labels at bar ends

## Data shape
```
{ labels: ["Q1", "Q2", "Q3", "Q4"], series: [{ name: "Online", values: [4 numbers] }, …3] }
```

## Interactions
- Orientation: Vertical / Horizontal
- Labels on/off
- Legend click hides/shows a series (one always stays)
- Hover a group: tooltip with every series and the group total

## Accessibility
- Legend present (≥ 2 series)
- Tooltip lists every value
- SVG aria-label summarises the largest bar

## Design tokens used
`--s1`, `--s2`, `--s3`, `--grid`, `--axis`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a grouped (clustered) bar chart in one self-contained HTML file with inline SVG and no libraries. Seeded quarterly revenue (Q1–Q4) for three channels (Online, Retail, Wholesale). Within each quarter, draw the channels' bars side by side with a 2px gap, each bar at most 24px thick with a 4px rounded data end and a square baseline end, in categorical slots 1–3. Add an orientation segmented control (Vertical / Horizontal) that redraws the same data with category labels on the appropriate axis, a Labels on/off toggle that prints values at bar ends, and a legend that hides/shows series without recolouring (never hide the last). Hairline gridlines and compact ticks on the value axis. Hovering a group shows a tooltip with each series and the group total. CSS variables for every colour, light and dark themes.
