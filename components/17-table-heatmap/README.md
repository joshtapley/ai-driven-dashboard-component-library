# Highlight table (heatmap table)

**Category:** Tables · **Tags:** conditional formatting, matrix, crosstab, totals

A region × month crosstab where every cell is shaded on a sequential ramp, with a switch to scale colour across the whole table, within each row, or within each column, plus marginal total bars.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Two categorical dimensions and one measure, and people want both exact numbers and the pattern
- Spotting seasonality per region, or which region leads each month
- Replacing a grid of numbers that nobody reads

## Avoid it when
- One dimension has more than ~20 members (switch to a heatmap without numbers)
- Signed values (use a diverging ramp version)

## Anatomy
- Row headers left, column headers top, both sticky in scroll
- Cells: number centred, tabular figures; fill from the 7-step sequential ramp; text ink switches by fill luminance
- Totals column and row: plain numbers with thin bars, not shaded — they are a different scale
- Scale switch: Whole table / By row / By column
- Crosshair highlight: hovering a cell outlines its row and column headers

## Data shape
```
{ rows: ["Northeast", …], cols: ["Jan", …], values: [[…], …] }
```

## Interactions
- Scale switch re-shades without moving anything
- Hover a cell: tooltip with value, share of row and of column; its row and column headers highlight
- Click a header to sort rows by that month (or columns stay chronological)

## Accessibility
- Real table with scope attributes
- Every value printed — colour is a reading aid, not the data
- Ink colour picked per cell for contrast

## Design tokens used
`--seq-0 … --seq-6`, `--s1`, `--grid`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a highlight table (heatmap crosstab) in one self-contained HTML file. Rows are 6 regions, columns are 12 months, cells hold seeded sales values printed in tabular figures and shaded from a 7-step single-hue sequential ramp, with white or dark text chosen per cell by luminance. Add a Totals column and Totals row shown as plain numbers with thin inline bars (not shaded, since they're a different scale). A segmented control switches colour scaling between Whole table, By row and By column. Hovering a cell shows a tooltip with value, share of its row and share of its column, and highlights its row and column headers. Clicking a month header sorts the rows by that month (click the Region header to reset). Semantic <table> with scope attributes and a small legend of the ramp. CSS variables for all colours, light and dark themes.
