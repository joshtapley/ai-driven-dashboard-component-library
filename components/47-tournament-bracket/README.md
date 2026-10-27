# Tournament bracket

**Category:** Flows & networks · **Tags:** single elimination, knockout, playoffs, path highlight, competition

A 16-team single-elimination bracket in four rounds plus a champion card: match boxes with seeds and scores, winners in bold, elbow connectors, hover any team to light up its path, and a round filter for narrow screens.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Knockout competitions, playoffs, internal contests, sales leaderboards run as brackets
- Showing how a winner got there, round by round
- 8, 16 or 32 entrants

## Avoid it when
- Round-robin or league formats (use a table or bump chart)
- More than 32 entrants on one screen (split into regions)

## Anatomy
- Columns per round with headers (Round of 16 → Quarterfinals → Semifinals → Final)
- Match box: two 26px rows, each with seed (muted), team name and score; winner semibold with ink score, loser in secondary ink
- Elbow connectors from each pair of matches to the next round, hairline axis colour
- Champion card at the end with a trophy glyph
- Path highlight: the hovered team's rows tint with the accent and their connectors turn accent

## Data shape
```
{ teams: [{ seed: 1, name: "Harbor Hawks" }, …16], results: [[{ a: 0, b: 15, sa: 3, sb: 1 }, …8], …per round] }
```

## Interactions
- Hover or focus a team: its whole path highlights across rounds
- Click a team to pin the highlight
- Round filter: All rounds / From quarterfinals (for narrow screens)
- 'Simulate new tournament' re-seeds results

## Accessibility
- Each match is a list item with an aria-label stating both teams, scores and the winner
- Path highlight uses tint and border, not colour alone
- Round headers are headings

## Design tokens used
`--s1`, `--axis`, `--surface`, `--surface-2`, `--ink`, `--ink-2` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build a 16-team single-elimination tournament bracket in one self-contained HTML file. Seeded fictional teams with seeds 1–16 paired 1v16, 8v9, 5v12, 4v13, 6v11, 3v14, 7v10, 2v15; simulate seeded results with scores (higher seeds favoured but upsets possible). Lay out columns for Round of 16, Quarterfinals, Semifinals and Final, with each match box vertically centred between its two feeder matches, plus a champion card. Match boxes have two 26px rows with seed (muted), team name and score; the winner is semibold. Draw elbow connectors in a hairline axis colour with inline SVG behind the boxes. Hovering or focusing a team highlights its entire path (accent-tinted rows and accent connectors); clicking pins it. Add a round filter (All / From quarterfinals) and a 'Simulate new tournament' button. Each match carries an aria-label with both teams, scores and winner. CSS variables for every colour, light and dark themes.
