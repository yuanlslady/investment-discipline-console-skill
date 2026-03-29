# Investment Discipline Console Skill

English | 中文

* * *

## English

Discipline-first investing workflow skill for Codex and compatible AI agents. It turns scattered trade ideas, holdings screenshots, and review notes into a structured operating system:

- First-run portfolio bootstrap
- Holdings review from manual input or broker screenshots
- Multi-account portfolio aggregation
- Watchlist intake
- Pre-trade review
- Post-trade attribution
- Behavior correction and mistake tagging

This skill is designed to behave like a discipline system, not a research-only assistant. It prioritizes portfolio context, risk budgets, and invalidation rules before deep company-level analysis.

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
    workflow-watchlist.md
    workflow-pre-trade.md
    workflow-attribution.md
    behavior-tags.md
    examples.md
    end-to-end-examples.md
```

### What It Covers

- `bootstrap`: define portfolio size, return target, drawdown tolerance, position cap, theme cap, leverage cap, profit-taking trigger, macro stance, and industry stance
- `portfolio review`: review current holdings, leverage exposure, concentration, profit-take candidates, and cross-account risk
- `watchlist`: convert vague ideas into explicit thesis + catalyst records
- `pre-trade review`: return `allow`, `review`, `reduce_size`, `delay`, or `block`
- `attribution`: separate process quality from outcome quality and turn mistakes into rules

### Install

Manual install:

```bash
cp -R investment-discipline-console "${CODEX_HOME:-$HOME/.codex}/skills/"
```

Or install from this GitHub repo using your preferred Codex skill installer if it supports GitHub sources.

### Usage

Typical prompts:

```text
Use $investment-discipline-console to help me set up my portfolio context before I review any trade.

Use $investment-discipline-console to combine my HK and US accounts into one portfolio view and tell me which limits I am breaching.

Use $investment-discipline-console to review whether I should open a Tencent starter position.
```

### Notes

- This skill is for structured decision support and review.
- It does not replace independent judgment.
- It is intentionally conservative when portfolio context is missing.

## 中文

这是一个面向 Codex 和兼容 AI Agent 的“投资纪律工作流” skill。它把零散的交易想法、持仓截图、复盘笔记，整理成一套可重复执行的操作系统：

- 首次使用的组合初始化
- 手工持仓 / 券商截图持仓 review
- 多账户组合汇总
- 观察池 intake
- 交易前审查
- 交易后归因
- 行为偏差修正与错误标签沉淀

这套 skill 的定位不是“只做研究”的助手，而是“纪律系统”。它会优先要求组合上下文、风险预算和失效条件，再进入更深的公司分析。

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
- `watchlist`：把模糊想法变成明确的 thesis + catalyst 记录
- `pre-trade review`：输出 `allow`、`review`、`reduce_size`、`delay`、`block`
- `attribution`：把结果与过程拆开，沉淀成可复用规则

### 安装

手动安装：

```bash
cp -R investment-discipline-console "${CODEX_HOME:-$HOME/.codex}/skills/"
```

如果你的 Codex skill 安装器支持 GitHub 源，也可以直接从本仓库安装。

### 使用示例

```text
Use $investment-discipline-console to help me set up my portfolio context before I review any trade.

Use $investment-discipline-console to combine my HK and US accounts into one portfolio view and tell me which limits I am breaching.

Use $investment-discipline-console to review whether I should open a Tencent starter position.
```

### 说明

- 这套 skill 用于结构化决策支持和复盘，不代替独立判断。
- 当组合上下文缺失时，它会刻意保守。
- 它强调“先制度，后研究；先组合，后单笔”。

