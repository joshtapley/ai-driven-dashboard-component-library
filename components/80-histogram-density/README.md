# Histogram and density plot

**Category:** Charts · **Tags:** histogram, density, distribution, kde, bins, spread, skew

How 1,400 delivery times are spread: a histogram with a bin-width switch, a smooth density curve, or both, with the mean and median marked. Compare two services on one axis to see which is faster and which is more predictable.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing the shape of one measure: where most values sit, how wide the spread is, whether it is skewed or has two peaks
- Comparing the distributions of two (at most three) groups on the same axis
- Hundreds to millions of values (each value is not shown, only the shape)

## Avoid it when
- Fewer than about 30 values (show every value with a beeswarm or strip plot)
- Comparing many groups (use box and violin plots)
- Readers expect exact counts per category (use a bar chart; categories are not bins)

## Anatomy
- x = value on a linear axis; y = count (histogram) or share of values per unit (density)
- Bars touch (1px surface gap) because bins are continuous; bin width is stated in the subtitle
- Density: a smooth curve from a Gaussian kernel (bandwidth by Silverman's rule), 2.5px stroke over a 15% fill
- Mean as a dashed ink line, median as a solid ink line, each with its value
- Compare mode: two groups in series colours 1 and 2, histograms as overlapping outlines and densities with light fills, plus a legend

## Data shape
```
[{ service: "Standard", minutes: 34.5 }, …] — one row per value
```

## Interactions
- View: Histogram / Density / Both
- Bins: 2 / 5 / 10 minutes
- Compare: One service / Two services
- Hover a bar for its range, count and share; hover the curve area for the density at that point

## Accessibility
- The svg has an aria-label giving count, mean, median and the middle 80% range
- Mean and median printed as text on the chart
- Groups differ by line style (outline vs filled) as well as colour

## Design tokens used
`--s1`, `--s2`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a histogram and density plot in one self-contained HTML file with inline SVG and no libraries. Seeded data: 800 'Standard' delivery times (right-skewed, mostly 25–60 minutes) and 600 'Express' times (tighter, around 22 minutes). x = minutes on a linear axis with compact ticks; y = count for the histogram or density for the curve, with hairline horizontal gridlines. Bars touch with a 1px gap. Draw the density with a Gaussian kernel (Silverman bandwidth) as a 2.5px line over a 15% fill. Mark the mean (dashed) and median (solid) in ink with labels. Controls: View Histogram / Density / Both (density scaled to counts when shown together), Bins 2 / 5 / 10 minutes, and Compare One service / Two services (series colours 1 and 2 with a legend; histograms become overlapping outlines). Tooltips on bars show the range, count and share. aria-label with count, mean, median and the 10th–90th percentile range, CSS variables for every colour, light and dark themes.
