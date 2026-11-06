# Flip-book dashboard

**Category:** For Fun · **Tags:** book, page turn, flip, storytelling, tabs, navigation, annual report, animation

A dashboard told as a book: a cover, two-page spreads of charts and a back cover. Pages turn with a 3D flip from a curled corner, the arrow keys or bookmark tabs along the top (jumping several spreads riffles through the pages in between). Wide screens show open spreads; narrow screens turn one page at a time.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- A yearly review, report or data story that readers go through in order
- A showcase or portfolio piece where the navigation itself should be memorable
- Content that splits naturally into 4–6 sections of one or two charts each

## Avoid it when
- Operational dashboards people scan many times a day (use plain tabs or one page)
- Readers need to compare charts on different pages side by side
- Pages that need scrolling: every page must fit its fixed size

## Anatomy
- Bookmark tabs: Front, Pages 2–3 … 8–9, Back; the open spread's tab is selected
- Book: two portrait pages around a gutter shadow; the closed cover sits centred and slides over as it opens
- Cover and back cover in the theme's first series colour; inside pages on --surface with a running header and page numbers
- Curled corners: bottom-right turns forward, bottom-left turns back, and the cover says 'Turn the page'
- Turning: each leaf rotates 180° around the spine with a passing shadow; a jump of several spreads starts each leaf a moment after the last
- Inside: KPI tiles, a column chart, pill bars, a waffle, a line against a target, quotes and goals with progress bars, all in theme colours

## Data shape
```
pages: [{ title: "Bags roasted by month", kind: "columns", data: [2810, 2640, …] }, …] — any content that fits a fixed page
```

## Interactions
- Click a page's curled corner to turn forward or back
- Click a bookmark tab or a contents entry to jump; the pages in between riffle past
- Arrow keys turn pages when the book or tabs have focus
- Layout: Auto / Spread / Single page (Auto shows spreads from 700px wide)
- Flip speed: Slow / Normal / Fast
- Hover chart marks for values

## Accessibility
- Tabs are a tablist with aria-selected; every page is a labelled region and pages out of view are inert
- Curls are buttons named 'Next page' and 'Previous page'
- Under prefers-reduced-motion pages change without the 3D turn
- Every chart has its numbers in text on the page

## Design tokens used
`--s1`, `--s2`, `--s3`, `--s4`, `--s5`, `--surface`, `--page`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--de-emph`, `--up` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a flip-book dashboard in one self-contained HTML file with inline SVG and no libraries: a small coffee roaster's year told as a ten-page book (cover, contents, the year in numbers, bags roasted by month as columns, top origins as rounded pill bars, brew methods as a 10×10 waffle, cup score by month against a target line, quotes from cafés, next year's goals with progress bars, back cover). Show two portrait pages side by side with a gutter shadow; the closed cover sits centred and slides over as the book opens. Pages are leaves that rotate 180° around the spine with CSS 3D transforms (backface-visibility hidden, a front and a back face per leaf, a passing shadow while turning). Navigate with curled page corners (bottom-right forward, bottom-left back, 'Turn the page' on the cover), bookmark tabs above the book (Front, Pages 2–3, 4–5, 6–7, 8–9, Back), clickable contents entries and the arrow keys; jumping several spreads turns each leaf a moment after the last. Under 700px wide, show one page at a time and turn single pages. Add Layout (Auto / Spread / Single page) and Flip speed (Slow / Normal / Fast) controls. Pages out of view are inert, tabs use aria-selected, reduced motion swaps pages without the turn. Cover in the theme's first series colour, pages on the card surface, CSS variables for every colour, light and dark themes.
