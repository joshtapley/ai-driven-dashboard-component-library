# Activity rings (goal tracker)

**Category:** Gauges · **Tags:** concentric rings, goals, daily targets, overflow

Three concentric rings track daily goals (calls, demos, deals); rings can lap past 100%, and a week strip of mini rings lets you pick the day.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- A person or team has 2–3 daily or weekly goals with different units
- Over-achievement should be visible (a second lap)
- A motivational, personal view — sales reps, coaches, habit trackers

## Avoid it when
- Comparing goals across many people (use a table or bullet charts)
- More than 3 rings — inner rings get too short to read

## Anatomy
- Three concentric 270°→full rings, outer to inner = series slots 1, 2, 3 in fixed order
- Track = 18% tint of each ring's colour
- Progress past 100% keeps going as a second lap with a surface-coloured ring on its end cap
- Legend column: swatch, goal name, value / goal and % — the legend is the readout
- Week strip: seven small ring sets; the selected day is outlined

## Data shape
```
{ goals: [{ name: "Calls", goal: 40 }, …], days: [{ date: "Mon", values: [38, 3, 1] }, …] }
```

## Interactions
- Click a day in the strip (or use arrow keys) to show it in the big rings
- Hover a ring: value, goal and %

## Accessibility
- Values and % written in the legend — rings are never the only channel
- Day buttons are real buttons with aria-pressed and arrow-key navigation
- Uses the three categorical slots validated for all-pairs colour-blind separation

## Design tokens used
`--s1`, `--s2`, `--s3`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an activity-rings goal tracker in one self-contained HTML file with inline SVG. Draw three concentric rings (outer → inner = categorical colours 1, 2, 3) on tracks that are 18% tints of each colour, 14px wide with round caps, starting at 12 o'clock and running clockwise; if progress exceeds 100%, continue drawing a second lap on top with a 2px surface-coloured outline around its end cap so the overlap is visible. To the right, a legend that doubles as the readout: swatch, goal name, 'value / goal' and percentage. Under it, a strip of seven small ring sets (Mon–Sun) as buttons; clicking one (or arrow keys) loads that day into the big rings, and the selected day is outlined. Hover tooltips on rings. CSS variables for every colour, light and dark themes.
