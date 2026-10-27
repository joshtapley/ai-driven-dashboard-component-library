# Line chart: this year vs last year vs target

**Category:** Charts · **Tags:** time series, crosshair, date range, legend toggle, cumulative

A time-series line chart with this year, last year and a dashed target, a date-range control (3M / 6M / YTD / 12M), cumulative vs periodic toggle, clickable legend and a shared crosshair tooltip.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Tracking a measure over time against a prior period and a plan
- The trend's shape matters more than individual values
- Up to 3–4 series on one shared axis

## Avoid it when
- Two measures with different units (never dual-axis — use two aligned charts)
- More than ~5 series (use small multiples)

## Anatomy
- Filters in one row above the chart: range control left, cumulative toggle right
- Series: current year 2px accent with 10% area wash; last year 1.5px grey; target 1.5px dashed ink
- Legend with line keys, each clickable to hide/show; plus direct end labels when lines don't collide
- Hairline horizontal grid, compact y ticks (0 / 50K / 100K), month or week x labels
- Crosshair: vertical hairline, a dot per visible series with surface ring, tooltip listing all values + variance vs target

## Data shape
```
{ dates: ["2026-01-01", …], cy: [daily values], py: [daily values], target: [daily values] }
```

## Interactions
- Range control re-slices and re-aggregates (daily ≤ 3M, weekly beyond)
- Cumulative toggle switches running totals on/off — useful against an annual target
- Legend click toggles a series; at least one stays visible
- Hover anywhere in the plot for the crosshair

## Accessibility
- Legend present (≥ 2 series); target distinguished by dash pattern, not just colour
- Tooltip text includes every value
- 'Table' toggle shows the aggregated numbers

## Design tokens used
`--s1`, `--de-emph`, `--ink`, `--grid`, `--axis` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an interactive time-series line chart in one self-contained HTML file with inline SVG (no libraries). Three series on ONE y-axis: this year (2px accent line, 10% area wash), last year (1.5px grey) and target (1.5px dashed ink), from seeded daily data through Oct 24. Put filters in one row above the chart: a segmented date-range control (3M / 6M / YTD / 12M — daily points for ≤3 months, weekly sums beyond) and a Cumulative toggle (running totals). Legend with line keys that toggle series on click (never hide the last one) plus direct end labels. Hairline grid, compact y ticks, month labels. Crosshair on hover: vertical hairline, a dot per visible series with a 2px surface ring and a tooltip with every value and this year's variance vs target. Add a Table toggle that swaps the chart for the aggregated numbers. CSS variables for every colour, light and dark themes.
