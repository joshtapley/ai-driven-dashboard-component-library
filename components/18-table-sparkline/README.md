# Leaderboard table with sparklines

**Category:** Tables · **Tags:** ranking, sparkline, rank change, share bar, top N

A ranked product leaderboard with a 12-week sparkline per row, rank movement arrows, the current value, change vs last week and a share-of-total bar; every column sorts.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Top-N lists where movement matters: products, pages, campaigns, reps
- Readers ask 'who's up, who's down, and is it a trend or a blip?'
- A compact replacement for a multi-line chart with too many lines

## Avoid it when
- Rows don't have a time series
- More than ~25 rows without paging

## Anatomy
- Rank number + movement (▲2 / ▼1 / –) since last week, muted
- Name with category in muted text
- Sparkline 96×24: 1.5px line in ink-2, last point dot in accent, min/max not marked
- Value: tabular, right-aligned
- Week-over-week change: signed % in up/down colour
- Share of total: thin bar on a track + % label

## Data shape
```
[{ name: "Trail Runner 2", category: "Footwear", weekly: [12 numbers] }, …] — rank and change derived
```

## Interactions
- Sort by rank, name, units, change or share (headers are buttons)
- Hover a sparkline: week-by-week tooltip
- Hover a row: wash highlight

## Accessibility
- Semantic table, aria-sort
- Rank movement uses glyph + number
- Sparklines have aria-labels summarising start → end

## Design tokens used
`--s1`, `--ink-2`, `--track`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a ranked leaderboard table with sparklines in one self-contained HTML file. 15 seeded fictional products, each with 12 weeks of unit sales. Columns: rank with movement since last week (▲2 / ▼1 / – in muted text), product name with category in muted text, a 96×24 inline SVG sparkline (1.5px secondary-ink line, last point dot in the accent colour), this week's units (tabular, right-aligned), week-over-week change as signed % in success/danger colour, and share of total as a thin bar on a pale track with a % label. All headers are sort buttons with aria-sort and ▲/▼. Hovering a sparkline shows a tooltip for the hovered week. Rows 40px, hairline dividers, hover wash. CSS variables for every colour, light and dark themes.
