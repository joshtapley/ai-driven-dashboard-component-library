# Scatter plot with trend line

**Category:** Basic charts · **Tags:** scatter, correlation, relationship, trend line, bubble, quadrants, regression

One dot per store, marketing spend against revenue, coloured by region. Add a least-squares trend line with its R², size dots by footfall to make it a bubble chart, and split the plot into quadrants at the medians to name the stand-outs.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing whether two measures move together (spend and revenue, price and volume, tenure and salary)
- Spotting outliers and clusters among 20–500 items
- Sorting items into four groups with quadrant lines (high spend, low return …)

## Avoid it when
- One of the measures is time (use a line chart)
- Thousands of overlapping points (use a hexbin or 2D density)
- Readers need exact values for each item (use a table)

## Anatomy
- x and y on linear scales with horizontal and vertical hairline grids and compact tick labels, both axes titled
- Dots: radius 5 (or 4–16 by area in bubble mode), 1px surface ring, 85% opacity so overlaps show
- Colour = region, categorical slots 1–4, with legend chips that dim a region
- Trend line: least-squares fit across the visible points, 2px ink dashed, labelled with its slope in words and R²
- Quadrants: dashed lines at the median x and y with a muted name in each corner
- Highlight: the hovered region keeps its colour, others drop to 25%

## Data shape
```
[{ store: "Store 104", region: "North", spend: 42000, revenue: 610000, footfall: 18400 }, …]
```

## Interactions
- Trend line: On / Off
- Size: Same / By footfall (bubble chart)
- Quadrants: Off / Medians
- Region chips dim or show each region; the trend line refits to what's shown
- Hover a dot for the store, region, spend, revenue, return per $ and footfall

## Accessibility
- The svg has an aria-label with the number of stores, the correlation in words and R²
- Region is shown by colour plus the legend and tooltip
- Dimming keeps hidden regions' shape visible
- Trend summary is printed as text above the chart

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a scatter plot in one self-contained HTML file with inline SVG and no libraries. Seeded data: 120 fictional stores in four regions, each with marketing spend ($8k–$80k), revenue (roughly 12× spend with noise and a few outliers) and footfall. x = spend, y = revenue, both linear with hairline grids, compact tick labels and axis titles. Dots have radius 5, a 1px surface ring and 85% opacity, coloured by region with legend chips that dim a region. Add three segmented controls: Trend line On / Off (least-squares fit across the visible points, a 2px dashed ink line, with a sentence above the chart such as 'Each extra $1k of spend comes with about $11k more revenue · R² 0.71'), Size Same / By footfall (area-scaled bubbles, radius 4–16, drawn largest first), and Quadrants Off / Medians (dashed lines at the median spend and revenue with muted corner labels like 'High spend, high revenue'). Hovering a legend chip highlights that region. Tooltips show store, region, spend, revenue, revenue per $ of spend and footfall. aria-label on the svg summarising the relationship, CSS variables for every colour, light and dark themes.
