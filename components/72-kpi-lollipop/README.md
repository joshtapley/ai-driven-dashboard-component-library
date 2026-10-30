# KPI lollipop cards

**Category:** KPI cards · **Tags:** lollipop, kpi card, journey, stage, voyage, progress

KPI cards for a journey with fixed stops (a voyage, a route, a pipeline): a big value and a delta pill on the left, and a mini lollipop chart of every stop on the right, with completed stops solid, the focus stop in the accent colour with a ring, and planned stops dashed. Click a stop to move the focus on every card at once.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- A metric that changes stop by stop along a known route (ports, warehouses, project phases)
- Readers need the current value and where it sits in the whole journey
- Two to four related metrics that should move together when the focus changes

## Avoid it when
- Continuous time series with many points (use the sparkline KPI card)
- More than about 10 stops (the stems crowd; use a small line chart)
- Metrics with no natural sequence

## Anatomy
- Card: uppercase label, a large value with an optional small unit, and a tinted delta pill (▲/▼ and percent) with 'vs previous voyage' beside it
- Optional 5px accent edge on the card's left side
- Mini lollipop: one stem and dot per stop, letters underneath; completed stops in --ink, the focus stop in --s1 with a ring, planned stops as dashed --de-emph stems with grey dots
- Each card scales its own lollipops from zero to its maximum
- Focus is shared: choosing a stop on one card updates every card

## Data shape
```
stops: ["Shanghai", "Hong Kong", …]; metrics: [{ label: "Containers on board", values: [1671, 1798, …], prev: [1640, …] }, …]; focus index
```

## Interactions
- Click a lollipop or its letter (or use the arrow keys on a focused card) to change the focus stop
- Planned stops switch: Dashed / Hidden
- Accent edge switch: On / Off
- Hover a lollipop for the stop, value and whether it is completed, current or planned

## Accessibility
- Every card has an aria-label with the value, delta and focus stop
- Lollipops are buttons named with the stop and value; arrow keys move the focus stop
- Completed, current and planned differ by line style and ring as well as colour

## Design tokens used
`--s1`, `--ink`, `--ink-2`, `--muted`, `--de-emph`, `--surface`, `--grid`, `--up`, `--down`, `--radius` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a row of three KPI lollipop cards in one self-contained HTML file with inline SVG and no libraries, for a container ship visiting seven ports (Shanghai, Hong Kong, Singapore, Colombo, Suez, Barcelona, Rotterdam). Metrics: containers on board, containers on/off and total weight in kg. Each card has an uppercase label, a large value (a small 'KG' unit for weight), a tinted pill with the change vs the previous voyage (▲/▼ and percent) and the words 'vs previous voyage', and on the right a mini lollipop chart with one stem and dot per port and the port's first letter underneath. Ports before the focus port are solid ink, the focus port uses the accent colour with an outer ring, and later ports are planned: dashed light-grey stems with grey dots. Each card scales from zero to its own maximum. Clicking any lollipop or letter moves the focus port on all cards; arrow keys do the same on a focused card. Add switches for planned ports (Dashed / Hidden) and a 5px accent edge on the cards (On / Off). Hover shows the port, value and status. aria-labels on every card, CSS variables for every colour, light and dark themes.
