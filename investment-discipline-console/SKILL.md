---
name: investment-discipline-console
description: "Structured investment-discipline workflow for turning scattered ideas, positions, screenshots, trade notes, and recurring behavior patterns into a repeatable process: first-run portfolio bootstrap, holdings review, holdings delta review, watchlist intake, pre-trade review, post-trade attribution, discipline memory, and behavior correction. Use when the user wants to build or apply a disciplined investing workflow, review current holdings from manual input or broker screenshots, compare portfolio snapshots across time, aggregate multiple accounts into one portfolio view, review a candidate trade before execution, write a pre-trade memo, record a trade thesis and invalidation, analyze a completed trade, summarize a user discipline profile, tag recurring execution mistakes, or bootstrap a personal investment operating system from notes that currently live only in the user's head."
---

# Investment Discipline Console

Use this skill to convert investment thinking into a process with explicit inputs, explicit red flags, and explicit review records. Treat it as a discipline system, not a prediction engine.

## Trigger Cues

Use this skill in two cases:

- The user explicitly names `$investment-discipline-console`.
- The user's request is about holdings review, trade review, comparing two portfolio snapshots, writing a pre-trade memo, post-trade attribution, or setting up the investing discipline system for the first time.

Common trigger scenarios include:

- The user uploads a broker screenshot and wants a review of current holdings.
- The user provides two snapshots across time and wants to explain why the book changed so much.
- The user asks whether a trade should be done at all.
- The user is using the system for the first time and wants to define portfolio size, drawdown, and position limits before any review.

Common trigger phrases include:

- "Use $investment-discipline-console to help me set up my portfolio context before I review any trade."
- "Use $investment-discipline-console to combine my HK and US accounts into one portfolio view and tell me which limits I am breaching."
- "Help me review whether I should open a Tencent starter position."
- "Review my current holdings and tell me what needs attention."
- "Compare my T-day holdings with my T+3-day holdings and tell me which changes need explanation."
- "Use $investment-discipline-console to run a weekly discipline review and summarize what mistakes I repeated this week."
- "使用 $investment-discipline-console，先帮我建立组合上下文，再开始审查任何交易。"
- "使用 $investment-discipline-console，把我的港股和美股账户合并成一个组合视角，并告诉我哪些仓位限制已经超了。"
- "使用 $investment-discipline-console，帮我审查一下我是否应该先开一个腾讯的初始仓位。"
- "使用 $investment-discipline-console，看看我当前持仓里哪些仓位最需要复盘。"
- "使用 $investment-discipline-console，对比我 T 日和 T+3 日的持仓变化，并指出哪些大变化需要我解释原因。"
- "使用 $investment-discipline-console，帮我做一次周度纪律复盘，总结这周我重复了哪些错误。"

## Workflow Decision

Choose the workflow before writing any analysis.

- If the user has a new idea or vague interest, use the watchlist intake flow in `references/workflow-watchlist.md`.
- If the user wants to review current holdings, concentration, winners, losers, leverage exposure, or uploads a broker screenshot, use `references/workflow-portfolio-review.md`.
- If the user wants to compare holdings across two dates, asks why the book changed so much, or provides a T-day snapshot and a T+N-day snapshot, use `references/workflow-holdings-delta-review.md`.
- If the user is considering a buy, sell, trim, add, or rotation, use the pre-trade review flow in `references/workflow-pre-trade.md`.
- If the user has already executed a trade and wants to learn from it, use the attribution flow in `references/workflow-attribution.md`.
- If the user wants the system to remember recurring discipline patterns, summarize a user style, or use prior review history to make future reviews more targeted, use `references/workflow-discipline-memory.md`.
- If the user is using the system for the first time or has no stable portfolio context, run `references/workflow-bootstrap.md` before anything else.
- If the user wants to set up the whole operating system, bootstrap the objects from `references/schemas.md`, then walk through all three flows in order.

## Operating Rules

- Start from explicit objects. If the user gives free-form notes, map them into the schemas in `references/schemas.md`.
- On first use, do not skip portfolio bootstrap. Capture total portfolio size with unit, numeric return and drawdown targets, numeric risk budgets, leveraged-tool policy, current macro judgment, and current industry judgment before formal trade review.
- Treat memory as discipline memory, not market prediction memory. Store user style, risk rules, recurring mistakes, and process lessons. Do not store or reuse “this symbol should be bought or sold” conclusions as memory.
- When bootstrap is incomplete, prioritize collecting missing portfolio context before doing deep company research or browsing for supporting evidence.
- Use holdings review before trade review when the existing book itself is unclear or when the user starts from screenshots.
- When two holdings snapshots differ materially, run holdings delta review before judging whether the changes were good or bad. Ask the user to explain large unexplained changes instead of inferring intent.
- When memory exists, use it to personalize process guidance: check whether the current action repeats a known mistake pattern, conflicts with the user's stated style, or breaks a previously confirmed rule.
- Keep the sequence intact: watchlist first, then trade review, then attribution.
- Separate process quality from PnL. A profitable trade can still be a bad process.
- Surface missing information instead of papering over it. Missing thesis, invalidation, position sizing, or trigger evidence should degrade confidence.
- Normalize industry judgment into the `industry_view` schema. Do not invent ad hoc field names for sector context.
- Default to conservative actions when evidence is incomplete. Use the action set in `references/workflow-pre-trade.md`.
- Output in the user's language.

## Core References

- Read `references/doctrine.md` for the philosophy and non-negotiable rules.
- Read `references/schemas.md` when the input is unstructured or when you need to create or repair a workflow record.
- Read `references/workflow-bootstrap.md` when the user is new, when portfolio context is missing, or when macro and industry context need to be refreshed.
- Read `references/workflow-portfolio-review.md` when the user wants a review of the current book or provides holdings screenshots.
- Read `references/workflow-holdings-delta-review.md` when the user wants to compare two snapshots of the book across time or when position changes need an explanation and process review.
- Read `references/workflow-watchlist.md` for new ideas, thesis capture, catalyst capture, and cooldown handling.
- Read `references/workflow-pre-trade.md` for pre-trade review, decision actions, and memo output.
- Read `references/workflow-attribution.md` for post-trade review, mistake tagging, and lessons.
- Read `references/workflow-discipline-memory.md` when you need to build or update a user discipline profile, summarize recurring patterns, or reuse prior process lessons in a new review.
- Read `references/behavior-tags.md` when you need to map execution problems into recurring behavior profiles.
- Read `references/examples.md` for canonical prompts and output shapes.
- Read `references/end-to-end-examples.md` for realistic end-to-end samples covering first-run bootstrap, multi-account holdings review, and trade review.

## Output Contract

Produce both a concise human-readable judgment and a structured artifact.

- Human-readable judgment: summarize the decision, key red flags, and next action.
- Structured artifact: return the normalized object or memo fields needed to continue the workflow.
- Prefer machine-comparable percentages over free-form threshold text whenever the workflow needs to judge breaches.

When running a pre-trade review, include:

- Final action
- Why this action was chosen
- Missing fields
- Red flags
- Suggested next step
- Pre-trade memo

When running attribution analysis, include:

- Process quality assessment
- Outcome quality assessment
- Mistake tags
- Behavior profile candidates
- Repeatable lesson
- Next safeguard

When running discipline memory, include:

- Updated user discipline profile
- Confirmed rule memory
- Repeated behavior patterns
- Decision samples worth remembering
- Weekly or periodic discipline digest when enough evidence exists
- Personalized review implications for the next trade or holdings review

When running a holdings review, include:

- Normalized holdings snapshot
- Concentration observations
- Leverage observations
- Position-level red flags
- Portfolio-level red flags
- Suggested actions for review, trim, exit, or further work
- Breach calculations that can be reused by later workflow steps

When running a holdings delta review, include:

- Normalized start and end snapshots
- Major adds, trims, exits, and new positions
- Concentration, leverage, and theme exposure changes
- Unexplained changes that require user rationale
- A process review of whether the change matched the stated discipline
- Follow-up questions when rationale is missing

## Guardrails

- Do not present outputs as investment advice or certainty.
- Do not make asset-selection recommendations. Focus on trade discipline, process quality, risk alignment, and behavior correction.
- Do not skip invalidation logic.
- Do not let recent price action substitute for thesis updates.
- Do not bless oversized positions without an explicit sizing rationale.
- Do not let attribution collapse into "made money = right" or "lost money = wrong".
