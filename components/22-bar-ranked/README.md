# Ranked bar chart with highlight

**Category:** Charts · **Tags:** horizontal bar, top N, other bucket, average line, click to select

Horizontal bars ranked by value with a Top 5 / 10 / All control that folds the rest into 'Other', an average reference line, value labels at the tips and click-to-highlight.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Comparing a measure across categories with long names
- The ranking itself is the insight (top sellers, worst performers)
- You want one item called out against the rest

## Avoid it when
- Categories have a natural order (months, stages) — keep that order and use columns
- Part-to-whole is the point (use a 100% bar or waffle)

## Anatomy
- Label column left (right-aligned text), bars from a single baseline, ≤ 24px thick with 4px rounded tips
- Bars in one hue; highlighted bar in the accent, the rest in de-emphasis grey once something is selected
- 'Other' row last: a text summary (combined total and average) rather than a bar, so the remainder never flattens the scale
- Value label at each bar tip in secondary ink
- Average: 1px ink vertical line with a small 'Avg' label

## Data shape
```
[{ name: "Pacific Northwest", value: 1840000 }, …]
```

## Interactions
- Top N control folds the remainder into 'Other'
- Sort: value (desc) or name (A–Z)
- Click a bar to highlight it and show its rank/gap to average in the subtitle; click again to clear
- Hover: tooltip with value, share and rank

## Accessibility
- Bars are focusable buttons-in-SVG with aria-labels; Enter selects
- Values printed at tips
- Highlight uses colour plus a bold label

## Design tokens used
`--s1`, `--de-emph`, `--ink`, `--ink-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a ranked horizontal bar chart in one self-contained HTML file with inline SVG. 18 seeded categories (sales territories). Bars grow from one baseline, max 24px thick with 4px rounded tips and square at the baseline; labels right-aligned in a left column; value labels at the bar tips in secondary ink. Controls: Top 5 / Top 10 / All (fold the remainder into an 'Other' row that always sits last and is shown as text — combined total and average — rather than a bar, so it never flattens the scale) and Sort by value or name. Draw a 1px ink vertical line at the average with a small 'Avg' label. Clicking a bar highlights it in the accent colour and turns the rest de-emphasis grey; the subtitle then states its rank and gap to average; clicking again clears. Bars are keyboard-focusable (Enter selects). Hover tooltips with value, share of total and rank. CSS variables for all colours, light and dark themes.
