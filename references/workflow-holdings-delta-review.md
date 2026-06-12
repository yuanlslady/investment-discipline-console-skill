# Holdings Delta Review Workflow

Use this flow when the user wants to compare two portfolio snapshots across time, asks why the book changed a lot, or wants a review of whether recent position changes matched the discipline system.

## Inputs

Accept either:

- two manual holdings lists for different dates
- two broker screenshots taken on different dates
- two `account_snapshot` objects
- two `portfolio_book` objects

Label them as:

- `start_snapshot`
- `end_snapshot`

If the dates are known, capture them explicitly. If the dates are approximate, say so.

## Primary Goal

Do not start by judging performance. Start by identifying what changed and whether the user can explain those changes.

The flow should answer:

- what positions were added, trimmed, exited, or materially resized
- whether leverage exposure changed materially
- whether theme concentration changed materially
- whether the changes matched the user's stated macro view, industry view, and risk budgets
- which changes require the user to explain process and intent

## Normalization Rule

First normalize both dates into the same structure:

- `account_snapshot` for single-account comparison
- `portfolio_book` for multi-account comparison

If FX assumptions are missing, still compare directionally and mark percentage judgments as approximate.

## Material Change Rule

Treat a change as material when any of the following appears:

- a new position is initiated
- a position is fully exited
- a position weight changes by more than 5 percentage points
- a leveraged position is added, removed, or materially resized
- a theme exposure moves enough to create or remove a budget breach
- the portfolio starts or stops conflicting with the user's macro stance

## Clarification Rule

When material changes are visible but the user has not explained why they happened, do not silently infer intent.

Ask concise follow-up questions such as:

- Why did this position move so much between the two dates?
- Was this a thesis-driven change, a risk reduction, or a reaction to price action?
- What new fact justified this add, trim, or exit?
- Did any of these moves follow a pre-defined plan, or were they discretionary?

If several positions changed at once, ask the user to explain the top one to three changes first.

## Review Lenses

Review the delta across these lenses:

- process consistency
- concentration change
- leverage change
- theme drift
- macro fit
- evidence quality

Use the user's thresholds from `portfolio_context` whenever available.

## Output

Return:

- normalized `start_snapshot`
- normalized `end_snapshot`
- a `holdings_delta_review`
- a short human-readable review

The `holdings_delta_review` should include:

- major adds
- major trims
- major exits
- new positions
- removed positions
- leverage exposure change
- theme exposure changes
- unexplained changes
- explanation prompts
- process verdict
- suggested next step

## Action Language

Suggested next steps should be explicit:

- explain the change
- run a pre-trade review retroactively
- run attribution on the exit or trim
- reduce overlapping risk
- refresh macro and industry context
