# Investment Discipline Console Skill

* * *

## English

This repository is natively packaged as a Codex skill. Its workflow and prompt structure can be adapted to other AI agents, but native compatibility depends on each agent's own extension mechanism. It turns scattered trade ideas, holdings screenshots, review notes, and recurring behavior patterns into a repeatable operating system:

- First-run portfolio bootstrap
- Holdings review from manual input or broker screenshots
- Multi-account portfolio aggregation
- Holdings delta review across two dates
- Watchlist intake
- Pre-trade review
- Post-trade attribution
- Discipline memory and user-profile refinement
- Behavior correction and mistake tagging

This skill is designed to behave like a discipline system, not a research-only assistant. It prioritizes portfolio context, risk budgets, and invalidation rules before deeper company analysis.

### When It Triggers

This skill is typically triggered in two cases:

- You explicitly call `$investment-discipline-console`
- Your request is about holdings review, trade review, comparing two portfolio snapshots, writing a pre-trade memo, post-trade attribution, or setting up the investing discipline system for the first time

Common trigger scenarios include:

- You upload a broker screenshot and want a review of current holdings
- You provide two snapshots across time and want to explain why the book changed so much
- You ask whether a trade should be done at all
- You are using the system for the first time and want to define portfolio size, drawdown, and position limits before any review
- You want a weekly discipline review that summarizes repeated mistakes and process drift

### Repository Structure

```text
investment-discipline-console/
  SKILL.md
  agents/openai.yaml
  references/
    doctrine.md
    schemas.md
    workflow-bootstrap.md
    workflow-portfolio-review.md
    workflow-holdings-delta-review.md
    workflow-discipline-memory.md
    workflow-watchlist.md
    workflow-pre-trade.md
    workflow-attribution.md
    behavior-tags.md
    examples.md
    end-to-end-examples.md
```

### What It Covers

- `bootstrap`: define portfolio size, target return, drawdown tolerance, single-position cap, single-theme cap, leverage cap, profit-taking or deleveraging trigger, macro view, and industry view
- `portfolio review`: review current holdings, leverage exposure, concentration, profit-take candidates, and cross-account risk
- `holdings delta review`: compare T-day and T+N-day holdings, identify major adds, trims, exits, and new positions, and require the user to explain large changes
- `discipline memory`: summarize user style, confirmed rules, repeated mistakes, and weekly discipline patterns so future reviews become more targeted
- `watchlist`: convert vague ideas into explicit thesis + catalyst records
- `pre-trade review`: return `allow`, `review`, `reduce_size`, `delay`, or `block`
- `attribution`: separate result from process and turn mistakes into reusable rules

Pre-trade action meanings:

- `allow`: execution is reasonable because the core information and sizing constraints are largely complete
- `review`: the direction may be right, but it is still too early to act because key fields or evidence are missing
- `reduce_size`: the direction may still be valid, but the position, leverage, or overlapping risk is too large and should be expressed with less size
- `delay`: do not act yet; this is better handled by collecting more information, waiting for new facts, or waiting for discipline conditions to be met
- `block`: do not proceed; the trade clearly violates the existing discipline or risk budget

### Install

From GitHub:

```bash
npx skills add https://github.com/yuanlslady/investment-discipline-console-skill/tree/main/investment-discipline-console
```

Manual install:

```bash
cp -R investment-discipline-console "${CODEX_HOME:-$HOME/.codex}/skills/"
```

### Usage

Typical prompts:

```text
Use $investment-discipline-console to help me set up my portfolio context before I review any trade.

Use $investment-discipline-console to combine my HK and US accounts into one portfolio view and tell me which limits I am breaching.

Use $investment-discipline-console to review whether I should open a Tencent starter position.

Use $investment-discipline-console to tell me which positions in my current portfolio need review first.

Use $investment-discipline-console to compare my T-day holdings with my T+3-day holdings and tell me which changes need explanation.

Use $investment-discipline-console to run a weekly discipline review and summarize what mistakes I repeated this week.

Use $investment-discipline-console to summarize what kind of trader I am becoming from my recent reviews and tell me what mistakes I repeat.
```

### Notes

- This skill is for structured decision support and review.
- It can build discipline memory, user-profile patterns, and weekly review summaries from prior reviews.
- It focuses on trade discipline, process quality, risk alignment, and behavior correction.
- It does not make symbol-selection or buy/sell recommendations for specific assets.
- It does not replace independent judgment.
- It is intentionally conservative when portfolio context is missing.

## 中文

这个仓库当前原生采用 Codex skill 格式打包；其中的方法论和提示结构也可以迁移到其他 AI Agent，但是否原生兼容取决于对方自己的扩展机制。
它把零散的交易想法、持仓截图、复盘笔记和重复行为模式，整理成一套可重复执行的操作系统：

- 首次使用的组合初始化
- 手工持仓 / 券商截图持仓 review
- 多账户组合汇总
- 两期持仓变化 review
- 观察池 intake
- 交易前审查
- 交易后归因
- 纪律记忆 / 用户画像迭代
- 行为偏差修正与错误标签沉淀

这套 skill 的定位不是“只做研究”的助手，而是“纪律系统”。它会优先要求组合上下文、风险预算和失效条件，再进入更深的公司分析。

### 什么时候会触发

一般有两种情况会触发这套 skill：

- 你直接点名使用 `$investment-discipline-console`
- 你的请求本身就在做持仓 review、交易审查、两期持仓对比、交易前 memo、交易后复盘，或者首次建立投资纪律系统

常见触发场景包括：

- 你上传持仓截图，希望 review 当前持仓
- 你给出两个时点的持仓，希望解释为什么变化这么大
- 你问“这笔交易我该不该做”
- 你第一次用这套系统，希望先把账户规模、回撤、仓位上限这些规则定下来
- 你希望做一次周度纪律复盘，看看这周重复了哪些错误

### 仓库结构

```text
investment-discipline-console/
  SKILL.md
  agents/openai.yaml
  references/
    doctrine.md
    schemas.md
    workflow-bootstrap.md
    workflow-portfolio-review.md
    workflow-holdings-delta-review.md
    workflow-discipline-memory.md
    workflow-watchlist.md
    workflow-pre-trade.md
    workflow-attribution.md
    behavior-tags.md
    examples.md
    end-to-end-examples.md
```

### 覆盖内容

- `bootstrap`：先定义账户规模、目标收益率、回撤容忍度、单仓上限、主题上限、杠杆上限、止盈降杠杆触发条件、宏观判断、产业判断
- `portfolio review`：review 当前持仓、杠杆暴露、集中度、止盈候选和跨账户风险
- `holdings delta review`：对比 T 日和 T+N 日持仓，识别大幅加仓、减仓、清仓、新开仓，并要求用户解释大变化
- `discipline memory`：沉淀用户风格、已确认规则、重复错误和周度纪律模式，让后续 review 更有针对性
- `watchlist`：把模糊想法变成明确的 thesis + catalyst 记录
- `pre-trade review`：输出 `allow`、`review`、`reduce_size`、`delay`、`block`
- `attribution`：把结果与过程拆开，沉淀成可复用规则

`pre-trade review` 几个状态的含义：

- `allow`：可以执行，核心信息和仓位约束基本完整
- `review`：方向可能对，但还不能直接下单，仍缺少关键字段或证据
- `reduce_size`：方向未必错，但仓位、杠杆或风险重叠过大，需要缩小表达
- `delay`：先别动，当前更适合补信息、等新事实或等纪律条件满足
- `block`：当前不应执行，这笔交易明显违反既定纪律或风险预算

### 安装

从 GitHub 安装：

```bash
npx skills add https://github.com/yuanlslady/investment-discipline-console-skill/tree/main/investment-discipline-console
```

手动安装：

```bash
cp -R investment-discipline-console "${CODEX_HOME:-$HOME/.codex}/skills/"
```

### 使用示例

```text
使用 $investment-discipline-console，先帮我建立组合上下文，再开始审查任何交易。

使用 $investment-discipline-console，把我的港股和美股账户合并成一个组合视角，并告诉我哪些仓位限制已经超了。

使用 $investment-discipline-console，帮我审查一下我是否应该先开一个腾讯的初始仓位。

使用 $investment-discipline-console，看看我当前持仓里哪些仓位最需要复盘。

使用 $investment-discipline-console，对比我 T 日和 T+3 日的持仓变化，并指出哪些大变化需要我解释原因。

使用 $investment-discipline-console，帮我做一次周度纪律复盘，总结这周我重复了哪些错误。

使用 $investment-discipline-console，根据我最近几次 review，总结一下我正在变成什么样的交易者，以及我最常重复的错误。
```

### 说明

- 这套 skill 用于结构化决策支持和复盘，只针对交易纪律与过程给建议，不代替独立判断，不针对具体标的是否值得买卖给建议。
- 它会基于历史 review 沉淀纪律记忆、用户画像和周度复盘摘要，但这些记忆只服务于过程建议，不服务于荐股或预测。
- 当组合上下文缺失时，它会刻意保守。
- 它强调“先制度，后研究；先组合，后单笔”。
