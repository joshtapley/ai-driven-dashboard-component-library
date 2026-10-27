# Conversion funnel

**Category:** Charts · **Tags:** conversion, drop-off, stages, segments, ordinal ramp

A stage-by-stage funnel drawn as aligned horizontal bars on an ordinal blue ramp, with step conversion and drop-off between stages, overall conversion, and a device segment switch.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- A process with ordered stages where people drop out (signup, checkout, hiring, sales pipeline)
- The biggest leak is the insight
- Comparing funnel shape across segments

## Avoid it when
- Stages aren't strictly sequential subsets
- Values can increase between stages (use a bar chart or Sankey)

## Anatomy
- One row per stage: name + count on the left, bar from a common left baseline, % of first stage at the tip
- Bars on an ordinal ramp (seq step 250 → 700 in light mode) — darker = deeper in the funnel
- Between rows: step conversion '↓ 42% continue' and drop-off count in muted text; the worst step flagged with a ▲ 'Biggest drop' marker
- Header readout: overall conversion first → last

## Data shape
```
{ stages: ["Visited", "Viewed product", "Added to cart", "Checkout", "Purchased"], segments: { All: [120000, 64000, 18500, 9100, 6400], Mobile: […], Desktop: […] } }
```

## Interactions
- Segment switch: All / Mobile / Desktop — bars animate to new widths
- Hover a bar: count, % of start, % of previous stage
- Hover a step connector: drop-off detail

## Accessibility
- All rates printed as text
- Biggest drop marked with a glyph + words
- Ordinal ramp starts at a step that clears 2:1 against the surface

## Design tokens used
`--seq-1 … --seq-6`, `--ink`, `--muted` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a conversion funnel in one self-contained HTML file. Five ordered stages (Visited → Viewed product → Added to cart → Checkout → Purchased) with seeded counts for three segments (All, Mobile, Desktop). Each stage is a row: name and count on the left, a horizontal bar from a shared left baseline whose width is the count relative to the first stage, and '% of start' at the bar tip. Colour bars with an ordinal single-hue ramp from a mid-light step (that still clears 2:1 contrast on the surface) to the darkest step, deeper stages darker. Between rows show step conversion ('↓ 48% continue') and the drop-off count in muted text, and flag the worst step with '▲ Biggest drop'. A header readout states overall conversion. A segmented control switches segments and bars animate to new widths with CSS transitions. Hover tooltips. CSS variables for every colour, light and dark themes.
