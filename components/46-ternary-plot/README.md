# Ternary plot

**Category:** Charts · **Tags:** three-part composition, simplex, channel mix, barycentric, change arrows

Each store's sales mix across three channels (online, in-store, wholesale) as a point in a triangle, sized by revenue and coloured by format, with guide lines to the three axes on hover and arrows showing how the mix moved since last year.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Every item is a mix of exactly three parts that sum to 100% (channel mix, soil texture, time allocation, vote shares)
- Clusters and drift in composition are the story
- 10–200 items

## Avoid it when
- More or fewer than three parts
- Readers are unfamiliar with the form and there's no room to explain it (use 100% stacked bars)
- Absolute amounts matter more than proportions

## Anatomy
- Equilateral triangle; each corner is 100% of one part, the opposite edge is 0%
- Grid lines every 20% parallel to each edge, ticks labelled on one edge per axis, in hairline grid
- Points: circles sized by revenue (√), coloured by store format (categorical slots 1–3), 2px surface ring
- Hover: dashed guide lines from the point to all three axes with the three percentages
- Change mode: thin arrows from last year's mix to this year's

## Data shape
```
[{ store: "Store 12", format: "Urban", revenue: 4.2e6, mix: { online: .38, inStore: .52, wholesale: .10 }, mixLastYear: { … } }, …]
```

## Interactions
- Toggle: This year / Change since last year (arrows)
- Format chips dim other formats
- Hover a point: guides to each axis and a tooltip with the three shares and revenue

## Accessibility
- Corner labels and an axis explainer in the subtitle
- Tooltip states all three percentages in words
- Only three categorical slots, validated all-pairs

## Design tokens used
`--s1`, `--s2`, `--s3`, `--grid`, `--axis`, `--ink`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an interactive ternary plot in one self-contained HTML file with inline SVG and no libraries. Seeded data: 36 fictional stores in 3 formats (Urban, Suburban, Outlet), each with revenue and a sales mix across Online / In-store / Wholesale for this year and last year (each mix sums to 1). Draw an equilateral triangle with Online at the top, In-store bottom-left and Wholesale bottom-right; add grid lines every 20% parallel to each edge in hairline grid with tick labels along one edge per axis and corner labels. Convert each mix to x,y with barycentric coordinates. Points are circles sized by √revenue, coloured by format (categorical slots 1–3) with a 2px surface ring. Hovering a point draws dashed guide lines from it to each axis and shows a tooltip with the three shares and revenue. A toggle switches to 'Change since last year', drawing thin arrows from last year's position to this year's. Format chips dim other formats. CSS variables for every colour, light and dark themes.
