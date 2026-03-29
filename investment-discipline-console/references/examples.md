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
