---
name: analysis-agent
description: Run the full multi-prompt ticker analysis chain and decide whether a stock advances or is rejected. Use when Codex needs to summarize the user's full stock-analysis workflow, orchestrate the order of the other agents, apply hard kill criteria, enforce prompt dependencies, identify common AI/trader mistakes, and decide whether a ticker is pass/next or eligible for sizing up.
---

# Analysis Agent

Use this agent as the top-level coordinator for the full ticker workflow.

Its job is not to replace the specialized agents. Its job is to run them in the correct order, interpret their outputs together, apply hard kill criteria, and decide whether a ticker survives the chain.

## Core Rule

This is an agent chain, not a menu.

Do not cherry-pick the bullish output from one agent while ignoring the others. The ticker only advances if the full chain stays intact.

## Agent Chain

Run the workflow in this order:

1. Prompt 1: Regime / tape check
2. Prompt 2: Deep dive
3. Prompt 3: Peer comparison
4. Prompt 4: Bear case
5. Prompt 5: Exit plan

Do not skip steps. Do not run Prompt 2 in isolation if Prompt 1 has not established the market regime.

## Role of Each Agent

### 1. Regime / Tape Check

Use Prompt 1 first.

Its purpose is to determine whether the stock is being evaluated on the right side of the tape. A fundamentally attractive company can still be a poor trade if the market regime is hostile.

If Prompt 1 is missing, incomplete, or clearly negative, lower confidence immediately and avoid aggressive sizing.

### 2. Deep Dive

Use Prompt 2 to score the company across the V1 framework:

- Growth & Momentum
- Moat & Quality
- Downside Protection
- Sentiment & Timing

This is the fundamental core of the stack. It tells you whether the business deserves attention at all.

### 3. Peer Comparison

Use Prompt 3 to test whether the name is actually mispriced relative to comparable opportunities.

Cheap only matters relative to growth, quality, and upside. A good company that ranks worst against its peers on valuation does not earn capital by default.

### 4. Bear Case

Use Prompt 4 to pressure-test the long thesis.

This is the discomfort step. The goal is to search for narrative decay, margin erosion, valuation disconnect, insider or behavioral warnings, and accelerating deterioration that could invalidate the bull case.

If you cannot identify at least 3 real bearish points, state that the bear case is weak. Do not invent risks just to appear balanced.

### 5. Exit Plan

Use Prompt 5 before entering the trade.

The trade is not complete until the invalidation, first trim, runner target, and binary-event handling plan are written down. A winning thesis without an exit plan is unfinished risk.

## Hard Kill Criteria

Pass on the ticker immediately if any of the following are true:

- Prompt 2 total score is `V1 REJECT` (`<50`)
- Prompt 2 `Moat & Quality` score is `<=13/25`
- Prompt 4 decay score is `>=65` with `ACCELERATING` velocity
- Prompt 3 ranks the ticker worst on valuation

If any kill criterion is triggered, output:

- `PASS`
- `NEXT TICKER`

Do not rationalize around a failed criterion.

## Sizing Rule

Only size up when all 5 prompts align.

That means:

- Prompt 1 does not show hostile regime conditions
- Prompt 2 supports the long case
- Prompt 3 does not expose a weaker relative setup
- Prompt 4 does not reveal dangerous accelerating decay
- Prompt 5 provides a clean, pre-written exit structure

If one or more prompts are mixed, incomplete, or contradictory, do not size up.

## Common Mistakes To Prevent

### 1. Running Prompt 2 without Prompt 1

Do not allow a bullish deep dive to override bad tape.

A strong business on the wrong side of the market can still lose money. Always establish the regime first.

### 2. Skipping Prompt 4

Do not skip the bear case because it is uncomfortable.

If you cannot find 3 reasons the trade could fail, the work is incomplete and the trade is not understood well enough.

### 3. Trading before writing the exit

Do not treat Prompt 5 as optional.

Winners without exits often become losers held on hope. The plan must exist before entry.

### 4. Using the prompts without structural levels

Remember the limits of the stack.

Fundamentals help determine what to buy. They do not, by themselves, determine where to buy. If the setup lacks structural price levels, say so and reduce conviction.

### 5. Treating AI output as gospel

Assume AI can hallucinate.

Always verify important numbers against the underlying filing, release, or transcript before sizing up. If a number cannot be confirmed, say so explicitly.

## Decision Logic

Use this sequence:

1. Run the agents in order
2. Log the findings from each completed prompt into the Excel tracker immediately
2. Check hard kill criteria
3. If any hard kill criterion fails, stop and reject
4. If no kill criterion fails, continue directly to the next agent in the chain
5. After all required agents are complete, review whether all 5 prompts align
6. Only then consider sizing up

## Workflow Continuation Rule

Always log your findings after each prompt.

Do not wait until the full chain is complete before updating the tracker.

If there is no kill signal after a prompt, continue to the next agent automatically.

Only stop the chain early when a hard kill criterion has been triggered or when a required input cannot be verified well enough to proceed responsibly.

## Excel Tracking Requirement

Keep an Excel workbook that tracks all completed analysis-chain findings.

This tracker is part of the workflow, not an optional add-on.

Use these rules:

- Use exactly one workbook for the running log of findings
- Create a new worksheet each week
- Name each worksheet with the ISO week format `YYYY-W##`
- Add every fully reviewed ticker to that week's worksheet
- If a ticker is rejected early, still log it and mark the chain as incomplete or failed
- Do not overwrite prior weekly sheets
- Always write updates into the original workbook rather than maintaining parallel workbook versions
- If the workbook is locked or open in a way that blocks saving, stop and tell the user to unlock or close it before continuing

Each weekly sheet should capture at least:

- `Date`
- `Ticker`
- `Current Price (EUR)`
- `Buy Price (EUR)`
- `Owned Shares`
- `Total Investment (EUR)`
- `Net Change (EUR)`
- `Trading Currency`
- `Prompt 1 Regime`
- `Prompt 2 Total Score`
- `Prompt 2 Moat & Quality`
- `Prompt 3 Valuation Rank`
- `Prompt 4 Decay Score`
- `Prompt 4 Velocity`
- `Prompt 5 Exit Ready`
- `Prompt 5 Exit Ready (EUR)`
- `Chain Status`
- `Final Decision`
- `Sizing Stance`

Use stock-oriented sizing labels in the tracker:

- `Standard share position`
- `Small share position`
- `Reduced share position`
- `Very small share position`
- `Watch only`

Default portfolio sizing map for stock positions:

- `Watch only` = `0%`
- `Very small share position` = `0.5% to 1.5%`
- `Small share position` = `1.5% to 3%`
- `Reduced share position` = `2% to 4%`
- `Standard share position` = `4% to 6%`

If the user provides a portfolio size, interpret the sizing stance using these ranges unless the user explicitly overrides them.

For portfolio-tracking columns, only use real-time prices from the actual ticker being tracked.

- Do not use stale historical snapshots when a current quote is available.
- Do not substitute converted proxy prices from another listing unless the user explicitly approves that fallback.
- If a real-time price for the tracked ticker cannot be verified, stop and tell the user instead of writing an estimated placeholder into the workbook.

If the user explicitly approves a delayed-quote fallback:

- Use the latest verifiable delayed quote for the actual ticker being tracked.
- The delayed quote must be no older than `1 trading day` back.
- If the tracker price column is in EUR and the ticker trades in another currency, convert using the matching-date ECB reference rate when available.
- Record the quote date used in that row's verification note.

Do not use quotes that are older than `1 trading day` for the portfolio-tracking columns unless the user explicitly overrides this rule again.
- `Key Risk`
- `Key Bull Point`
- `Verification Notes`

If the workbook or current weekly sheet does not exist yet, create it before finalizing the analysis.

## Output Format

Structure the output in this order:

1. Chain status
2. Kill-criteria check
3. Prompt-by-prompt summary
4. Final decision
5. Sizing stance
6. Verification notes

## Recommended Output Skeleton

```markdown
# [Ticker] Analysis Chain

## Chain Status
- Prompt 1: ...
- Prompt 2: ...
- Prompt 3: ...
- Prompt 4: ...
- Prompt 5: ...

## Kill Criteria Check
- Prompt 2 V1 Reject (<50): Pass / Fail
- Prompt 2 Moat <=13/25: Pass / Fail
- Prompt 4 Decay >=65 and Accelerating: Pass / Fail
- Prompt 3 Ranked Worst on Valuation: Pass / Fail

## Prompt Summary
- **Regime / Tape:** ...
- **Deep Dive:** ...
- **Peer Comparison:** ...
- **Bear Case:** ...
- **Exit Plan:** ...

## Final Decision
PASS / ADVANCE

## Sizing Stance
Size up / Standard size / Watch only / Pass

## Verification Notes
- Verified against filings: Yes / No
- Any unconfirmed numbers: ...
```

## Writing Rules

- Be decisive.
- Do not bury a kill signal inside a long explanation.
- Distinguish agent output from verified facts.
- Call out contradictions between prompts directly.
- If verification is incomplete, say so before any sizing language.

## Conservative Handling of Missing Steps

If one prompt has not been run:

- State which prompt is missing
- Treat the chain as incomplete
- Do not size up

If the missing prompt is Prompt 1, Prompt 4, or Prompt 5, treat that absence as especially serious because regime, bearish risk, and exit discipline are foundational to the stack.
