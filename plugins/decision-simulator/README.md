# Decision Simulator

Decision Simulator is a Claude Code plugin for better technical judgment.

It helps when Claude is close to a decision that can quietly make the rest of the task better or worse:

- whether a refactor is worth doing at all
- whether a new abstraction is earning its keep
- whether a library solves the real problem or just looks more proper
- whether logic belongs in the frontend, backend, or nowhere new
- whether Claude should keep pushing down the current path or stop and switch approaches

This is not a workflow plugin. It does not try to own planning, testing, or execution. It exists to improve the quality of the choices made inside whatever workflow you already use.

## How It Works

Most weak agent outcomes do not come from obviously bad code. They come from reasonable-sounding decisions made too quickly.

Claude often has the right general instinct, but not enough pressure behind the analysis. It can sound balanced without being decisive. It can list pros and cons without identifying which tradeoff actually matters. It can also drift into expensive, low-reversibility choices because they feel architecturally neat in the moment.

Decision Simulator pushes in the opposite direction.

With it installed, Claude should be more likely to:

- define the real decision before solving the wrong problem
- compare realistic options, including doing less or leaving the code alone
- surface second-order effects like migration cost, ownership confusion, debugging burden, or rule drift
- separate facts from assumptions and name the missing context
- make a recommendation when one path clearly wins
- challenge its own current direction before it overbuilds

The goal is not more analysis. The goal is sharper calls.

## Installation

### Claude Code

Add the marketplace:

```text
/plugin marketplace add echoo19/decision-simulator-marketplace
```

Install the plugin:

```text
/plugin install decision-simulator@decision-simulator-marketplace
```

After that, `decision-simulator` is available in Claude Code like any other installed plugin.

## How To Use It

You can use Decision Simulator in two ways.

### 1. Ask Claude for decision help directly

Use it when you want a recommendation, not just a list of generic tradeoffs.

Example prompts:

- "Should I keep this caching logic in the frontend or move it to the API?"
- "Should we adopt TanStack Query here or is that overkill?"
- "Is this refactor actually worth doing right now?"
- "Compare an incremental refactor versus a rewrite for this auth flow."
- "What information am I missing before I decide to introduce Kafka?"
- "Pressure-test this architecture choice and tell me the strongest case against it."

### 2. Invoke the skill explicitly

If you want to force a focused decision pass, call the skill directly:

```text
/decision-simulator:decision-simulator Should I refactor this service now or leave it alone?
```

That is useful when Claude is already in the middle of a task and you want it to stop, evaluate the choice, and recommend a path before continuing.

## What It Helps With

### Planning

- deciding whether work is local or architectural
- comparing a minimal path against a heavier "proper" path
- identifying missing constraints before a plan hardens around the wrong assumptions

### Implementation

- deciding whether to patch locally or extract shared logic
- deciding whether a new abstraction is actually buying enough
- deciding whether to stay the course or switch approaches mid-task

### Debugging

- comparing containment patches versus root-cause fixes
- weighing time-to-recovery against long-term maintenance cost
- spotting when a "quick fix" is likely to become a recurring incident

### Review And Self-Correction

- surfacing the strongest argument against the current path
- identifying hidden rollout or maintenance costs
- calling out assumptions that should be verified before confidence is high

## What's Inside

### Skills

- `decision-simulator` - flagship skill for high-signal decision analysis
- `evaluate-tradeoffs` - compares options across the dimensions that actually matter
- `detect-context-gaps` - finds missing information and hidden assumptions
- `compare-implementation-paths` - compares practical technical approaches to the same goal

### Agent

- `decision-reviewer` - lightweight read-oriented subagent for deeper decision analysis when Claude needs a stronger recommendation

## Example Output

> **Decision:** Move validation from the frontend into the backend API, while keeping lightweight client-side checks for immediate UX feedback.
>
> **Key tradeoff:** Frontend-only validation is faster to ship, but it duplicates rules, weakens guarantees, and makes inconsistent state harder to debug.
>
> **Hidden cost:** If validation remains split informally, rule drift becomes an ongoing support problem instead of a one-time engineering cost.
>
> **Recommendation:** Centralize authoritative validation in the backend. Keep client checks only for UX. This is slightly slower now, but materially cheaper to maintain.
>
> **Confidence:** Medium-high. The main uncertainty is whether existing integrations depend on undocumented frontend-only behavior.

## Why Use This Alongside Other Plugins

Decision Simulator is a judgment layer, not a process layer.

It works well with planning and execution systems because it does not try to replace them. It improves the quality of the decisions made inside them.

In practice that means:

- better brainstorming because weak options get pressure-tested earlier
- better plans because the decisive tradeoffs are explicit
- better implementation because Claude is less likely to overbuild
- better reviews because counterarguments are surfaced before merge

## Limitations

- It cannot replace missing business context, production data, or team constraints.
- It is only as good as the factual inputs available in the conversation or repository.
- It improves decision analysis, not empirical validation. Some choices still need measurement, experiments, or rollout data.
- It does not execute the decision after the recommendation is made.

## License

MIT License. See `LICENSE` for details.
