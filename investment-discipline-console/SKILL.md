---
name: investment-discipline-console
description: "Structured investment-discipline workflow for turning scattered ideas, positions, screenshots, and trade notes into a repeatable process: first-run portfolio bootstrap, holdings review, watchlist intake, pre-trade review, post-trade attribution, and behavior correction. Use when the user wants to build or apply a disciplined investing workflow, review current holdings from manual input or broker screenshots, aggregate multiple accounts into one portfolio view, review a candidate trade before execution, write a pre-trade memo, record a trade thesis and invalidation, analyze a completed trade, tag recurring execution mistakes, or bootstrap a personal investment operating system from notes that currently live only in the user's head."
---

# Investment Discipline Console

Use this skill to convert investment thinking into a process with explicit inputs, explicit red flags, and explicit review records. Treat it as a discipline system, not a prediction engine.

## Workflow Decision

Choose the workflow before writing any analysis.

- If the user has a new idea or vague interest, use the watchlist intake flow in `references/workflow-watchlist.md`.
- If the user wants to review current holdings, concentration, winners, losers, leverage exposure, or uploads a broker screenshot, use `references/workflow-portfolio-review.md`.
- If the user is considering a buy, sell, trim, add, or rotation, use the pre-trade review flow in `references/workflow-pre-trade.md`.
- If the user has already executed a trade and wants to learn from it, use the attribution flow in `references/workflow-attribution.md`.
- If the user is using the system for the first time or has no stable portfolio context, run `references/workflow-bootstrap.md` before anything else.
- If the user wants to set up the whole operating system, bootstrap the objects from `references/schemas.md`, then walk through all three flows in order.

## Operating Rules

- Start from explicit objects. If the user gives free-form notes, map them into the schemas in `references/schemas.md`.
- On first use, do not skip portfolio bootstrap. Capture total portfolio size with unit, numeric return and drawdown targets, numeric risk budgets, leveraged-tool policy, current macro judgment, and current industry judgment before formal trade review.
- When bootstrap is incomplete, prioritize collecting missing portfolio context before doing deep company research or browsing for supporting evidence.
- Use holdings review before trade review when the existing book itself is unclear or when the user starts from screenshots.
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
- Read `references/workflow-watchlist.md` for new ideas, thesis capture, catalyst capture, and cooldown handling.
- Read `references/workflow-pre-trade.md` for pre-trade review, decision actions, and memo output.
- Read `references/workflow-attribution.md` for post-trade review, mistake tagging, and lessons.
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

When running a holdings review, include:

- Normalized holdings snapshot
- Concentration observations
- Leverage observations
- Position-level red flags
- Portfolio-level red flags
- Suggested actions for review, trim, exit, or further work
- Breach calculations that can be reused by later workflow steps

## Guardrails

- Do not present outputs as investment advice or certainty.
- Do not skip invalidation logic.
- Do not let recent price action substitute for thesis updates.
- Do not bless oversized positions without an explicit sizing rationale.
- Do not let attribution collapse into "made money = right" or "lost money = wrong".
