# Radar chart

**Category:** Charts · **Tags:** spider chart, profile comparison, multivariate, benchmark

Product profiles across seven scored attributes on a shared 0–100 scale: up to three products as outlined polygons with light fills, an industry benchmark as a dashed ink outline, toggleable legend and per-vertex tooltips, plus a table view.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Comparing the shape of 2–3 profiles across 5–8 attributes on the same scale (product reviews, skills, vendor scorecards)
- Showing strengths and gaps at a glance
- The audience is used to spider charts

## Avoid it when
- Attributes have different units or scales (normalise first or use bullet charts)
- Precise comparison per attribute (use grouped bars or a dot plot — area exaggerates differences)
- More than three series (shapes become unreadable)

## Anatomy
- Spokes: one per attribute, axis-grey; rings every 20 points in hairline grid with small value labels on the first spoke
- Series polygons: 2px outline in categorical slots 1–3, 12% fill, 8px vertex dots with surface rings
- Benchmark: 1.5px dashed ink outline, no fill
- Attribute labels outside the rim, anchored by side
- Legend with toggles; a single hover highlights one series and fades the others

## Data shape
```
{ axes: ["Ease of use", "Speed", …7], series: [{ name: "Product A", values: [82, 64, …] }, …3], benchmark: [70, 70, …] }
```

## Interactions
- Click legend items to show/hide a series (at least one stays)
- Hover a polygon or legend item to bring that series forward
- Hover a vertex: attribute, value and difference from benchmark
- Chart / Table toggle

## Accessibility
- Legend present (≥ 2 series); benchmark distinguished by dash, not colour
- Table view lists every value
- Uses only the three categorical slots validated for overlapping shapes

## Design tokens used
`--s1`, `--s2`, `--s3`, `--ink`, `--grid`, `--axis`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an interactive radar (spider) chart in one self-contained HTML file with inline SVG and no libraries. Seven attributes scored 0–100 for three fictional products plus an industry benchmark. Draw spokes in axis grey, concentric polygon rings every 20 points in hairline grid with small value labels along the first spoke, and attribute labels outside the rim anchored left/right/middle by angle. Each product is a polygon with a 2px outline in categorical slots 1–3, a 12% fill and 8px vertex dots with a 2px surface ring; the benchmark is a 1.5px dashed ink outline with no fill. Legend items toggle series (never hide the last) and hovering a legend item or polygon brings it to the front and fades the others. Vertex hover shows the attribute, value and difference from benchmark. Add a Chart / Table toggle. CSS variables for all colours, light and dark themes.
