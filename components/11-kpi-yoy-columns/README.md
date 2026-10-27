# KPI cards with year-over-year columns

**Category:** KPI cards · **Tags:** month selector, prior year, mini column chart, click to drill

KPI cards whose mini column chart doubles as a month picker: grey columns for the year, the selected month in accent, prior-year ticks above each, and the headline value follows your click.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Monthly business reviews: 'how did March do, and vs last March?'
- Seasonality matters, so year-over-year beats month-over-month
- You want the KPI and its 12-month context in one card

## Avoid it when
- Daily or weekly granularity (use a sparkline card)
- There is no prior-year data

## Anatomy
- Header: label + selected month name
- Value (semibold 26px) and YoY delta with ▲/▼
- 12 mini columns (max 16px wide, 4px rounded top, 2px gaps): de-emphasis grey, selected month in accent
- Prior-year value per month as a short 2px ink tick
- Month initials under the columns

## Data shape
```
[{ label: "Bookings", cy: [12 monthly values], py: [12 monthly values], upIsGood: true }, …]
```

## Interactions
- Click any column (in any card) to select that month across all cards
- Arrow keys move the selection when a card has focus
- Hover a column: this year, last year and the change

## Accessibility
- Columns are focusable via the card; arrow keys change month
- Delta text includes direction glyph
- aria-live region announces the selected month

## Design tokens used
`--s1`, `--de-emph`, `--ink`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build three KPI cards with year-over-year mini columns in one self-contained HTML file. Each card: label and the selected month name in muted text, the selected month's value (26px semibold), a YoY delta with ▲/▼ (green if good, red if bad, respecting metrics where down is good), and a 12-month column chart (bars ≤16px wide, 4px rounded tops, square at the baseline, de-emphasis grey) where the selected month is the accent colour and each month has a short 2px ink tick at last year's value. Month initials sit under the columns. Clicking a column selects that month in every card; when a card is focused, Left/Right arrow keys move the month. Hover tooltips show this year, last year and the change. Seeded synthetic data with seasonality. CSS variables for all colours, light and dark themes.
