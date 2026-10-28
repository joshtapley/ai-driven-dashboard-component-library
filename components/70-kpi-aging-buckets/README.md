# Aging buckets KPI card

**Category:** KPI cards · **Tags:** accounts receivable, aging, DSO, stacked bar, status colours, finance, toggle

An accounts-receivable aging card: open total and DSO up top, one tall 100% bar split into Current, 1–30, 31–60, 61–90 and 90+ days in a green-to-red status ramp, bucket totals beneath, and an optional list of the largest open balances, each with its own aging mix and its oldest bucket.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Money or work is sorted into ordered age bands that get worse with time (receivables, payables, open tickets, backlog, inventory age)
- The headline is how much is current vs overdue, with the biggest contributors one glance below
- Finance or ops dashboards where DSO (or another age metric) sits beside the total

## Avoid it when
- The categories aren't ordered by severity (use the breakdown bar with categorical colours)
- More than 6 bands
- You need the trend of aging over time (use a stacked area or column chart by month)

## Anatomy
- Header: title, open total and invoice count; the age metric (DSO) right-aligned at 28px bold with its change vs last month coloured by whether it's good
- A 44px 100% bar: one rounded segment per bucket with 3px gaps, the share printed inside segments of 12% or more
- Bucket legend: swatch, monospaced band label, total at 20px bold
- Optional detail (Top balances: Show / Hide): customer, open amount, a 12px 100% bar of that customer's aging mix, and the oldest bucket it has, in that bucket's colour

## Data shape
```
{ total, invoices, dso: 52, dsoPrev: 49, buckets: [{ key: "cur", label: "Current", value: 3810000 }, … ], top: [{ name: "Cedarline Foods", split: [312000, 158000, 61000, 43000, 0] }, …] }  — split is one amount per bucket, in bucket order.
```

## Interactions
- Hover or focus a bucket (bar segment or legend item): that bucket stays full strength in the main bar, the legend and every customer bar; the rest fade to 30%
- Hover any segment for a tooltip with amount and share
- Top balances: Show / Hide switches the bottom section on or off

## Accessibility
- Every bucket total is in the legend as text; the bars are summaries
- The status ramp is never the only cue: band labels are printed and the oldest bucket is named in words
- Legend items are focusable and highlight on focus as well as hover

## Design tokens used
`--good`, `--warn`, `--serious`, `--crit`, `--surface`, `--ink-2`, `--muted`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an accounts-receivable aging KPI card in one self-contained HTML file. Header: title 'Receivables aging', a subline with the open total and invoice count, and the DSO right-aligned (28px bold) with its change vs last month (fewer days is good, coloured accordingly). Below, one 44px-tall 100% bar split into five ordered buckets (Current, 1–30, 31–60, 61–90, 90+) coloured green → lime → amber → orange → red from status tokens, 3px gaps, 8px rounding on every segment, the share printed inside segments of at least 12%. Under it a five-column legend: swatch, monospaced band label, total (20px bold). Then an optional 'Top open balances' list (toggle Show / Hide in the header): customer name, open amount, a 12px 100% bar of that customer's aging mix, and the oldest bucket it carries in that bucket's colour. Hovering or focusing a bucket highlights it everywhere and fades the rest to 30%; tooltips give amount and share. CSS variables for every colour, light and dark themes.
