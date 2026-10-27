# KPI donut cards

**Category:** KPI cards · **Tags:** progress to goal, donut, ring, target, kpi card

The standard KPI card with a progress donut: a ring fills toward the goal with the percent in its centre, beside the value, the goal and a delta vs the previous period. Switch between ring-beside and ring-on-top layouts.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Each KPI has a goal and 'how far along are we?' is the headline
- A row of 2–5 goals for the same period (month, quarter, year)
- You want progress cards that sit beside ordinary KPI cards without looking like a different system

## Avoid it when
- Metrics with no goal (use the sparkline KPI card)
- Comparing progress precisely across many goals (use bullet charts or progress bars)
- Values that routinely run far past 100% (the ring caps at full)

## Anatomy
- Same card as the KPI row: 1px hairline border, card radius, label in secondary ink, 28px semibold value
- Donut: a full ring with a pale track in the series hue, the fill starting at 12 o'clock with a round cap; percent of goal in the centre
- A small tick on the ring marks where you should be today (share of the period elapsed)
- Under the value: 'of <goal> goal' and a delta (▲/▼ vs the same point last period, coloured by good/bad)
- Goal met: ring fills fully and a ✓ Goal met note replaces the pace line
- Layout switch: ring beside the text, or ring on top with the text centred

## Data shape
```
[{ label: "Revenue", fmt: money, goal: 2400000, actual: 1840000, prev: 1710000 }, …] per period, plus the share of the period elapsed
```

## Interactions
- Period switch (Month / Quarter / Year) redraws every card
- Layout switch (Beside / On top)
- Hover a ring: actual, goal, remaining, and where pace says you should be today

## Accessibility
- role=meter on each ring with aria-valuenow, -min and -max
- Percent of goal is printed in the ring, never only implied by the arc
- Ahead / behind pace is stated in words, not colour alone

## Design tokens used
`--s1`, `--track`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--up`, `--down`, `--radius` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a responsive row of KPI donut cards in one self-contained HTML file with inline SVG and no libraries. Each card follows the standard KPI card (1px hairline border, rounded corners, a secondary-ink label, a 28px semibold value) and adds a progress donut: a full ring with a pale track in the accent hue, the fill starting at 12 o'clock with a round cap, sized by actual ÷ goal and capped at 100%, with the percent of goal printed in the centre. Put a small ink tick on the ring at the share of the period elapsed so readers can see if they're on pace. Under the value print 'of <goal> goal' and a delta vs the same point last period (▲/▼, green when good, red when bad), then a line saying how far ahead or behind pace the metric is; when the goal is met, fill the ring and show '✓ Goal met'. Seeded data for Month, Quarter and Year with a segmented control to switch, and a second control to switch the layout between ring beside the text and ring on top with the text centred. Hover a ring for actual, goal, remaining and expected-by-today. role=meter with aria values. CSS variables for every colour, light and dark themes.
