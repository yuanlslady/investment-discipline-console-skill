# Behavior Tags

Use these labels when mapping repeated review failures into behavior profiles.

## Common Keys

- `not_on_watchlist`: traded before watchlist incubation
- `missing_thesis`: thesis was absent or too vague
- `missing_invalidator`: no explicit wrong-if condition
- `non_competence_trade`: outside competence circle
- `panic_sell_risk`: sold from pressure instead of thesis change
- `emotion_driven`: urgency came from emotion, not evidence
- `chasing_risk`: entered after price excitement without enough new facts
- `no_new_information`: repeated or stale rationale
- `large_reallocation`: large size change without a clear trigger
- `weakened_thesis`: trade continued despite a weaker thesis
- `overweight_position`: size exceeded the position cap
- `theme_concentration`: portfolio became too concentrated in one theme
- `realized_thesis`: continued holding after the thesis had already played out
- `plan_drift`: execution diverged from the original plan
- `instrument_horizon_mismatch`: used the wrong instrument for the intended horizon
- `invalidated_thesis`: stayed in despite thesis failure
- `review_overdue`: skipped or delayed the planned review
- `probe_to_long_hold_drift`: a probe silently became a core position
- `cooldown_active`: traded during the cooldown window
- `profit_pressure`: changed behavior mainly because gains became emotionally salient
- `volatility_reactivity`: abandoned plan because of market noise or fast tape
- `rule_override`: knowingly broke a previously confirmed rule
- `style_mismatch`: executed in a way that does not match the declared style or horizon

## Mapping Rule

When the same tag appears repeatedly across reviews, propose a `behavior_profile` with:

- `profile_key`
- `profile_name`
- `profile_summary`
- evidence snippets from prior reviews
