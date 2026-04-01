# Attribution Workflow

Use this flow after execution when the user wants to review a completed decision.

## Core Rule

Separate process quality from outcome quality.

- Good process + bad outcome is possible.
- Bad process + good outcome is possible.

## Steps

1. Restate the original trade intent in plain language.
2. Identify the declared `trade_type` at entry (catalyst_trade or fundamental_holding). If it was never declared, flag it as a process gap.
3. Compare the executed action against the original plan.
4. Identify whether the thesis changed, the market changed, or the user changed the plan.
5. Check `decision_source`: was this trade self-initiated, AI-prompted, or externally triggered? Note whether the source affected execution quality.
6. Assign mistake tags.
7. Convert the lesson into a repeatable safeguard.

## Decision Source Assessment

Record `decision_source` and assess its implications:

- **self_initiated**: Did the user have clear logic before acting, or was it impulse framed as conviction?
- **ai_prompted**: Did the user genuinely agree with the reasoning, or did they defer without real buy-in? Passive compliance is a process risk.
- **external_triggered**: Was the external signal evaluated independently, or did the user act on noise?

The `decision_source` itself is not a quality judgment — self-initiated trades can have poor process; ai-prompted trades can be well-executed. The question is whether the user owned the decision at the moment of execution.

## Trade Type Consistency Check

Compare the declared `trade_type` at entry against how the position was actually held:

- If entry was `catalyst_trade` but the user held through the catalyst without following the `contingency_plan`, flag as **trade_type_drift**.
- If entry was `catalyst_trade` and it was converted to `fundamental_holding`, verify the conversion went through the conversion checkpoint in `workflow-pre-trade.md`. If not, flag as **undeclared_conversion**.
- If entry was `fundamental_holding` but was exited due to price volatility without thesis invalidation, flag as **thesis_noise_confusion**.

## Required Outputs

- `process_quality`
- `outcome_quality`
- `mistake_tags`
- `lesson`
- `next_safeguard`
- `decision_source`
- `trade_type` at entry (declared or reconstructed)

## Lesson Standard

A lesson is only acceptable if it can be turned into a future rule, threshold, or checklist item.

Bad lesson:

- "Need more discipline."

Good lesson:

- "Do not add to a probe position until at least one new fact strengthens the thesis."
- "Catalyst trades require a written contingency plan before entry. If it is missing, the action is delay, not proceed."
- "When AI surfaces a cleanup action, agree or disagree explicitly — do not execute on passive acceptance."
