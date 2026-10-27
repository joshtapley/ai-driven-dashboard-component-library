# Collapsible tree diagram

**Category:** Hierarchies · **Tags:** org chart, hierarchy, dendrogram, tidy tree, drill down

A left-to-right tidy tree of an organisation (company › departments › teams › squads): node size = headcount, branches coloured by department, click any node to expand or collapse it, with expand-all, collapse-all and a search that opens the path to a match.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing structure and size of a hierarchy together (org charts, product taxonomies, account hierarchies, decision trees)
- Readers explore by drilling into one branch
- Up to ~200 nodes with a few expanded at a time

## Avoid it when
- Part-to-whole proportion is the point (use a treemap)
- The structure is a network with cross-links (use a node-link diagram)

## Anatomy
- Columns by depth, rows by visible leaves; parents centred on their children
- Links: smooth horizontal S-curves from parent to child, 1.5px in the branch colour at 45% opacity
- Nodes: circles with radius ∝ √headcount; filled when collapsed (has hidden children), ring when expanded, small dot for leaves
- Labels to the right of each node: name and headcount; the root and departments in ink weight
- Department colours: categorical slots 1–5, inherited down the branch

## Data shape
```
{ name: "Northstar Retail", children: [{ name: "Engineering", children: [{ name: "Platform", size: 42 }, …] }, …] } — internal sizes are summed
```

## Interactions
- Click (or Enter) a node with children to expand/collapse it
- Expand all / Collapse to departments buttons
- Search: type a team name to expand the path and outline the match
- Hover: tooltip with headcount, share of the parent and of the company

## Accessibility
- role=tree with treeitem nodes, aria-level and aria-expanded
- Every node is focusable and togglable with Enter/Space
- Headcount printed beside every node

## Design tokens used
`--s1 … --s5`, `--ink`, `--ink-2`, `--surface` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a collapsible tidy tree in one self-contained HTML file with inline SVG and no libraries. Seeded org data: company → 5 departments → 3–5 teams → 2–4 squads with headcounts at the leaves (parents summed). Layout left to right: x by depth, y by visible-leaf order with 26px rows, each parent centred on its visible children; the SVG height follows the number of visible leaves. Links are horizontal S-curves (cubic Béziers) in the branch's department colour at 45% opacity; departments take categorical slots 1–5 and children inherit them. Node circles have radius ∝ √headcount, filled when collapsed with hidden children, a ring when expanded, and a small dot for leaves; labels to the right show name and headcount. Clicking a node or pressing Enter toggles it; add Expand all and Collapse buttons and a search box that expands the path to a matching team and outlines it. Use role=tree / treeitem with aria-level and aria-expanded. Tooltips show headcount and shares. CSS variables for every colour, light and dark themes.
