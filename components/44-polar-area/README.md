# Polar area (Nightingale rose)

**Category:** Charts · **Tags:** coxcomb, rose chart, seasonality, cyclical, stacked

Twelve monthly wedges whose area (not radius) is proportional to value, stacked by cause like Nightingale's rose, with a stacked / single-cause switch, square-root rings and hover readouts.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Cyclical data where the circle itself means something (months, hours, compass directions)
- Showing seasonality in a striking, editorial way
- 2–3 stacked components

## Avoid it when
- Precise comparison between non-adjacent wedges (use a bar chart)
- Linear time without a cycle
- More than three stacked components (outer layers get distorted)

## Anatomy
- 12 equal-angle wedges starting at 12 o'clock with 1.5px surface gaps
- Radius = √(cumulative value) so each layer's area is proportional to its value (never linear radius — that squares the differences)
- Stacked layers in categorical slots 1–3, innermost first; legend above
- Reference rings at round values on the square-root scale, labelled along the top spoke
- Month labels outside the rim

## Data shape
```
[{ month: "Jan", causes: { Preventable: 42, Wounds: 12, Other: 8 } }, …12]
```

## Interactions
- Switch: All causes (stacked) or one cause at a time
- Hover a wedge: month, cause, value and share of that month
- Hover a legend item to highlight that layer

## Accessibility
- Legend present; values in tooltips and in a Table view
- Area-true scaling noted in the subtitle
- Only the three categorical slots validated for all-pairs use

## Design tokens used
`--s1`, `--s2`, `--s3`, `--grid`, `--surface`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a polar area (Nightingale rose / coxcomb) chart in one self-contained HTML file with inline SVG and no libraries. Twelve monthly wedges of equal angle starting at 12 o'clock with 1.5px surface-coloured gaps, each stacked from three seeded components (e.g. incident causes). Make AREA proportional to value: the outer radius of each stacked layer is r = R × √(cumulative value ÷ max monthly total). Fill layers with categorical slots 1–3, innermost first. Draw reference rings at round values on the same square-root scale with labels on the top spoke, and month labels outside the rim. A segmented control switches between All causes (stacked) and each single cause (rescaled to its own max). Hovering a wedge shows month, cause, value and share of the month; hovering a legend item highlights that layer. Include a Table toggle. CSS variables for every colour, light and dark themes.
