# Waffle chart (part of 100)

**Category:** Charts · **Tags:** unit chart, percent, part to whole, isotype, storytelling

A 10 × 10 grid where each square is 1% — 'of every $100 we spend…' — with a dataset switch, a legend that highlights its squares on hover, and largest-remainder rounding so it always totals 100.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Communicating proportions to a general audience ('3 in 10 customers…')
- Shares between ~2% and ~80% for 2–5 categories
- Editorial or executive summary panels

## Avoid it when
- Shares under 1% matter (they vanish)
- Precise comparison between similar shares (use bars)

## Anatomy
- 10 × 10 squares, 3px gap, 3px radius; filled column-by-column so each category forms a solid block
- Categorical colours in fixed order; squares beyond the data in surface tint (when showing a single share)
- Headline sentence above: the biggest share stated in words
- Legend list: swatch, name, % — hover a row to dim other squares

## Data shape
```
{ title: "Of every $100 in operating spend", parts: [{ name: "Payroll", pct: 46.2 }, …] }
```

## Interactions
- Dataset switch (Spend / Headcount / Customers) re-flows the squares with a quick stagger
- Hover a legend row or a square: that category stays full colour, others dim
- Rounding uses largest remainder so squares always sum to 100

## Accessibility
- Headline sentence carries the main number in text
- Legend lists every share
- SVG aria-label lists all parts

## Design tokens used
`--s1 … --s5`, `--surface-2`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a 10×10 waffle chart in one self-contained HTML file with inline SVG, where each square is 1%. Squares have 3px gaps and 3px radius and fill column by column (top to bottom, left to right) so each category forms a contiguous block, coloured by categorical slots in fixed order. Round shares to whole squares with the largest-remainder method so they always total 100. Above the grid, a headline sentence states the largest share in words ('Payroll takes $46 of every $100'). Beside it, a legend list (swatch, name, %) where hovering a row or a square keeps that category in full colour and dims the rest. A segmented control switches between three seeded datasets and the squares recolour with a short staggered transition (skip under prefers-reduced-motion). CSS variables for all colours, light and dark themes.
