# US state choropleth map

**Category:** Maps · **Tags:** map, choropleth, US states, Albers, filter

A filled (choropleth) map of all 50 states and DC on an Albers projection with Alaska and Hawaii inset. Each state is shaded by its value on a sequential scale from zero (or a diverging scale for change), with a gradient legend, an optional value-label layer and click-to-filter.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The question is geographic: which states are high or low, and where they cluster
- Values are rates or shares (normalised), not raw totals
- A dashboard needs a state filter that's also a chart

## Avoid it when
- Values are raw counts that just track population or size (map a rate instead, or use a tile map / bar chart)
- Small states carry the story (they nearly disappear; use a tile map or ranked bars beside the map)
- Readers need exact comparisons (pair it with a ranked list)

## Anatomy
- Real state boundaries as inline SVG paths, separated by thin card-coloured borders
- Sequential fill from the theme's ramp, anchored at 0; 'YoY change' switches to a diverging scale centred on 0
- Gradient legend with the scale ends, plus a No data swatch for grey context shapes
- Show labels Off/On switch: value labels with a contrast-checked ink and halo; tiny shapes skip theirs
- Subtitle turns into 'Filtered to X · Clear' while a filter is set
- Boundary source credit in the footer

## Data shape
```
{ <state id>: { share: 0.142, yoy: 0.011 } }  — keyed by the shape ids in GEO.shapes (USPS state codes). GEO = { w, h, shapes: [{ id, name, d (SVG path), lx, ly (label point), a (area), data }] }, pre-projected and simplified by _geo/make_geo.py.
```

## Interactions
- Hover a state: outline plus tooltip with value and rank
- Click (or Enter/Space when focused) to filter to it; others fade to 30%. Click again, Clear or Esc to remove
- The filter is announced as a dc-filter event on window and postMessage({ dcFilter: { id, name } }) to a parent dashboard
- Measure switch (Share / YoY change) and Show labels switch

## Accessibility
- Each state with data is a focusable button with its name and value as the label, and aria-pressed for the filter
- A visually hidden ranked list repeats every value for screen readers
- Labels pick black or white ink against the fill
- Legend states the scale ends in text

## Design tokens used
`--seq-0…--seq-6`, `--div-neg`, `--div-mid`, `--div-pos`, `--surface`, `--surface-2`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a state choropleth map in one self-contained HTML file with inline SVG (no libraries, no network): all 50 states and DC on an Albers projection with Alaska and Hawaii inset. Embed pre-projected, simplified boundary paths with a label point per shape. Shade each state on a sequential colour ramp anchored at 0 (a 'YoY change' measure uses a diverging ramp centred on 0); shapes without data are neutral grey. Thin card-coloured borders between shapes. A gradient legend with the scale ends and a No data swatch. A 'Show labels' Off/On switch adds value labels (black or white ink by contrast, with a halo; skip tiny shapes). Hover shows a tooltip with value and rank; click or Enter/Space filters to that state (others fade to 30%, subtitle reads 'Filtered to X · Clear', Esc clears) and fires a dc-filter CustomEvent plus a parent postMessage. Every state is a focusable button with an aria-label; include a visually hidden ranked list. Credit the boundary source in the footer. CSS variables for every colour, light and dark themes. Seeded synthetic data.
