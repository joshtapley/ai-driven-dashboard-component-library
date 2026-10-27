# Network (node-link) diagram

**Category:** Flows & networks · **Tags:** force-directed, graph, relationships, collaboration, draggable

A force-directed network of who collaborates with whom: node size = connections, colour = team, link width = interactions; hover to see neighbours, drag nodes, filter by team and search by name.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Relationships are the data: collaboration, service dependencies, referrals, co-purchases
- Finding hubs, bridges between groups and isolated clusters
- Up to ~80 nodes and a few hundred links

## Avoid it when
- Hundreds of nodes (becomes a hairball — aggregate, or use an adjacency matrix)
- Flows have a direction and stages (use a Sankey)

## Anatomy
- Nodes: circles, radius ∝ √degree (5–16px), team colour from the first three categorical slots, 2px surface ring
- Links: 1–4px lines ∝ interaction count, axis-grey at 60% opacity
- Labels only for the top hubs by default; every node labelled on hover/focus
- Team legend chips that double as filters; search box highlights a match
- Side panel: selected person, team, degree and their strongest connections

## Data shape
```
{ nodes: [{ id: "p01", name: "Avery Kim", team: "Engineering" }, …], links: [{ source: "p01", target: "p07", weight: 12 }, …] }
```

## Interactions
- Hover a node: it and its neighbours stay full strength, everything else fades; tooltip with degree
- Drag a node to reposition (simulation re-heats briefly)
- Click a node to select it and fill the side panel
- Team chips filter; search jumps to and selects a person
- 'Re-layout' re-runs the simulation

## Accessibility
- Side panel lists the selected node's connections as text
- Search provides a keyboard path to any node
- Team is shown by colour plus legend and panel text; only three categorical slots are used (validated all-pairs)

## Design tokens used
`--s1`, `--s2`, `--s3`, `--axis`, `--surface`, `--ink` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an interactive force-directed network diagram in one self-contained HTML file with inline SVG and a hand-written force simulation (no libraries): many-body repulsion, link springs, a weak pull to the centre, collision padding and velocity damping, run with requestAnimationFrame until it cools. Seeded data: ~40 fictional people in 3 teams with ~90 weighted collaboration links, denser within teams and a few cross-team bridges. Node radius ∝ √degree (5–16px), fill = team colour (first three categorical slots), 2px surface ring; links 1–4px ∝ weight in axis grey at 60% opacity. Label only the top 6 hubs by default. Hover highlights a node and its neighbours and fades the rest; drag nodes with pointer events (re-heat the simulation); click selects a node and fills a side panel with name, team, degree and the strongest connections. Team legend chips act as filters, a search box selects a person by name, and a 'Re-layout' button restarts the simulation. CSS variables for all colours, light and dark themes.
