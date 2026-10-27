# Status KPI cards

**Category:** KPI cards · **Tags:** threshold, ops board, status colour, alerting, sparkline

The standard KPI card (label, big value, delta, sparkline) colour-coded by status — OK, Warning or Critical against configurable thresholds — with a switch between a full-colour tint and a left-edge highlight only.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- An ops or on-call view where 'what needs attention?' matters as much as the numbers
- Every metric has agreed warning and critical thresholds
- You want status cards that sit next to ordinary KPI cards without looking like a different system

## Avoid it when
- Business reporting where most metrics have no threshold (status colour becomes decoration)
- Comparing magnitudes across cards (status hides scale)

## Anatomy
- Same card as the KPI row: 1px hairline border, 10px radius, label in secondary ink, 28px semibold value with unit, delta line, 48px sparkline
- Status badge top-right: icon + word (✓ OK, ! Warning, ✕ Critical) — status is never colour alone
- Full colour mode: background is a 12% tint of the status colour and the border a 40% tint
- Left edge mode: neutral card with a 4px status-coloured edge on the left
- Sparkline: 2px line and 10% area wash in the status colour, warning and critical thresholds as faint dashed lines, end dot with a surface ring
- Delta: change vs 30 minutes ago with ▲/▼, green when it moved the good way, red when the bad way
- Footer: the threshold rule as text ('warn ≥ 250 ms · crit ≥ 400 ms')

## Data shape
```
[{ name: "p95 latency", unit: "ms", warn: 250, crit: 400, higherIsWorse: true, last30: [ … ] }, …]
```

## Interactions
- Style switch: Full colour / Left edge
- Threshold profile switch (Default / Strict) re-evaluates every card
- 'Simulate tick' appends a new point to every series
- Hover a sparkline: value at that minute; hover the card header: thresholds and distance to the next state

## Accessibility
- Status as icon + word in the badge
- Each card's aria-label states value and status; a polite live region announces status changes
- Status colours are reserved and never used for series; value text stays in ink

## Design tokens used
`--good / --warn / --crit`, `--ink`, `--ink-2`, `--grid`, `--surface`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a row of status-coded KPI cards in one self-contained HTML file with inline SVG. Each card uses the standard KPI card layout — 1px hairline border, 10px radius, a secondary-ink label, a 28px semibold value with its unit, a delta line (▲/▼ change vs 30 minutes ago, green when it moved the good way and red when the bad way, respecting higher-is-worse vs lower-is-worse metrics) and a 48px sparkline — plus a status badge top-right with an icon and word (✓ OK, ! Warning, ✕ Critical) from warning and critical thresholds. Colour the card by status in one of two modes chosen with a segmented control: Full colour (background = 12% tint of the status colour, border = 40% tint) or Left edge (neutral card with a 4px status-coloured left edge). Draw the sparkline as a 2px line with a 10% area wash in the status colour, the two thresholds as faint dashed lines and an end dot with a surface ring. Add a footer stating the threshold rule, a threshold-profile control (Default / Strict), a 'Simulate tick' button that appends a random-walk point to every card, and an aria-live region announcing status changes. Keep all text in ink tokens, never in the status colour. CSS variables for all colours, light and dark themes.
