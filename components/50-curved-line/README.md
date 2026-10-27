# Curved line chart

**Category:** Basic charts · **Tags:** smooth line, monotone, spline, step, moving average

Daily sessions as faint raw points with a smoothed 7-day average on top, and a curve switch between monotone (no overshoot), natural spline and step interpolation, so you can see how each curve treats the same data.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The trend matters more than each point and a gentle curve reads calmer than zig-zags
- Noisy daily data where a rolling average tells the story
- Step curves for values that change at moments (prices, plan tiers, headcount)

## Avoid it when
- Few points (curves imply data between them that doesn't exist)
- Exact values at each point matter more than the shape
- Natural splines on data near zero or bounded values (they overshoot)

## Anatomy
- Raw daily values: 1.5px line in de-emphasis grey with no markers
- 7-day average: 2.5px accent curve
- Curve options: Monotone (Fritsch–Carlson; never overshoots the data), Natural (Catmull–Rom style; may overshoot), Step (holds each value until the next)
- Weekend bands as faint tints behind the plot
- Legend for both series; crosshair tooltip with raw and average

## Data shape
```
{ days: ["2026-08-26", …60], sessions: [60 numbers] } — the average is computed on the page
```

## Interactions
- Curve switch: Monotone / Natural / Step
- Show raw data on/off
- Hover: crosshair with the day, raw sessions and the 7-day average

## Accessibility
- Legend for both series; the average is also in the tooltip
- Weekend bands are context only, not data
- SVG aria-label states the latest average

## Design tokens used
`--s1`, `--de-emph`, `--surface-2`, `--grid`, `--axis` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a curved line chart in one self-contained HTML file with inline SVG and no libraries. Seeded daily website sessions for 60 days with weekly seasonality (weekend dips) and noise. Draw the raw daily series as a 1.5px de-emphasis grey line and a 7-day rolling average as a 2.5px accent curve. Add a curve-type segmented control: Monotone (implement Fritsch–Carlson monotone cubic interpolation so the curve never overshoots), Natural (Catmull–Rom style cubic through the points) and Step (step-after). Shade weekends with faint bands, use hairline gridlines, compact y ticks and week labels on x. A toggle shows/hides the raw series. Legend for both series; hover crosshair tooltip with the date, raw value and average. CSS variables for every colour, light and dark themes.
