# Scorecard table vs target

**Category:** Tables · **Tags:** balanced scorecard, diverging cells, target, team comparison

Teams × KPIs scorecard where each cell is tinted on a diverging scale by its distance from target (blue = better, red = worse, grey = on target), with an overall score bar and best-in-column markers.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Comparing many units (teams, stores, agents) on several KPIs with targets
- Monthly performance reviews where 'who needs help on what?' is the question
- KPIs have different units and directions, so raw colour scales would mislead

## Avoid it when
- No targets exist (use a highlight table)
- Readers need trend, not position (add sparklines instead)

## Anatomy
- Header row: KPI name, target, and direction hint (↑ better / ↓ better)
- Cells: value centred; fill = diverging tint by normalised gap to target (capped at ±25%), neutral grey within ±2%
- Best value per column gets a 2px ink ring
- Overall score column: mean of capped normalised gaps → 0–100, shown as a bar + number
- Rows sortable by any column

## Data shape
```
{ kpis: [{ key: "csat", name: "CSAT", target: 4.5, better: "up", fmt: "0.0" }, …], rows: [{ team: "Atlanta", csat: 4.6, aht: 312, … }, …] }
```

## Interactions
- Click a column header to sort by it (direction-aware: best first)
- Hover a cell: value, target, gap and whether it beats target
- 'Show gaps' toggle swaps values for signed % vs target

## Accessibility
- Values (or gaps) always printed
- Direction of 'better' written in each header
- Best marker is a ring (shape), not colour

## Design tokens used
`--div-neg / --div-mid / --div-pos`, `--ink`, `--s1`, `--track` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a scorecard table in one self-contained HTML file. Rows are 10 teams; columns are 6 KPIs with different units and directions (e.g. CSAT ↑, average handle time ↓, first-contact resolution ↑, abandonment rate ↓, QA score ↑, cost per contact ↓), each with a target shown in the header together with '↑ better' or '↓ better'. Each cell prints the value and is tinted on a diverging red ↔ grey ↔ blue scale by its normalised gap to target (direction-aware, capped at ±25%, grey within ±2%), with text colour chosen by luminance. Ring the best value in each column with a 2px ink outline. Add an Overall column: average of the capped normalised gaps mapped to 0–100, shown as a bar and number. Clicking any header sorts rows best-first by that column. A toggle swaps values for signed % vs target. Hover tooltips show value, target and gap. CSS variables for all colours, light and dark themes.
