# Chord diagram

**Category:** Flows & networks · **Tags:** flows between groups, switching, migration, matrix, net gain

Customer switching between five brands drawn as a chord diagram: arc length = customers lost, ribbon ends sized by flow in each direction and coloured by the brand that wins the exchange, with net gain/loss on hover and a matrix view.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Flows between members of the same set go both ways (brand switching, migration between regions, transfers between teams)
- Net winners and losers are the story
- 4–8 groups

## Avoid it when
- Flows go through stages (use a Sankey)
- More than ~8 groups or many tiny flows (use a heatmap matrix)
- Exact comparison of flows (pair with the matrix view)

## Anatomy
- Outer arcs: one per group, 14px thick, length ∝ customers that left the group, 0.04 rad padding, categorical slots in fixed order
- Ribbons: each pair drawn once; each end's width ∝ the flow leaving that side; coloured by the side that gained more, at 65% opacity
- Labels outside each arc with the group name and its net change (signed)
- Matrix view: from × to table with row and column totals

## Data shape
```
{ groups: ["Aurora", "Bramble", …], matrix: [[0, 420, 180, …], …] } — matrix[i][j] = customers who moved from i to j
```

## Interactions
- Hover an arc: its ribbons stay, the rest fade; tooltip with lost, gained and net
- Hover a ribbon: 'A → B 420 · B → A 180 · net +240 to A'
- Click an arc to pin the highlight
- Diagram / Matrix toggle

## Accessibility
- Net change written in every label
- Matrix view carries every number
- Ribbon colour is explained in the subtitle and tooltip

## Design tokens used
`--s1 … --s5`, `--surface`, `--ink`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a chord diagram in one self-contained HTML file with inline SVG and no libraries (compute the layout yourself). Seeded 5×5 brand-switching matrix where matrix[i][j] is customers who moved from brand i to brand j (diagonal zero). Lay out one outer arc per brand around a circle, arc length proportional to the row total (customers lost), with 0.04 radian padding, 14px thick, coloured by categorical slots 1–5 in fixed order. Inside each arc, sub-divide by destination; draw each pair once as a ribbon from the i→j sub-arc to the j→i sub-arc with quadratic curves through the centre, coloured by the brand that gained more from the exchange, at 65% opacity. Label each arc outside the circle with the brand name and its signed net change. Hovering an arc keeps its ribbons and fades others (tooltip: lost, gained, net); hovering a ribbon shows both directions and the net; clicking an arc pins it. Add a Diagram / Matrix toggle that shows the from × to table with totals. CSS variables for every colour, light and dark themes.
