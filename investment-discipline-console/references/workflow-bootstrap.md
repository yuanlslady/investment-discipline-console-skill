# Bootstrap Workflow

Use this flow on first use or whenever the portfolio context is missing or stale.

## Required Inputs

- Total portfolio size as a number
- Unit for total portfolio size, usually a currency such as HKD, USD, or CNY
- Target return as a percentage
- Maximum acceptable drawdown as a percentage
- Single-position risk budget as a percentage
- Single-theme risk budget as a percentage
- Maximum total exposure to leveraged tools as a percentage
- Profit-taking or deleveraging trigger as a percentage gain
- Whether leveraged tools are allowed at all
- Current macro judgment
- Current industry judgment for the relevant sector or theme

## Minimum Bootstrap Output

Return a normalized `portfolio_context` object and, when relevant, one or more `industry_view` objects.

When enough style information exists, also initialize:

- `user_profile`
- `rule_memory`

Always map sector or theme context into `industry_view`. If the user gives a vague statement such as "AI is still a big opportunity", rewrite it into the closest valid `industry_view` object and mark any missing fields explicitly.

## Bootstrap Questions

Ask for these fields explicitly:

- What is the total size of the portfolio?
- What is the unit or currency?
- What target return percentage are you trying to achieve?
- What maximum drawdown percentage can you accept?
- What is the largest position percentage you allow for a single idea?
- What is the largest total portfolio percentage you allow for a single theme?
- What is the largest total portfolio percentage that leveraged tools may occupy?
- Are leveraged tools allowed in this system at all? If yes, under what conditions?
- At what unrealized gain percentage do you require partial profit-taking or deleveraging?
- What is the current macro stance?
- What is the current liquidity, rates, or risk-appetite view if the user has one?
- What is the current industry judgment for the target area?
- What holding horizon best describes the user?
- What kind of mistakes does the user think they repeat most often?

## Decision Rule

- If this is the first use and the portfolio context is missing, do not produce a final `allow` on a trade review.
- If target return, max drawdown tolerance, single-position risk budget, single-theme risk budget, leveraged exposure cap, profit-taking trigger, or leveraged-tool policy is missing, do not produce a final `allow` on a trade review.
- At most, produce `review` or `delay` until the bootstrap fields are captured.
- If the user does not know a macro or industry view, state that it is missing rather than fabricating one.

## Why This Matters

Sizing without portfolio size is not real sizing.
Sizing without target return, drawdown tolerance, and risk budget is not aligned sizing.
Leverage without an aggregate cap and profit-taking rule is unmanaged leverage.
Trade review without macro and industry context is an isolated opinion, not a disciplined process.
Discipline memory is stronger when the user's intended style and self-identified weak points are explicit from the start.
