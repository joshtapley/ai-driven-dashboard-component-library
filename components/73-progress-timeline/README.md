# Progress timeline

**Category:** UI patterns · **Tags:** timeline, stepper, journey, progress, animation, voyage

A journey timeline of fixed stops with completed stops filled, the current stop ringed in the accent colour and the route behind it drawn in the accent, plus per-stop figures underneath. Click a stop to move the focus. Animation options: draw the route on load, pulse the current stop's ring (three times or continuously) and refill the route on a repeat timer.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing where something is along a known sequence of stops: a voyage, a delivery route, an order or project pipeline
- Each stop has one or two figures worth reading in place
- The focus stop drives other views on the page

## Avoid it when
- Dates matter more than order (use a Gantt or a dated timeline axis)
- More than about 10 stops in one row (wrap to the vertical layout or group stops)
- Branching or parallel paths (use a flow diagram)

## Anatomy
- Track: a 3px line through every stop; the part up to the current stop is drawn in --s2, the rest in --de-emph
- Stops: completed are filled --ink dots, the current stop is an --s2 dot with an outer ring, upcoming stops are --de-emph
- Under each stop: its name in bold, then ▲ Loaded and ▼ Offloaded figures with green and red arrows
- Narrow containers switch to a vertical layout with figures beside each stop
- Animation: route draws from the first stop to the current one, stops fill as the line reaches them; the ring pulses after the draw finishes

## Data shape
```
[{ port: "Shanghai", loaded: 1671, offloaded: 0 }, …] plus the current stop index
```

## Interactions
- Click a stop (or use the arrow keys on the timeline) to change the current stop; the route animates to it
- Animate on load: On / Off
- Pulse current stop: Off / 3 times / Continuous
- Refill the route: Off / every 5 s / 10 s / 30 s
- Hover a stop for its status and figures

## Accessibility
- The timeline is a focusable list; each stop is a button with an aria-label giving its status and figures
- The current stop is marked aria-current="step" and named in the subtitle
- Status is shown by fill, ring and position as well as colour
- All animation is off under prefers-reduced-motion, and the continuous pulse only runs when chosen

## Design tokens used
`--s2`, `--ink`, `--ink-2`, `--muted`, `--de-emph`, `--surface`, `--up`, `--down` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a progress timeline in one self-contained HTML file with inline SVG and no libraries, for a container ship's voyage through seven ports (Shanghai, Hong Kong, Singapore, Colombo, Suez, Barcelona, Rotterdam) with containers loaded and offloaded at each. A 3px track joins the stops: the part up to the current port is in the accent colour and the rest is grey. Completed ports are filled ink dots, the current port is an accent dot with an outer ring, upcoming ports are grey. Under each port show its name in bold, then '▲ Loaded: n' and '▼ Offloaded: n' with green and red arrows. Clicking a port (or arrow keys) makes it current and animates the accent line to it. Add three option groups: Animate on load (On / Off: the line draws from the first port and each dot fills as the line reaches it), Pulse current port (Off / 3 times / Continuous: the outer ring gently scales and fades, starting after the draw), and Refill (Off / every 5 s / 10 s / 30 s: clear and redraw the route on a timer). Switch to a vertical layout under 620px wide. Disable all animation under prefers-reduced-motion. Focusable stops with aria-labels and aria-current="step", CSS variables for every colour, light and dark themes.
