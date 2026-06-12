# End-to-End Examples

Use these examples to forward-test the skill on realistic requests.

## Example 1: First-Run Bootstrap

### User Request

`Use $investment-discipline-console to help me set up my portfolio context before I review any trade.`

### Expected Behavior

- ask for total portfolio size and unit
- ask for target return percentage
- ask for max drawdown percentage
- ask for single-position budget percentage
- ask for single-theme budget percentage
- ask for leveraged exposure cap percentage
- ask for profit-taking trigger percentage
- ask whether leveraged tools are allowed
- ask for macro stance
- ask for industry stance

### Expected Structured Output

```yaml
portfolio_context:
  total_portfolio_value: 500000
  portfolio_value_unit: CNY
  target_return_pct: 20
  target_return_notes: "Long-term target, not a quarterly target."
  max_drawdown_tolerance_pct: 15
  single_position_risk_budget_pct: 20
  single_theme_risk_budget_pct: 50
  max_total_leveraged_exposure_pct: 30
  profit_take_or_deleverage_trigger_pct: 100
  leveraged_tools_allowed: true
  leveraged_tool_policy_notes: "Allowed only for tactical expressions, not for permanent core holdings."
  macro_stance: cautious
  macro_summary: "Macro is tight and broad multiples may compress."
```

## Example 2: Multi-Account Holdings Review

### User Request

`Use $investment-discipline-console to combine my HK and US accounts into one portfolio view and tell me which limits I am breaching.`

### Expected Behavior

- normalize each account into an `account_snapshot`
- build a `portfolio_book`
- estimate FX if assumptions are available
- compute total leveraged exposure
- compute single-position and single-theme breaches
- flag profit-take candidates when gains exceed the trigger

### Expected Structured Output

```yaml
portfolio_book:
  base_currency: HKD
  fx_assumptions: "USD/HKD 7.8, CNY/HKD 1.08"
  accounts:
    - account_name: HK
      snapshot_completeness: full
    - account_name: US
      snapshot_completeness: partial

holdings_review:
  total_leveraged_exposure_pct: 34
  leveraged_exposure_breached: true
  single_position_breaches:
    - "7709 exceeds the 20% single-position budget after FX normalization."
  theme_breaches:
    - "AI hardware exposure exceeds the 50% single-theme budget."
  profit_take_candidates:
    - ticker: "7709"
      trigger_pct: 100
      current_pnl_pct: 108
      reason: "Gain exceeds the deleveraging trigger."
  suggested_actions:
    - "Reduce size in 7709."
    - "Reclassify tactical leveraged tools versus long-term core holdings."
    - "Review whether AI hardware and broad tech are really separate themes."
```

## Example 3: Pre-Trade Review After Bootstrap

### User Request

`Use $investment-discipline-console to review whether I should open a Tencent starter position.`

### Expected Behavior

- confirm bootstrap context already exists
- require target weight, thesis, catalyst, and invalidation
- refuse to return `allow` when the thesis is too narrative or sizing is undefined
- produce a `pre_trade_review` object and a readable memo

### Expected Structured Output

```yaml
pre_trade_review:
  final_action: review
  missing_fields:
    - target_weight_after_trade
    - clearer Tencent-specific industry judgment
  red_flags:
    - no explicit target weight
    - catalyst is still expectation-based
  reasoning: "The direction may be reasonable, but the thesis and sizing are not yet explicit enough for a clean allow."
```

## Example 4: Holdings Delta Review Across Two Dates

### User Request

`Use $investment-discipline-console to compare my T-day holdings with my T+3-day holdings and tell me which changes need explanation.`

### Expected Behavior

- normalize the start and end book into comparable structures
- identify major adds, trims, exits, and new positions
- check whether leverage and theme exposure changed materially
- ask the user to explain the top unexplained changes before making a strong process judgment
- return a structured `holdings_delta_review`

### Expected Structured Output

```yaml
holdings_delta_review:
  start_date: null
  end_date: null
  major_adds:
    - ticker: "SEMILEV"
      weight_change_pct: 12
      note: "New leveraged semiconductor exposure added."
  major_trims:
    - ticker: "B"
      weight_change_pct: -8
      note: "Position was cut sharply over the review window."
  major_exits: []
  new_positions:
    - "SEMILEV"
    - "AI1"
    - "AI2"
  removed_positions: []
  leverage_exposure_change_pct: 12
  theme_exposure_changes:
    - theme: "AI hardware"
      start_exposure_pct: 10
      end_exposure_pct: 28
      change_pct: 18
  unexplained_changes:
    - "Large new leveraged semiconductor exposure"
    - "Sharp trim in B without stated trigger"
  explanation_prompts:
    - "What new fact justified adding the leveraged semiconductor position?"
    - "Was the trim in B planned by thesis, valuation, or risk control?"
  process_verdict: mixed
  suggested_next_step: "Explain the top two changes first, then review whether the resulting theme and leverage exposure still fit the portfolio rules."
```
