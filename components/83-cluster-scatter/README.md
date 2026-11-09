# Cluster scatter with named groups

**Category:** Charts · **Tags:** scatter, clusters, k-means, segmentation, groups, annotation, editorial, blob, contour, callouts, template

An editorial scatter plot that finds its own groups and says whether they're real. K-means clusters the points, a built-in test checks the split against what one undivided cloud would produce, a dashed organic outline wraps each group, and every group gets a bold name and one or two labelled items. Paste your own CSV, rename groups on the chart and drag any label.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Telling a story about the kinds of thing in a set (the three types of customer, film, store or feature)
- 20–300 items with two measures that fall into visible groups
- A presentation or article where named groups and a few famous examples matter more than exact values

## Avoid it when
- The points form one continuous cloud with no real groups (use a scatter plot with a trend line)
- Thousands of points (use a hexbin or 2D density)
- Exact values are the main point for every item (use a table component; the built-in table view is for quick lookup)
- The groups need dozens of names (the chart reads best with 2–6)

## Anatomy
- Editorial header: large bold title and one-line subtitle, both editable in place
- Hairline grid with heavy zero lines; mono tick labels that carry the unit only on the top y tick and the first x tick
- Clustering: in Auto, k-means++ on x and y robustly scaled by median and IQR, with the group count set by a real-groups test against simulated single clouds; a fixed group count uses range-normalised x and y with 24 seeded restarts; a cluster column in the data skips clustering
- Verdict note above the plot (Auto only): clear groups or no clear groups, the separation score against a single cloud of the same size, and how many outliers were set aside
- Outliers: in Auto, a point the test set aside that sits beyond twice its nearest group's reach stays on the plot as a grey dot outside the groups; the rest rejoin their nearest group
- Blob: the outer contour of a metaball field built from the points and their minimum spanning tree, traced with marching squares, so every group is one connected shape that follows its points; a keep-out band stops neighbouring blobs touching
- Blob style: categorical fill at 14%, 1.2px dashed outline
- Dots: radius 6, group colour, darker ring of the same hue
- Group name: bold, in the group's colour, placed in open space next to its own blob and closer to it than to any other
- Callouts: one or two per group (the most extreme items by default), with thin leader lines, placed to avoid dots, names and other labels
- Table view: one section per group, highest average y first, with the group's size and medians on its section row, items sorted by y inside it, and outliers last

## Data shape
```
CSV with a header row: name,x,y and optionally cluster (your own groups) and label (1 pins that item's callout). As JS: [{ name: "Hartwell's", x: 81, y: 4.6, cluster: "The Institutions", label: true }, …]
```

## Interactions
- Groups: Auto / 2–6 re-clusters, and From data when a cluster column exists
- Callouts: None / 1 / 2 per group
- Outline: Snug / Medium / Roomy
- Click a group name to rename it; drag group names and callouts to move them
- Click a dot to add or remove its callout
- Hover a blob to spotlight its group and read its size and medians; hover a dot for its values
- Edit data: paste CSV or tab-separated rows and set axis titles and number formats such as $#m
- Spreadsheet icon: switch between the chart and a table of every item by group; the table follows the Groups control, renames and new data
- Download the finished chart with its title and source as PNG or SVG

## Accessibility
- The svg has an aria-label listing each group and its size
- The verdict note is a live status region, so a screen reader hears when it changes
- Group identity is carried by the enclosing outline and the adjacent name, not by colour alone
- Group names are focusable; Enter opens the rename box
- The table view is a real table with row-group headers, and its icon button reports its state with aria-pressed
- The data stays readable as text in the Edit data panel

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--s5`, `--s6`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--axis`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an editorial cluster scatter plot in one self-contained HTML file with inline SVG and no libraries. Data: rows of name, x, y, with optional cluster and label columns. If there is no cluster column, offer a segmented control for Auto or a fixed k. A fixed k normalises x and y to 0–1 and runs k-means++ (24 seeded restarts). Auto scales x and y by (value − median) / IQR, sets aside at most 5% of points that are far from every neighbour (after clustering, each rejoins its nearest group unless it lies beyond twice that group's widest member, and then it's drawn as a grey dot in no group), then scores the best k-means split for each k from 2–6 by mean silhouette and compares it with the same steps run on simulated single clouds of matching size, spread and correlation (half Gaussian, half evenly filled). Draw the k that beats those clouds by the widest margin in either case, and show a one-line note above the plot saying clear groups or no clear groups, with the silhouette against the simulated average. Below 12 points, say there are too few to test and use the highest silhouette. Above 100 points, run the test on a seeded random 100 and label every point at the k it finds. For each group draw one organic outline: on a 4px grid over the plot compute a metaball field F = cube root of the sum of exp(−3d²/2σ²) over the group's points, plus the same term weighted 0.216 using distance to each edge of the group's minimum spanning tree (this guarantees one connected shape); set G = min(F − 0.35, distance to the nearest other group's skeleton − distance to this group's skeleton − 2×gap) so neighbours never touch; trace G = 0 with marching squares, keep the largest loop, apply five 1-2-1 smoothing passes, keep every third point and draw a closed Catmull-Rom path, with a 14% categorical fill and a 1.2px dashed outline. Dots have radius 6 and a darker ring. Pick one or two callouts per group automatically (the point farthest from the centroid, then the point farthest from it) and place each by scoring candidate positions around the dot: penalise overlap with dots, other labels and other blobs, and leaders crossing dots. Place each bold, group-coloured name in open space beside its blob, nearer its own blob than any other. Click a name to rename it, drag names and callouts, click a dot to toggle its callout. Heavy zero axes, hairline grid, mono tick labels with the unit on only the top y tick and first x tick. Large bold title, one-line subtitle, source line. Add a spreadsheet icon button that switches the plot to a table with one section per group (name, size and median x and y on the section row, then items by descending y, outliers last) and hides the chart-only controls. Sample data must be fictional. CSS variables for every colour, light and dark themes.
