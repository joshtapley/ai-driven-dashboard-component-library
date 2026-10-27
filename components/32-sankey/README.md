# Sankey diagram

**Category:** Flows & networks · **Tags:** flow, journey, draggable, attribution, budget

A three-stage Sankey (traffic source → landing page → outcome) with ribbons sized by volume, coloured by source, hover-to-trace highlighting, click-to-pin and vertically draggable nodes.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing how a quantity splits and recombines across 2–4 stages (traffic to outcomes, budget to spend, energy, patient pathways)
- The biggest flows are the story
- Up to ~20 nodes

## Avoid it when
- Flows loop back (cycles) — use a network diagram
- Exact comparison of small flows matters (pair with a table)
- Only one stage of splits (a stacked bar is simpler)

## Anatomy
- Nodes: 12px-wide rounded bars in columns, height ∝ throughput, 10px vertical padding
- Ribbons: cubic Bézier bands whose width ∝ flow, ordered to avoid crossings, 35% opacity in the source node's colour
- First-column nodes use categorical slots in fixed order; later nodes are neutral ink-2
- Labels: name + value beside each node (right of nodes, left of the last column)

## Data shape
```
{ nodes: [{ id: "organic", name: "Organic search", col: 0 }, …], links: [{ source: "organic", target: "home", value: 18200 }, …] }
```

## Interactions
- Hover a node: every ribbon through it highlights (65% opacity), others fade to 8%
- Hover a ribbon: tooltip with source → target, value and its share of the source
- Click a node to pin the highlight; click again or Esc to clear
- Drag a node up or down to untangle; ribbons follow

## Accessibility
- SVG aria-label summarises the largest flows
- A 'Table' toggle lists every flow with values
- Ribbon colour carries source identity, and every node is labelled

## Design tokens used
`--s1 … --s5`, `--ink-2`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a draggable Sankey diagram in one self-contained HTML file with inline SVG and no libraries (write the layout yourself). Three columns: 5 traffic sources → 4 landing pages → 3 outcomes (Purchase, Sign-up, Bounce), with seeded link values. Layout: node height ∝ max(inflow, outflow) using one global scale, 10px padding between nodes, 12px-wide rounded node bars, columns evenly spaced. Links are filled Bézier ribbons whose width is the flow value, sorted at each node by the other end's vertical position to minimise crossings, coloured by the first-column source (categorical slots in fixed order; downstream ribbons inherit the colour of the traffic that feeds them, so split second-stage links by source) at 35% opacity. Label every node with name and value (to the right, or to the left for the last column). Hovering a node highlights all ribbons through it (others fade to 8%); hovering a ribbon shows source → target, value and share; clicking a node pins the highlight; nodes can be dragged vertically with pointer events and ribbons follow. Add a Diagram / Table toggle. CSS variables for all colours, light and dark themes.
