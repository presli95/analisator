---
name: bear-case
description: Produce a skeptical short-seller research report on a public company ticker and score narrative decay across a 4-part framework: Growth Deterioration, Margin & Cash Flow Erosion, Valuation Disconnect, and Insider & Behavioral. Use when Codex is asked to build a bear case, evaluate short risk/reward, assess narrative decay, pressure-test a long thesis, or apply the user's V1 bearish framework with cited sources.
---

# Bear Case

Use this skill to build a disciplined bearish research memo for a single public-company ticker.

## Inputs

Gather or infer:

- Ticker
- Company name
- Reporting currency
- Most recent quarter and fiscal year
- Sector and business model

If the company or exchange is ambiguous, resolve it first.

## Non-Negotiables

- Browse for current data and verify every time; do not rely on stale memory.
- Search SEC filings, earnings transcripts, and recent news as the default evidence set because the framework requires all three.
- Prefer primary sources first: 10-K, 10-Q, 8-K, earnings release, shareholder letter, transcript, Form 4, proxy.
- Cite every major factual claim with a link.
- Distinguish facts from inference and from bearish interpretation.
- Use exact dates for filings, calls, quarter comparisons, and insider trades.
- If a required data point cannot be verified, say so explicitly and score conservatively.

## Core Objective

Act like a skeptical short-seller, not a neutral summarizer.

The job is to test whether the story is breaking beneath the headline narrative. Look for evidence that deterioration is being hidden by framing, adjustments, or backward-looking comparisons.

If you cannot identify at least 3 concrete bearish points, say that the short thesis is weak rather than inventing one.

## Workflow

### 1. Establish the decay packet

Collect:

- Last 4 quarterly revenue figures
- Revenue YoY for each of the last 4 quarters
- Sequential revenue trend for each of the last 4 quarters
- Latest guidance and changes versus prior guidance
- Bookings, backlog, pipeline, RPO, or equivalent forward-demand indicators if relevant
- Last 4 quarterly gross margins
- Last 4 quarterly operating margins
- TTM free cash flow and FCF trend
- Capex trend over the last 4 quarters or TTM where more useful
- Current valuation multiples and, if possible, historical valuation range context
- Recent Form 4 activity
- GAAP versus non-GAAP gap indicators
- Short-interest trend
- Estimate-dispersion clues if available

Build a compact working table before writing conclusions.

### 2. Score each framework dimension

Score out of the exact max shown below. Do not change the weights.

Higher scores mean stronger bearish evidence and greater narrative decay.

#### 1. Growth Deterioration (35 points)

Evaluate:

- Revenue deceleration rate across the last 4 quarters
- Sequential declines that management may be obscuring with YoY framing
- Guidance cuts, cautious language, or hedging language
- Shrinking bookings, backlog, pipeline, RPO, or forward-demand indicators

Look for:

- Growth slowing faster than the market narrative implies
- Management emphasizing annual comparisons while quarter-to-quarter demand weakens
- Soft guide buried inside selective highlights

Suggested scoring posture:

- 30-35: Clear and worsening deterioration with cuts or obvious demand weakness
- 22-29: Meaningful slowdown with several warning signs
- 12-21: Mixed evidence, some softness but not a clean break
- 0-11: Little evidence of deterioration

#### 2. Margin & Cash Flow Erosion (25 points)

Evaluate:

- Gross margin compression over the last 4 quarters
- Operating margin compression over the last 4 quarters
- FCF deterioration
- Capex divergence

Capex divergence is mandatory to assess:

- Flag when capex is rising into a slowdown
- Treat spending into weakening demand as one of the most dangerous signals in the framework
- Explain whether management is investing for genuine capacity needs or defending a weakening narrative

Suggested scoring posture:

- 20-25: Broad margin compression plus worsening FCF and dangerous capex behavior
- 14-19: Real erosion with partial offsets
- 7-13: Early or mixed pressure
- 0-6: Margins and cash flow remain resilient

#### 3. Valuation Disconnect (25 points)

Evaluate:

- Premium valuation despite deteriorating fundamentals
- Implied growth versus actual delivery
- Current multiple versus historical valuation range

Look for:

- A stock priced for strength while revenue, margins, or cash flow are weakening
- A multiple near the high end of history while operating results sit near the low end
- A market narrative that still assumes reacceleration without evidence

Suggested scoring posture:

- 20-25: Severe mismatch between price and fundamentals
- 14-19: Clear but not extreme disconnect
- 7-13: Some disconnect, partly justified
- 0-6: Valuation already reflects the weakness

#### 4. Insider & Behavioral (15 points)

Evaluate:

- Unscheduled Form 4 selling
- GAAP versus non-GAAP gap
- Narrative inflation in earnings calls
- Rising short interest
- Estimate dispersion widening

Rules:

- Ignore routine 10b5-1 selling as a core bearish signal unless the pattern is unusual and worth separate discussion
- Prioritize open-market discretionary selling
- Treat a widening adjustment gap as a sign that reported "performance" may be diverging from economic reality
- Call out promotional language if transcripts become more optimistic while numbers worsen

Suggested scoring posture:

- 12-15: Strong behavioral and insider warning signals
- 8-11: Several meaningful soft-warning indicators
- 4-7: Limited but notable concerns
- 0-3: Weak behavioral evidence

## Decay Velocity

After scoring, classify decay velocity as one of:

- `ACCELERATING`: Deterioration is worse than last quarter
- `STABLE`: Weakness persists but is not clearly worsening
- `DECELERATING`: Deterioration is stabilizing and may be bottoming

Base the velocity call on direction of change, not absolute badness. A company can still look weak while decay is decelerating.

## Short-Signal Tiers

Always translate the score into one of these conclusions:

- `80+` and `ACCELERATING` = high-conviction short via put LEAPS
- `65-79` = medium-conviction short, defined-risk only
- `55-64` = avoid the long, not enough for an active short
- `<55` = no short signal; decay may be stabilizing

Do not force a high-conviction short unless both score and velocity support it.

## Output Format

Structure the report in this exact order:

1. One-paragraph bearish setup
2. Scorecard table with all 4 dimensions, points earned, max points, and one-line rationale
3. Detailed analysis section for each dimension
4. Three strongest bearish points
5. Total score and decay velocity
6. Short-signal tier
7. One invalidation trigger
8. Sources

## Writing Rules

- Be direct and skeptical without becoming sensational.
- Focus on evidence of breakage, not generic business risk.
- Prefer quarter-by-quarter tables for trend deterioration.
- Separate facts from interpretation.
- If the evidence is mixed, say the short thesis is incomplete.
- Do not overstate insider selling if the activity is mostly pre-planned.

## Recommended Report Skeleton

```markdown
# [Ticker] Bear Case

## Setup
[1 short paragraph]

## Scorecard
| Dimension | Score | Max | Key takeaway |
| --- | ---: | ---: | --- |
| Growth Deterioration | X | 35 | ... |
| Margin & Cash Flow Erosion | X | 25 | ... |
| Valuation Disconnect | X | 25 | ... |
| Insider & Behavioral | X | 15 | ... |
| Total | XX | 100 | Decay velocity + tier |

## 1. Growth Deterioration
[analysis]

## 2. Margin & Cash Flow Erosion
[analysis]

## 3. Valuation Disconnect
[analysis]

## 4. Insider & Behavioral
[analysis]

## Strongest Bearish Points
- ...
- ...
- ...

## Verdict
**Score:** XX/100
**Decay Velocity:** ACCELERATING | STABLE | DECELERATING
**Tier:** ...

## Invalidation Trigger
[1 sentence on what would break the short thesis]

## Sources
- [Source name](https://...)
```

## Default Research Order

Use this order unless a better source is obvious:

1. Earnings release / shareholder letter
2. 10-K / 10-Q / 8-K
3. Earnings transcript
4. Form 4 filings
5. Recent news on demand, customers, pricing, or guidance changes
6. Market-data source for valuation context
7. Short-interest source
8. Historical multiple source if needed

## Invalidation Standard

The invalidation trigger must be specific and falsifiable.

Prefer a trigger such as:

- Reacceleration in revenue plus stabilizing sequential demand
- Margin compression reversing for 2 consecutive quarters
- Cash-flow recovery while capex normalizes
- Guidance raised with evidence, not just rhetoric

Avoid vague invalidations like "if sentiment improves."

## Conservative Handling of Missing Data

If one element is unavailable:

- State what is missing
- Use the closest credible proxy if one exists
- Lower confidence
- Avoid giving full points to that subsection

If several core elements are unavailable, complete the report but label it lower-confidence.
