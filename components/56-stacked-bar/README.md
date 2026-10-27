# Stacked bar chart

**Category:** Basic charts · **Tags:** stacked bar, 100% bar, composition, orientation, totals

Monthly support tickets stacked by channel, switchable between vertical and horizontal and between absolute and 100%, with 2px surface gaps between segments, totals on top, inside labels where they fit, and per-segment hover.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- The total per category and its composition both matter (absolute)
- Comparing mix across categories (100%)
- 2–5 segments per bar

## Avoid it when
- Comparing a middle segment across bars precisely (its baseline moves — use grouped bars or small multiples)
- More than ~5 segments (fold into 'Other')
- Negative values

## Anatomy
- Bars ≤ 24px thick (wider allowed for few bars), segments in categorical slot order from the baseline out
- 2px surface gap between segments; 4px rounding on the outermost segment's data end only
- Totals at the bar ends in absolute mode; segment labels inside only when they fit with padding (ink chosen by fill luminance)
- Hairline grid on the value axis; 0–100% axis in 100% mode
- Legend toggles segments without recolouring

## Data shape
```
{ labels: ["Jan", …], series: [{ name: "Email", values: [ … ] }, …4] }
```

## Interactions
- Orientation: Vertical / Horizontal
- Mode: Stacked / 100%
- Legend click hides/shows a segment (one always stays)
- Hover a segment: value, share of its bar and the bar total

## Accessibility
- Legend present; inside labels only where they fit, everything else in tooltips
- Colour follows the series, never its position
- SVG aria-label states the busiest month

## Design tokens used
`--s1 … --s4`, `--surface`, `--grid`, `--axis`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a stacked bar chart in one self-contained HTML file with inline SVG and no libraries. Seeded monthly support tickets for 8 months split by four channels (Email, Chat, Phone, Self-serve). Stack segments from the baseline outward in categorical slots 1–4 with a 2px surface-coloured gap between segments, rounding only the outer data end of the last visible segment by 4px. Controls: Orientation (Vertical / Horizontal), Mode (Stacked / 100% — normalise each bar to its total, axis 0–100%), and a legend that hides/shows segments without recolouring (never hide the last). In stacked mode print each bar's total at its end; print a segment's value inside it only if the text fits with padding (pick white or dark text by fill luminance), otherwise leave it to the tooltip. Hairline gridlines and compact ticks on the value axis. Hover a segment for value, share of the bar and the total. CSS variables for every colour, light and dark themes.
