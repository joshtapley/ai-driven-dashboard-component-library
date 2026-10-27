# Beeswarm

**Category:** Charts · **Tags:** distribution, dot plot, individuals, salary bands, jitter-free

Every employee as a dot along a salary axis, swarmed so no dot overlaps, one row per department with a median tick, coloured by level, with level filters and an All-together view.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- You want the distribution and the individuals at once (salaries, response times, deal sizes, scores)
- Comparing distributions across a few groups
- Up to a few hundred points per row

## Avoid it when
- Thousands of points (use a histogram or violin)
- Only the summary matters (a box plot or bar of medians is faster to read)

## Anatomy
- x = value on a shared linear axis with compact ticks and hairline grid
- One swarm per group; dots (r = 4) are placed outward from the row's centre line so none overlap
- Colour = level (categorical slots 1–3, validated all-pairs) with a legend
- Median: a 2px ink tick across each swarm with its value
- Group labels with counts on the left

## Data shape
```
[{ name: "Employee 104", department: "Engineering", level: "Manager", salary: 148000 }, …]
```

## Interactions
- Layout switch: By department / All together (re-swarms)
- Level chips filter (dim) levels
- Hover a dot: person, department, level, salary and percentile within the department

## Accessibility
- Medians printed as text
- Level shown by colour plus legend and tooltip; dimming instead of removal keeps the shape
- SVG aria-label gives each department's median

## Design tokens used
`--s1`, `--s2`, `--s3`, `--ink`, `--grid`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a beeswarm chart in one self-contained HTML file with inline SVG and no libraries. Seeded data: ~260 fictional employees in 5 departments and 3 levels (Individual contributor, Manager, Director) with salaries that differ by department and level. Shared x axis for salary with compact ticks and a hairline grid. One row per department: place each dot (radius 4, 1px surface ring) on the x position of its value, then swarm it vertically by trying offsets 0, +d, −d, +2d, … until it doesn't overlap any already-placed dot (process dots sorted by value). Colour by level using the first three categorical slots, with a legend whose chips dim a level when toggled. Draw each department's median as a 2px ink tick with a label, and department names with counts on the left. A segmented control switches between By department and All together. Hover tooltips show name, department, level, salary and percentile within the department. CSS variables for every colour, light and dark themes.
