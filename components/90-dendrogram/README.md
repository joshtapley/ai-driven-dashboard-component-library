# Dendrogram with draggable cut

**Category:** Hierarchies · **Tags:** dendrogram, hierarchical clustering, tree, radial, linkage, cut, groups, heatmap

A dendrogram that clusters items on several measures and shows how they merge, step by step. Drag the cut line to choose the groups, switch between tree and radial layouts, and read a profile strip and plain-language descriptions of what makes each group different.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing how items group at every level of similarity, not just at one chosen number of groups
- Deciding how many groups a set should have
- Up to about 60 items with several numeric measures, such as stores, products or survey questions

## Avoid it when
- There are hundreds of items, because leaf labels stop being readable (use a cluster scatter)
- The hierarchy is already known, such as an org chart (use a tree diagram)
- There are only two measures and a clear picture of them matters (use a cluster scatter)

## Anatomy
- Tree or radial layout, with branches joining at the distance where items merge
- A dashed cut line with a handle: branches below it take their group's color and branches above it stay neutral
- A distance axis on the tree layout
- Leaf labels in tree order
- A profile strip showing each measure's position against the average, on the tree layout
- A group list with size and the measures that most set each group apart
- Switches for sample, layout, linkage, group count and profile strip

## Data shape
```
{ items: ["Harbor St", …], measures: ["Sales per sq ft", …], values: [[612, 38, 1240, .41, .06], …] }  with one row per item and one number per measure. Measures are scaled by median and IQR before clustering.
```

## Interactions
- Drag the cut line, or focus its handle and use the arrow keys, to change the number of groups
- Groups: Auto picks the count with the best silhouette score; 2 to 6 set it directly
- Layout: Tree or Radial
- Linkage: Average, Complete, Ward or Single
- Hover a branch for what merges there, or a leaf for its values
- Hover a group in the list to spotlight its branches

## Accessibility
- The cut handle is a keyboard slider that states the number of groups
- The group list names each group's size, traits and members as text
- A live readout states the current cut
- Groups are identified by labels in the list as well as color
- The svg has an aria-label naming the items and groups

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--s5`, `--s6`, `--s7`, `--s8`, `--div-neg`, `--div-mid`, `--div-pos`, `--ink`, `--ink-2`, `--muted`, `--axis`, `--grid`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a dendrogram in one self-contained HTML file with inline SVG and no libraries. Input: named items with several numeric measures. Scale each measure by (value - median) / IQR, then run agglomerative clustering with Lance-Williams updates for average, complete, single and Ward linkage. Draw a tree with the root at left and leaves at right, plus a radial layout with the root at the center and arcs joining children. Add a dashed, draggable cut line, also operable from the keyboard: branches below the cut take their group's color and those above stay neutral. Auto picks the group count from 2 to 8 with the highest mean silhouette. Beside the tree leaves, show a heat strip of each measure against the median on a diverging scale. List each group with its size and the two measures furthest from average. Hover a branch to see what merges and at what distance. Up to 8 group colors from the theme, moving near-duplicates to the end. CSS variables for every color, light and dark themes. Fictional seeded data.
