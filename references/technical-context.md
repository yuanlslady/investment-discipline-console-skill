# Technical Context

Technical indicators serve as timing and risk signals for fundamental investors — not as primary decision drivers. They flag momentum extremes, trend breaks, and relative pricing anomalies. They cannot override thesis quality, invalidation logic, or risk budget discipline.

## Indicator Set

Use exactly these four indicators. Do not invent additional indicators.

### 1. RSI(14) — Momentum Extreme

14-period Relative Strength Index. Measures whether a security is in overbought or oversold territory.

**Thresholds:**

| RSI Value | Label | Implication |
|-----------|-------|-------------|
| >= 75 | Overbought | Short-term momentum is stretched. Timing risk for new entries. |
| 60–74 | Elevated | No signal. Note if combined with 52W percentile > 80. |
| 40–59 | Neutral | No signal. |
| 26–39 | Depressed | No signal. |
| <= 25 | Oversold | Price may have over-corrected. Does not justify entry on its own. |

**Rules:**
- RSI >= 75 on a new entry → escalate to `delay` or `reduce_size` in pre-trade review
- RSI >= 75 on an existing position → note in portfolio review; do not change action on its own
- RSI <= 25 → reduce urgency of any panic-sell red flag; do not escalate to `allow` without fundamental check

### 2. Price vs Moving Averages — Trend Position

Compare current price to 20-day, 50-day, and 200-day simple moving averages.

**Thresholds:**

| Condition | Label | Implication |
|-----------|-------|-------------|
| Price > MA200 | Above long-term trend | Neutral to positive trend backdrop |
| Price < MA200 | Below long-term trend | Long-term trend break; flag in pre-trade review |
| Price < MA200 + MA200 slope falling | Confirmed downtrend | Escalate concern level in pre-trade review |
| Price < MA20 + MA20 slope falling | Short-term deterioration | Note in portfolio review for flagged positions |

**Rules:**
- Price below MA200 alone: note as a red flag in pre-trade context
- Price below MA200 with declining MA200: escalate pre-trade concern; do not block on its own
- MA data unavailable: mark as `data_unavailable`; do not block workflow

### 3. 52-Week Range Percentile — Historical Price Position

Where the current price sits within the 52-week high–low range.

Formula: `(current_price - 52w_low) / (52w_high - 52w_low) × 100`

**Thresholds:**

| Percentile | Label | Implication |
|------------|-------|-------------|
| >= 85 | Near 52W high | Buying near recent peak; increase sizing caution |
| 40–84 | Mid-range | Neutral |
| <= 20 | Near 52W low | Price has corrected significantly; check if fundamental thesis holds |

**Rules:**
- 52W percentile >= 85 AND RSI >= 70: trigger `reduce_size` in pre-trade review
- 52W percentile <= 20: surface "is the thesis intact?" prompt in pre-trade review; do not auto-allow
- 52W data unavailable: mark as `data_unavailable`; skip signal

### 4. Relative Strength vs Benchmark — Market Pricing Signal

3-month total return of the security minus the return of the relevant benchmark index (e.g., S&P 500 for US stocks, HSI for HK stocks, CSI 300 for CN stocks).

**Thresholds:**

| Relative Return | Label | Implication |
|-----------------|-------|-------------|
| >= +10% | Outperforming | Price reflects positive momentum; note if RSI is also high |
| -10% to +10% | In line | Neutral |
| <= -15% | Underperforming | Market may be pricing a risk not yet visible in the thesis; prompt investigation |

**Rules:**
- Relative strength <= -15%: surface "what is the market pricing that is not in my thesis?" prompt in both pre-trade and portfolio reviews
- Relative strength >= +10% + RSI >= 70: compound caution signal for pre-trade sizing
- Benchmark mapping: US → S&P 500 or sector ETF; HK → HSI or HSCEI; CN → CSI 300; mixed → use the dominant market index

## Data Availability Rule

If any indicator data is unavailable (no tool, no user input, no search result):

- Mark that field as `data_unavailable`
- Skip the signal for that indicator
- Do not assume a neutral reading
- Do not block the workflow

Prefer asking the user to supply data over skipping the technical context entirely. When the user is about to execute a trade, suggest fetching RSI and MA data before finalizing the action.

## Scope Rules

- **Pre-trade review**: run all four indicators for the target security
- **Portfolio review**: run all four indicators only for positions with weight > 5% OR positions already flagged with a red flag
- Do not run technical context for watchlist intake or post-trade attribution
- Technical signals do not override the pre-trade action set. They can upgrade an action (e.g., `review` → `reduce_size`) but cannot downgrade a `block` (a discipline violation stays blocked regardless of RSI)

## Output Format

Return a `technical_context` block alongside the primary review output.

```yaml
technical_context:
  ticker: string
  data_date: ISO date or "user_supplied"
  rsi_14: number | "data_unavailable"
  rsi_signal: overbought | elevated | neutral | depressed | oversold | data_unavailable
  price_vs_ma20: above | below | data_unavailable
  price_vs_ma50: above | below | data_unavailable
  price_vs_ma200: above | below | data_unavailable
  ma200_slope: rising | flat | falling | data_unavailable
  w52_percentile: number | "data_unavailable"
  w52_signal: near_high | mid_range | near_low | data_unavailable
  rel_strength_3m_vs_benchmark: number | "data_unavailable"
  rel_strength_signal: outperforming | in_line | underperforming | data_unavailable
  benchmark_used: string
  technical_summary: string   # one sentence: overall technical posture and its implication
  action_influence: none | note | delay | reduce_size
  # none: no signal strong enough to influence action
  # note: flagged for awareness, no action change
  # delay: timing risk sufficient to suggest waiting
  # reduce_size: combination of signals suggests smaller initial position
```
