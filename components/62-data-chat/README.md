# Ask-your-data chat assistant

**Category:** UI patterns · **Tags:** chat, assistant, natural language, AI, Q&A, conversational analytics

An in-dashboard chat panel that answers plain-English questions about the dashboard's data: a value for a period, the monthly trend, the year-over-year change or a split by region, each with an inline chart and a note on how it was calculated. It remembers context, so 'show it trended' and 'what's the YoY change?' follow on from the last answer.

Live demo: [`index.html`](index.html) — one self-contained file, no dependencies. Light and dark themes; add `?theme=dark` or `?embed=1` to the URL.

## Use it when
- Readers ask ad-hoc questions the fixed charts don't answer
- Executives want one number fast ('what was revenue in Q3?') without filtering
- You plan to put an AI model behind the dashboard and need the front end

## Avoid it when
- The questions are always the same (build the chart instead)
- Numbers must come from an unvetted model (always compute them from the data, as this component does)
- There's no room for a panel at least 320px wide

## Anatomy
- Header: title, data freshness and a Clear button
- Message log (role=log): user questions as right-aligned bubbles, answers with a small assistant mark
- Answer = one-sentence reply with the key numbers in bold, then a card: a KPI (value + delta vs a year earlier), a monthly line chart (dashed line = a year earlier, asked period highlighted), grouped year-over-year columns or ranked region bars
- 'How this was calculated' disclosure under each answer: metric definition, period, comparison period, region, source
- Context line showing what 'it' currently means (metric · period · region)
- Suggestion chips that change with the conversation
- Input with send button; Enter sends, ↑ recalls the last question

## Data shape
```
Monthly rows per region of additive measures { sessions, orders, revenue, newc } (Jan 2024 – Oct 2026). Ratio metrics (AOV, conversion) are computed from summed parts, so any period or region aggregates correctly. Metrics: { key: { label, re (synonyms), calc(sums), f, fs, def } }.
```

## Interactions
- Type a question or click a suggestion; follow-ups reuse the last metric, period and region
- Understands metrics and synonyms (sales, traffic, AOV…), periods (Q3, Q3 2025, last quarter, this month, March, 2025, YTD, last 12 months, last 6 months), regions ('in the West', 'by region') and intents (value, trend, YoY, breakdown, 'which region grew fastest')
- Hover chart points or columns for exact values
- Plug in a model: set window.DC_CHAT = { plan: async (question, context) => ({ intent, metric, period: { from: 'YYYY-MM', to: 'YYYY-MM' }, region }) }; the component still computes and writes every number

## Accessibility
- Message list is role=log with aria-live=polite, so answers are announced
- Input has a label; suggestions are real buttons
- Every chart answer also states its key numbers in the text
- Deltas use ▲/▼ and words (up/down), not colour alone

## Design tokens used
`--s1`, `--de-emph`, `--surface-2`, `--grid`, `--up`, `--down`, `--border` — defined once on `:root` in the demo, with dark-mode values.

## Prompt
Paste this into Claude, Cursor or any coding assistant (attach `index.html` as a reference for an exact match):

> Build an in-dashboard 'ask your data' chat panel in one self-contained HTML file (no libraries, inline SVG). Data: seeded synthetic monthly rows per region (4 regions, Jan 2024 – Oct 2026) of additive measures sessions, orders, revenue and new customers; ratio metrics (AOV = revenue ÷ orders, conversion = orders ÷ sessions) are computed from summed parts. Write a small rule-based question parser: metric synonyms, periods (Q1–Q4 with optional year, last/this quarter, this/last month, month names, a year, YTD, last N months), regions ('in the West'), and intents: value, trend ('show it trended'), year-over-year change, breakdown by region ('which region grew fastest'). Keep conversation context so follow-ups without a metric or period reuse the last ones, and show that context above the input. Each answer is one sentence with bold numbers plus a card: KPI with ▲/▼ delta vs a year earlier; a 12-month line chart with a dashed year-earlier line and the asked period highlighted; grouped year-over-year columns per month; or ranked horizontal region bars with deltas. Under each answer, a 'How this was calculated' disclosure (definition, period, comparison, region, source). Suggestion chips update after each answer. role=log with aria-live, Enter to send, ↑ to recall, Clear button, hover tooltips on charts. Expose window.DC_CHAT.plan(question, context) as an optional hook so an LLM can return the query plan while the component computes every number. CSS variables for every colour, light and dark themes. Pre-play a sample conversation: 'What was revenue in Q3?', 'Show it to me trended', 'What's the YoY change?'.
