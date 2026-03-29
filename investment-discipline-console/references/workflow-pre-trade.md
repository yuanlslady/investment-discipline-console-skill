# Pre-Trade Workflow

Use this flow when the user wants to execute, size, trim, add, sell, or rotate a position.

## Required Inputs

- `portfolio_context`
- `trade_intent`
- Related `watchlist_item` or `position_snapshot`
- Thesis summary
- Invalidation logic
- Target size after the trade

## Action Set

Use exactly one of these final actions:

- `allow`: thesis, trigger, sizing, and invalidation are all coherent
- `review`: the idea may be valid, but evidence or articulation is incomplete
- `reduce_size`: the direction may be acceptable, but sizing is too aggressive
- `delay`: the user should wait for clearer evidence, a catalyst, or cooldown completion
- `block`: the trade violates core discipline rules

## First-Use Gate

If the user is using the system for the first time, require:

- Total portfolio size
- Unit for total portfolio size
- Target return percentage
- Maximum acceptable drawdown percentage
- Single-position risk budget percentage
- Single-theme risk budget percentage
- Maximum total leveraged exposure percentage
- Profit-taking or deleveraging trigger percentage
- Leveraged-tool policy
- Current macro judgment
- Current industry judgment

If these fields are missing, do not return `allow`. Return `review` or `delay` instead.

Before bootstrap is complete, prefer gathering missing portfolio context over doing deep company-level research. The discipline system comes first; research detail comes after the operating constraints are explicit.

## Red Flags

Escalate concern when any of the following appears:

- Not on watchlist
- Portfolio context is missing
- Risk budget is missing or not aligned
- Leveraged exposure would exceed the user's cap
- The trade would push a theme beyond the user's cap
- The trade conflicts with the user's leveraged-tool policy
- Industry context is not yet normalized into `industry_view`
- Missing thesis
- Missing invalidation
- Outside competence circle
- Emotion-driven urgency
- No new information
- Large reallocation without justification
- Position exceeds limit
- Theme concentration is too high
- Thesis has weakened or already played out
- Cooldown is still active

## Memo Structure

The pre-trade memo should contain:

- Trade summary
- Portfolio context
- Return target and drawdown tolerance
- Risk budget alignment
- Thesis
- Why now
- What would make the trade wrong
- Planned size and holding plan
- Final action
- Required next step

## Output Shape

Return a `pre_trade_review` object plus a readable memo.
