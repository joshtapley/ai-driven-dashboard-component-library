# Calendar heatmap

**Category:** Charts · **Tags:** contribution graph, daily activity, seasonality, streaks

A GitHub-style year calendar: one square per day in week columns, shaded on a 5-step sequential scale, with month labels, a Less → More legend, streak and busiest-day stats, and click-to-inspect.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Daily data where weekday patterns and seasonality both matter (activity, sales, incidents, habits)
- You want a whole year in one compact panel
- Gaps and streaks are interesting

## Avoid it when
- Exact values must be compared (use a line or bar chart)
- Data is weekly or monthly

## Anatomy
- 53 week columns × 7 weekday rows; 2–3px gaps; 2px corner radius
- Mon / Wed / Fri labels on the left, month labels above the first week of each month
- 5 bins: zero is the surface tint; then four ramp steps by quantile
- Legend: 'Less' + 5 swatches + 'More'
- Stats strip: total, best day, longest streak, current streak
- Selected day outlined in ink with a detail line below

## Data shape
```
[{ date: "2026-01-01", count: 4 }, …] — one row per day
```

## Interactions
- Year switch (2025 / 2026)
- Hover a day: date and count
- Click a day: outlines it and shows that day's breakdown below
- Keyboard: arrow keys move the selection by day/week

## Accessibility
- Each cell has an aria-label with the date and count
- Arrow-key navigation; selection announced
- Binned legend explains the scale

## Design tokens used
`--seq-0 … --seq-6`, `--surface-2`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a GitHub-style calendar heatmap in one self-contained HTML file with inline SVG. Seeded daily counts for two years with weekday and seasonal patterns plus a few zero days. Layout: 53 week columns × 7 weekday rows (Monday first) of rounded 2px squares with small gaps, Mon/Wed/Fri labels on the left and month labels above the first week of each month. Colour by 5 bins: zero = a surface tint, then 4 sequential ramp steps by quantile. Add a 'Less ▢▢▢▢▢ More' legend, a stats strip (total, best day, longest streak, current streak), a year segmented control, hover tooltips, and click-to-select that outlines the day in ink and shows its detail under the chart; arrow keys move the selection (±1 day, ±7 days). Each cell has an aria-label. Scale cells to the container width. CSS variables for all colours, light and dark themes.
