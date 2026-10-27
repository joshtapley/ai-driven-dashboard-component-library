# Area bump chart

**Category:** Charts · **Tags:** ranked stream, rank and size, market share, ribbons

A bump chart whose lines are ribbons: at each quarter the services are stacked in rank order, ribbon thickness is their share, and smooth crossovers show overtakes, with direct labels and hover focus.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Both rank and size matter over time (market share, watch time, votes)
- Overtakes are the story but you don't want to hide how big the gaps are
- 5–8 series over 6–20 periods

## Avoid it when
- Only rank matters (a plain bump chart is cleaner)
- Exact values must be compared (use lines or small multiples)
- Many series with similar sizes (ribbons become a tangle)

## Anatomy
- At each period, series stack top to bottom by rank with a 6px gap; thickness ∝ value
- Between periods, each ribbon's edges follow cubic curves with horizontal tangents, so swaps read as crossovers
- Categorical slots in fixed order per series; 1px surface stroke separates overlapping ribbons
- Direct labels at the right edge (name + share) and left edge (name), placed in each ribbon's middle
- Period labels along the bottom; hover crosshair

## Data shape
```
{ periods: ["Q1 '24", …], series: [{ name: "Streamly", values: [ …share per period ] }, …] }
```

## Interactions
- Hover a ribbon: it stays full strength, others fade to 20%; tooltip with rank and share at the hovered period
- Click a ribbon to pin the focus; click again to clear
- Metric switch: Share of watch time / Hours

## Accessibility
- Every ribbon is labelled at both ends, so colour is not the only identifier
- Tooltip lists rank and value as text
- SVG aria-label names the current leader and the biggest climber

## Design tokens used
`--s1 … --s6`, `--surface`, `--ink`, `--grid` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an area bump chart in one self-contained HTML file with inline SVG and no libraries. Seeded quarterly data for 6 fictional streaming services over 10 quarters (share of watch time, with a couple of overtakes). At each quarter, sort services by value and stack them top to bottom with a 6px gap so each ribbon's thickness is proportional to its value and its vertical position is its rank. Between quarters, draw each ribbon's top and bottom edges as cubic Bézier curves with horizontal tangents so rank swaps become smooth crossovers; fill with categorical slots 1–6 in fixed per-service order and a 1px surface-coloured stroke. Label every ribbon at the right edge (name + latest share) and at the left edge (name), centred in the ribbon. Hovering a ribbon fades the others to 20% and shows a tooltip with its rank and value at the hovered quarter; clicking pins the focus. Add a metric switch between share and absolute hours. CSS variables for every colour, light and dark themes.
