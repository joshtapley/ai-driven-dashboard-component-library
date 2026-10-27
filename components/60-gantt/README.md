# Gantt chart with progress

**Category:** Charts · **Tags:** gantt, project plan, timeline, schedule, milestones

A project plan as a Gantt chart: a task table (owner, status, due) beside a month timeline where each task's bar fills with its progress, grouped into collapsible phases with tinted bands, milestones as diamonds and a today line.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Showing a project's schedule and how far each task has got
- Status reviews where 'what's late and who owns it?' matters
- 10–40 tasks grouped into a handful of phases

## Avoid it when
- Hundreds of tasks (use a filtered table or a roll-up by phase)
- Dependencies are the main story (use a network or critical-path view)
- Comparing durations precisely (use a sorted bar chart)

## Anatomy
- Left: a task table with Task, Owner, Status and Due columns; phase rows are bold with a ▾ chevron, a people count and the phase's last due date
- Right: a month axis with light gridlines, a today line labelled with the date, and one 28px row per task aligned with the table
- Bars: 12px tall, 3px radius, start to end date; the done share is solid, the rest a pale tint of the same hue
- Phase rows: the whole row tinted with the phase's hue across both panes, with a thin summary bar spanning the phase
- Milestones: a diamond on the due date (zero-length tasks)
- Status: icon + word — ✓ Completed, ◐ In progress, ▲ Delayed (past its end date and not done), ○ Not started
- Colour switch: by phase (categorical slots in order) or by status (status colours, the done share still solid)

## Data shape
```
[{ phase: "Build", task: "Model", owner: "Sofia", start: "2026-10-05", end: "2026-10-23", progress: 0.8 }, …] — status derived from progress, dates and today
```

## Interactions
- Click or press Enter on a phase row to collapse or expand it; Expand all / Collapse all
- Colour switch: Phase / Status
- Hover a bar or a row: dates, duration, progress and status

## Accessibility
- Status is an icon plus a word, never colour alone
- Phase rows are buttons with aria-expanded
- SVG aria-label summarises how many tasks are completed, in progress, delayed and not started

## Design tokens used
`--s1 … --s4`, `--surface`, `--ink`, `--ink-2`, `--muted`, `--grid`, `--good`, `--warn`, `--crit` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a Gantt chart in one self-contained HTML file with inline SVG and no libraries. Data: about 16 tasks in 4 phases (Plan, Build, Test, Launch), each with an owner, start and end dates and a progress share; zero-length tasks are milestones. Lay it out as a task table on the left (Task, Owner, Status, Due) aligned row-for-row with a month timeline on the right; 28px rows. Phase rows are bold with a chevron, the number of people and the phase's last due date, and the whole row is tinted with the phase's hue across both panes, with a thin summary bar spanning the phase. Each task bar runs from start to end (12px tall, 3px radius): the done share is solid and the rest a pale tint of the same hue. Milestones are diamonds. Derive status: Completed when progress is 1, Delayed when the end date has passed and it isn't done, In progress once started, otherwise Not started; show it as icon + word (✓ ◐ ▲ ○). Draw month gridlines and a labelled today line. Clicking a phase row collapses it; add Expand all / Collapse all and a switch to colour bars by phase or by status. Hover shows dates, duration, progress and status. On narrow screens drop the Owner and Due columns. CSS variables for every colour, light and dark themes.
