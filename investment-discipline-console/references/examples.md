# Examples

## Trigger Examples

- "Help me decide whether to add to my Tencent position."
- "I have an idea on a new stock but it is still fuzzy."
- "Review this trade and tell me whether I broke my own rules."
- "Turn my notes into a pre-trade memo."
- "Help me build a disciplined investing workflow from scratch."
- "This is my first time using the system. Help me set up my portfolio context before I review a trade."
- "Before we review any trade, help me define my return target, max drawdown, and position risk budget."
- "Before we review any trade, help me define my numeric return target, max drawdown, position cap, theme cap, leverage cap, and profit-taking trigger."
- "Here is my current holdings screenshot. Review my book and tell me what needs attention."
- "Look at my current portfolio and tell me where the concentration and leverage risks are."
- "Help me define how much leverage I allow in total, how much one theme can occupy, and when large winners must be reduced."
- "Combine my HK and US accounts into one portfolio view and tell me which limits I am breaching."
- "Compare my T-day holdings with my T+3-day holdings and tell me which changes need explanation."
- "Summarize what kind of trader I am becoming from my recent reviews, and tell me what mistakes I repeat."
- "Use $investment-discipline-console to run a weekly discipline review and summarize what mistakes I repeated this week."
- "使用 $investment-discipline-console，帮我做一次周度纪律复盘，总结这周我重复了哪些错误。"

## Pre-Trade Example Output

```yaml
final_action: reduce_size
missing_fields:
  - explicit invalidation
red_flags:
  - theme concentration is too high
  - no new information
reasoning: "The idea may still be valid, but the proposed size is too large for the current evidence."
```

## Attribution Example Output

```yaml
process_quality: poor
outcome_quality: favorable
mistake_tags:
  - chasing_risk
  - plan_drift
lesson: "Do not treat a profitable chase as proof of a good process."
next_safeguard: "Require one written new fact before adding after a sharp move."
```

## Holdings Review Example Output

```yaml
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
```

## Discipline Memory Example Output

```yaml
user_profile:
  style_label: balanced
  holding_horizon: medium_term
  weakness_patterns:
    - "Tends to add risk after large gains."
    - "Often skips invalidation on fast-moving trades."
  coaching_notes:
    - "When unrealized gain becomes emotionally salient, default to checking deleveraging rules first."

rule_memory:
  confirmed_rules:
    - rule_key: "profit_take_100"
      rule_text: "When unrealized gain exceeds 100%, partial profit-taking or deleveraging is recommended."
      source: bootstrap

weekly_discipline_digest:
  period_label: "2026-W13"
  top_strengths:
    - "Writes clearer sizing rules than before."
  top_mistakes:
    - "Still reacts to volatility too quickly."
  recurring_tags:
    - "profit_pressure"
    - "volatility_reactivity"
  next_focus:
    - "Do not add or trim during fast moves without a written new fact."
```
