# Box and violin plot

**Category:** Charts · **Tags:** box plot, violin, distribution, quartiles, outliers, compare groups, spread

First-response times for five support channels side by side: box plots (median, quartiles, whiskers and outliers), violins that show the full shape, or both together, with the raw points as an optional jittered strip.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Comparing the spread of one measure across 3–12 groups (channels, teams, regions)
- Medians alone hide the story: some groups are consistent, others are unpredictable or have two peaks
- Showing outliers without letting them stretch the picture

## Avoid it when
- Audiences unfamiliar with quartiles and no room to explain (use a dot plot of medians with ranges)
- Fewer than about 15 values per group (show every value with a beeswarm)
- One group only (use a histogram)

## Anatomy
- One column per group on a shared y axis with hairline horizontal gridlines; group names and counts underneath
- Box: the middle 50% (Q1 to Q3) as a 15% tinted box with a 1.5px outline, the median as a 2.5px ink line
- Whiskers: lines to the furthest values within 1.5 × IQR, with short caps; outliers beyond them as open circles
- Violin: a mirrored Gaussian kernel density, widest at the most common values, in the series colour at 30%
- Points: every value as a small dot jittered across 60% of the column at 35% opacity
- Groups coloured by categorical slot 1–5 with no legend (names sit under each column)

## Data shape
```
[{ channel: "Chat", minutes: 3.2 }, …] — one row per value
```

## Interactions
- Shape: Box / Violin / Both
- Points: Off / Show all
- Sort: By median / As listed
- Hover a group for n, median, quartiles, whisker ends and the number of outliers

## Accessibility
- The svg has an aria-label giving each group's median and IQR
- Each group is a focusable element with its summary in an aria-label
- Medians are drawn as ink lines (not colour alone) and stated in the tooltip

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--s5`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a box and violin plot in one self-contained HTML file with inline SVG and no libraries. Seeded data: first-response times in minutes for five support channels (Chat ~3 min, tight; Phone ~6; Social ~45, wide; Email ~180 with a long tail; Web form two peaks at ~60 and ~240), 120–300 values each. One column per channel on a shared y axis (minutes, square-root scale so short and long times are both readable) with hairline gridlines, names and counts underneath. Box: Q1–Q3 as a tinted box with an outline, the median as a heavy ink line, whiskers to the furthest values within 1.5 × IQR with caps, outliers as open circles. Violin: a mirrored Gaussian kernel density in the channel's colour. Controls: Shape Box / Violin / Both (a narrow box inside the violin), Points Off / Show all (jittered dots at low opacity) and Sort By median / As listed. Hover or focus a channel for n, median, quartiles, whisker ends and outlier count. aria-label with medians and IQRs, CSS variables for every colour, light and dark themes.
