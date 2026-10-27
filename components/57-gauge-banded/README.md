# Speedometer gauge (configurable)

**Category:** Gauges · **Tags:** speedometer, banded gauge, segmented gauge, tapered needle, target

A bold speedometer: a thick arc that sweeps 180–270°, three gauge styles (banded zones, progress fill, lit segments), a tapered needle with a round hub, an optional target notch and the value set large in the gauge's opening.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- One headline KPI against a range or target, where the dial itself is the hero of the panel
- Executive summaries and wallboards that need an at-a-glance 'how close are we?'
- Ranges with meaningful zones (poor / fair / good)

## Avoid it when
- Comparing several metrics precisely (use bullet charts)
- The trend matters more than the current value (use a KPI card with sparkline)
- Small spaces — the thick arc needs ~220px to read

## Anatomy
- Arc: thick annular band (inner radius ≈ 56% of outer), sweep 180° / 240° / 270°, opening at the bottom
- Banded style: three zones in an ordinal single-hue ramp (light → dark), no gaps between zones
- Progress style: pale track of the same hue with the accent filled from the start to the value
- Segmented style: 12 segments with small gaps; segments up to the value light up along the ramp, the rest stay track-coloured
- Needle: tapered triangle from the hub to the inner edge of the band, ink colour, with a round hub; or a thin line; or none
- Target: an ink notch across the band with a small label outside the arc
- Value: 44px bold in the opening (or under the hub for 180°) with a caption in secondary ink; min and max at the arc ends

## Data shape
```
{ value: 71.6, min: 0, max: 100, target: 80, bands: [50, 80], label: "Progress to target", format: "%" }
```

## Interactions
- Style: Banded / Progress / Segmented
- Sweep: 180° / 240° / 270°
- Needle: Tapered / Line / None
- Target on/off
- Value slider animates the needle and fill (400ms ease-out; instant under prefers-reduced-motion)
- Hover: value, target gap and which zone the value is in

## Accessibility
- role=meter with aria-valuemin / max / now and a text label
- The value and zone are printed, never implied by colour alone
- The slider is a labelled native range input
- Motion respects prefers-reduced-motion

## Design tokens used
`--seq-0 … --seq-6`, `--track`, `--s1`, `--ink`, `--ink-2`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a configurable speedometer gauge in one self-contained HTML file with inline SVG and no libraries, in a bold modern style: a thick annular arc (inner radius about 56% of the outer) with its opening at the bottom, a tapered triangular needle in the ink colour running from just behind a round hub to the inner edge of the band, and the value set large and bold in the opening with a caption under it. Add controls for: Style — Banded (three zones split at two thresholds, filled with an ordinal single-hue ramp from light to dark, no gaps), Progress (pale track of the same hue, accent fill from the start to the value) and Segmented (12 segments with small gaps that light up along the ramp up to the value); Sweep — 180°, 240° or 270° (for 180° put the value under the hub and shrink the SVG height to fit); Needle — Tapered, Line or None; and a Target toggle that draws an ink notch across the band with a small label outside the arc. A labelled range slider sets the value and animates the needle and fill over 400ms with ease-out (instant under prefers-reduced-motion). Print min and max at the arc ends. Give the gauge role=meter with aria values. Hover shows the value, the gap to target and the zone name. CSS variables for every colour, light and dark themes.
