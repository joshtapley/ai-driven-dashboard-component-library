# Treemap and sunburst

**Category:** Hierarchies · **Tags:** treemap, sunburst, part to whole, hierarchy, nested, drill down, squarified

Revenue by department and category as a squarified treemap or a two-ring sunburst. Area (or angle) is share of the total; click a department to zoom in and the breadcrumb to zoom back out.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Part-to-whole with two levels (department › category, region › country, team › person)
- 10–60 leaves where the big contributors matter more than exact comparisons
- Letting readers drill from the whole into one branch

## Avoid it when
- Precise comparisons between similar values (use a sorted bar chart)
- Values that can be negative (area can't show them)
- Deep hierarchies (more than three levels: use a collapsible tree)
- Only a handful of parts with no nesting (use a bar chart or waffle)

## Anatomy
- Treemap: departments as squarified blocks with a 20px header strip naming them; categories tiled inside with 2px surface gaps
- Sunburst: departments on the inner ring, categories on the outer ring, a hole in the middle showing the total (or the zoomed department)
- Colour: each department takes a categorical slot (1–5); its categories are lighter-to-darker tints of that colour, largest darkest
- Labels show the name, plus the value and share when there's room; tiles too small for text rely on the tooltip
- Breadcrumb above the chart: All departments › Electronics

## Data shape
```
[{ name: "Electronics", children: [{ name: "Phones", value: 18.4 }, …] }, …] — values in $M
```

## Interactions
- Layout: Treemap / Sunburst
- Labels: Names / Names and values
- Click (or Enter on) a department or one of its categories to zoom into that department; click the breadcrumb, the centre or press Escape to zoom out
- Hover a tile or arc for its value, share of its department and share of the total

## Accessibility
- Each tile and arc is focusable with an aria-label giving name, value and share
- The breadcrumb is a nav with buttons
- Departments differ by position and labels as well as colour
- The svg has an aria-label naming the three largest departments

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--s5`, `--surface`, `--ink`, `--muted`, `--grid` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a treemap and sunburst in one self-contained HTML file with inline SVG and no libraries. Data: an online store's revenue in $M for five departments (Electronics, Fashion, Home, Sports, Beauty), each with 3–5 categories (19 leaves). Treemap: use the squarified algorithm; departments are blocks with a 20px header naming them and their total, categories tile inside with 2px surface gaps. Sunburst: departments on an inner ring, categories on an outer ring, angle = share, a centre circle showing the total. Each department takes a categorical colour; its categories are tints of it (largest darkest). Labels show name, and value and share when there's room. Controls: Layout Treemap / Sunburst and Labels Names / Names and values. Clicking a department or category zooms into that department (it fills the chart), with a breadcrumb 'All departments › Electronics'; the breadcrumb, the sunburst centre or Escape zooms out. Tiles and arcs are focusable (Enter zooms) with aria-labels; hover shows value, share of department and share of total. CSS variables for every colour, light and dark themes.
