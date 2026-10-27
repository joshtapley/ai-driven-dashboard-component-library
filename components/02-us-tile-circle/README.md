# Circle tile US map

**Category:** Maps · **Tags:** proportional symbol, tile grid map, diverging, two encodings

States as circles on the tile grid: circle area shows size (revenue) and a diverging colour shows change (growth), with a region filter that dims the rest.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- You need two measures per state at once: a magnitude and a signed change
- Big states should look big without hiding small ones
- The question is 'where is growth coming from, and does it matter?'

## Avoid it when
- Precise comparison of the size measure matters (circle area is read loosely; add a ranked bar)
- Only one measure is needed (use the square tile map)

## Anatomy
- Faint square grid cell behind every state keeps the map shape readable when circles are small
- Circle area ∝ value (radius = √value), largest circle fills the cell
- Diverging fill: red = decline, grey ≈ flat, blue = growth; symmetric around 0
- State abbreviation inside circles large enough to fit it, otherwise below
- Two legends: size key (3 nested circles) and colour ramp with signed labels

## Data shape
```
[{ state: "TX", revenue: 52100000, growth: 0.064 }, …]
```

## Interactions
- Hover: tooltip with revenue, growth and share of total
- Region filter (All / West / Midwest / South / Northeast) dims other regions to 25% and totals the selection
- Size toggle: 'Revenue' or 'Equal' (equal circles turn it into a pure colour map)

## Accessibility
- Circles carry aria-labels
- Growth is also written in the tooltip and summary line, so colour is not the only channel
- Dimmed states stay hoverable

## Design tokens used
`--div-neg / --div-mid / --div-pos`, `--surface-2`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a circle tile-grid US map as a single self-contained HTML file with no libraries. Use the standard 12×8 tile positions for the 50 states + DC. In each cell draw a faint rounded square in a surface tint, then a circle whose AREA is proportional to revenue (radius = sqrt(value / max) × half the cell) and whose fill comes from a diverging red ↔ grey ↔ blue scale for year-over-year growth, symmetric around zero. Put the state abbreviation inside the circle when it fits, choosing white or dark text by fill luminance, otherwise just below it in muted text. Add a size legend (three nested circles with values) and a diverging colour legend with signed % labels. Add a region segmented control that dims other regions to 25% opacity and updates a summary line ('South: $X revenue, +Y% growth'). Add a Size toggle for Revenue vs Equal circles. Hover tooltips show revenue, growth and share of total. Use CSS variables for every colour and support light and dark themes.
