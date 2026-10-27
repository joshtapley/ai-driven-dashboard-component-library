# Expandable pivot table

**Category:** Tables · **Tags:** hierarchy, tree table, subtotals, drill down, profit and loss

A three-level tree table (category › sub-category › product) with subtotals, expand/collapse per row or all at once, % of total bars and a profit-margin column that flags losses.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Data has a natural hierarchy and people drill from summary to detail
- Finance-style reviews where subtotals must be exact
- Replacing a pivot table exported from Excel

## Avoid it when
- The hierarchy is deeper than 3–4 levels (use a treemap or a drill-through page)
- Only one level exists

## Anatomy
- Indented name column: 20px per level, chevron button for expandable rows, leaf rows without a chevron
- Level-1 rows semibold on a faint tint; deeper levels regular
- Numeric columns right-aligned, tabular: Sales, Profit, Margin, % of total
- Negative profit in danger text with a minus sign; margin < 0 gets a ▼ glyph
- % of total: thin bar scaled to the largest top-level row + number
- Grand total row pinned at the bottom, top border

## Data shape
```
[{ name: "Furniture", children: [{ name: "Chairs", children: [{ name: "Task Chair Pro", sales: 41200, profit: 6100 }, …] }, …] }, …] — parents are summed
```

## Interactions
- Click a chevron (or Enter/Space) to expand/collapse that node
- Expand all / Collapse all buttons
- Measure switch for the bar column: % of total sales or % of total profit

## Accessibility
- role=treegrid with aria-level and aria-expanded on rows
- Chevrons are buttons with labels
- Losses marked with sign and glyph, not only colour

## Design tokens used
`--s1`, `--surface-2`, `--grid`, `--down`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an expandable pivot (tree) table in one self-contained HTML file. Seeded data: 3 categories › 3–4 sub-categories each › 3–5 products each, with sales and profit at the leaf level; parents are summed. Columns: indented name (20px per level, chevron button on expandable rows, aria-expanded), Sales, Profit (negative in danger text with a minus sign), Margin (profit ÷ sales, ▼ glyph if negative) and '% of total' as a thin bar plus number. Level-1 rows are semibold on a faint tint; a grand-total row sits at the bottom with a top border. Add Expand all / Collapse all buttons and a segmented control switching the bar column between share of sales and share of profit. Use role=treegrid with aria-level. Tabular, right-aligned numbers. CSS variables for every colour, light and dark themes.
