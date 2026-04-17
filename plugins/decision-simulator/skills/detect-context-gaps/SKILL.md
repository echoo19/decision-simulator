---
name: detect-context-gaps
description: Identify missing information, hidden assumptions, and uncertainty that make a technical decision unreliable. Use when the current recommendation may be under-informed, when the user asks what they are missing, or when a decision could flip based on unknown constraints, scale, ownership, security, rollout, or operational details, including when Claude's own current plan depends on assumptions that have not been checked.
---

# Detect Context Gaps

Find the missing inputs that materially affect the decision. Do not ask for a long generic questionnaire.

## Method

1. Restate the current decision and provisional recommendation.
2. Identify which assumptions are carrying the answer.
3. Flag unknowns that could materially change the ranking of options.
4. Explain the risk created by each unknown.
5. Prefer the cheapest clarifying question, measurement, or experiment that reduces uncertainty.

## Focus Areas

Check for gaps in:

- real traffic or scale assumptions
- failure tolerance and recovery expectations
- latency or throughput requirements
- data sensitivity and compliance constraints
- ownership and team boundaries
- rollout and migration constraints
- testing and observability maturity
- dependency constraints and platform limits
- time horizon: quick patch versus long-lived system
- reversibility: how painful it is to undo the choice

## Quality Bar

- Only ask for information that changes the decision, confidence, or rollout plan.
- Name the consequence of not knowing.
- Distinguish `[assumption]`, `[unknown]`, and `[nice-to-know]`.
- If the answer is still directionally clear despite gaps, say so.

## Suggested Output

### Current decision frame

State the decision and the current leaning.

### Critical unknowns

List the few unknowns that could change the recommendation.

### Hidden assumptions

List the assumptions currently doing too much work.

### Risk of deciding now

Explain what could go wrong if the decision is made without resolving the gaps.

### Fastest ways to de-risk

Suggest the smallest checks, measurements, or clarifying questions that improve confidence.
