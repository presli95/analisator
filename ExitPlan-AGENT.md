---
name: exit-plan
description: Build a 3-leg exit plan for a public company ticker at the current price, including invalidation, first trim, runner target, and a 90-day binary catalyst check. Use when Codex is asked to plan exits before entering a stock, define stop and trim levels, assess whether to use shares or options around confirmed catalysts, or apply the user's V1 exit framework with cited sources.
---

# Exit Plan

Use this skill to create a disciplined pre-entry exit plan for a single public-company ticker.

## Inputs

Gather or confirm:

- Ticker
- Company name
- Current price
- Trading currency
- Entry assumption: entering today

If the user supplies a price, verify it against the live market price and note any mismatch.

## Non-Negotiables

- Browse for current market data every time; do not rely on stale memory.
- Use exact dates for prices, earnings dates, and catalyst timing.
- Cite every major factual claim with a link.
- Separate technical interpretation from factual event data.
- If the chart context or event timing cannot be confirmed, say so explicitly and reduce confidence.
- Respect the user's hard rule: exit any long the moment its decay score crosses `65`, with no override.

## Core Objective

Write the exit plan before entry, not after.

The plan must define:

- One invalidation level that breaks the long thesis
- One first trim target for selling one-third
- One runner target for the remaining position
- One decision on shares versus defined-risk options if a confirmed binary event is near

Avoid vague language like "watch support" or "take profits gradually." Give specific levels and reasoning.

## Workflow

### 1. Establish the trade context

Collect:

- Current price
- Recent daily chart structure
- Nearby support and resistance levels
- 52-week range
- Trend context such as higher highs/higher lows, consolidation, base, or breakdown risk

Use daily-close logic for invalidation because the framework explicitly requires a daily close breach.

### 2. Define the 3-leg exit plan

#### 1. Invalidation (stop)

Identify:

- The technical level that, if broken on a daily close, tells you the long thesis is wrong
- The exact price
- The reason the level matters

Good invalidation anchors include:

- Loss of key support
- Breakdown below a prior swing low
- Failure of a breakout retest
- Violation of a well-respected moving level only if price has clearly reacted to it

Do not place the invalidation at an arbitrary percentage loss. Tie it to structure.

Also state the standing V1 rule:

- Exit any long immediately if the decay score crosses `65`, regardless of chart position

#### 2. First Target (trim 1/3)

Identify:

- The most logical first resistance level
- The exact price
- The reason it is the correct first trim zone

Prefer obvious resistance such as:

- Prior range high
- Recent failed breakout level
- Gap-fill zone
- Major supply shelf

Choose the first target where taking one-third off improves risk management without prematurely capping the trade.

#### 3. Runner Target (let the rest ride)

Identify:

- The next major resistance above the first target or a measured-move objective
- The exact price
- The reason it is a logical runner target

Prefer:

- Higher timeframe resistance
- Measured move from a base or breakout
- Extension to prior major highs

Do not set a runner target only slightly above the first trim unless the chart genuinely lacks higher structure.

### 3. Run the binary catalyst check

Search only the next 90 days for confirmed binary events.

Mandatory checks:

- Next earnings date
- Confirmed FDA PDUFA decisions, if relevant
- Scheduled court rulings
- Analyst day
- Confirmed guidance updates or similarly date-certain company events

Ignore:

- Unconfirmed product launches
- Vague partnership announcements
- Rumored catalysts
- Generic future strategic initiatives without dates

### 4. Make the instrument decision

If a confirmed binary event is within 30 days:

- Prefer defined-risk options such as calls or LEAPS instead of shares
- State whether to trim before the event or hold through it
- Explain why using event asymmetry, implied gap risk, and thesis dependence on the catalyst

If no confirmed binary event is within 30 days:

- Default to shares unless there is another strong reason to prefer options

Do not recommend holding full share size through a near-term binary event without discussing downside gap risk.

## Output Format

Structure the report in this exact order:

1. One-paragraph trade setup
2. Current price and context
3. 3-leg exit plan
4. Binary catalyst check
5. Shares versus options decision
6. Final action summary
7. Sources

## Writing Rules

- Be specific and execution-oriented.
- Tie every level to chart structure, not preference.
- Distinguish confirmed events from speculation.
- Use exact prices rather than broad zones when possible.
- If the chart is messy or level quality is poor, say so plainly.
- Keep the exit logic consistent with the thesis rather than maximizing optimism.

## Recommended Report Skeleton

```markdown
# [Ticker] Exit Plan

## Setup
[1 short paragraph]

## Current Context
- **Current price:** $...
- **Date checked:** ...
- **Trend context:** ...

## 1. Invalidation
- **Level:** $...
- **Rule:** Exit on a daily close below this level
- **Reasoning:** ...
- **V1 overlay:** Exit immediately as well if decay score crosses 65

## 2. First Target
- **Level:** $...
- **Action:** Trim 1/3
- **Reasoning:** ...

## 3. Runner Target
- **Level:** $...
- **Action:** Let the remaining position ride toward this level
- **Reasoning:** ...

## Binary Catalyst Check
- **Next earnings date:** ...
- **Other confirmed binary events in next 90 days:** ...
- **Within 30 days?:** Yes / No

## Instrument Decision
- **Use:** Shares | Defined-risk options
- **Event plan:** Trim before event | Hold through event
- **Reasoning:** ...

## Final Action Summary
[2-4 sentences summarizing the full plan]

## Sources
- [Source name](https://...)
```

## Technical-Level Heuristics

Use these tie-breakers when several levels look plausible:

- Prefer horizontal price structure over indicator-only levels
- Prefer levels with repeated market reaction
- Prefer recent daily levels over old historical levels when both are relevant
- Prefer cleaner invalidation below clear support rather than directly at support
- Prefer first targets that offer a credible reward relative to the invalidation distance

## Binary Event Rules

Treat an event as binary only if the date is confirmed by a credible source.

Examples that can qualify:

- Company-confirmed earnings date
- FDA calendar or company-confirmed PDUFA date
- Court calendar with a scheduled ruling or hearing date
- Company-confirmed analyst day
- Company-confirmed guidance update event

If an event is only rumored or tentatively discussed, exclude it.

## Conservative Handling of Missing Data

If one required input is unclear:

- State what is unclear
- Use the closest credible source if one exists
- Lower confidence
- Avoid pretending the level is precise if the structure is not

If binary-event timing cannot be confirmed, say the catalyst check is incomplete and avoid strong event-trading recommendations.
