# Streamgraph

**Category:** Charts · **Tags:** stacked area, wiggle, composition over time, 100% area, trends

Six categories as flowing streams over a year, centred on a wavy baseline, with a Stream / Stacked / 100% offset switch, direct labels on the widest part of each stream and a hover crosshair that reads every layer.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing how the mix of several categories rises and falls over time, where overall shape and rhythm matter more than exact values
- Seasonal or event-driven popularity (genres, topics, product lines)
- Editorial or overview panels

## Avoid it when
- Exact values or precise comparison matter (use small multiples or lines)
- More than ~8 categories (fold into 'Other')
- Values can be negative

## Anatomy
- Layers in categorical slot order, largest-total stream in the middle (inside-out ordering) to minimise wiggle
- Smooth curves; a 1px surface-coloured stroke between layers acts as the gap
- Offset modes: Stream (silhouette, centred), Stacked (zero baseline with y axis), 100% (expand, with % axis)
- Direct labels at each stream's widest point when the label fits; legend always present
- Month labels on x; hairline crosshair on hover

## Data shape
```
{ weeks: ["2026-01-04", …52], series: [{ name: "Pop", values: [52 numbers] }, …6] }
```

## Interactions
- Offset switch re-shapes the layers
- Hover: crosshair at the nearest week, hovered layer stays full strength, tooltip lists every layer's value and share (hovered first)
- Click a legend item to isolate that stream; click again to restore

## Accessibility
- Legend present plus direct labels
- Tooltip lists every value as text
- Isolating a stream gives a single, readable shape

## Design tokens used
`--s1 … --s6`, `--surface`, `--grid`, `--axis` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a streamgraph in one self-contained HTML file with inline SVG and no libraries. Seeded weekly listening hours for 6 music genres over 52 weeks, each with its own seasonal peak. Order layers inside-out (largest total in the middle), colour with categorical slots 1–6 in fixed order, draw smooth curves (cubic interpolation) and separate layers with a 1px surface-coloured stroke. Offer three offsets in a segmented control: Stream (silhouette: centred on zero), Stacked (zero baseline with a y axis) and 100% (normalised with a percent axis). Put a direct label at each stream's widest point when it fits, plus a clickable legend that isolates one stream. Month labels on x. Hover shows a hairline crosshair at the nearest week, keeps the hovered layer at full opacity while dimming the rest, and a tooltip lists every genre's value and share for that week. CSS variables for all colours, light and dark themes.
