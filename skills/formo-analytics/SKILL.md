---
name: formo-analytics
description: Analyze a Formo project with the Formo tools. Use when the user asks about their app's visitors, connected wallets, transactions, revenue, funnels, retention, cohorts, traffic sources, top wallets, or a wallet's profile, or wants to build Formo boards and charts, create segments, set alerts, or label wallets.
---

# Formo Analytics

Formo is product analytics for onchain apps. The Formo tools read one project: the project the user picked when they connected. Use this skill to answer questions about that project and to keep its dashboards and alerts up to date.

## Ground rules

- Every tool is already scoped to the connected project. Never add a project or project_id argument, and never claim to see data from another project.
- Read tools never change data. Call them freely.
- Tools that change data (create, update, toggle, move, reorder, label, import) need the user's approval first. Say what you will change, then call the tool.
- Delete tools also need `confirm: true`. Only set it after the user says yes to that exact deletion.
- Formo cannot move funds, sign transactions, or contact wallet owners. Say so when asked.

## Pick the tool

Use a named analytics tool first. Use SQL only when no named tool fits.

| Question | Tool |
|---|---|
| Visitors, wallets, transactions, revenue for a period | `kpis` (set `include_previous_period` to compare) |
| A metric over time | `event_timeseries`, `revenue_timeseries` |
| Most common events | `top_events` |
| Step-by-step conversion | `funnel` |
| Paths users take | `flow` |
| Do users come back | `retention`, `cohort_analysis` |
| New, active, churned users | `lifecycle` |
| How often users return | `frequency` |
| Where users come from | `top_sources`, `top_pages`, `top_locations` |
| Page speed | `web_vitals` |
| Revenue and volume breakdowns | `revenue_overview`, `revenue_by_metric`, `volume_by_metric` |
| Biggest wallets, main chains | `top_wallets`, `top_chains` |
| One wallet's profile | `search_profile` |
| A filtered list of users | `project_users` |
| Valid values for a filter | `distinct_values` |
| Formo product questions | `search_formo_docs` |

For a custom question:

1. Call `list_datasources` to see tables and columns.
2. Draft the query with `text_to_sql` or write it yourself.
3. Run it with `execute_query`. Queries are read-only.
4. To show the result as a chart, call `preview_chart` once with the final query and a clear title. Do not use it to test queries.

## Workflows

### Weekly growth review

1. `kpis` for the last 7 days with the previous period.
2. `top_sources` and `top_events` for the same 7 days.
3. `top_wallets` with a limit of 10.
4. Report: headline numbers with the change from last week, the biggest mover, and one thing to look at next. Keep it short.

### Conversion problem

1. Ask which steps matter if the user did not say (for example: page view, wallet connect, first transaction).
2. `funnel` with those steps and the date range.
3. Find the step with the largest drop. Use `flow` to see where users go instead.
4. Suggest one change to test.

### Wallet questions

- One address: `search_profile`, then summarize net worth, chains, tokens, and labels.
- The best users: `top_wallets`, then `search_profile` on the top few if the user wants detail.
- Save a group for later: propose a `create_segment` filter and create it after approval.

### Dashboards

1. `list_boards` to find the board, or propose `create_board`.
2. Test the query with `execute_query`, then `preview_chart` once.
3. After approval, `create_chart` on the board.

### Alerts

Alerts fire when an event or a user matches the filters, and they deliver to email, Slack, or a webhook.

1. `list_alerts` to avoid duplicates.
2. Propose the trigger, filters, and recipient.
3. After approval, `create_alert`. Use `toggle_alert` to pause one.

## Answer style

- Lead with the answer and the numbers. Give the date range you used.
- Name the tool result you relied on when a number could surprise the user.
- If a tool returns an error about missing permissions, tell the user which permission the connection needs (for example `query:read` or `alerts:write`) and stop.
