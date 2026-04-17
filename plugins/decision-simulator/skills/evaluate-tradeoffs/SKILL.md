---
name: evaluate-tradeoffs
description: Compare technical options across the factors that actually matter in context. Use when Claude or the user needs a concrete tradeoff analysis between two or more approaches, such as library choice, architecture choice, refactor vs leave it, frontend vs backend ownership, build vs buy, short-term speed vs long-term maintainability, or when Claude is deciding between multiple plausible next implementation paths mid-task.
---

# Evaluate Tradeoffs

Compare options across the dimensions that are actually decision-driving in this case. Do not blindly enumerate every possible factor.

## Method

1. Name the options clearly.
2. Choose the smallest set of relevant dimensions.
3. For each dimension, explain the mechanism behind the difference.
4. Identify which dimensions are decisive versus merely nice-to-have.
5. Say when one option dominates and why.
6. State the conditions that would flip the recommendation.

## Common Dimensions

Use only the dimensions that matter here:

- UX
- DX
- system boundaries
- maintainability
- delivery speed
- scalability
- performance
- reliability
- security and privacy
- infra cost
- engineering time
- team coordination overhead
- debugging difficulty
- flexibility
- reversibility
- operational burden

## Quality Bar

- Avoid empty labels like "faster" or "cleaner" without explaining what becomes faster or cleaner.
- Make asymmetry visible. Some options will have one major win and three serious liabilities.
- Highlight non-obvious tradeoffs first.
- Prefer saying "Option A dominates because..." over pretending the choice is balanced.

## Suggested Output

### Options

List the options.

### Relevant dimensions

Name the dimensions that matter and why they matter here.

### Tradeoff analysis

For each decisive dimension, compare the options with concrete implications.

### Dominant option

Name the option that wins on the dimensions that matter most, or state that the answer depends on a specific missing input.

### Recommendation

Make a call and explain what would change the answer.
