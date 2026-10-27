# Voronoi treemap

**Category:** Hierarchies · **Tags:** treemap, weighted voronoi, power diagram, part to whole, hierarchy, zoom

A two-level hierarchy (category › product line) packed into a circle as organic Voronoi cells whose areas match their values; click a category to zoom in and re-pack its lines to fill the circle.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing part-to-whole for a two-level hierarchy with a memorable, organic look (budgets, revenue mix, market share)
- Editorial or hero panels where a rectangular treemap feels too rigid
- Up to ~40 leaf cells

## Avoid it when
- Precise comparison of similar values (areas of irregular shapes are hard to compare — use bars)
- Deep hierarchies (beyond two levels, use a tree diagram or a zoomable rectangular treemap)
- Data that updates often (the layout is iterative and positions move)

## Anatomy
- Boundary: a circle; top-level cells are a weighted Voronoi (power) diagram whose areas converge to each category's share
- Second level: each category cell is subdivided the same way for its product lines
- Category colours: categorical slots 1–5; lines are tints of their category's hue
- Borders: 4px surface lines between categories, 1.5px between lines
- Labels: category name + share at each category's centroid (overview); line name + value inside cells large enough (zoomed)
- Side list: categories with value and share, doubling as zoom buttons

## Data shape
```
{ name: "Revenue", children: [{ name: "Electronics", children: [{ name: "Phones", value: 32 }, …] }, …] }
```

## Interactions
- Click a category (cell or side list) to zoom in; Back or Esc to return
- Hover a cell: tooltip with value, share of category and of total
- Layout is computed once per view (deterministic seed) and reused on resize

## Accessibility
- Side list gives every category value and share as text and acts as keyboard-accessible zoom buttons
- Zoomed view labels every line large enough to hold text; the rest are in tooltips and the list
- SVG aria-label lists the categories with shares

## Design tokens used
`--s1 … --s5`, `--surface`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a two-level Voronoi treemap in one self-contained HTML file with inline SVG and no libraries. Implement a weighted Voronoi (power diagram) layout yourself: each cell is the boundary polygon clipped by the half-planes 2(pj−pi)·x ≤ |pj|²−|pi|²−wj+wi for every other site j (Sutherland–Hodgman clipping). Iterate ~150 times: compute cells, move each site to its cell centroid, scale its weight by target area ÷ current area, cap each weight at the squared distance to its nearest neighbour site, and reset any empty cell. Seed sites deterministically inside the boundary. Use a circle (72-gon) as the top boundary for 5 categories, then subdivide each category cell for its 3–5 product lines. Colour categories with categorical slots 1–5 and lines as lighter tints of their category; separate categories with 4px surface-coloured borders and lines with 1.5px borders. Overview labels show category name and share at each centroid with a surface halo. Clicking a category (or its entry in a side list) zooms: re-pack its lines to fill the whole circle with name and value labels; Back or Esc returns. Hover tooltips show value and shares. Compute layouts in a fixed 500×500 space and scale via viewBox so resizing doesn't re-run them. CSS variables for every colour, light and dark themes.
