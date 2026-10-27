# Toast notifications

**Category:** UI patterns · **Tags:** toast, snackbar, alert, notification, status, undo

Card-style toasts with a 4px status edge, a filled status icon, a bold title, a one-line message and a close button, in four variants, plus a live stack with position control, auto-dismiss progress, pause on hover and an Undo action.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Confirming a background action finished (export ready, filters saved, data refreshed)
- Short, non-blocking warnings and errors that don't need a decision
- Offering a quick Undo after a destructive action

## Avoid it when
- The message needs a decision or blocks the task (use a dialog)
- Persistent state (a data source is offline) — use an inline banner
- Long messages or more than one action

## Anatomy
- Card: surface background, 8px radius, soft shadow, 4px left edge in the status colour
- Icon: 22px filled circle in the status colour with a white glyph (✓ i ! ✕) — icon and colour together, never colour alone
- Title (semibold 14px) above a one-line message in secondary ink
- Close ×: 28px hit area, muted until hover
- Optional action button (Undo) right-aligned before the close
- Auto-dismiss bar: 2px progress line along the bottom in the status colour

## Data shape
```
toast({ type: "success" | "info" | "warning" | "error", title: "Export ready", message: "sales_q3.csv has been generated.", action?: { label: "Undo", onClick }, duration?: 5000 })
```

## Interactions
- Trigger buttons fire each variant; up to 4 toasts stack, the oldest leaves first
- Position control: top-right, bottom-right, top-centre, bottom-centre
- Auto-dismiss after 5s (errors stay until closed); hovering or focusing the stack pauses every timer
- Close with ×, Esc closes the newest, Undo runs its action and dismisses
- Enter and exit animate (slide + fade, 180ms); instant under prefers-reduced-motion

## Accessibility
- Success/info/warning go to a polite live region (role=status); errors to an assertive one (role=alert)
- Toasts never steal focus; the close button has an aria-label
- Errors don't auto-dismiss, so nobody misses them
- Status colours are the reserved status set and always paired with an icon and a title

## Design tokens used
`--good`, `--s1`, `--warn`, `--crit`, `--surface`, `--ink`, `--ink-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a toast notification system in one self-contained HTML file (no libraries). Toast design: a white surface card with 8px radius, a soft shadow and a 4px left edge in the status colour; a 22px filled circular icon in the status colour with a white glyph (✓ success, i info, ! warning, ✕ error); a semibold title and a one-line secondary-ink message; a muted × close button (28px hit area) on the right; an optional action button such as Undo; and a 2px auto-dismiss progress line along the bottom. Show the four variants statically in a 'Designs' panel, and provide a live demo: buttons that fire each variant, a position control (top-right, bottom-right, top-centre, bottom-centre), a stack of at most 4 (oldest leaves first), 5-second auto-dismiss (errors persist), pause all timers while the stack is hovered or focused, Esc closes the newest, slide-and-fade enter/exit (instant under prefers-reduced-motion). Announce success/info/warning in a polite role=status region and errors in a role=alert region; never move focus. Expose a toast({type,title,message,action,duration}) function. CSS variables for every colour, light and dark themes.
