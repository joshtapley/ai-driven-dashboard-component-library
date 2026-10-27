# Radial Sankey

**Category:** Flows & networks · **Tags:** sunburst flow, budget allocation, hierarchy flow, circular sankey

A budget flowing outward from a centre total through departments to programmes: concentric rings of arcs with curved bands fanning between them, coloured by department, with hover tracing and a list view.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- A total splits into categories and then sub-categories and you want the split to feel like a flow (budgets, revenue allocation, headcount plans)
- Hero or summary panels where a sunburst feels too static
- 2 levels, up to ~30 outer items

## Avoid it when
- Flows recombine or cross between branches (use a regular Sankey)
- Precise value comparison (pair with the list view or bars)
- Deep hierarchies (beyond two levels the outer ring gets crowded)

## Anatomy
- Centre: total value and label
- Ring 1: department arcs (angle ∝ value), 14px thick, categorical slots 1–5
- Ring 2: programme arcs spread with extra padding so the bands fan out, 14px thick, tints of the department hue
- Bands: curved ribbons from each department's arc segment to each programme's arc, 45% opacity
- Labels: department names along ring 1 (outside when they fit), programme names radially outside ring 2

## Data shape
```
{ total: "FY2027 budget", children: [{ name: "Engineering", children: [{ name: "Platform", value: 18.4 }, …] }, …] }
```

## Interactions
- Hover a department or programme: its branch stays, the rest fade; tooltip with value and shares
- Click a department to pin its branch
- Chart / List toggle

## Accessibility
- List view gives every value with its department
- Centre total in text; tooltips state shares
- Department labels name every colour

## Design tokens used
`--s1 … --s5`, `--surface`, `--ink`, `--ink-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a radial Sankey in one self-contained HTML file with inline SVG and no libraries. Seeded two-level budget: 5 departments, each with 3–5 programmes. In the centre, print the total. Ring 1 (inner) holds department arcs whose angles are proportional to value, 14px thick, in categorical slots 1–5 with small angular padding. Ring 2 (outer, at a larger radius) holds programme arcs, also proportional to value but with larger padding so they fan out, coloured as lighter tints of their department. Connect each programme to its department's arc segment with a curved band: start at the department ring's outer edge across the programme's share of that arc, end at the programme arc's inner edge, using cubic curves through a mid radius, at 45% opacity. Label departments near ring 1 and programmes radially outside ring 2, rotated to read outward and flipped on the left half. Hover highlights a whole branch and shows a tooltip; clicking a department pins it. Add a Chart / List toggle. CSS variables for every colour, light and dark themes.
