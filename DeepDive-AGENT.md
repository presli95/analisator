---
name: deep-dive
description: Run a deep research report on a public company ticker and score it across a 4-part investment framework: Growth & Momentum, Moat & Quality, Downside Protection, and Sentiment & Timing. Use when Codex is asked to evaluate a stock, produce a conviction score, rank tickers, generate an equity deep dive, or apply the user's V1 framework to any new ticker with cited sources.
---

# Deep Dive

Use this skill to produce a repeatable deep research memo for a single public-company ticker.

## Inputs

Gather or infer:

- Ticker
- Company name
- Reporting currency
- Most recent quarter and fiscal year

If the exchange or company name is ambiguous, resolve it before continuing.

## Non-Negotiables

- Browse for current data and verify every time; do not rely on stale memory.
- Use primary sources first: earnings releases, shareholder letters, 10-K, 10-Q, 8-K, proxy, Form 4, and investor presentations.
- Use secondary sources only when primary sources do not cover the item directly.
- Cite every major factual claim with a link.
- Distinguish facts from inference.
- Use exact dates for quarters, filings, and analyst actions.
- If a required data point cannot be confirmed, say so explicitly and score conservatively.

## Workflow

### 1. Establish the base packet

Collect:

- Last 4 quarterly revenue figures
- Revenue YoY for each of the last 4 quarters
- Sequential revenue trend for each of the last 4 quarters when meaningful
- Last 4 EPS results and consensus-surprise outcomes
- Latest forward guidance language: raised, in-line, cut, or no guide
- Last 4 quarterly gross margins
- Cash, debt, and net cash/net debt
- TTM free cash flow and FCF margin
- Current market cap and price-to-FCF
- Short interest
- Recent Form 4 activity
- Major institutional ownership trend if available

Prefer building a small working table before writing conclusions.

### 2. Score each framework dimension

Score out of the exact max shown below. Do not change the weights.

#### 1. Growth & Momentum (35 points)

Evaluate:

- Revenue YoY trend across the last 4 quarters
- Sequential trend across the last 4 quarters
- Whether growth is accelerating or decelerating
- Earnings surprise history for the last 4 quarters
- Forward guidance: raised, in-line, cut, or withdrawn

Weight acceleration more heavily than absolute size. A company moving from 8% to 14% growth should beat one moving from 30% to 25% if the rest is comparable.

Suggested scoring posture:

- 30-35: Clear acceleration, consistent beats, supportive guidance
- 22-29: Healthy but mixed trend, limited acceleration, modest execution
- 12-21: Deceleration or uneven execution
- 0-11: Deteriorating trend, repeated misses, weak guide

#### 2. Moat & Quality (25 points)

Evaluate:

- Top 3 competitors
- Moat type: network effects, switching costs, IP, brand, scale, cost advantage, regulatory position
- Gross margin level and trend over the last 4 quarters
- Customer concentration from 10-K or 10-Q footnotes

Customer concentration check is mandatory:

- Flag if any single customer exceeds 25% of revenue
- Flag if the top 3 customers exceed 50% of revenue
- For suppliers, semis, and component makers, explain whether bargaining power sits with the customer rather than the company

Suggested scoring posture:

- 20-25: Durable moat, stable/improving margins, low concentration risk
- 14-19: Some moat evidence but with caveats
- 7-13: Weak moat or margin pressure
- 0-6: Commodity profile or severe concentration risk

#### 3. Downside Protection (25 points)

Evaluate:

- Net cash vs net debt
- FCF margin
- Price/FCF using the best available current market value and TTM FCF
- Insider Form 4 buying or unscheduled selling

Interpretation rules:

- FCF margin above 15% is strong
- FCF margin below 5% signals survival or quality risk
- Price/FCF below 15x suggests a cheaper floor
- Price/FCF above 40x implies premium expectations
- Ignore routine 10b5-1 selling as a bullish or bearish signal unless the pattern is unusual and worth discussing separately
- Prioritize open-market insider buying and unscheduled discretionary selling

Suggested scoring posture:

- 20-25: Net cash or manageable leverage, strong cash generation, reasonable valuation, supportive insider signal
- 14-19: Acceptable balance sheet with some valuation or cash-flow risk
- 7-13: Thin margin of safety
- 0-6: Leverage, weak cash flow, expensive multiple, or negative insider read

#### 4. Sentiment & Timing (15 points)

Evaluate:

- TipRanks top-rated analyst stance only
- Short interest
- Institutional accumulation or distribution
- Whether the setup is contrarian, early, neutral, or crowded

Rules:

- Do not use broad analyst consensus as a substitute
- Focus on proven analysts with documented outperformance versus the S&P 500
- Treat crowded bullish positioning as a timing risk even if fundamentals are solid

Suggested scoring posture:

- 12-15: Favorable high-quality analyst read with supportive positioning and non-crowded setup
- 8-11: Mixed but acceptable setup
- 4-7: Crowded, controversial, or distribution-heavy setup
- 0-3: Clear sentiment/timing headwind

## Output Format

Structure the report in this exact order:

1. One-paragraph company snapshot
2. Scorecard table with all 4 dimensions, points earned, max points, and one-line rationale
3. Detailed analysis section for each dimension
4. Red flags
5. Final score and tier
6. Three-sentence asymmetric thesis
7. Sources

## Scoring Output

Always finish with:

- Final score: `X/100`
- Tier:
  - `80+ HIGH conviction`
  - `65-79 MEDIUM`
  - `50-64 WATCHLIST`
  - `<50 V1 REJECT`

Do not inflate scores to force a name into HIGH conviction. Reserve 80+ for rare cases.

## Writing Rules

- Be concise, specific, and evidence-led.
- Prefer tables for numeric quarter-by-quarter data.
- Label any estimate or interpretation as inference.
- Call out stale or missing information.
- Do not hide negatives inside neutral wording.
- If the business is strong but the setup is crowded or expensive, say so clearly.

## Recommended Report Skeleton

```markdown
# [Ticker] Deep Dive

## Snapshot
[1 short paragraph]

## Scorecard
| Dimension | Score | Max | Key takeaway |
| --- | ---: | ---: | --- |
| Growth & Momentum | X | 35 | ... |
| Moat & Quality | X | 25 | ... |
| Downside Protection | X | 25 | ... |
| Sentiment & Timing | X | 15 | ... |
| Total | XX | 100 | Tier |

## 1. Growth & Momentum
[analysis]

## 2. Moat & Quality
[analysis]

## 3. Downside Protection
[analysis]

## 4. Sentiment & Timing
[analysis]

## Red Flags
- ...

## Final Verdict
**Score:** XX/100
**Tier:** ...

## Asymmetric Thesis
[exactly 3 sentences]

## Sources
- [Source name](https://...)
```

## Default Research Order

Use this order unless a better source is obvious:

1. Investor relations earnings release / shareholder letter
2. 10-K / 10-Q / 8-K
3. Proxy and Form 4 filings
4. Company investor presentation
5. Market data source for valuation inputs
6. TipRanks for top-rated analyst stance
7. Exchange or data-provider source for short interest
8. Institutional ownership source

## Conservative Handling of Missing Data

If one element is unavailable:

- State what is missing
- Use the best proximate source if credible
- Reduce confidence
- Avoid giving full points to that subsection

If several core elements are unavailable, finish the report but mark it as lower-confidence.
