# KPI tabs driving a chart

**Category:** KPI cards · **Tags:** tabs, master-detail, line chart, crosshair, Stripe style

A strip of compact KPI tiles that act as tabs: the selected KPI drives the large line chart below (this year vs last year with a crosshair), so one panel shows five metrics.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Space is tight but several metrics each need a trend
- Metrics share the same time axis
- Product analytics or finance overviews (the Stripe / GA pattern)

## Avoid it when
- Readers need to compare two metrics' trends side by side (use small multiples)
- Mobile-first layouts with >4 tabs (tiles get cramped)

## Anatomy
- Tab strip: label, value and delta per tile; the selected tab gets a 2px accent top border and surface background, others sit on the tinted strip
- Chart title repeats the selected metric
- Two series: this year (2px accent) and last year (1.5px grey); legend with both + direct end label
- Hairline y-grid, compact y ticks, monthly x labels
- Crosshair with both values and the change

## Data shape
```
[{ key: "revenue", label: "Gross volume", cy: [52 weekly values], py: [52 weekly values], fmt: "$" }, …]
```

## Interactions
- Click a tab or use ←/→ when the tab strip has focus (proper ARIA tabs pattern)
- Hover the chart: crosshair, two dots and tooltip

## Accessibility
- role=tablist / tab / tabpanel with aria-selected and roving tabindex
- Legend present for the two series; delta has glyph and sign

## Design tokens used
`--s1`, `--de-emph`, `--surface-2`, `--grid`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a KPI-tabs-plus-chart panel in one self-contained HTML file with inline SVG. Across the top, a strip of 5 compact KPI tiles (label, value, YoY delta with ▲/▼) implemented as an accessible ARIA tablist with roving tabindex and Left/Right arrow keys. The selected tab has a surface background and 2px accent top border; the rest sit on a tinted strip. Below, a 260px line chart for the selected KPI: 52 weeks of this year (2px accent line, 10% area wash) and last year (1.5px grey line), hairline gridlines, compact y ticks, month labels on x, a legend for both series, and a crosshair tooltip with both values and the change. Switching tabs redraws the chart. Seeded synthetic data. CSS variables for every colour, light and dark themes.
