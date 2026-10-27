# Area chart

**Category:** Basic charts · **Tags:** area, volume over time, target line, date range, gradient

A single-series area chart for a volume measure: accent line over a soft fill anchored at zero, a dashed target line with a label, a date-range switch, and a crosshair that reports the value and the gap to target.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- One cumulative or volume-like measure over time where the filled mass helps (revenue, users, storage)
- You want a hero trend with more presence than a bare line
- Comparing against a single reference value

## Avoid it when
- Several overlapping series (fills hide each other — use lines or a stacked area)
- Values can be negative or the axis can't start at zero (an area implies a zero baseline)

## Anatomy
- 2px accent line with a fill from the line down to zero; fill is a vertical gradient from 22% to 2% opacity
- Always a zero baseline in axis grey
- Target: 1.5px dashed ink line with a right-aligned label
- Hairline grid, compact y ticks, adaptive x labels
- End dot with a surface ring and the latest value labelled

## Data shape
```
{ dates: ["2026-01-01", …], values: [daily numbers], target: 52000 }
```

## Interactions
- Range switch: 1M / 3M / 6M / YTD
- Hover: crosshair, value and difference from target

## Accessibility
- Single series, so the title names it (no legend box needed)
- Latest value and target printed as text
- SVG aria-label states the latest value vs target

## Design tokens used
`--s1`, `--ink`, `--grid`, `--axis`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a single-series area chart in one self-contained HTML file with inline SVG and no libraries. Seeded daily active users from January to Oct 24 with growth and weekly dips. Draw a 2px accent line and fill the area from the line to a zero baseline with a vertical linearGradient from about 22% to 2% opacity of the accent. Add a dashed 1.5px ink target line with a right-aligned 'Target 52K' label, hairline gridlines, compact y ticks and adaptive date labels. Mark the last point with an 8px dot and a surface ring and label its value. A segmented control switches the range (1M / 3M / 6M / YTD). Hover shows a crosshair with the date, value and difference from target. The axis always starts at zero. CSS variables for every colour, light and dark themes.
