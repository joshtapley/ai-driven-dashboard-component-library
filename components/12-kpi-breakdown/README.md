# KPI cards with breakdown bar

**Category:** KPI cards · **Tags:** part to whole, stacked bar, composition, legend highlight

A KPI total with a single 100% stacked bar beneath it showing what it's made of; hovering a segment or legend row highlights the pair and shows its share.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The total matters and so does its mix (revenue by channel, tickets by tier, spend by team)
- There are 2–5 parts
- You need composition without a donut taking up a whole panel

## Avoid it when
- More than 5 parts (fold the tail into 'Other')
- The parts don't add up to the total (overlapping categories)

## Anatomy
- Label, value (28px semibold) and delta
- One 12px-tall 100% bar; segments in categorical order with 2px surface gaps; outer ends rounded 4px
- Legend list under the bar: swatch, name, value, share — right-aligned tabular numbers
- Highlight: hovered part stays full strength, others drop to 30%

## Data shape
```
{ label: "Revenue", total: 1280000, parts: [{ name: "Online", value: 610000 }, …] }
```

## Interactions
- Hover a segment or a legend row: both highlight together and a tooltip shows value and share
- Toggle Value / Share in the legend

## Accessibility
- Every value is in the legend as text — the bar is a summary, not the only carrier
- Legend rows are focusable and highlight on focus as well as hover

## Design tokens used
`--s1 … --s5`, `--surface`, `--ink-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build two KPI cards with a composition bar in one self-contained HTML file. Each card: label, total value (28px semibold), a delta vs last period with ▲/▼, then a single 12px-tall 100% stacked bar with segments in fixed categorical colour order, 2px surface-coloured gaps between segments and 4px rounding only on the two outer ends. Under it, a legend list with swatch, part name, value and share (tabular numbers, right-aligned). Hovering or focusing a segment or a legend row highlights that pair (others drop to 30% opacity) and shows a tooltip. A segmented control switches the legend between Value and Share. Max 5 parts; fold extras into 'Other'. CSS variables for every colour, light and dark themes.
