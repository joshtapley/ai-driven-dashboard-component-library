# Waterfall (bridge) chart

**Category:** Charts · **Tags:** P&L, bridge, variance, EBITDA, contributions

A profit-and-loss bridge from revenue to net income: floating bars for each increase or decrease, solid subtotal bars, connector lines between steps and value labels; switch quarters to watch the bridge rebuild.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Explaining how a starting value becomes an ending value through additions and subtractions
- P&L walks, budget-to-actual variance, headcount bridges, price-volume-mix
- The audience is finance or leadership

## Avoid it when
- Steps aren't additive
- There are more than ~12 steps (group minor ones)

## Anatomy
- Columns ≤ 48px with 4px rounding on the free end only
- Increase = diverging positive hue, decrease = diverging negative hue, totals/subtotals = solid ink-2
- 1px dashed connectors from each bar's end to the next bar's start
- Value labels above increases and below decreases (signed), totals labelled in ink weight
- Hairline grid and compact y ticks; category labels wrap to two lines

## Data shape
```
[{ label: "Revenue", value: 4.82e6, type: "total" }, { label: "COGS", value: -1.93e6 }, { label: "Gross profit", type: "subtotal" }, …]
```

## Interactions
- Quarter switch animates bars to new heights
- Hover a bar: start, change and end values, plus % of revenue

## Accessibility
- Every step labelled with a signed value — direction not carried by colour alone
- Legend explains increase / decrease / total
- SVG has an aria-label summarising start and end

## Design tokens used
`--div-pos`, `--div-neg`, `--ink-2`, `--axis`, `--grid` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a P&L waterfall (bridge) chart in one self-contained HTML file with inline SVG. Steps: Revenue (total) → COGS → Gross profit (subtotal) → Sales & marketing → R&D → G&A → EBITDA (subtotal) → D&A → Interest → Taxes → Net income (total), with seeded values for four quarters. Draw floating columns (≤48px wide, 4px rounding on the free end only): increases in the diverging positive colour, decreases in the diverging negative colour, totals and subtotals solid in secondary ink, all starting from zero. Connect each bar's end to the next bar's start with a 1px dashed line. Label values above increases, below decreases (signed, compact $), and in ink weight on totals. Category labels under the axis wrap to two lines. Add a legend (Increase / Decrease / Total) and a quarter segmented control that animates bar positions. Hover tooltips show start, change, end and % of revenue. CSS variables for every colour, light and dark themes.
