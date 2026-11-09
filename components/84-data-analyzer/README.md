# Data analyzer

**Category:** UI patterns · **Tags:** analysis, profiling, kpi, breakouts, trends, recommendations, auto dashboard, csv, excel, tool, template

Drop in a CSV or Excel file and it works out the likely KPIs, the most useful breakouts, trends, data problems and the charts that suit the data, then builds a standard and a non-standard dashboard you can adjust with checkboxes. It runs on rules in the browser, so the file never leaves the computer and the same file always gives the same answer.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Exploring a new dataset before designing a dashboard
- Deciding which KPIs and charts a dataset can support
- Giving an AI assistant a short summary of a dataset instead of the raw file

## Avoid it when
- The data needs joining across several tables first (it reads one table)
- A finished, curated dashboard is the goal (use it to start, then build with the components)
- Column names are meaningless codes such as val1, because roles are inferred from names and values

## Anatomy
- Sample switch, file picker and drop zone; a Copy short summary button
- What stands out: up to six plain-language findings
- Likely Big Numbers, each with a comparison, sparkline, reason and a checkbox for the KPI bar
- Recommended charts in Standard and Non-standard lists, each tied to real columns, with a reason and a checkbox
- Dashboards: tabs for Standard and Non-standard, each a KPI bar above a two-column chart grid
- Trends with direction, comparisons, seasonality, level shifts and unusual periods
- Breakouts ranked by how much of the variation a split explains
- Relationships, the real-groups test, data quality issues and a table of how every column was read

## Data shape
```
Any CSV, TSV or Excel (.xlsx) file with a header row. Column roles are inferred: dates, measures, categories, IDs, yes/no flags, states and clock times.
```

## Interactions
- Sample: switch between two fictional datasets
- Drop or choose a file to analyze it in the browser
- Tick KPIs and charts; both dashboards update at once
- Standard and Non-standard tabs switch dashboards
- Hover any mark for exact values
- Copy short summary puts a few hundred tokens of findings on the clipboard for an AI assistant
- Each recommendation links to its component

## Accessibility
- The status line is a live region
- Every checkbox names the chart or KPI it adds
- Charts carry an aria-label, and the tables stay real tables
- Changes carry an arrow as well as a color
- Multi-series charts always have a legend

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--s5`, `--s6`, `--s7`, `--s8`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--axis`, `--surface`, `--surface-2`, `--up`, `--down`, `--good`, `--crit` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a self-contained data analysis page with no AI and no network calls. Parse CSV, TSV or .xlsx in the browser and infer each column's role from its name and values: date, measure (sum or average), category, ordinal, yes/no, ID, label, state or clock time. Rank likely KPIs by column name, with the latest complete period compared to a year earlier or the prior period. Rank breakouts by eta squared adjusted for the number of groups. For trends use a Mann-Kendall test and a Theil-Sen slope, require at least a 5% change, drop partial or nearly empty edge periods, and move scattered events to a coarser time grain. Report correlations, data quality issues and whether two measures form real groups against simulated single clouds. From rules tied to the columns found, recommend standard and non-standard charts, each naming its columns and a reason. Show checkboxes for KPIs and charts, then draw two live dashboards, Standard and Non-standard, each a KPI bar above a chart grid in inline SVG with hover tooltips. Use CSS variables for every color, in light and dark themes, and fictional sample data.
