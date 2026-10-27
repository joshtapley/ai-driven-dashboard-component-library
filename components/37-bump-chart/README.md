# Bump chart

**Category:** Charts · **Tags:** ranking, rank over time, leaderboard history, highlight

Rank over time for ten apps across twelve weeks: smooth lines between rank positions, everything grey except up to three picked apps in colour with rank numbers at every point, and labels at both ends.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The order matters more than the values (charts positions, league tables, market share rank)
- You want to show climbers, fallers and swaps across many periods
- 5–15 entities

## Avoid it when
- The gaps between values matter (a #1 that leads by 40% looks the same as one that leads by 1%) — use a line chart
- Only two periods (use a slopegraph)

## Anatomy
- y = rank (1 at the top), evenly spaced; x = periods
- Lines: smooth S-curves with flat tangents at each period, 2px de-emphasis grey; selected lines 3px in categorical slots 1–3
- Points: 4px grey dots; selected lines get 20px circles with the rank number inside
- Labels at the start (left) and end (right): rank and name; selected labels in ink weight
- Legend chips for the current selection with a clear button

## Data shape
```
{ periods: ["W1", …12], series: [{ name: "Lumen Notes", ranks: [3, 2, 2, 1, …] }, …10] }
```

## Interactions
- Hover a line or label: it darkens and a tooltip summarises best, worst and net change
- Click a line or label to add or remove it from the selection (max 3; the oldest drops off)
- Selection keeps its colour while selected — colour follows the app, never its rank

## Accessibility
- Rank numbers printed inside selected points
- Labels at both ends name every line
- SVG aria-label summarises the biggest climber and faller

## Design tokens used
`--s1`, `--s2`, `--s3`, `--de-emph`, `--ink`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an interactive bump chart in one self-contained HTML file with inline SVG and no libraries. Seeded weekly rankings for 10 fictional apps over 12 weeks (derive ranks from noisy scores so lines cross). y is rank with 1 at the top, evenly spaced; x is weeks. Draw each app as a smooth line using cubic curves with horizontal tangents at every week; unselected lines are 2px de-emphasis grey with 4px dots, selected lines (up to 3) are 3px in categorical slots 1–3 with 20px circles that show the rank number in white. Label every line at the left (start rank + name) and right (end rank + name). Hover darkens a line and shows best rank, worst rank and net change; clicking a line or label toggles it in the selection (max 3, oldest drops off), and colours stay attached to the app while selected. Show the selection as legend chips with a Clear button. Default selection: the biggest climber, the biggest faller and the final #1. CSS variables for every colour, light and dark themes.
