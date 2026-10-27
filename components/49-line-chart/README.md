# Line chart

**Category:** Basic charts · **Tags:** line, multi-series, time series, crosshair, markers

The everyday multi-series line chart: three channels over twelve months with straight segments, a toggleable legend, optional point markers, direct end labels and a shared crosshair tooltip.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing change over continuous time for 1–5 series on one scale
- Comparing trends and crossovers between a few categories
- The default answer to 'how did X move over time?'

## Avoid it when
- Categories without an order (use bars)
- Two measures with different units (never dual-axis — use two aligned charts)
- More than ~5 series (use small multiples or highlight one)

## Anatomy
- Series lines 2px, round joins, categorical slots in fixed order
- Optional markers: 8px dots with a 2px surface ring
- Hairline horizontal grid, compact y ticks starting at zero, month labels on x
- Legend with line keys that toggle series; direct end labels when lines don't collide
- Crosshair: hairline + a dot per series + tooltip with every value

## Data shape
```
{ labels: ["Jan", …12], series: [{ name: "Online", values: [12 numbers] }, …] }
```

## Interactions
- Click a legend item to hide/show a series (one always stays)
- Markers on/off
- Y axis: from zero / fit to data
- Hover anywhere for the crosshair tooltip

## Accessibility
- Legend present for ≥ 2 series plus direct labels
- Tooltip text lists every value
- SVG aria-label summarises the latest values

## Design tokens used
`--s1`, `--s2`, `--s3`, `--grid`, `--axis`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a multi-series line chart in one self-contained HTML file with inline SVG and no libraries. Three seeded series (Online, Retail, Wholesale revenue) over 12 months. Lines are 2px with round joins in categorical slots 1–3; optional 8px point markers with a 2px surface ring (segmented toggle). Hairline horizontal gridlines, compact y ticks ($0, $50K, $100K) and month labels; a second toggle switches the y axis between starting at zero and fitting the data (with padding). A legend with line keys toggles series (never hiding the last one), and direct end labels sit at the right of each line unless they would collide. Hover shows a crosshair: a vertical hairline, a dot per visible series and a tooltip listing every value. CSS variables for every colour, light and dark themes.
