# Slide-out dashboard menu

**Category:** UI patterns · **Tags:** sidebar, navigation, icon rail, drawer, filters, collapsible

A dashboard sidebar that collapses to an icon rail and slides out to a full menu: workspace monogram, page links with an active accent bar, a collapsible Reports group, a filters section that drives the page, and an off-canvas drawer with a scrim on narrow screens.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Multi-page dashboards that need persistent navigation plus a home for global filters
- Users switch between 'focus on the charts' (rail) and 'find my way' (expanded)
- The same dashboard must work on desktop and phone

## Avoid it when
- A single-page dashboard with two or three filters (put them in one row above the charts)
- Fewer than three destinations (use tabs across the top)

## Anatomy
- Header: monogram logo button + workspace name; collapse toggle (⌘/Ctrl + B); in rail mode only the logo shows, centred, and clicking it expands the sidebar
- Nav items: 20px icon + label, 40px rows; active item gets a 3px accent bar on the left and a tinted pill background
- Collapsible group (Reports) with a chevron and indented children
- Filters section: a period segmented control and region checkboxes with counts, plus a one-line plain-English summary of what's applied
- Footer: user avatar + name and a help link
- Rail mode: 64px wide, icons only, labels in tooltips; expanded: 248px; drawer (narrow screens): slides over content with a 40% scrim
- Two skins from the library: Neutral (hairline, shadcn-like) and Navy (dark rail, GA4/Data Forge-like)

## Data shape
```
{ workspace: "Northstar Retail", pages: [{ id: "overview", label: "Overview", icon: "grid" }, …], groups: [{ label: "Reports", items: […] }], filters: { period: ["7D","30D","QTD","YTD"], regions: [{ name: "West", count: 12 }, …] } }
```

## Interactions
- Collapse/expand with the toggle button or Ctrl/⌘ + B; clicking the logo re-expands a collapsed rail; the choice is remembered per viewer
- Collapse style switch: Collapse to rail (64px icons) or Hide completely (0px; a hamburger in the top bar brings it back, also on desktop)
- Hover a rail icon: tooltip with the page name
- Click a page: active state moves and the content header updates
- Reports group expands/collapses (aria-expanded)
- Filters update the page summary immediately; Reset clears them
- Narrow screens: hamburger opens a drawer; Esc, scrim click or choosing a page closes it; focus is trapped inside while open and returns to the hamburger

## Accessibility
- <nav aria-label> landmark; active link has aria-current=page
- Toggle buttons expose aria-expanded and aria-controls
- Drawer is a modal dialog while open (focus trap, Esc to close, focus restored)
- Rail icons keep accessible names even when labels are hidden
- Visible focus rings; respects prefers-reduced-motion

## Design tokens used
`--s1`, `--surface`, `--surface-2`, `--ink`, `--ink-2`, `--grid`, `--hover` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a responsive slide-out dashboard sidebar in one self-contained HTML file (no libraries), shown inside a mock dashboard frame. Sidebar contents: a header with a monogram tile, workspace name and a collapse toggle (also Ctrl/⌘+B); a nav list of pages with inline SVG icons (Overview, Sales, Customers, Inventory) where the active item has a 3px accent bar on the left, a tinted pill background and aria-current=page; a collapsible 'Reports' group with a chevron and indented children; a Filters section with a period segmented control (7D/30D/QTD/YTD), region checkboxes with counts and a Reset link; and a footer with a user avatar and name. Modes: expanded (248px) and a collapsed state that is either an icon rail (64px, labels hidden but kept as accessible names and shown as hover tooltips, the monogram logo centred and clickable to expand again) or hidden completely (0px wide and inert, with a hamburger in the top bar to bring it back) — chosen with a 'Collapse to rail / Hide completely' switch, animated with a width transition, with the choice remembered in localStorage. Below 720px the sidebar becomes an off-canvas drawer opened by a hamburger, sliding over the content with a 40% scrim; Esc, scrim click or picking a page closes it, focus is trapped while open and returned to the hamburger. Selecting a page or changing filters updates the content header and a plain-English summary ('Sales · last 30 days · West, South'). Offer two skins via a switch: Neutral (light surface, hairline border) and Navy (dark navy rail with white text). CSS variables for all colours, light and dark themes, prefers-reduced-motion respected.
