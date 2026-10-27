# Ring meters with severity

**Category:** Gauges · **Tags:** donut gauge, utilisation, capacity, meter

A grid of 270° ring meters for capacity-style metrics, where the fill colour carries severity (accent → warning → critical) and each ring shows used / total underneath.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing utilisation of a fixed capacity: quota, storage, budget spent, seats
- Several resources share the same 0–100% scale
- Severity bands are well understood (e.g. >80% warning, >95% critical)

## Avoid it when
- Values can exceed 100% meaningfully (use activity rings or a bullet chart)
- Comparing values that aren't percentages of a whole

## Anatomy
- 270° ring (open at the bottom) so the end is easy to judge, 10px stroke, round caps
- Track is a lighter step of the fill's own hue so state reads across the whole ring
- Fill: accent below 75%, warning 75–90%, critical above 90%
- Centre: % used (semibold) and the resource name
- Below: used / total in absolute units and an icon + word status

## Data shape
```
[{ name: "Storage", used: 7.4, total: 10, unit: "TB" }, …]
```

## Interactions
- Workspace switch re-draws all rings
- Hover a ring: used, total, headroom left

## Accessibility
- role=meter with aria-valuenow
- Severity has an icon and word next to it
- Percent is printed, never only implied by the arc

## Design tokens used
`--s1`, `--warn`, `--crit`, `--track`, `--surface-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a responsive grid of 270° ring meters (open at the bottom) as one self-contained HTML file with inline SVG. Each ring has a 10px round-capped stroke; the track is a pale tint of the same hue as the fill; the fill colour encodes severity — accent under 75%, warning 75–90%, critical over 90% — and the track tints follow. Centre the percentage (semibold, ~22px) with the resource name under it; below the ring print 'used / total unit' and a status with an icon (● Healthy, ▲ High, ■ Critical). Add a segmented control to switch between workspaces with different values. Hover shows used, total and headroom. role=meter with aria values. CSS variables for every colour, light and dark themes.
