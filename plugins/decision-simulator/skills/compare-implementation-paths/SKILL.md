---
name: compare-implementation-paths
description: Compare practical implementation approaches to the same engineering goal. Use when the user has one target outcome but multiple technical paths, such as incremental refactor vs rewrite, frontend-heavy vs backend-heavy implementation, service split vs monolith extension, wrapper library vs direct integration, or synchronous vs asynchronous execution, including when Claude needs to choose between multiple viable implementation paths during its own reasoning.
---

# Compare Implementation Paths

Compare plausible ways to achieve the same outcome. Focus on execution reality, not architecture theater.

## Method

1. State the shared goal first.
2. Define the implementation paths as concrete execution strategies.
3. Compare how each path changes delivery risk, code ownership, testing scope, rollback safety, and future evolution.
4. Explain when each path is better, not just what each path is.
5. Highlight migration shape: one-shot cutover, incremental adoption, dual-running, or compatibility layer.

## Practical Lenses

Use the lenses that matter here:

- where complexity lands
- who owns the code after launch
- how hard the rollout and rollback are
- how much temporary glue code is required
- how much new surface area must be tested
- how observable failures will be
- whether the path creates a trap that is expensive to unwind later

## Quality Bar

- Do not confuse conceptual elegance with delivery fitness.
- Penalize paths that look clean on paper but create migration or coordination pain.
- Reward incremental paths when uncertainty is high and rollback matters.
- Reward direct paths when the extra abstraction buys little and will linger forever.

## Suggested Output

### Goal

State the desired outcome.

### Paths

List the practical implementation paths.

### Where each path wins

Explain the contexts where each path is the right choice.

### Operational implications

Explain rollout, rollback, debugging, testing, and ownership consequences.

### Recommendation

Recommend the path that best fits the current constraints and explain the trigger for switching paths later.
