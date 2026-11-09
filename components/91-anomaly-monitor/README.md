# Anomaly monitor

**Category:** Charts · **Tags:** anomaly, monitoring, outliers, alerts, expected range, time series, control chart, operations

A time-series monitor that learns each day's expected range from recent history, flags values outside it as Watch or Alert, and explains every incident in plain words. A status strip gives the current state, and clicking an incident finds it on the chart.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Watching a daily or hourly metric for unusual values
- Normal levels change by day of the week, so one fixed threshold would raise false alarms
- Readers need to know what is unusual now, and by how much

## Avoid it when
- There are fewer than about seven weeks of history, because the expected range needs it
- A fixed target or limit is what matters (use KPI cards with target and pace)
- The goal is explaining why the number moved (use contribution bars)

## Anatomy
- Flagged days are left out of the range calculation, so an incident can't widen the range that judges it
- Status strip: latest value, expected value and range, current status with an icon and label, and the incident count
- Shaded expected range with a dashed expected line behind the actual line
- Alert circles and Watch diamonds, with the incident's days shaded
- Incident list, newest first, each stating the date, value, and how far it was from expected
- Legend and a one-line note on how the range is calculated
- Switches for metric, period, sensitivity and direction

## Data shape
```
[{ date: "2026-10-31", value: 1284 }, …]  one row per day, oldest first, with no gaps. Each metric has a name, a formatter and a flag for whether lower is worse.
```

## Interactions
- Metric, Period, Sensitivity and Direction switches
- Hover the chart for the day's value, expected value and range
- Click an incident to mark it on the chart; click again to clear
- New incidents are found from history before each day, so the chart never uses the future to judge the past

## Accessibility
- Incidents are real buttons with full sentences
- Status uses an icon and a word as well as color
- Alert and Watch use different marker shapes
- The status strip is a live region and the svg has a summary label

## Design tokens used
`--s1`, `--crit`, `--warn`, `--good`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--axis`, `--surface`, `--surface-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an anomaly monitor in one self-contained HTML file with inline SVG. Input: a daily series with at least seven weeks of history. For each day, using only earlier days, set the expected value to the median of the same weekday over the previous five weeks, and the spread to 1.4826 times the median absolute deviation of the last 28 days of forecast errors, with a floor of 2% of expected. Flag a day when its z-score passes the sensitivity (low 4, medium 3, high 2.2); it is Watch up to 1.5 above that and Alert beyond. Merge adjacent flagged days into one incident. Draw a shaded expected range, a dashed expected line and the actual line, with Alert circles, Watch diamonds and shaded incident days. Above it show the latest value, expected range, status with an icon and word, and incident count. Beside it list incidents newest first as full sentences with the percent difference; clicking one marks it on the chart. Add metric, period, sensitivity and spikes/drops switches, a legend and a crosshair tooltip. CSS variables for every color, light and dark themes. Fictional seeded data.
