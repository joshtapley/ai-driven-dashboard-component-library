# Bivariate heatmap

**Category:** Charts · **Tags:** heatmap, bivariate, matrix, two measures, day by hour, color grid

A grid where each cell shows two measures at once through one color from a 3 × 3 key, so hot spots where both are high, or where one is high and the other low, stand out. The key shows how many cells fall in each combination, and picking a square isolates them.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Two measures matter for the same grid, such as volume and wait time by day and hour
- The interesting cells are combinations, such as high revenue with low margin
- A dashboard has room for one heatmap instead of two side by side

## Avoid it when
- Readers need exact values (use a highlight table)
- One measure tells the story (use a highlight table or calendar heatmap)
- The two measures are almost perfectly related, because only the diagonal colors appear (use one measure)

## Anatomy
- Row and column labels around a grid of rounded cells
- Each cell colored by its pair of low, mid or high classes
- A 3 × 3 color key with the count in each square, an arrow label per measure and tooltips stating each range
- A plain-language readout of the cells that are high on both measures
- A Colors switch: theme hues or two fixed pairs
- A Bins switch: equal count or equal range

## Data shape
```
{ rows: ["Pacific", …], cols: ["Jan", …], x: { name, f }, y: { name, f }, cells: [[{ x: 1200, y: .31 }, …], …] }  with one cell per row and column.
```

## Interactions
- Hover a cell for both values and their classes
- Pick a square in the key to isolate those cells; pick it again, use Show all or press Esc to clear
- Arrow keys move between cells when the grid has focus, and the readout announces each one
- Sample, Colors and Bins switches

## Accessibility
- The grid is one tab stop with arrow-key movement and a live readout
- Key squares are focusable buttons that state the combination and count
- Each square shows a number, so identity doesn't depend on color alone
- A visually hidden list repeats every value

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--ink`, `--ink-2`, `--muted`, `--surface`, `--surface-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a bivariate heatmap in one self-contained HTML file with inline SVG. Each cell has two measures. Bin each measure into three classes (equal count by default, equal range as a switch) and color each cell from a 3 × 3 grid: low-low near neutral, each axis running to its own hue, and high-high at the far end of the lightness range, interpolated in OKLab, with a matching dark-mode grid. Take the two hues from the theme's main color and its most different partner. Show a 3 × 3 key with the count in each square, arrow labels for both measures and tooltips with each range. Picking a square isolates those cells. Add a plain-language readout of the cells that are high on both. Make the grid one tab stop with arrow keys and a live region. CSS variables for every color, light and dark themes. Fictional seeded data.
