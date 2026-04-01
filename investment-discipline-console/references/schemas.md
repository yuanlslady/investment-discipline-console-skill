# Schemas

Use these lightweight schemas to normalize free-form user input.

## portfolio_context

```yaml
total_portfolio_value: number
portfolio_value_unit: HKD | USD | CNY | other
target_return_pct: number
target_return_notes: string
max_drawdown_tolerance_pct: number
single_position_risk_budget_pct: number
single_theme_risk_budget_pct: number
max_total_leveraged_exposure_pct: number
profit_take_or_deleverage_trigger_pct: number
leveraged_tools_allowed: boolean
leveraged_tool_policy_notes: string
risk_budget_notes: string
macro_stance: bullish | balanced | cautious | bearish | unknown
liquidity_view: easing | neutral | tightening | unknown
rates_view: falling | sideways | rising | unknown
risk_appetite: strong | neutral | weak | unknown
macro_summary: string
updated_at: ISO date
```

## industry_view

```yaml
industry_or_theme: string
status: favorable | neutral | unfavorable | unknown
cycle_view: upcycle | stabilizing | sideways | downcycle | unknown
thesis: string
key_signals: string
invalidation: string
review_date: ISO date
```

## watchlist_item

```yaml
ticker: string
name: string
market: HK | US | CN | other
source: manual | screen | note | other
thesis: string
catalyst: string
added_at: ISO date
cooldown_days: number
```

## position_snapshot

```yaml
ticker: string
name: string
market: HK | US | CN | other
instrument_type: single_stock | leveraged_etf | leveraged_note | option | fund | other
position_type: core_midterm | probe | trading | other
share_count: number
market_value: number
portfolio_weight: number
max_weight_allowed: number
last_price: number
avg_cost: number
unrealized_pnl: number
unrealized_pnl_pct: number
day_pnl: number
entry_reason_summary: string
exit_invalidators_summary: string
theme: string
source: manual | screenshot | broker_ocr | note | other
```

## account_snapshot

```yaml
account_name: string
account_market: HK | US | CN | mixed | other
total_account_value: number
account_value_unit: HKD | USD | CNY | other
positions: position_snapshot[]
snapshot_completeness: full | partial | unknown
```

## portfolio_book

```yaml
base_currency: HKD | USD | CNY | other
fx_assumptions: string
accounts: account_snapshot[]
```

## holdings_review

```yaml
base_currency: HKD | USD | CNY | other
total_portfolio_value_base: number
total_leveraged_exposure_pct: number
leveraged_exposure_breached: boolean
single_position_breaches: string[]
theme_breaches: string[]
profit_take_candidates:
  - ticker: string
    trigger_pct: number
    current_pnl_pct: number
    reason: string
theme_exposures:
  - theme: string
    exposure_pct: number
portfolio_level_flags: string[]
position_level_flags:
  - ticker: string
    flags: string[]
concentration_summary: string
leverage_summary: string
winner_loser_summary: string
suggested_actions: string[]
```

## holdings_delta_review

```yaml
start_date: ISO date
end_date: ISO date
major_adds:
  - ticker: string
    weight_change_pct: number
    note: string
major_trims:
  - ticker: string
    weight_change_pct: number
    note: string
major_exits: string[]
new_positions: string[]
removed_positions: string[]
leverage_exposure_change_pct: number
theme_exposure_changes:
  - theme: string
    start_exposure_pct: number
    end_exposure_pct: number
    change_pct: number
unexplained_changes: string[]
explanation_prompts: string[]
process_verdict: aligned | mixed | drifted | unknown
suggested_next_step: string
```

## trade_intent

```yaml
trade_action: buy | sell | add | trim | rotate
trade_type: catalyst_trade | fundamental_holding
# catalyst_trade: event-driven, defined time window, exit on catalyst resolution
# fundamental_holding: long-term thesis, position sized to portfolio weight, exit on thesis invalidation
target_weight_after_trade: number
why_now: string
what_changed: string
wrong_if: string
holding_plan_after_trade: string
alternative_action: string
in_competence_circle: boolean
is_on_watchlist: boolean
portfolio_context_ready: boolean
risk_budget_aligned: boolean
leveraged_exposure_aligned: boolean
theme_budget_aligned: boolean
contingency_plan: string
# Required when trade_type = catalyst_trade.
# Must be one of: (A) exit at close on catalyst day if result disappoints,
# (B) hold X days then exit regardless, (C) halve position and reassess.
# Choose one before entry. Not modifiable in real time.
```

## pre_trade_review

```yaml
final_action: allow | review | reduce_size | delay | block
missing_fields: string[]
red_flags: string[]
reasoning: string
pre_trade_memo: string
```

## post_trade_review

```yaml
review_date: ISO date
action_review: string
reason: string
mistake_tags: string[]
lesson: string
process_quality: good | mixed | poor
outcome_quality: favorable | neutral | unfavorable
next_safeguard: string
decision_source: self_initiated | ai_prompted | external_triggered
# self_initiated: user identified and acted independently
# ai_prompted: AI surfaced the action, user agreed and executed
# external_triggered: news, third-party recommendation, or market event triggered the action
decision_source_notes: string
# Optional. Record whether the decision_source affected process quality.
# Example: "ai_prompted —碎股清理属于被推动后行动，阻力来自惰性非实质异议"
```

## trade_type_conversion_check

```yaml
ticker: string
original_trade_type: catalyst_trade
converted_to: fundamental_holding
conversion_date: ISO date
acknowledged: boolean
# Must be true. The user must explicitly state this is a conversion, not a drift.
new_thesis_written: boolean
# Must be true. A fresh fundamental thesis must exist, independent of the original catalyst logic.
invalidation_written: boolean
# Must be true. Specific invalidation conditions must be defined for the fundamental holding.
position_size_reviewed: boolean
# Must be true. Position weight must be re-evaluated against fundamental_holding standards.
conversion_verdict: approved | blocked
# approved only when all four boolean fields are true.
```

## behavior_profile

```yaml
profile_key: string
profile_name: string
profile_summary: string
evidence: string[]
```
