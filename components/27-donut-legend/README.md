# Donut with interactive legend

**Category:** Charts · **Tags:** donut, part to whole, legend filter, centre readout

A donut chart whose centre shows the total (or the hovered slice), with a legend table that toggles slices on and off and recomputes shares — the polished way to do the pie everyone asks for.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Stakeholders insist on a pie/donut for 2–6 parts of a whole
- One or two parts dominate and that's the message
- The legend doubles as the precise readout

## Avoid it when
- More than 6 parts or similar-sized parts (use a ranked bar)
- Comparing composition across groups (use 100% stacked bars)

## Anatomy
- Ring 20px thick with 2px surface gaps between slices; starts at 12 o'clock, largest first, 'Other' last
- Centre: total (or hovered slice value + name) in ink, label in secondary ink
- Legend table to the right: toggle swatch, name, value, share — tabular numbers
- Hidden slices show a hollow swatch and struck-through name; shares recompute over the visible parts

## Data shape
```
[{ name: "Organic search", value: 48200 }, …]
```

## Interactions
- Hover a slice or legend row: slice pops out 4px, others dim, centre shows that slice
- Click a legend row to hide/show the slice (never hides the last one)
- Keyboard: legend rows are checkbox-like buttons

## Accessibility
- Legend rows use role=switch with aria-checked
- Every value and share is in the legend text
- Uses categorical slots in fixed order, so colours never shift when slices hide

## Design tokens used
`--s1 … --s6`, `--surface`, `--ink`, `--ink-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a donut chart with an interactive legend in one self-contained HTML file using inline SVG. Six seeded traffic sources sorted largest first with 'Other' last, coloured by categorical slots in fixed order (colours never change when slices hide). Ring 20px thick with 2px surface-coloured gaps between slices, starting at 12 o'clock. The centre shows the total visible sessions; hovering a slice or legend row pops that slice out 4px, dims the others and shows the slice's value, name and share in the centre. To the right (stacked below on narrow screens), a legend table with a toggle swatch, name, value and share; clicking a row hides/shows that slice (role=switch, aria-checked, never hide the last visible) and shares recompute over visible parts. CSS variables for all colours, light and dark themes.
