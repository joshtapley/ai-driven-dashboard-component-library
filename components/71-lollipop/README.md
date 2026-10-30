# Lollipop chart

**Category:** Basic charts · **Tags:** lollipop, dot plot, ranking, deviation, bar alternative

A bar chart's lighter cousin: a thin stem and a prominent dot per category, sorted by value. Switch between columns and rows, stem from zero or from the average (a diverging view that colours each side), and click a lollipop to highlight it while everything else steps back.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Ranking 6–25 categories where many bars would look heavy
- The end value matters more than the filled area
- Showing how each category sits above or below an average or target

## Avoid it when
- Values that are close together (the dots overlap; use bars or a dot plot with a zoomed axis)
- Part-to-whole comparisons (use stacked bars or a waffle)
- Negative and positive values on a zero baseline with no reference (use diverging bars)

## Anatomy
- Stems: 2px lines in the series colour from the baseline to the value; dots: 12px circles with a 2px surface ring so they read over gridlines
- Baseline: zero (axis line) or the average (a dashed reference line labelled with its value); in average mode stems above use --s1 and below use --s2, named in a legend
- Sorted by value by default, with an A–Z option; long labels switch the chart to rows
- Value labels at the dot end; gridlines in --grid along the value axis only
- Highlight: the clicked lollipop keeps its colour and gains a label, the rest turn --de-emph
- On load the stems grow from the baseline once (skipped for reduced motion)

## Data shape
```
[{ port: "Singapore", days: 3.1 }, …] plus the optional reference value (average or target)
```

## Interactions
- Orientation switch: Columns / Rows
- Baseline switch: Zero / Average
- Sort switch: By value / A–Z
- Click a lollipop (or press Enter on it) to highlight it; click again to clear
- Hover for the value and its difference from the average

## Accessibility
- The svg has an aria-label naming the top and bottom categories
- Each lollipop is a focusable group with its own aria-label
- Above / below average is shown by position and the legend, not colour alone
- Growth animation respects prefers-reduced-motion

## Design tokens used
`--s1`, `--s2`, `--de-emph`, `--grid`, `--axis`, `--ink`, `--ink-2`, `--muted`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a lollipop chart in one self-contained HTML file with inline SVG and no libraries. Twelve container ports with an average dwell time in days, sorted by value. Each category is a 2px stem in the accent colour from the baseline to the value, ending in a 12px dot with a 2px ring in the card surface colour, with the value labelled past the dot; gridlines only along the value axis. Add three segmented controls: Columns / Rows (rows put long labels on the left), Zero / Average baseline (average mode draws a dashed reference line with its value and stems out from it, accent colour above and a second colour below, with a legend), and By value / A–Z sort. Clicking a lollipop highlights it (others turn a muted grey) and clicking again clears; hovering shows the value and the difference from the average. Stems grow from the baseline once on load, skipped under prefers-reduced-motion. Focusable lollipops with aria-labels, CSS variables for every colour, light and dark themes.
