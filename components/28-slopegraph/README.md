# Slopegraph

**Category:** Charts · **Tags:** before and after, rank change, two periods, highlight

Two vertical axes (before and after) joined by one line per category: biggest riser and faller highlighted by default, everything else grey, hover to spotlight any line, and a Value / Rank switch.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Exactly two time points (or two conditions) per category
- Both the change and the re-ordering matter
- A cleaner alternative to clustered bars for before/after

## Avoid it when
- More than two periods (use a line chart)
- Many categories crossing at similar values (labels collide — use a dumbbell or table)

## Anatomy
- Two labelled period axes at left and right
- Lines 1.5px de-emphasis grey; highlighted lines 2.5px in diverging positive (riser) / negative (faller) hues with 8px end dots + surface ring
- Labels at both ends: name + value; labels nudged apart by a minimum spacing with thin leader ticks so they never overlap
- Value mode uses a shared linear scale; Rank mode uses evenly spaced ranks (1 at top)

## Data shape
```
[{ name: "Austin", before: 61.2, after: 74.8 }, …]
```

## Interactions
- Hover a line or label: it turns ink and comes to front; others fade
- Value / Rank switch
- Click a line to pin the highlight

## Accessibility
- Every line labelled at both ends with values
- Riser/faller called out in the subtitle in words
- Highlight uses width and dots, not only colour

## Design tokens used
`--div-pos`, `--div-neg`, `--de-emph`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a slopegraph in one self-contained HTML file with inline SVG. 12 seeded cities each with a 2025 and 2026 score. Draw two vertical period axes (left 2025, right 2026) and one line per city; by default all lines are 1.5px de-emphasis grey except the biggest riser (diverging positive colour) and biggest faller (diverging negative colour), drawn 2.5px with 8px end dots that have a 2px surface ring. Label both ends with name and value; resolve label collisions by enforcing a minimum vertical spacing and drawing thin leader ticks from the dot to the moved label. Hovering a line or label turns it ink, brings it to the front and fades the others; clicking pins it. A Value / Rank segmented control switches between a shared linear value scale and evenly spaced ranks. The subtitle names the riser and faller in words. CSS variables for every colour, light and dark themes.
