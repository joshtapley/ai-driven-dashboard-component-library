# Contribution bars (why it moved)

**Category:** Basic charts · **Tags:** drivers, contribution, why it moved, pill bars, variance, explainer, rounded bars

Explains what drove a change in one KPI: each driver is a row with its label on the left, its signed contribution on the right and a thick, fully rounded bar underneath, sized to the biggest driver. Colour the bars by driver, in one colour or by sign; show amounts or share of the change; click a driver to highlight it.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- A headline KPI moved and readers ask why: 3–7 drivers that add up to the change
- Driver names are long phrases that need the full width of the card
- A compact side panel beside a trend chart or a narrative summary

## Avoid it when
- Showing how the start value walks to the end value step by step (use the waterfall)
- Many categories to rank (use the ranked bar chart)
- Drivers that overlap or don't add up to the change (say so, or use a table)

## Anatomy
- Header: the KPI's net change in bold and the start → end values in muted text
- Each row: driver label (left, ink) and signed value (right, tabular figures, --up or --down) on one line, with the bar on the line below
- Bars: fully rounded pills (radius = half the height), widths scaled to the largest absolute contribution, drawn over an optional faint --grid track
- Colour: By driver uses the series colours in order; One colour uses --s1; By sign uses --up and --down. Negative drivers always print a − sign and say 'down' in their label, so colour is never the only cue
- Bars grow from the left once on load (skipped for reduced motion)

## Data shape
```
{ kpi: "New MRR", start: 62400, end: 73900, drivers: [{ label: "Trials upgraded early", value: 5800 }, …] } — the driver values add up to end − start
```

## Interactions
- Colour: By driver / One colour / By sign
- Values: Amount / Share of change
- Sort: By size / As listed
- Bar thickness: Thin / Medium / Thick
- Track: On / Off
- Click a row (or press Enter) to highlight it and dim the rest; click again to clear
- Hover a row for its amount, share of the change and rank

## Accessibility
- The rows are a list; each row is a button whose aria-label gives the driver, signed amount and share
- Values are printed as text, so the bars are decorative
- Signs are written out (+ / −), not shown by colour alone
- Growth animation respects prefers-reduced-motion

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--s5`, `--up`, `--down`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--de-emph` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a 'Why it moved' contribution bar panel in one self-contained HTML file with no libraries. The KPI is New MRR this week: $62,400 last week, $73,900 this week (+$11,500). Five drivers add up to the change: Trials upgraded early +5,800, Seats added by existing teams +3,100, New self-serve customers +2,200, Switches to annual plans +900, Downgrades −500. Show the net change and the start → end values at the top. Each driver is a row: the label on the left and the signed value on the right (green for up, red for down, tabular figures) on one line, then underneath a thick, fully rounded pill bar whose width is scaled to the largest absolute driver, over a faint track. Add controls: Colour (By driver: a different series colour per row / One colour / By sign), Values (Amount / Share of change), Sort (By size / As listed), Bar thickness (Thin 6px / Medium 10px / Thick 14px) and Track (On / Off). Clicking a row highlights it and dims the others; clicking again clears. Hover shows the amount, the share of the change and the rank. Bars grow from the left once on load, skipped under prefers-reduced-motion. Rows are buttons with aria-labels, signs are always written out, CSS variables for every colour, light and dark themes.
