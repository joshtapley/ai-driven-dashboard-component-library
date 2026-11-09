# KPI flip cards with a narrative

**Category:** KPI cards · **Tags:** kpi, flip card, narrative, storytelling, explanation, drivers, commentary, scorecard

KPI cards that turn over. The front is the number: value, change and a sparkline. The back is the story behind it: a sentence on what happened, how it compares with target, what drove it and what to do next, all written from the data so it stays true when the period changes.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- An executive scorecard where readers ask why a number moved
- Replacing a separate commentary slide with an explanation attached to each KPI
- Keeping a dashboard compact while still giving each metric a written takeaway

## Avoid it when
- The explanation must be visible all the time or printed (put the sentence on the card instead)
- A wall display nobody can click
- Metrics with no known drivers or target, where the back would have little to say

## Anatomy
- Card grid: columns of at least 270px that fill the row; both faces share one grid cell, so the card is always as tall as its longer side and nothing clips
- Front: period, metric name, large value, a signed change pill coloured by whether the move is good, and an area sparkline of 24 months that fills the card, with the current period shaded and a dashed target line
- Back: metric name, a status chip with a word and an icon, a bold one-sentence lead, target and driver sentences, up to three signed driver bars, and a Next line
- Status: On track when the move is good and the target is met, Needs attention when neither is true, Watch otherwise
- Flip: a 0.55s rotation around the vertical axis; the hidden face is inert, so screen readers and the Tab key only reach the side showing

## Data shape
```
[{ name: "Revenue", kind: "sum", change: "pct", better: "up", series: [24 monthly values], target: 1180000, drivers: [["Enterprise", 0.62], ["Self-serve", 0.5], ["Partner", -0.12]], next: { good: "…", bad: "…" } }, …]. kind: sum adds months in a period, level uses the period-end value. change: pct or abs. Driver weights add up to 1 and split the change.
```

## Interactions
- Click anywhere on a card, or its flip button, to turn it over; selecting text on the back doesn't flip it
- Enter or Space on the flip button turns the card and moves focus to the side now showing
- Flip on: Click or Hover (hover also keeps click to pin a card open)
- Period: Month or Quarter rewrites every number and sentence
- Show all stories turns every card at once
- Hover a sparkline for a month's value
- Optional hook: set window.DC_FLIP = { narrate(ctx) } to return { lead, points, next } from your own logic or an LLM; the component still computes the numbers

## Accessibility
- Each face has a real button with an aria-label naming the metric and action
- The hidden face is inert
- Status uses a word and an icon as well as colour
- Change pills use ▲/▼ as well as colour
- With reduced motion the card swaps sides without rotating

## Design tokens used
`--s1`, `--ink`, `--ink-2`, `--muted`, `--surface`, `--surface-2`, `--border`, `--up`, `--down`, `--good`, `--warn`, `--crit`, `--radius` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build KPI flip cards in one self-contained HTML file with inline SVG and no libraries. Seeded data: six fictional metrics (revenue, active customers, churn, gross margin, first response time, NPS), 24 months each, with a target, a better direction, a kind (sum or level), a change type (percent or absolute), and driver weights that add up to 1. Lay the cards out in a grid with columns of at least 270px. Put both faces in the same grid cell so a card is as tall as its longer side, with backface-visibility hidden, the inner element rotating 180 degrees around Y over 0.55s, and perspective on an outer element that doesn't rotate so hover doesn't jitter. Front: period, name, large value, signed change pill coloured by whether the move is good (with an up or down triangle), area sparkline that fills the remaining height with the current period shaded and a dashed target line, and a flip button. Back: name, status chip (On track, Watch, Needs attention, each with an icon and a word), then a narrative generated from the numbers: a bold lead such as 'Revenue rose 3.1% to $1.24M, its third straight monthly gain', a sentence comparing with target, a sentence naming the largest driver and any offset, three signed driver bars, and a Next line chosen by whether the news is good. Add a Month or Quarter control that recomputes all of it, a Click or Hover flip control, and a Show all stories button. Clicking anywhere on a card flips it unless text is selected. Make the hidden face inert, move keyboard focus to the side now showing, and allow a window.DC_FLIP.narrate(ctx) override that returns lead, points and next. CSS variables for every colour, light and dark themes, and no rotation under prefers-reduced-motion.
