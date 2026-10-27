# Sparkline tile US map

**Category:** Maps · **Tags:** small multiples, tile grid map, trend, sparkline

Each state tile holds its own 24-month trend line, so the map shows shape over time instead of a single number; a filter highlights rising or falling states.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The story is how each state's trend moved, not where the level is highest
- You want regional patterns in trajectories (e.g. the South rising, the Midwest flat)
- There is room for ~60px tiles

## Avoid it when
- Phone-width layouts (tiles become too small for lines; switch to a ranked list of sparklines)
- Exact values matter (use a table with sparklines)

## Anatomy
- Tile background in surface tint; state code top-left; % change bottom-right
- Each line indexed to its own first month (local y-scale) — shape, not size, is compared
- Line in the accent colour, end dot ≥ 8px with a surface ring
- Tiles with the selected trend stay full strength, the rest fade

## Data shape
```
[{ state: "GA", series: [100, 101.4, …24 monthly values] }, …]
```

## Interactions
- Highlight control: All / Rising / Falling / Flat
- Hover a tile: tooltip with first and last value and % change, plus a crosshair-free enlarged line

## Accessibility
- % change printed on each tile so trend direction is never colour-only
- aria-label per tile with start, end and change

## Design tokens used
`--s1`, `--surface-2`, `--up`, `--down`, `--ink-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a sparkline tile-grid US map in a single self-contained HTML file. Use the standard 12×8 US tile grid; each state tile is a rounded square in a light surface tint containing: the state code top-left (small, semibold), a 24-month sparkline filling the middle (2px accent line, a light 10% area wash, an end dot with a surface-coloured ring), and the % change bottom-right in green or red text with a ▲/▼ glyph. Each sparkline uses its own y-scale so shapes are comparable. Add a segmented control (All / Rising / Falling / Flat, where flat = within ±2%) that fades non-matching tiles to 20% opacity, and a summary count. Hover shows start, end and change. CSS variables for every colour, light and dark themes.
