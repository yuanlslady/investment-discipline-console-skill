# Portfolio Review Workflow

Use this flow when the user wants to review current holdings, uploads a broker screenshot, or asks what needs attention in the existing book.

## Inputs

Accept either:

- a manual list of holdings
- a broker screenshot with visible position rows
- an `account_snapshot`
- a `portfolio_book` spanning multiple accounts

If the input is a screenshot, first extract a best-effort normalized holdings table. State uncertainty when names or numbers are hard to read.

## Extraction Rule

For each visible row, try to capture:

- ticker
- name
- market
- market_value
- share_count
- last_price
- avg_cost
- unrealized_pnl or day_pnl when visible
- whether the instrument is leveraged

If total account value is visible, use it to estimate portfolio weights. If it is not visible, keep `portfolio_weight` blank instead of inventing it.

## Multi-Account Aggregation

If the user provides multiple accounts:

- normalize each account into an `account_snapshot`
- convert them into a common base currency if FX assumptions are available
- return a `portfolio_book`
- if FX assumptions are missing, still return the multi-account structure and clearly mark aggregate percentage judgments as approximate

## Review Objectives

Review the book across five lenses:

- concentration
- leverage
- thesis clarity
- macro and industry fit
- behavior drift

Use the user's thresholds from `portfolio_context` whenever available, especially:

- `single_position_risk_budget_pct`
- `single_theme_risk_budget_pct`
- `max_total_leveraged_exposure_pct`
- `profit_take_or_deleverage_trigger_pct`

## Technical Snapshot for Key Positions

After completing the standard review, run a `technical_context` check for positions that meet either condition:

- portfolio weight > 5%, or
- already flagged with a red flag in this review

**Data sourcing:** Fetch indicator data via search or ask the user to supply it. If unavailable, mark as `data_unavailable` and skip the signal — do not block the review.

For each qualifying position, return a `technical_context` block (see `references/schemas.md` and `references/technical-context.md`). The `technical_summary` field should be one sentence describing the technical posture and whether it reinforces or contradicts the action already suggested for that position.

Technical signals in portfolio review influence suggested actions as follows:
- RSI >= 75 on a position already flagged for "keep and monitor": upgrade to "reduce size, reassess timing"
- Relative strength <= -15% vs benchmark on a position without explicit thesis update: add "what is the market pricing?" to the follow-up question list
- Price below MA200 with falling slope on a core position: add to portfolio-level red flags

## Red Flags

Escalate concern when any of the following appears:

- a single position is too large relative to stated budget
- total leveraged exposure exceeds the stated cap
- a single theme exceeds the stated cap
- multiple leveraged instruments dominate the book
- the book is full of theme overlap disguised as different tickers
- large winners are held only because of greed
- large losers are held without explicit invalidation logic
- the user is using short-term tools to express long-term views
- a position exceeds the user's profit threshold but has not been partially reduced or delevered
- the current book conflicts with the user's macro stance

## Output

Return:

- a normalized `account_snapshot` when possible
- a normalized `portfolio_book` when multiple accounts are involved
- a `holdings_review`
- a short human-readable review with the top three issues and the next action list
- a `technical_context` block for each qualifying position (weight > 5% or flagged)

The `holdings_review` should calculate or estimate:

- total leveraged exposure percentage
- single-position breaches
- theme-level exposures and breaches
- profit-take candidates when gains exceed the trigger

## Action Language

Suggested actions should be explicit:

- keep and monitor
- reduce size
- convert to a non-levered expression
- define thesis and invalidation
- schedule a formal pre-trade or attribution review
