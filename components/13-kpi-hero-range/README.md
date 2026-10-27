# Hero KPI with expected range

**Category:** KPI cards · **Tags:** hero number, anomaly, expected range, narrative, Pulse style

One big number with its change, a trend line drawn inside an expected-range band, and a generated sentence that says whether the latest value is normal, unusually high or unusually low.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- One metric deserves the spotlight (the north-star or the metric a page is about)
- Readers need to know if a move is noise or signal
- You want the dashboard to explain itself in words

## Avoid it when
- Several metrics are equally important (use a KPI row)
- Too little history to estimate a range (< ~8 periods)

## Anatomy
- Hero value ≥ 48px semibold, exactly one per view
- Delta vs prior week with ▲/▼ and vs-period text
- Narrative sentence built from the data; the key phrase in ink weight
- Line: 2px accent; expected range: band of mean ± 2σ of the trailing 8 weeks in a 12% accent wash
- Latest point: 8px marker with a surface ring; points outside the band get a hollow ring

## Data shape
```
{ metric: "Weekly active users", weekly: [ …26 numbers ] }
```

## Interactions
- Metric switch rebuilds the number, sentence and band
- Hover the line: crosshair with value, expected range and whether it was inside

## Accessibility
- The sentence states the conclusion in words
- Outliers are marked by shape (hollow ring), not colour alone

## Design tokens used
`--s1`, `--ink`, `--ink-2`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a hero KPI panel in one self-contained HTML file with inline SVG. Show one metric: its latest weekly value as a hero number (≥48px semibold), a delta vs the prior week with ▲/▼ coloured by whether the move is good, and a generated plain-English sentence such as 'Weekly active users were 48.2K, unusually high — 6% above the expected range of 41.0K–45.5K.' Below, a 26-week line chart (2px accent line) inside an expected-range band computed per week as mean ± 2 standard deviations of the previous 8 weeks, drawn as a 12% accent wash; mark the latest point with an 8px dot and a surface ring and give any out-of-band week a hollow ring. Hover shows a crosshair with value, range and in/out status. A segmented control switches between three metrics. Seeded synthetic data. CSS variables for all colours, light and dark themes.
