# US state bivariate map

**Category:** Maps · **Tags:** map, bivariate, choropleth, US states, two measures, filter

A bivariate choropleth of all 50 states and DC on an Albers projection with Alaska and Hawaii inset. One color from a 3 × 3 key shows two measures at once, so places that are high on both, or high on one and low on the other, stand out on a single map.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The question is how two rates line up across states
- The interesting places are combinations, such as high sales with low satisfaction
- Side-by-side maps would force readers to compare back and forth

## Avoid it when
- One measure tells the story (use a standard choropleth)
- Values are raw totals that just track population (map rates)
- Readers need exact values (pair it with a ranked table)
- The two measures are almost perfectly related, because only the diagonal colors appear

## Anatomy
- Real state boundaries as inline SVG paths
- Each measure binned into low, mid and high
- One fill per pair of classes: low-low near neutral, each axis running to its own hue, high-high at the far end of the lightness range
- A 3 × 3 color key with the count in each square, arrow labels and tooltips stating each range
- A plain-language readout of how many are high on both and low on both
- A Colors switch (theme hues or two fixed pairs) and a Bins switch (equal count or equal range)
- Boundary source credit

## Data shape
```
{ <state id>: { x: 214, y: 71 } }, keyed by the shape ids (USPS state codes), with a name and formatter for each measure.
```

## Interactions
- Hover a state for both values and their classes
- Pick a square in the key to isolate those places; pick it again, use Show all or press Esc to clear
- Click a state to filter to it, announced as a dc-filter event and postMessage({ dcFilter: { id, name } }) to a parent dashboard
- Colors and Bins switches

## Accessibility
- Key squares are focusable buttons that state the combination and count
- Each square shows a number, so identity doesn't depend on color alone
- A visually hidden list repeats every value
- The readout is a live region

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--surface`, `--surface-2`, `--ink`, `--ink-2`, `--muted` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a bivariate state choropleth in one self-contained HTML file with inline SVG: all 50 states and DC on an Albers projection with Alaska and Hawaii inset, using pre-projected boundary paths. Bin each of two measures into three classes (equal count by default, equal range as a switch). Fill each state from a 3 × 3 grid: low-low near neutral, each axis running to its own hue, and high-high at the far end of the lightness range, interpolated in OKLab, with a matching dark-mode grid. Take the two hues from the theme's main color and its most different partner. Show a 3 × 3 key with the count in each square, arrow labels and tooltips with each range. Picking a square isolates those places. Hover shows both values; click filters and fires a dc-filter event. Add a plain-language readout and a hidden list of all values. CSS variables for every color, light and dark themes. Seeded synthetic data.
