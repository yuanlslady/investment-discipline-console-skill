# Pre-Trade Workflow

Use this flow when the user wants to execute, size, trim, add, sell, or rotate a position.

## Required Inputs

- `portfolio_context`
- `trade_intent` (including `trade_type` and, for catalyst trades, `contingency_plan`)
- Related `watchlist_item` or `position_snapshot`
- Thesis summary
- Invalidation logic
- Target size after the trade

## Step 0 — Define Trade Type First

Before any analysis, ask the user to define the trade type:

- **catalyst_trade**: Entry is driven by a specific event with a defined time window (earnings, policy announcement, merger vote, product launch). Exit is event-driven. Do not hold through thesis drift.
- **fundamental_holding**: Entry is driven by long-term thesis and valuation. Holding period is determined by logic, not price. Exit only when the thesis is invalidated.

If the user cannot answer this question, return `delay`. Do not proceed to trade review without a declared `trade_type`.

## Catalyst Trade Checklist

Required before `allow`:

1. What is the catalyst? Is it specific and observable?
2. What is the time window? When does the catalyst resolve?
3. What is the market's current expectation? Where is the user's edge?
4. **Contingency plan — choose one before entry, not modifiable in real time:**
   - Option A: Exit at close on catalyst resolution day if result disappoints
   - Option B: Hold X days to let market digest, then exit regardless
   - Option C: Trim to half position on disappoint, reassess with time limit
5. Position size must match the event risk window, not a long-term conviction level.

If `contingency_plan` is missing, return `block`. A catalyst trade without a pre-committed exit plan is a discipline violation.

## Fundamental Holding Checklist

Required before `allow`:

1. What is the long-term thesis? (Specific — not "the industry is good")
2. What specific condition would invalidate this thesis?
3. When and under what circumstances will the market reprice this holding?
4. What is the target portfolio weight, and does it fit within the single-position and single-theme risk budgets?

If `wrong_if` (invalidation) is missing, return `block`.

## Trade Type Conversion Checkpoint

Use this section when the user says the trade is shifting from catalyst to fundamental (or vice versa).

Run `trade_type_conversion_check` and verify all four conditions:

- [ ] User explicitly acknowledges this is a conversion, not "I'm just holding through it"
- [ ] A new thesis has been written independently of the original catalyst logic
- [ ] Specific invalidation conditions for the fundamental holding have been defined
- [ ] Position size has been re-evaluated against fundamental holding weight standards

If any condition is unmet, return `block` with a note explaining which condition is missing.

Do not allow a conversion that is driven by being underwater. The question is not "can I justify holding?" but "would I buy this at today's price, at this size, with this thesis?"

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

## Technical Context Check

Before finalizing the action, run a `technical_context` check using the four indicators defined in `references/technical-context.md`: RSI(14), price vs moving averages, 52-week range percentile, and relative strength vs benchmark.

**Data sourcing:** Ask the user to supply indicator data, or fetch it via search if available. If data is unavailable, mark each field as `data_unavailable` and proceed without blocking the workflow.

**Action influence rules:**
- RSI >= 75: upgrade action toward `delay` or `reduce_size` unless there is a compelling catalyst with defined exit
- Price below MA200 with falling slope: note as an additional red flag; does not block on its own
- 52W percentile >= 85 AND RSI >= 70: trigger `reduce_size`
- Relative strength <= -15% vs benchmark: surface "what is the market pricing that is not in my thesis?" as a required question before proceeding
- Technical signals cannot downgrade a `block`. Discipline violations stay blocked regardless of indicator readings.

## Red Flags

Escalate concern when any of the following appears:

- `trade_type` not declared
- Catalyst trade missing `contingency_plan`
- Fundamental holding missing `wrong_if` (invalidation)
- Trade type conversion not going through conversion checkpoint
- Not on watchlist
- Portfolio context is missing
- Risk budget is missing or not aligned
- Leveraged exposure would exceed the user's cap
- The trade would push a theme beyond the user's cap
- The trade conflicts with the user's leveraged-tool policy
- Industry context is not yet normalized into `industry_view`
- Missing thesis
- Outside competence circle
- Emotion-driven urgency without new information
- Large reallocation without justification
- Position exceeds limit
- Theme concentration is too high
- Thesis has weakened or already played out
- Cooldown is still active
- RSI >= 75 on entry (timing caution)
- Price below MA200 with falling slope (trend break)
- 52W percentile >= 85 AND RSI >= 70 (compound overbought signal)
- Relative strength <= -15% vs benchmark with no explanation in thesis (hidden risk flag)

## Memo Structure

The pre-trade memo should contain:

- Trade summary
- **Trade type** (catalyst_trade or fundamental_holding)
- Portfolio context
- Return target and drawdown tolerance
- Risk budget alignment
- Thesis
- Why now
- What would make the trade wrong
- Planned size and holding plan
- **Contingency plan** (for catalyst trades)
- **Technical context** (RSI, MA position, 52W percentile, relative strength — one sentence summary and `action_influence`)
- Final action
- Required next step

## Output Shape

Return a `pre_trade_review` object plus a readable memo.
