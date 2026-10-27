# KPI icon cards

**Category:** KPI cards · **Tags:** icon, kpi card, kpi row, delta, scorecard

A full-width row of compact KPI cards, each led by an icon from one consistent line-icon set: the label beside the icon, a large value, a coloured delta (percent or points) and the comparison period. Switch the icon style between tinted badges, coloured outlines and a single neutral ink.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- A scorecard strip across the top of an operational dashboard (6–8 metrics)
- Readers scan for one metric by shape as much as by name
- Metrics mix money, counts, rates and averages and need one shared card

## Avoid it when
- Metrics need a trend to make sense (use the sparkline KPI card)
- Each KPI has a goal (use KPI donut cards)
- Icons would be decoration only, with no consistent meaning across dashboards

## Anatomy
- Card: 1px hairline border, card radius, compact padding; 8 cards wrap to fit the row
- Icon: 24px grid, 2px rounded strokes, no fills, so every icon has the same weight; shown in a 32px tinted circle
- Label beside the icon in secondary ink, wrapping to two lines
- Value: 26px bold display type with tabular figures
- Delta: ▲/▼ with percent change, or pp for rates; green when good and red when bad, where lower is better for metrics like callback rate
- Comparison line: 'vs <previous period dates>' in muted ink

## Data shape
```
[{ label: "Total revenue", icon: "money", fmt: money, cur: 9.34e6, prev: 9.0e6, better: "up" }, …] per period, with the comparison period's date range
```

## Interactions
- Period switch (Month / Quarter / Year to date) redraws every card
- Icon style switch (Badge / Outline / Mono)
- Hover or focus a card: this period, previous period, the change and whether it is good

## Accessibility
- Icons are aria-hidden; every card has an aria-label with the label, value, change and comparison
- Good and bad are stated with ▲/▼ and the tooltip, not colour alone
- Cards are focusable so keyboard users get the same tooltip

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--surface`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--up`, `--down`, `--radius` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a responsive row of eight KPI icon cards in one self-contained HTML file with inline SVG and no libraries. Each card has a 1px hairline border and rounded corners; at the top an icon in a 32px circle tinted with the icon's colour, with the metric label beside it in secondary ink (wrapping to two lines); then a 26px bold value with tabular figures; then a delta (▲/▼ and percent change, or percentage points for rates) coloured green when good and red when bad, where some metrics are better when lower (callback rate); then 'vs <previous period dates>' in muted ink. Draw all icons from one consistent set on a 24px grid with 2px round-capped strokes and no fills: dollar coin, pie slice, trend arrow, wrench, price tag, person-plus, incoming phone, gauge. Colour icons in a fixed rotation of the first four series colours. Metrics: total revenue, gross margin, net profit, service calls completed, average ticket size, membership revenue, callback rate and technician utilization, with seeded data for Month, Quarter and Year to date and a segmented control to switch. A second control switches the icon style between tinted badges, coloured outlines and one neutral ink colour. Hover or focus a card for this period, the previous period and the change. Icons aria-hidden, an aria-label on every card. CSS variables for every colour, light and dark themes.
