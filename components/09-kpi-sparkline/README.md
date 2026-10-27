# KPI cards with sparkline

**Category:** KPI cards · **Tags:** stat tile, sparkline, delta badge, period comparison

The workhorse KPI row: label, big value, signed delta vs the previous period, and a sparkline of the current period over a grey ghost of the previous one, with a 7D / 30D / 90D switch.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The top row of almost any dashboard: 3–5 headline numbers
- Readers need both 'how much' and 'which way' at a glance
- Comparing to the immediately previous period is meaningful

## Avoid it when
- More than ~6 KPIs (group them or use a table with sparklines)
- There is a single headline number (use a hero KPI)

## Anatomy
- Label in secondary ink, sentence case, no colon
- Value: 28px semibold, auto-compacted ($1.28M, 12.9K), proportional figures
- Delta: signed %, ▲/▼, colour = direction × whether up is good, followed by 'vs prev. 30 days' in muted text
- Sparkline: current period as a 2px accent line with a 10% area wash; previous period as a 1.5px grey line behind it
- Crosshair readout on hover

## Data shape
```
{ label: "Revenue", fmt: "$", upIsGood: true, daily: [ …180 numbers, oldest first ] } — current and previous periods are sliced from the same series
```

## Interactions
- Period switch re-slices every card (7 / 30 / 90 days)
- Hover a sparkline: crosshair dot and tooltip with the day's value and the same day last period

## Accessibility
- Delta direction carried by ▲/▼ and sign, not just colour
- Each card is an article with an aria-label summarising value and change
- Sparkline is decorative-plus: the numbers it encodes are in the tooltip and label

## Design tokens used
`--s1`, `--de-emph`, `--up`, `--down`, `--ink-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a responsive row of four KPI cards in one self-contained HTML file with inline SVG. Each card: a label in secondary ink, the value in 28px semibold (auto-compact: $1.28M, 12.9K), a delta line with ▲/▼, signed percent and 'vs prev. N days' (green when the change is good, red when bad — respect metrics where down is good, like refund rate), and a 48px-tall sparkline of the current period as a 2px accent line with a 10% area wash, drawn over the previous period as a thinner grey line. Generate 180 days of seeded synthetic data per metric and add a 7D / 30D / 90D segmented control that re-slices current vs previous period and recomputes totals and deltas (sum for counts, mean for rates). Hovering a sparkline shows a dot and a tooltip with that day's value and the same day in the previous period. CSS variables for all colours, light and dark themes.
