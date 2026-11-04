# US county small multiples

**Category:** Maps · **Tags:** map, choropleth, small multiples, US counties, FIPS, diverging, linked highlight, canvas, search

A grid of small US county maps, one per measure, sharing one diverging scale: here the percent change in death rates from 1980 to 2014 for six causes of death across all 3,142 counties. Hovering a county highlights it in every map and the tooltip compares its values side by side.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Several measures share one unit and one geography, and the story is how their spatial patterns differ
- Readers should compare regions across measures at a glance (where one rises, does another fall?)
- A single map with a measure switch would hide the comparison behind clicks

## Avoid it when
- The measures use different units or scales (one shared legend would mislead)
- There are more than about nine measures (the maps get too small to read)
- Readers need exact county values (pair it with a ranked table)

## Anatomy
- Header with title, subtitle, Scale (Binned / Smooth), Causes (Six / All eight) switches and a Find a county search box
- Responsive grid of panels (3 columns wide, 2 on tablets, 1 on phones), each a cause name, a US-level chip and a county map with state borders
- One fixed 10-step diverging palette for every panel (dark blue → teal → green | orange → red → dark red), 10-point steps from −50% to +50% with the break at 0, or a smooth ramp across the same stops
- Linked highlight: the hovered or selected county is outlined and ringed in every panel
- Pinned strip: after a click or search, the county's value for every cause sits under the header (an aria-live region)
- Legend with the steps and their end labels, a note and the data and boundary sources in the footer

## Data shape
```
CAUSES = [{ name, us: <national % change>, v: [<% change ×10 per county, in GEO order>] }]; GEO = { w, h, k: [id, name, d, lx, ly], s: [[…one array per county]], outline }: pre-projected, simplified SVG paths (drawn to canvas as Path2D) with a label point, written by _geo/make_geo.py. Ids are 5-digit county FIPS codes.
```

## Interactions
- Hover a county in any panel: it is outlined and ringed in all panels; the tooltip lists its value for every cause (the hovered cause in bold) beside the US figure
- Click a county (or pick it in Find a county) to pin it; click again, Clear or Esc to unpin
- Pinning fires a dc-filter event on window and postMessage({ dcFilter: { id, name } }) to a parent dashboard
- An info icon beside each map title: hover it (or focus it with the keyboard) for a bulleted summary of that cause: national change, how many counties rose or fell, the typical county and middle half, regional medians, the largest rise and fall, and which other cause has the most and least alike county pattern
- Scale switch (Binned / Smooth) and Causes switch (Six / All eight)

## Accessibility
- Find a county is the keyboard route to every county; the maps themselves are images with an aria-label
- The pinned strip is an aria-live region that reads out the county's values for every cause
- A visually hidden list gives each cause's US change and its largest county rise and fall
- The legend states its ends in text; the palette runs blue to red through light green and orange, so the two sides differ in lightness as well as hue

## Design tokens used
`--surface`, `--surface-2`, `--ink`, `--ink-2`, `--muted`, `--border`, `--s1` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build US county small multiples in one self-contained HTML file (no libraries, no network): a responsive grid of six county maps (3 columns, 2 on tablets, 1 on phones), one per cause of death, showing the percent change in death rates per 100,000 from 1980 to 2014 for all 3,142 counties on an Albers projection with Alaska and Hawaii inset and state borders on top. Embed pre-projected, simplified county paths and draw them to canvas with Path2D (19,000 SVG paths would be slow); group fills by colour. Every panel shares one diverging scale centred on 0 and clamped at ±50%: 10 binned steps by default using a fixed palette (#20628c, #2b83ba, #5ea7b1, #91cba8, #bbe3a9 for falls; #fdbe73, #f59256, #e65437, #d7191c, #a11315 for rises), a smooth ramp across the same stops behind a Scale switch. Each panel shows the cause name and a chip with the US-level change. Hover hit-testing uses an off-screen pick canvas (each county painted in an id colour) confirmed with isPointInPath. Hovering highlights the same county in every panel (outline plus a ring at its label point) and shows a tooltip listing its value for every cause beside the US figure. Click or a Find a county search box pins a county: a strip under the header lists its values (aria-live), it fires a dc-filter CustomEvent plus a parent postMessage, and Esc, Clear or a second click unpins. A Causes switch adds two more maps. Legend with the steps and end labels, a short note on the pattern, and data plus boundary sources in the footer. A visually hidden summary per cause. CSS variables for every other colour, light and dark themes.
