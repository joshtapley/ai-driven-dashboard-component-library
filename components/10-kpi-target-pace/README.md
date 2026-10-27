# KPI cards with target and pace

**Category:** KPI cards · **Tags:** progress, month to date, pacing, forecast

Month-to-date KPI cards that show actual vs target as a progress meter, plus a pace marker for where you should be today and a projected month-end finish.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Goals reset each month or quarter and the question is 'are we on pace?'
- Sales quotas, fundraising, hiring plans, content output
- You want an early warning before the period ends

## Avoid it when
- Values are not cumulative within the period (rates, averages)
- There is no target

## Anatomy
- Value as a fraction: actual (semibold) / target (muted)
- Progress meter: 8px track in a pale accent, fill in accent; fill switches to warning when behind pace by >5%
- Pace marker: 2px ink tick at (day ÷ days in month) × target, labelled 'Today'
- Status line with icon: ✓ Ahead of pace / ! Behind pace, by how much
- Projected finish: actual ÷ day × days in month, shown vs target

## Data shape
```
[{ name: "New ARR", target: 400000, daily: [ …30 numbers ] }, …]
```

## Interactions
- 'Day of month' slider replays the month so you can see pacing change
- Hover a meter: actual, expected by today, projected finish

## Accessibility
- role=progressbar on each meter with aria-valuenow / max
- Status is an icon + sentence, not just the meter colour
- Slider has a visible label and value

## Design tokens used
`--s1`, `--warn`, `--track`, `--ink`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build month-to-date KPI cards with pacing in one self-contained HTML file. Each card shows the metric name, then actual / target as a fraction (actual semibold, target muted), an 8px progress meter (pale accent track, accent fill that turns to the warning colour when more than 5% behind pace), a 2px ink pace tick at (day ÷ days in month) × target labelled 'Today', a status line with an icon (✓ Ahead of pace by X / ! Behind pace by X) and a projected month-end finish (actual ÷ day × days) vs target. Generate seeded daily data for 30 days and add a labelled 'Day of month' range slider that recomputes everything as if it were that day. Meters are role=progressbar. Hover tooltips with actual, expected and projected. CSS variables for every colour, light and dark themes.
