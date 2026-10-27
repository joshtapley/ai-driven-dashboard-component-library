# Vertical bar (column) chart

**Category:** Basic charts · **Tags:** column, bar, negative values, target line, highlight

Monthly profit as columns that grow up from zero for gains and down for losses, with rounded data ends, an optional target line, best/worst highlighting and value labels on demand.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Comparing a measure across ordered categories, especially time periods (months, quarters)
- Values can be negative and the sign matters
- Up to ~24 columns

## Avoid it when
- Long category names (use horizontal bars)
- Continuous time with many points (use a line)
- Part-to-whole (use stacked bars or a waffle)

## Anatomy
- Columns ≤ 24px wide, single hue; 4px rounded data end, square at the zero baseline
- Negative columns grow downward in the diverging negative hue; the zero line is axis grey and heavier than the grid
- Highlight mode: best and worst months keep their colour and get labels, the rest go de-emphasis grey
- Optional target: 1.5px dashed ink line with label
- Value labels: off, all (on the cap), or highlights only

## Data shape
```
{ labels: ["Jan", …12], values: [41200, -8300, …] }
```

## Interactions
- Labels: None / All / Best & worst
- Target line on/off
- Hover a column: value and change vs previous month

## Accessibility
- Single series — the title names it
- Negative values carry a minus sign in labels and tooltips, not just colour
- SVG aria-label names the best and worst months

## Design tokens used
`--s1`, `--div-neg`, `--de-emph`, `--axis`, `--grid`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a column (vertical bar) chart in one self-contained HTML file with inline SVG and no libraries. Seeded monthly profit for 12 months including two loss months. Columns are at most 24px wide in the accent colour with a 4px rounded data end and a square end at the zero baseline; negative columns grow downward in the diverging negative colour. The zero line is a heavier axis-grey line; other gridlines are hairline. Controls: value labels None / All / Best & worst (in the last mode, the best and worst months keep their colour and get labels while others turn de-emphasis grey), and a Target line toggle (dashed ink line with a label). Hover tooltips show the value and the change vs the previous month. Labels sit on the column cap (above positives, below negatives). CSS variables for every colour, light and dark themes.
