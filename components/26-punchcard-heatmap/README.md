# Day × hour heatmap with marginals

**Category:** Charts · **Tags:** punchcard, time of day, staffing, marginal bars

A 7 × 24 weekday-by-hour heatmap with marginal bar charts on top (by hour) and right (by day), a metric switch, and crosshair highlighting of the hovered row and column.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Planning staffing, send times or maintenance windows
- You suspect patterns by both time of day and day of week
- Data is aggregated to hour buckets

## Avoid it when
- You need trend across dates (this collapses dates)
- Values are sparse (most cells zero) — use a dot plot

## Anatomy
- Grid: 24 columns (hours) × 7 rows (Mon–Sun), 2px gaps, 3px radius, sequential ramp
- Hour labels every 3 hours (12a, 3a, 6a…), day labels left
- Top marginal: column bars = total per hour; right marginal: row bars = total per day; both in de-emphasis grey with the hovered bar in accent
- Peak cell outlined in ink with a 'Peak' annotation
- Legend ramp with min/max values

## Data shape
```
{ metric: "tickets", cells: [[24 values for Mon], …7 rows] }
```

## Interactions
- Metric switch (Tickets / Avg wait) recolours and recomputes marginals
- Hover a cell: value, % of the day, and its row/column marginals light up

## Accessibility
- aria-label per cell
- Peak called out in text
- Marginals give exact totals via tooltip

## Design tokens used
`--seq-0 … --seq-6`, `--de-emph`, `--s1`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a weekday × hour heatmap with marginal bar charts in one self-contained HTML file using inline SVG. Grid of 7 rows (Mon–Sun) × 24 columns (hours) with 2px gaps and 3px radius, shaded on a sequential single-hue ramp; hour labels every 3 hours (12a, 3a, 6a…) and day labels on the left. Above the grid, a column chart of totals per hour; to the right, a bar chart of totals per day; both in de-emphasis grey. Outline the peak cell in ink with a small 'Peak' label. On hover, show a tooltip (value, share of that day) and light up the matching hour and day marginal bars in the accent colour. A segmented control switches between two metrics (ticket volume = sum marginals; average wait = mean marginals). Include a gradient legend with min and max. Seeded synthetic data with business-hours and weekend patterns. CSS variables for every colour, light and dark themes.
