# Decision Simulator

Claude Code is often good at writing code and bad at choosing the right path.

It can:

- introduce an abstraction because it feels cleaner
- turn a local fix into a cross-cutting refactor
- choose a library that looks proper but adds long-term drag
- move logic across boundaries without enough payoff
- give you balanced pros and cons when one option is clearly better

`decision-simulator` is a Claude Code plugin for that exact failure mode.

It improves Claude's judgment at decision points:

- when you ask, "Should I do X or Y?"
- when Claude itself reaches a crossroads during planning or implementation
- when a valid solution is not the same thing as the right solution

## Install

Install directly from GitHub through Claude Code:

```text
/plugin marketplace add echoo19/decision-simulator
/plugin install decision-simulator@decision-simulator
```

Or test it locally from the repo root:

```bash
claude --plugin-dir ./plugins/decision-simulator
```

## Why This Is Useful

Most agent mistakes are not syntax mistakes. They are judgment mistakes.

Claude can write code that works and still choose a path that is:

- harder to debug
- harder to roll back
- harder for the team to own
- overbuilt for the real problem
- cheap this hour and expensive next month

This plugin makes Claude more likely to stop and ask:

- Is this refactor actually worth it?
- Is this the right boundary or just a tidy-looking one?
- Should this stay local instead of becoming shared infrastructure?
- Is the next step reversible if we learn we were wrong?
- What hidden cost shows up after merge, rollout, or maintenance?

That is the value. It helps Claude pick the boring-right path more often.

## What Changes With The Plugin

Without a decision-quality layer, Claude often follows momentum:

- first plausible solution wins
- "clean architecture" gets overrated
- local fixes become shared abstractions too early
- tradeoff analysis becomes generic and non-committal

With Decision Simulator active, Claude is pushed to:

- define the actual decision before solving the wrong problem
- compare realistic options, including leaving the code alone
- choose the few dimensions that matter instead of dumping every possible factor
- surface second-order effects like migration burden, rule drift, monitoring cost, and ownership confusion
- state when one option clearly dominates
- say what missing information could still flip the answer
- make a recommendation with confidence instead of hiding behind "it depends"

## Where You Will Feel It

### Planning

Claude gets better at deciding the shape of the work before it starts.

- Should this be a targeted patch or a real refactor?
- Is a new shared module justified yet?
- Is this architecture buying leverage or just complexity?
- Which unknowns matter enough to answer before implementation?

### Implementation

Claude gets better at course-correcting while already in the task.

- Should this logic stay local or move into a shared layer?
- Is the current approach still the best one, now that the codebase context is clearer?
- Is this abstraction paying for itself, or am I about to create cleanup debt?
- Should I keep building on this path or back up and choose a simpler one?

### Debugging

Claude gets better at choosing between a symptom patch and a durable fix.

- Is this a local bug or a boundary problem?
- Is the real fix worth the scope increase right now?
- What is the lowest-risk fix that does not create recurring debt?

### Review And Self-Correction

Claude gets better at challenging its own preferred answer.

- What is the strongest argument against the current path?
- Which assumption is doing too much work?
- What looks elegant right now but will be painful after rollout?

## Concrete Examples

This plugin is meant for decisions like:

- "Should this validation live in the frontend or the backend?"
- "Should I refactor this now or leave it alone?"
- "Should I introduce TanStack Query here or is that overkill?"
- "Should this become a new service or stay in the monolith?"
- "Should I patch the bug locally or move the logic into a shared module?"
- "What am I missing before I commit to this architecture?"
- "Before you keep going, check whether this abstraction is actually worth introducing."

## What It Actually Improves In Claude Code

This is not a workflow takeover plugin.

It does not try to become your planner, reviewer, or orchestrator. It acts as a judgment layer inside the workflow you already use.

That means it works well for:

- casual Claude Code users who just want better answers to technical tradeoff questions
- people using Claude interactively while coding and debugging
- agentic workflows where Claude needs to decide its own next move
- structured setups like Superpowers, where it can improve the quality of decisions made inside brainstorming, planning, implementation, and review

In practice:

- a planning plugin can structure the work
- Decision Simulator can improve the choices made inside that structure

## Included In The Plugin

The plugin ships with:

- `decision-simulator`
  The flagship skill for high-signal decision analysis
- `evaluate-tradeoffs`
  Compares options across the dimensions that actually matter
- `detect-context-gaps`
  Finds the missing information that could flip the answer
- `compare-implementation-paths`
  Compares practical technical approaches to the same goal
- `decision-reviewer`
  A lightweight subagent for deeper decision analysis when Claude needs a stronger recommendation

## Quick Example

Instead of:

> Both approaches have tradeoffs. Backend validation is more secure, but frontend validation is faster and simpler. It depends on your needs.

The plugin pushes Claude toward something closer to:

> Keep lightweight client checks for UX, but move authoritative validation to the backend. Frontend-only validation is faster this week, but it duplicates rules, weakens guarantees, and creates debugging drift once multiple clients exist. The real cost is not the validation logic itself; it is rule divergence over time.

That is the difference: less generic balance, more usable judgment.

## Local Usage

From the repository root:

```bash
claude --plugin-dir ./plugins/decision-simulator
```

Then inside Claude Code:

```text
/reload-plugins
/decision-simulator:decision-simulator Should I split this service now or wait?
```

## Repository Structure

```text
decision-simulator/
  .claude-plugin/
    marketplace.json
  plugins/
    decision-simulator/
      .claude-plugin/
        plugin.json
      skills/
        decision-simulator/
          SKILL.md
        evaluate-tradeoffs/
          SKILL.md
        detect-context-gaps/
          SKILL.md
        compare-implementation-paths/
          SKILL.md
      agents/
        decision-reviewer.md
      README.md
  README.md
  .gitignore
  LICENSE
```

## Validation

```bash
claude plugin validate ./.claude-plugin/marketplace.json
claude plugin validate ./plugins/decision-simulator
```

## Limitations

- It improves judgment, not factual access. Missing business context or production data can still change the answer.
- It does not replace measurement, experiments, or rollout evidence.
- It does not manage execution after the decision is made.

## If You Like This

Use it on a real decision point, not a toy prompt.

The best tests are places where Claude is tempted to overbuild:

- a refactor you are not sure is worth it
- a shared abstraction that might be premature
- a library decision with hidden long-term cost
- a patch-vs-rewrite-vs-boundary-change call

If it saves you from one expensive wrong turn, it has already paid for itself.
