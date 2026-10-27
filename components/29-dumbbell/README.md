# Dumbbell (gap) chart

**Category:** Charts · **Tags:** gap analysis, two values, range, sorted dot plot

One row per category with two dots joined by a bar — this year vs target, or group A vs group B — sortable by gap, current value or name, with the gap printed at the end of each row.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The gap between two values per category is the story (actual vs target, before vs after, men vs women)
- Values don't start at zero, so bars would waste space
- 10–25 categories

## Avoid it when
- Only one value per category (use a bar or dot plot)
- More than two values per row (use a strip plot)

## Anatomy
- Two dots ≥ 8px (series slots 1 and 2) with a 2px surface ring, legend at top
- Connector: 4px rounded bar in a neutral tint between the dots
- Category labels left, gap value right (signed, coloured by whether the gap is good)
- Hairline vertical grid with compact ticks; scale does not need to start at zero

## Data shape
```
[{ name: "Engineering", a: 82, b: 76 }, …] — a = this year, b = target (or group A / B)
```

## Interactions
- Sort by gap, by this year, or by name
- Hover a row: both values and the gap; the row gets a wash
- Toggle 'Show only misses' to filter to rows below target

## Accessibility
- Legend present (two series)
- Gap printed as signed text
- Dots differ by colour and the legend; the gap colour follows the up/down text tokens

## Design tokens used
`--s1`, `--s2`, `--de-emph`, `--up`, `--down`, `--grid` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a dumbbell (gap) chart in one self-contained HTML file using inline SVG. 14 seeded departments, each with an engagement score this year and a target. Each row: department label on the left, two dots (8px, categorical slots 1 and 2, with a 2px surface ring) joined by a 4px rounded neutral connector, and the signed gap on the right in success/danger text colour. Hairline vertical grid with compact ticks; the axis need not start at zero. Legend at top for the two series. Controls: sort by gap / this year / name, and a 'Misses only' toggle that filters to rows below target. Rows animate when sorted. Hover a row for a tooltip and a hover wash. CSS variables for every colour, light and dark themes.
