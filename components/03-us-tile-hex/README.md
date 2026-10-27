# Hex tile US map

**Category:** Maps · **Tags:** hexbin, tile grid map, categorical, legend filter

A hexagon tile map coloured by a category (the leading sales channel per state), where the legend doubles as a filter and shows each category's count.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Each state has one winning category (top channel, party, plan tier, vendor)
- You want a softer, more organic map than squares with the same equal-area fairness
- Three or fewer categories — the colour set stays distinguishable for colour-blind readers

## Avoid it when
- More than 3–4 categories (fold extras into 'Other' or use small multiples)
- The value is continuous (use a sequential tile map)

## Anatomy
- Pointy-top hexagons; odd rows shifted half a hex so neighbours nest
- Categorical fills in fixed order (slot 1, 2, 3); never re-coloured when filtered
- 2px surface-coloured gap between hexes
- Legend chips: swatch + label + count, clickable
- Margin of victory shown as fill opacity is NOT used — opacity is reserved for filtering

## Data shape
```
[{ state: "OH", channel: "Retail", share: 0.46 }, …]
```

## Interactions
- Click a legend chip to isolate that category (others drop to 15%); click again to reset
- Hover a hex: state, winning channel and its share
- Keyboard: legend chips are buttons

## Accessibility
- Legend chips are real buttons with aria-pressed
- Category name always appears in the tooltip and legend text
- Uses only the first three categorical slots, which pass all-pairs colour-blind checks

## Design tokens used
`--s1`, `--s2`, `--s3`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a hexagon tile-grid US map in one self-contained HTML file (no libraries). Use pointy-top hexagons laid out from the standard 12×8 US tile grid, shifting odd rows right by half a hex width so tiles nest; leave a 2px gap. Colour each state by its leading category (e.g. top sales channel: Online, Retail, Partner) using the first three categorical colour tokens in fixed order. Centre the state abbreviation with text colour chosen by fill luminance. Below the title, render legend chips (swatch, label, count of states) that act as filters: clicking one dims every other category to 15% opacity, clicking again resets; colours never change when filtering. Hover tooltips show the state, the winning category and its share. CSS variables for all colours, light and dark themes.
