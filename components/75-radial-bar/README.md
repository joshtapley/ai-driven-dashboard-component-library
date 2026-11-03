# Radial bar chart

**Category:** Charts · **Tags:** radial bar, circular bar, concentric arcs, race track, trend, highlight

Bars bent into concentric arcs that all start at 12 o'clock and sweep clockwise by value, labelled at their start, with the latest (or fastest) bar highlighted and its value as a big KPI beside the chart. Here: how the fastest scheduled train from Tokyo to Shin-Osaka got shorter.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- A short series (3–8 items) tells one story, such as a journey time that keeps shrinking, and a striking shape matters more than precise comparison
- One bar is the hero (the latest, the record) and the rest are context
- A KPI card or poster-style tile needs more character than a plain bar chart

## Avoid it when
- Readers must compare values precisely (outer arcs look longer than inner arcs for the same value; use a bar or lollipop chart)
- There are more than about 8 items (inner rings get too short to read)
- Values can be negative

## Anatomy
- Concentric arcs, oldest or largest on the outside, starting at 12 o'clock and sweeping clockwise; the full value scale covers 270° (or 360° with the Sweep switch)
- Rounded data ends, faint tracks showing the full sweep, and dotted guide rings with tick labels (1h, 2h, 3h…) around the outside
- Labels sit to the left of the start line, right-aligned at each ring: the item name in ink and its value in muted ink
- One highlighted bar in the accent colour (latest or fastest, switchable); the others in de-emphasised greys that lighten toward the inside
- KPI block beside the chart: the highlighted value large, with a caption and the change since the first item
- Stacks the KPI under the chart on narrow screens

## Data shape
```
[{ label: "1964", value: 240, note: "Hikari, 0 Series" }, …] in minutes, plus the scale maximum (a nice round value) and the KPI caption
```

## Interactions
- Hover an arc: tooltip with the value, note and change against the item before and the first item
- Click an arc (or Enter on it) to highlight it instead; arrow keys move between arcs; Esc returns to the default highlight
- Highlight switch: Latest / Fastest; Sweep switch: 270° / 360°
- Arcs grow in from 12 o'clock on first draw (skipped under reduced motion)

## Accessibility
- Each arc is a focusable group with an aria-label giving its label, value and note
- Every value is written as text beside its arc, so the arc length is never the only channel
- A visually hidden list repeats the series in order
- The highlight uses colour plus a bolder label, not colour alone

## Design tokens used
`--s1`, `--de-emph`, `--track`, `--grid`, `--ink`, `--ink-2`, `--muted`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a radial (circular) bar chart in one self-contained HTML file with inline SVG and no libraries. Six items, the fastest scheduled train from Tokyo to Shin-Osaka by year (1964 4h00, 1965 3h10, 1986 2h56, 1992 2h30, 2015 2h22, 2020 2h21), drawn as concentric arcs with the oldest on the outside. Every arc starts at 12 o'clock and sweeps clockwise; the scale maximum (4 hours) covers 270°, with a Sweep switch for 360°. Use rounded data ends, a faint track under each arc for the full sweep, and dotted guide rings with tick labels (1h, 2h, 3h, 4h) around the outside. Right-align each label to the left of the start line at its ring: the year in ink, the time in muted ink. Highlight one arc in the accent colour (a Highlight switch picks Latest or Fastest) and draw the rest in greys that lighten toward the inside; beside the chart show the highlighted value as a big KPI ("2h 21") with the route and the change since the first year, stacked below on narrow screens. Hover shows a tooltip with the note and the change against the previous and first item; click or Enter highlights an arc, arrow keys move between arcs, Esc resets. Arcs grow in on first draw unless reduced motion is set. CSS variables for every colour, light and dark themes, and a visually hidden list of the values.
