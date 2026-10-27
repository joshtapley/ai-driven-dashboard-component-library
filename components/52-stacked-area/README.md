# Stacked area chart

**Category:** Basic charts · **Tags:** stacked area, 100% area, composition over time, part to whole

Four product lines stacked over twelve months with a Stacked / 100% switch, straight or smooth edges, a legend that toggles layers, and a crosshair tooltip with every layer, its share and the total.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The total over time and its make-up both matter
- 100% mode: how the mix shifts, regardless of total
- 2–5 layers

## Avoid it when
- Comparing the trend of a middle layer precisely (its baseline wobbles — use lines or small multiples)
- Negative values
- More than ~5 layers (fold into 'Other')

## Anatomy
- Layers stacked bottom-up in categorical slot order; 1px surface-coloured stroke separates layers
- Fills at 85% opacity so the separating strokes read
- Stacked: y axis in units from zero; 100%: y axis 0–100%
- Legend toggles layers (colours never shift when a layer hides)
- Crosshair: hairline + tooltip listing layers top-down with value, share and the total

## Data shape
```
{ labels: ["Jan", …12], series: [{ name: "Subscriptions", values: [12 numbers] }, …] }
```

## Interactions
- Mode: Stacked / 100%
- Edges: Straight / Smooth
- Click legend items to hide/show layers (one always stays)
- Hover for the crosshair tooltip

## Accessibility
- Legend present; tooltip lists every value and share
- Colour follows the layer, never its position
- SVG aria-label summarises the latest mix

## Design tokens used
`--s1 … --s4`, `--surface`, `--grid`, `--axis` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a stacked area chart in one self-contained HTML file with inline SVG and no libraries. Four seeded revenue streams (Subscriptions, Services, Hardware, Marketplace) over 12 months. Stack layers bottom-up in categorical slot order (1–4) at 85% opacity with a 1px surface-coloured stroke between them. Add segmented controls for Stacked vs 100% (normalise each month) and Straight vs Smooth edges (cubic interpolation of both the top and bottom of each layer). The y axis starts at zero with compact ticks (or 0–100% in 100% mode), hairline gridlines and month labels. A legend toggles layers on and off without recolouring the rest (never hide the last). Hover shows a crosshair and a tooltip listing layers top-down with value and share plus the month total. CSS variables for every colour, light and dark themes.
