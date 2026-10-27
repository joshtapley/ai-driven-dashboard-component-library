# Horizontal bar chart

**Category:** Basic charts · **Tags:** bar, ranking, long labels, prior period marker, sort

Product categories as horizontal bars with readable long labels, sorting by value or name, value labels at the tips, and an optional last-year tick on each bar for a quiet comparison.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Comparing a measure across unordered categories, especially with long names
- Ranking is useful but you also want an alphabetical lookup
- Adding a light prior-period comparison without a second bar

## Avoid it when
- Time on the category axis (use columns or a line)
- More than ~25 categories (show the top N and fold the rest)

## Anatomy
- Bars ≤ 24px thick (here 18px) from a single left baseline, 4px rounded data end
- Category labels right-aligned in a left column, sized to the longest label
- Value labels at the bar tips in secondary ink
- Last year: a 2px ink tick across each bar, explained in the legend
- Hairline vertical grid with compact ticks at the bottom

## Data shape
```
[{ category: "Kitchen & dining", value: 412000, lastYear: 368000 }, …]
```

## Interactions
- Sort: Value / A–Z
- Last-year ticks on/off
- Hover a row: value, last year and change

## Accessibility
- Rows are labelled text, values printed at tips
- Tick meaning stated in the legend and tooltip
- SVG aria-label lists the top three

## Design tokens used
`--s1`, `--ink`, `--ink-2`, `--grid`, `--axis` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a horizontal bar chart in one self-contained HTML file with inline SVG and no libraries. 10 seeded product categories with long names, each with this year's sales and last year's. Bars are 18px thick from a single left baseline with a 4px rounded data end, in the accent colour; category labels are right-aligned in a left column sized to the longest label; value labels sit at the bar tips in secondary ink; hairline vertical gridlines with compact tick labels along the bottom. Add a Sort control (Value / A–Z) and a 'Last year' toggle that draws a 2px ink tick across each bar at last year's value, with a small legend explaining bar vs tick. Hover a row for value, last year and % change. CSS variables for every colour, light and dark themes.
