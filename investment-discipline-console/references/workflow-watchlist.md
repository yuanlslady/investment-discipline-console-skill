# Watchlist Workflow

Use this flow when the user has an idea but has not yet earned the right to trade it.

## Minimum Fields

- Ticker or asset name
- Initial thesis
- Expected catalyst

## Steps

1. Normalize the idea into a `watchlist_item`.
2. Rewrite the thesis in one sentence if the user gives scattered notes.
3. Rewrite the catalyst as an observable trigger, not a vibe.
4. If no thesis or no catalyst exists, stop and ask for the missing field.
5. Assign or preserve a cooldown period before formal trade review.

## Output

Return:

- A normalized `watchlist_item`
- The missing fields, if any
- The next condition that would justify moving into pre-trade review

## Decision Rule

Do not escalate a watchlist item into a trade review unless the idea has at least:

- A thesis
- A catalyst or trigger
- A reason the user can monitor
