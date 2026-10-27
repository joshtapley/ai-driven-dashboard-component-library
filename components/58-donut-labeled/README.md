# Donut chart (optional labels)

**Category:** Basic charts · **Tags:** donut, part to whole, direct labels, no legend, leader lines, minimal

A clean donut with no legend and the total in the centre. Labels are off by default for a minimal ring with a hover readout; switch them on to name every slice directly with its share, joined by a short leader line.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing how a total splits into 2–6 parts at a glance
- Space for a legend is tight, or a legend would make readers look back and forth
- A minimal ring next to text that already names the parts (labels off)
- One or two slices dominate and that's the message

## Avoid it when
- More than 6 slices (fold the tail into 'Other' or use a ranked bar)
- Slices are similar in size and need precise comparison (use bars)
- Composition across several groups (use 100% stacked bars)

## Anatomy
- Ring about 24% of the radius thick, 2px surface gaps between slices, starting at 12 o'clock, largest first, 'Other' last
- Direct labels outside the ring: name in ink and share in secondary ink, right-aligned on the left side and left-aligned on the right
- Leader lines: 1px from the slice's midpoint to an elbow, then horizontal to the label; labels are spaced so they never overlap
- Centre: the total and its unit; on hover it shows the slice's value instead
- Categorical slots in fixed order; no legend
- Labels off (default): the ring is centred and larger, and slices are named by the hover readout and the centre text

## Data shape
```
[{ name: "Mobile", value: 61200 }, …] — sorted largest first, 'Other' last
```

## Interactions
- Labels switch (Off / On), off by default: on adds the direct labels and leader lines and shrinks the ring to make room
- Dataset switch (Device / Region / Plan) redraws the slices and labels
- Hover a slice or its label: that slice stays full strength, the rest dim, and the centre shows its value and share

## Accessibility
- With labels on, each slice is named and its share printed beside it, so colour never carries identity alone; with labels off, pair the ring with text or a table that names the parts
- SVG aria-label lists every slice with its share
- Hover readout is mirrored by the labels when they are on

## Design tokens used
`--s1 … --s6`, `--surface`, `--ink`, `--ink-2`, `--axis` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a donut chart with no legend in one self-contained HTML file using inline SVG and no libraries. Seeded data for three datasets (sessions by device, by region, by plan), each 3–6 slices sorted largest first with 'Other' last, coloured by categorical slots in fixed order. A Labels switch (off by default) toggles direct labels; with labels off the ring is centred and larger. Draw the ring about 24% of the radius thick with 2px surface-coloured gaps, starting at 12 o'clock. With labels on, label every slice directly outside the ring: a 1px leader line from the slice's midpoint to an elbow just outside the ring, then horizontal to the label; the label shows the name in ink and the share in secondary ink, right-aligned on the left half and left-aligned on the right half. Space labels on each side so they never overlap (push them apart vertically and keep the leader lines attached). Put the total and its unit in the centre; hovering a slice or its label dims the others and swaps the centre to that slice's value and share. Segmented controls switch labels and datasets. CSS variables for every colour, light and dark themes.
