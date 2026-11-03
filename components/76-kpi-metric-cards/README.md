# KPI metric cards (overview grid)

**Category:** KPI cards · **Tags:** KPI grid, performance overview, month to date, sparkline, progress to target, delta pill, source, pager

A paged 'Performance overview' grid of full metric cards. Each card has a period label, a centred title and a big value, then either a trend sparkline or a progress bar to target, with a footer naming the data source and a coloured delta pill. Trend and goal cards mix in one grid.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- An overview page shows 6–12 headline metrics from different sources at once
- Some metrics are tracked against a target (show progress) and others as a trend (show a sparkline), and both belong in one grid
- Readers need to know where each number comes from (the source footer)

## Avoid it when
- Only 2–4 metrics: use a single row of compact cards (KPI sparkline or KPI icon cards)
- Metrics need detailed comparison over time (use a line chart, or KPI tabs with a chart)
- Space is tight: each card needs about 220×200px

## Anatomy
- Header: title, period subtitle and ‹ › pager buttons with a page count (6 cards per page)
- Cards on a responsive grid: 3 columns, 2 on tablets, 1 on phones
- Card top: muted period label ('Month to date'), centred metric title, big centred value
- Trend card: the value in ink and a 30-day area sparkline in the status colour (green when the metric moves the good way, red when it moves the bad way)
- Goal card: the percent of target as the big value in its status colour (on pace, slightly behind, behind), a progress bar with a pace tick, the current value on the left and the target on the right
- Footer: a small line icon and the source name on the left, a ▲/▼ delta pill on the right; metrics where lower is better flip the pill colour

## Data shape
```
[{ name: "Sessions", kind: "trend" | "goal", value, prev, target?, series?: [30 daily values], source: "Website", icon: "web" | "app" | "social" | "store" | "mail" | "support", fmt: "num" | "money" | "pct", better: "up" | "down" }]
```

## Interactions
- ‹ › pager (and Left/Right arrow keys on the pager) moves between pages of six cards
- Hover a sparkline: a dot and guide follow the pointer, with the day's value in a tooltip
- Hover a progress bar: current, target, percent and pace in a tooltip
- Period switch: Month to date / Last 30 days

## Accessibility
- Each card is an article with an aria-label that reads the title, value, target or trend and the change
- Status is shown by the ▲/▼ arrow, the sign and the words in the label, never colour alone
- Pager buttons are real buttons with aria-labels and are disabled at the ends; the page count is an aria-live region
- A visually hidden list repeats every metric on the current page

## Design tokens used
`--good`, `--warn`, `--down`, `--up`, `--track`, `--surface`, `--surface-2`, `--ink`, `--ink-2`, `--muted`, `--border` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a 'Performance overview' grid of KPI metric cards in one self-contained HTML file with inline SVG and no libraries. Twelve metrics in two pages of six, a ‹ › pager with a page count in the header, and a Period switch (Month to date / Last 30 days). Cards sit on a responsive grid (3 columns, 2 on tablets, 1 on phones). Each card has a muted period label, a centred title and a big centred value, then one of two visuals: a trend card draws a 30-day area sparkline in green or red depending on whether the metric moved the good way (lower-is-better metrics flip), and a goal card shows the percent of target as the big value in a status colour (green on pace, amber slightly behind, red behind) above a progress bar with a pace tick, the current value on the left and the target on the right. A footer shows a small line icon with the data source name and a ▲/▼ delta pill coloured by good or bad. Hovering a sparkline shows a dot, guide and the day's value; hovering a progress bar shows current, target and pace. Each card is an article with an aria-label; status never relies on colour alone. CSS variables for every colour, light and dark themes, seeded synthetic data.
