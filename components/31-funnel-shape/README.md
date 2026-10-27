# Tapered funnel

**Category:** Flows & networks · **Tags:** funnel, conversion, pipeline, stages, tapered

A true funnel shape: each stage is a slice whose top width is that stage's count and whose curved sides narrow to the next stage, with conversion between stages on the right and a segment switch that morphs the shape.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Presenting a pipeline or conversion process to an audience that expects the classic funnel silhouette
- Executive or marketing summaries where the shape itself tells 'we lose most people here'
- 4–7 ordered stages

## Avoid it when
- Precise comparison of stage sizes matters (use the bar funnel: aligned bars read more accurately than tapering widths)
- Stages can grow (the shape implies narrowing)

## Anatomy
- Stages stacked top to bottom with a 2px surface gap; each slice's top width ∝ its count, its bottom width ∝ the next stage's count, sides drawn as smooth curves
- The last slice tapers to a short spout of its own width
- Ordinal single-hue ramp from a mid-light step (top) to the darkest (bottom)
- Inside each slice: count (semibold) and % of the first stage, ink chosen by fill luminance
- Left column: stage names; right column: step conversion ('↓ 52%') with the weakest step flagged

## Data shape
```
{ stages: ["Leads", "Qualified", "Demo", "Proposal", "Won"], segments: { All: [4200, 2310, 1150, 520, 238], … } }
```

## Interactions
- Segment switch morphs the funnel to the new counts (400ms ease-out; instant under prefers-reduced-motion)
- Hover a slice: it stays full strength while others dim; tooltip with count, % of start and % of previous stage

## Accessibility
- Every count and rate is printed as text
- SVG aria-label lists the stages and counts
- Weakest step marked with ▲ and words, not colour

## Design tokens used
`--seq-1 … --seq-6`, `--surface`, `--ink`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a true tapered funnel chart in one self-contained HTML file using inline SVG (no libraries). Five ordered sales stages (Leads → Qualified → Demo → Proposal → Won) with seeded counts for three segments. Stack the stages top to bottom with a 2px gap; each slice is centred, its top width proportional to the stage's count and its bottom width proportional to the next stage's count, with the sides drawn as smooth cubic curves so the outline reads as one continuous funnel; the final slice narrows into a short spout. Fill slices with an ordinal single-hue ramp from a mid-light step at the top to the darkest at the bottom. Inside each slice print the count and % of the first stage with text colour chosen by luminance; stage names sit in a left column, and step conversion ('↓ 52% continue') sits in a right column, with the weakest step flagged '▲ Biggest drop'. A segmented control switches segments and morphs the shape with a 400ms tween (instant under prefers-reduced-motion). Hover dims the other slices and shows a tooltip. CSS variables for every colour, light and dark themes.
