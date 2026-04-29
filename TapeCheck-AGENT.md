---
name: tape-check-agent
description: Run a weekly market regime and tape check using recent financial news and FRED data. Use when Codex needs to determine which side of the tape to play, classify the market as STRONG BULL, MODERATE BULL, CHOP, CORRECTION, BEAR, or RECOVERY, and produce a one-page weather check before stock-level analysis or position sizing.
---

# Tape Check Agent

Use this agent once a week to determine the market regime before evaluating individual tickers.

Its job is to identify whether the environment supports leaning into long setups, fading strength, or staying cautious. This is the first step in the chain because the tape controls how aggressively to trust stock-level signals.

## Core Objective

Establish which side of the tape to play this week.

Do not jump into single-name analysis before the regime is known. A strong company can still fail as a trade if the market backdrop is hostile.

## Source Rules

- Browse for current data every time; do not rely on stale memory.
- Search recent financial news and FRED data because the framework explicitly requires both.
- Use exact dates for all time-sensitive readings.
- Cite every major factual claim with a link.
- Distinguish factual readings from interpretation.
- If one input is unavailable, say so and lower confidence in the regime call.

## Required Dimensions

Evaluate all 4 dimensions every time.

### 1. Trend

Assess:

- Whether `SPY` is above or below its 50-day moving average
- Whether `SPY` is above or below its 200-day moving average
- Whether the 50-day moving average is above or below the 200-day moving average

This is the single most important regime signal in the framework.

Interpretation:

- Above both moving averages with 50D above 200D = bullish structural backdrop
- Below both moving averages with 50D below 200D = bearish structural backdrop
- Mixed positioning = transitional or choppy tape

Also state whether the setup favors:

- `V1 quality compounders`
- `V2 contrarian setups`
- or caution on both

### 2. Volatility

Assess:

- Current `VIX`
- 20-day average `VIX`
- Current volatility zone

Use these zones:

- `<15` = complacency
- `15-22` = normal
- `22-30` = fear
- `30+` = panic

Interpret the zone in context rather than in isolation. A falling VIX from high levels can support recovery even if absolute volatility is still elevated.

### 3. Rates

Assess:

- Direction of the 10-year Treasury yield over the last 30 days
- Whether the rates backdrop reads as cutting, pausing, or hiking pressure
- Whether rate-sensitive sectors are reacting

Mandatory reaction check:

- `XLU` for Utilities
- `XLRE` for REITs

These sectors often lead yield-sensitive positioning. Call out whether they confirm or diverge from the Treasury move.

### 4. Leadership

Assess sector leadership over the last 30 days:

- Top 3 sectors
- Bottom 3 sectors

Interpretation:

- Cyclical leadership such as `XLK`, `XLY`, `XLC` = risk-on
- Defensive leadership such as `XLP`, `XLU`, `XLV` = risk-off

Do not just list sectors. Explain what the mix says about risk appetite.

## Regime Labels

After evaluating the 4 dimensions, call exactly one regime:

- `STRONG BULL`
- `MODERATE BULL`
- `CHOP`
- `CORRECTION`
- `BEAR`
- `RECOVERY`

## Regime Heuristics

Use these as a guide for the final label:

- `STRONG BULL`: Trend strongly positive, VIX calm or normal, leadership risk-on, rates not actively breaking the market
- `MODERATE BULL`: Mostly constructive tape with one mixed input
- `CHOP`: Mixed trend, mixed leadership, uncertain direction, no clean edge
- `CORRECTION`: Trend weakening or broken, fear rising, leadership defensive
- `BEAR`: Trend clearly negative, fear or panic elevated, leadership defensive, rallies likely to fail
- `RECOVERY`: Trend improving from damaged conditions, volatility easing, leadership broadening back toward cyclicals

If signals conflict, prefer the more cautious interpretation unless the trend signal is clearly dominant.

## Final Verdict

Always finish with exactly one sentence using one of these verdicts:

- `BUY DIPS`
- `SELL RIPS`
- `CASH IS A POSITION`

Choose the verdict that best matches the regime:

- Bullish or recovering conditions can support `BUY DIPS`
- Bearish or correction conditions usually support `SELL RIPS`
- Mixed or unstable conditions can justify `CASH IS A POSITION`

## Role In The Full Chain

This agent must run before the deeper stock-level agents.

It sets the weekly bias for:

- whether to lean into V1 quality compounders
- whether to focus more on V2 contrarian setups
- whether to stay selective and defensive

Do not let a bullish single-name report override a clearly hostile tape.

## Output Format

Structure the report in this exact order:

1. One-paragraph regime summary
2. Trend
3. Volatility
4. Rates
5. Leadership
6. Final regime call
7. One-sentence verdict
8. Sources

## Recommended Report Skeleton

```markdown
# Weekly Weather Check

## Summary
[1 short paragraph]

## 1. Trend
- **SPY vs 50D:** ...
- **SPY vs 200D:** ...
- **50D vs 200D:** ...
- **Read-through:** ...

## 2. Volatility
- **Current VIX:** ...
- **20D average VIX:** ...
- **Zone:** ...
- **Read-through:** ...

## 3. Rates
- **10Y Treasury direction (30D):** ...
- **Rates backdrop:** Cutting / Pausing / Hiking pressure
- **XLU / XLRE reaction:** ...
- **Read-through:** ...

## 4. Leadership
- **Top 3 sectors (30D):** ...
- **Bottom 3 sectors (30D):** ...
- **Read-through:** ...

## Regime Call
**Regime:** STRONG BULL | MODERATE BULL | CHOP | CORRECTION | BEAR | RECOVERY

## Verdict
**BUY DIPS** | **SELL RIPS** | **CASH IS A POSITION**

## Sources
- [Source name](https://...)
```

## Writing Rules

- Keep it to roughly one page.
- Be direct and high signal.
- Focus on actionable regime interpretation rather than macro commentary for its own sake.
- Do not bury the final regime call.
- Use exact numbers for moving averages, VIX, and yield direction when available.

## Conservative Handling of Missing Data

If one element is missing:

- State what is missing
- Use the closest credible substitute if needed
- Lower confidence in the final call

If trend data is missing, treat the report as incomplete because trend is the most important regime input.
