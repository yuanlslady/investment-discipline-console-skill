# Discipline Memory Workflow

Use this flow when the user wants the system to remember recurring discipline patterns, summarize a trading style, or make future reviews more targeted through stored process memory.

## Core Principle

This memory system is for discipline, not prediction.

Store and reuse:

- user style and risk habits
- confirmed rules and limits
- repeated behavior mistakes
- prior process lessons
- periodic discipline summaries

Do not store or reuse:

- symbol-specific buy or sell calls
- market predictions as persistent truth
- a remembered conclusion that a particular asset is "good" or "bad"

## Memory Objects

Use these objects when available:

- `user_profile`
- `rule_memory`
- `behavior_memory_entry`
- `decision_memory_entry`
- `weekly_discipline_digest`

## Write Triggers

Update discipline memory when any of the following happens:

- bootstrap defines or changes a core rule
- attribution identifies a clear mistake and safeguard
- holdings review reveals repeated concentration, leverage, or horizon mismatch
- holdings delta review reveals repeated discretionary drift
- pre-trade review clearly matches a known mistake pattern

## Read Triggers

Before giving a targeted review, check whether memory already shows:

- repeated mistake tags
- a stable style label or holding horizon
- known weak points under volatility or profit pressure
- confirmed rules that the current trade might violate

## Output Goals

When using memory, answer these questions:

- What kind of trader is this user trying to be?
- What mistakes does this user repeat most often?
- What rules has the user already confirmed?
- Does the current action fit the user's style and rules?
- What coaching note would be most useful right now?

## Personalization Rule

Personalize the process advice, not the asset call.

Good:

- "You have repeatedly added risk after strong gains, so this setup should default to `reduce_size` unless there is a clearly new fact."
- "Your last three weak trades all lacked an invalidation rule. Do not move past `review` until `wrong_if` is explicit."

Bad:

- "Because you liked Tencent last month, you should buy Tencent again."
- "You usually win in semis, so this semiconductor trade should be allowed."

## Suggested Cadence

- Update `user_profile` and `rule_memory` when rules or style become clearer.
- Append `behavior_memory_entry` after meaningful review failures or safeguards.
- Append `decision_memory_entry` after completed trades with a clear lesson.
- Generate `weekly_discipline_digest` when enough evidence exists across the period.
