# Watchlist Workflow

Use this flow when the user has an idea but has not yet earned the right to trade it.

## Minimum Fields

- Ticker or asset name
- Initial thesis
- Expected catalyst or observable trigger

## Steps

1. Normalize the idea into a `watchlist_item`.
2. Rewrite the thesis in one sentence if the user gives scattered notes.
3. Rewrite the catalyst as an observable trigger, not a vibe.
4. If no thesis or no catalyst exists, stop and ask for the missing field.
5. Assign or preserve a cooldown period before formal trade review.
6. Run the odds evaluation below before marking the item ready for pre-trade review.

## Odds Evaluation

Before escalating a watchlist item to pre-trade review, evaluate the payoff structure:

- **Upside**: If the thesis plays out as expected, what is the realistic price target or return range?
- **Downside**: If the thesis is wrong, what is the realistic loss range?
- **Risk/reward ratio**: Is the upside at least 2x the downside? If not, flag it.
- **Edge question**: Why does the user have an edge here? Is it from industry knowledge, a variant view on consensus, or access to a non-obvious signal?

A low-odds idea should stay on the watchlist until the ratio improves, not be fast-tracked because the user is excited. Record the odds estimate in the `watchlist_item` notes field.

If the user cannot articulate why they have an edge, that is a required field, not an optional one.

## Output

Return:

- A normalized `watchlist_item` (with odds evaluation in notes)
- The missing fields, if any
- The next condition that would justify moving into pre-trade review

## Decision Rule

Do not escalate a watchlist item into a trade review unless the idea has at least:

- A thesis
- A catalyst or trigger
- A reason the user can monitor
- A payoff structure where upside is materially larger than downside
