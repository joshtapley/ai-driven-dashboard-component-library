# AI Driven Dashboard Component Library

**[Open the live library →](https://joshtapley.github.io/ai-driven-dashboard-component-library/)**

A reference library of 59 dashboard components for people building dashboards with Claude, Cursor or any AI coding assistant. Every component is one self-contained HTML file with no libraries. Each comes with a spec and a tested, ready-to-paste build prompt, and all of them share one colour-blind-safe token set in light and dark.

## What's inside

| Category | Components |
|---|---|
| Basic charts | line, curved line, area, stacked area, column, horizontal bar, grouped bar, stacked bar, donut |
| Maps | square, circle, hex and sparkline tile US maps, globe with flight paths |
| Gauges | speedometer gauge, ring meters, activity rings, bullet charts |
| KPI cards | sparkline, target and pace, YoY columns, breakdown, hero with range, status tiles, tabs driving a chart, progress donuts |
| Tables | interactive data table, highlight table, leaderboard with sparklines, expandable pivot, scorecard vs target |
| Charts | line vs last year and target, ranked bars, waterfall, funnel, calendar and day × hour heatmaps, slopegraph, dumbbell, waffle, streamgraph, bump, beeswarm, radar, polar area, ternary plot, Gantt and more |
| Flows & networks | tapered funnel, Sankey, force-directed network, chord diagram, radial Sankey, tournament bracket |
| Hierarchies | collapsible tree, Voronoi treemap |
| UI patterns | toast notifications, slide-out dashboard menu |

- **Three sample dashboards:** Revenue overview, Product growth and Service health. Each is assembled from live components.
- **Twelve themes:** Quiet Instrument is the default, and the Josh Tapley theme matches [joshtapley.github.io](https://joshtapley.github.io/). Switch themes from any page.
- **Excel download:** every data table can export a formatted `.xlsx`, with colours, number formats and data bars.
- **Light and dark:** every component supports both and is keyboard accessible.

## Use it with your AI assistant

- **Download the skill:** open any component and choose **Download skill**. You get `dashboard-components.zip`: the whole library (workflow, rules, catalogue, themes, dashboard layouts, and every component's spec and reference file) as one Agent Skill. Add it to Claude as a skill, or unzip it into your Claude Code skills folder.
- **Copy one component:** each component page has the build prompt and the standalone file. Paste the prompt into your assistant, or attach the file for an exact match.

## Layout

```
index.html                     the gallery
themes.html                    the twelve themes
dashboards/<name>.html         sample dashboards
components/<NN-slug>/          index.html (live demo, standalone) + README.md (spec and prompt)
components.json                metadata for every component
```

Every file runs straight from disk or any static host. There's no build step to view it.
