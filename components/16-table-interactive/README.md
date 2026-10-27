# Interactive data table

**Category:** Tables · **Tags:** sort, search, filter, pagination, row expand, inline bars, CSV export, Excel export

A full-featured accounts table: search, region and status filters, sortable columns, pagination, inline MRR bars, status pills, expandable rows with a 12-month trend, and CSV export of the filtered set.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- People need to find, rank and act on individual records (accounts, orders, tickets)
- The dashboard's charts summarise and this table lets people drill to the rows
- More than ~15 rows

## Avoid it when
- Fewer than ~8 rows (a simple static table or bar list reads faster)
- The point is a pattern, not lookup (chart it)

## Anatomy
- Toolbar: search box, region select, status filter chips with counts, result count, Export CSV
- Header: sentence-case labels, numeric columns right-aligned, sort indicator ▲/▼ and aria-sort
- Account cell: initials avatar + name + owner in muted text
- Status pill: icon + word on a tinted background
- MRR: tabular number with a thin inline bar scaled to the column max
- Growth: signed % in up/down text colour
- Rows: 44px, hairline dividers, hover wash; expand chevron reveals a detail row
- Footer: page x of y, rows per page, prev/next

## Data shape
```
[{ account: "Northwind Labs", owner: "A. Rivera", region: "EMEA", plan: "Business", status: "Active", mrr: 18400, growth: 0.12, seats: 42, lastActive: "2026-10-21", history: [12 numbers] }, …]
```

## Interactions
- Type to search account or owner (debounced)
- Region select and status chips combine as AND filters; counts update
- Click a header to sort (click again to flip); keyboard: headers are buttons
- Chevron expands a row to show plan, seats, last activity and a 12-month MRR sparkline
- Pagination with rows-per-page; filters reset to page 1
- Export CSV downloads exactly the filtered, sorted rows

## Accessibility
- Real <table> with <th scope=col>, aria-sort on the sorted column
- Sort and expand controls are buttons with labels; expanded state via aria-expanded
- Status pills use icon + word
- Live region announces the result count

## Design tokens used
`--s1`, `--good / --warn / --crit`, `--grid`, `--hover`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a full-featured interactive data table in one self-contained HTML file (no libraries). Generate ~64 seeded fictional SaaS accounts with: account name, owner, region (AMER/EMEA/APAC), plan, status (Active, Trial, Past due, Churned), MRR, YoY growth, seats, last active date and 12 months of MRR history. Toolbar: search (account or owner, debounced), region <select>, status filter chips with live counts, a result count and an 'Export CSV' button that downloads the currently filtered and sorted rows. Table: semantic <table> with sortable header buttons (aria-sort, ▲/▼), numeric columns right-aligned with tabular numbers, an account cell with an initials avatar and the owner in muted text, status pills with icon + word on a tinted background, MRR with a thin inline bar scaled to the max, growth as signed % in success/danger text colour, 44px rows with hairline dividers and a hover wash. Each row has a chevron button (aria-expanded) that reveals a detail row with plan, seats, last active and a 12-month MRR sparkline. Footer pagination with rows-per-page (10/25/50) and prev/next; changing filters returns to page 1. Announce result counts in an aria-live region. CSS variables for every colour, light and dark themes.
