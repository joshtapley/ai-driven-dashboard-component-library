# Square tile US map

**Category:** Maps · **Tags:** choropleth, tile grid map, geo, click to inspect

Every state is an equal square on a 12×8 grid, coloured on a binned sequential or diverging scale, with a metric switch and a click-to-inspect detail panel.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- You compare a rate or per-capita value across states and small states (RI, DE, DC) must be as visible as Texas
- The audience knows US geography roughly; exact borders don't matter
- You need a compact map that fits in a dashboard card

## Avoid it when
- The value is a raw total that tracks population (show a ranked bar instead, or normalise first)
- Exact location or distance matters (use a real projection)
- You have county or ZIP data

## Anatomy
- Header: title + one-line subtitle naming the metric and period
- Metric switch (segmented control) above the map
- 12×8 grid of square tiles, 2px gap, 4px corner radius, state abbreviation centred
- Label ink chosen per tile by fill luminance (white on dark fills, ink on light)
- Binned legend (5 classes) with range labels below the map
- Detail panel: state name, value, national rank, region average and a share-of-region bar

## Data shape
```
[{ state: "CA", revenue: 48200000, growth: 0.081, orders_per_1k: 31.2 }, …] — one row per state + DC (51 rows)
```

## Interactions
- Hover a tile: tooltip with state, value and rank
- Click or Enter on a tile: selects it (2px ink ring) and fills the detail panel
- Metric switch: re-bins and re-colours; growth switches to a diverging blue↔red scale centred on 0
- Keyboard: every tile is focusable (Tab), Enter selects

## Accessibility
- Each tile has an aria-label with state name and formatted value
- Legend shows ranges as text, never colour alone
- "Table" toggle swaps the map for a sortable list of the same numbers

## Design tokens used
`--seq-0…--seq-6`, `--div-neg / --div-mid / --div-pos`, `--ink`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a square tile-grid US map in a single self-contained HTML file (no libraries). Lay out all 50 states + DC as equal squares on a 12-column × 8-row grid using the standard NPR-style tile positions (AK top-left, ME top-right, HI and TX on the bottom row, FL bottom-right). Tiles are squares with a 2px gap and 4px radius, the state abbreviation centred; choose white or near-black label text per tile from the fill's luminance. Colour with 5 equal-interval bins from a single-hue sequential ramp (light = low); for a signed metric such as growth, switch to a diverging blue↔red ramp with a neutral grey midpoint at 0 and symmetric bins. Put a segmented control above the map to switch metrics, a binned legend with numeric ranges below it, and a detail panel to the right (stacked below on narrow screens) that shows the clicked state's value, national rank and region average. Hover shows a tooltip; tiles are keyboard-focusable and Enter selects. Add a Table toggle that shows the same data as a sorted list. Use CSS variables for every colour and support light and dark themes.
