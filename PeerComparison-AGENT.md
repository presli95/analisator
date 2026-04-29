---
name: peer-comparison
description: Build a relative valuation comparison for a public company ticker versus two peers using Yahoo Finance, Macrotrends, and TipRanks. Use when Codex is asked to compare a stock against peers, rank relative valuation, find the cheapest growth name, assess upside versus competitors, or apply the user's V1 peer-comparison framework with cited sources.
---

# Peer Comparison

Use this skill to compare one target ticker against exactly two named peers and rank all three by relative attractiveness.

## Inputs

Gather or confirm:

- Target ticker
- Peer 1 ticker
- Peer 2 ticker
- Company names
- Sector / industry classification
- Reporting currency

If the peers operate in different business models, say so and reduce confidence in the ranking.

## Source Rules

- Browse for current data every time; do not rely on memory.
- Use Yahoo Finance, Macrotrends, and TipRanks as the default external sources because the framework explicitly calls for them.
- Prefer company filings or earnings releases for latest-quarter revenue growth and gross margin when source values conflict.
- Cite each metric row with links or cite clearly by source block.
- Use exact dates for price targets, quarter references, and 52-week-high context when available.
- If a metric cannot be verified consistently, mark it `N/A` and explain why.

## Required Table

Build a comparison table with one row per company and these exact columns:

- Forward PE
- PEG ratio
- Price/FCF
- Analyst price target upside %
- Distance below 52-week high %
- YoY revenue growth (latest quarter)
- Gross margin (latest quarter)

Add a final `Rank` column after analysis if it improves readability.

## Metric Definitions

- Forward PE: Use the current forward price/earnings multiple from a current market-data source
- PEG ratio: Forward PE divided by expected growth; use the same growth convention across all names if possible
- Price/FCF: Current market value relative to trailing twelve-month free cash flow
- Analyst price target upside %: `(consensus or selected target - current price) / current price`
- Distance below 52-week high %: `(52-week high - current price) / 52-week high`
- YoY revenue growth: Latest reported quarter versus the same quarter last year
- Gross margin: Latest reported quarter if available, otherwise latest reported trailing company figure with a note

## V1 Valuation Rules

Apply these rules explicitly in the write-up:

- PEG <1.0 = growth significantly underpriced
- Price/FCF <15x = strong cash-flow floor
- Target upside >20% = meaningful room to run
- More than 30% below the 52-week high = deep contrarian discount

Cheap only matters relative to growth. The winner should reflect the best combination of valuation, growth support, and upside rather than the single lowest multiple.

## Cyclical Exception

Check whether the names are cyclical or commodity-linked first.

For Energy, Materials, Mining, or other clearly cyclical commodity businesses:

- Skip PEG entirely
- Say PEG is not meaningful because trough or peak earnings distort it
- Base the valuation conclusion mainly on target upside and Price/FCF
- Still show Forward PE if available, but do not let it dominate the ranking

If only one of the three companies is cyclical while the others are not, call out that the comparison is structurally imperfect.

## Workflow

### 1. Verify comparability

Before scoring, check:

- Same or adjacent industry
- Similar business model
- Similar exposure to cycles, regulation, or commodity pricing

If the peer set is weak, continue but note the limitation prominently.

### 2. Collect the raw metrics

For all 3 companies, collect:

- Current share price
- 52-week high
- Forward PE
- PEG, if applicable
- Price/FCF
- Analyst price target
- Latest quarter revenue growth
- Latest quarter gross margin

Keep the underlying numbers in a working table before writing conclusions.

### 3. Evaluate cheapness relative to quality

Interpret the table with emphasis on:

- Whether low valuation is justified by weaker growth or margins
- Whether high growth is already fully priced in
- Whether upside-to-target is meaningful or mostly exhausted
- Whether the name has a cash-flow floor
- Whether the discount to the 52-week high is an opportunity or a warning sign

### 4. Rank best to worst

Rank all 3 names from best to worst.

The winner should have the best combination of:

- Cheap valuation
- Room to run
- Cash-flow support
- Adequate growth and margin quality

Do not automatically crown the fastest grower or the cheapest multiple.

## Output Format

Structure the report in this exact order:

1. One-paragraph setup explaining the peer set
2. Relative valuation table
3. Short analysis of each company
4. Best-to-worst ranking with rationale
5. Winner summary
6. Sources

## Writing Rules

- Be crisp and comparative rather than writing three isolated mini-profiles.
- Highlight which metrics are most decision-relevant.
- When metrics conflict, explain the tradeoff plainly.
- Separate facts from inference.
- Do not overstate precision if data comes from mixed sources.

## Recommended Report Skeleton

```markdown
# [Ticker] Peer Comparison

## Setup
[1 short paragraph explaining why these peers are relevant]

## Relative Valuation Table
| Company | Forward PE | PEG | Price/FCF | Analyst Target Upside % | Below 52W High % | YoY Revenue Growth | Gross Margin | Notes |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| Target | ... | ... | ... | ... | ... | ... | ... | ... |
| Peer 1 | ... | ... | ... | ... | ... | ... | ... | ... |
| Peer 2 | ... | ... | ... | ... | ... | ... | ... | ... |

## Comparison Read
### [Target]
[short comparative read]

### [Peer 1]
[short comparative read]

### [Peer 2]
[short comparative read]

## Ranking
1. [Winner] - ...
2. [Second] - ...
3. [Third] - ...

## Winner Summary
[2-4 sentences on why the winner offers the best mix of cheapness, growth support, and upside]

## Sources
- [Yahoo Finance](https://...)
- [Macrotrends](https://...)
- [TipRanks](https://...)
```

## Ranking Heuristics

Use these as tie-breakers:

- Prefer the name with both valuation support and real upside over a statistically cheap name with no catalyst room
- Prefer stronger gross margins when the valuation gap is small
- Prefer stronger revenue growth when valuation is only modestly higher
- Penalize names already near price targets or near 52-week highs unless the fundamentals are clearly superior
- Penalize weak FCF support

## Conservative Handling of Missing Data

If a metric is missing or inconsistent:

- Mark it `N/A`
- Note the source conflict or absence
- Avoid forcing false precision
- Lower confidence in the final ranking

If PEG is unavailable for a non-cyclical business, explain whether the expected-growth source is missing or not credible enough to use.
