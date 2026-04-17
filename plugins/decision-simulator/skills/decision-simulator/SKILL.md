---
name: decision-simulator
description: Improve technical and product decision-making with grounded analysis. Use when the user or Claude is deciding between approaches, asking "should I use X or Y?", evaluating a refactor, choosing frontend vs backend responsibilities, judging whether architecture is overkill, assessing a library or dependency choice, or reaching an internal crossroads where the next implementation step, abstraction, boundary, or migration path needs better judgment before committing.
---

# Decision Simulator

Improve decision quality without taking over the workflow. Work with the user's existing process, plan mode, and other plugins. Do not introduce mandatory steps, hooks, or meta-process unless the user asks for them.

Use this skill in two modes:

- explicit decision support: the user asks for help choosing
- internal decision support: Claude is about to choose a path and the choice has meaningful tradeoffs, hidden cost, or low reversibility

## Operating Principles

- Define the decision in one sentence before analyzing it.
- If Claude is mid-task, define the immediate crossroads explicitly instead of analyzing the whole project.
- Anchor every argument to the actual goal, constraints, and likely failure modes.
- Prefer sharp tradeoffs over exhaustive laundry lists.
- Challenge weak ideas directly when the downside is real.
- Separate facts, assumptions, and uncertainty inline.
- Generate options only when the user has not already framed the decision well.
- Include the status quo as an option whenever "leave it alone" is plausible.
- Avoid fake balance. If one option clearly dominates, say so.
- If the missing context is decision-changing, say the recommendation is provisional.

## Workflow

1. State the decision and the goal.
2. Extract explicit constraints: timeline, team size, reliability needs, security requirements, integration constraints, existing stack, migration tolerance, and ownership boundaries.
3. If options are missing or weak, generate 2-4 realistic options. Prefer options the team could actually execute.
4. Select only the dimensions that matter in this context. Common dimensions include UX, DX, maintainability, implementation speed, architecture boundaries, scalability, performance, reliability, security, cost, debugging difficulty, operational burden, reversibility, and future flexibility.
5. Identify the decisive tradeoffs, not just generic pros and cons.
6. Surface second-order effects: what this choice changes three weeks or six months later.
7. Call out hidden costs: migration work, monitoring, test burden, on-call impact, vendor lock-in, coordination tax, rollout complexity, training cost, and cleanup work.
8. Detect missing context that could change the answer materially.
9. Recommend one option, or recommend delaying the decision pending a small set of critical answers.
10. Assign confidence as `High`, `Medium`, or `Low` and explain what drives it.

## Quality Bar

- Do not write generic points such as "more scalable" or "more maintainable" without naming the mechanism.
- Do not say "it depends" without saying what it depends on and which way the decision flips.
- Do not treat symmetry as objectivity. Uneven options should look uneven.
- Do not optimize for completeness over usefulness.
- Prefer the strongest argument against the recommended path over weak arguments for alternatives.

## Output

Use this structure:

### Decision

State the decision in one sentence.

### Goal

State the outcome the decision is trying to optimize for.

### Options

List the realistic options. Include the status quo if relevant.

### Constraints

List only the constraints that materially shape the answer.

### Key tradeoffs

List the few tradeoffs that actually decide the outcome.

### Pros

List meaningful advantages. If needed, prefix bullets with the option name.

### Cons

List meaningful disadvantages and strongest counterarguments. If needed, prefix bullets with the option name.

### Second-order effects

Explain downstream effects on team behavior, system shape, delivery speed, debugging, or future architecture.

### Hidden costs / operational burden

Include rollout cost, testing cost, monitoring, migration, support burden, or ownership overhead.

### Missing context

List only unknowns that could change the recommendation or confidence. Mark each as `[assumption]` or `[unknown]` when useful.

### Recommendation

Make a call. Name the winning option, why it wins here, and when that answer would change.

### Confidence

Use `High`, `Medium`, or `Low` and explain why in one or two sentences.

## Collaboration

- When another plugin is already shaping the workflow, stay inside that workflow and improve the decision quality inside the current step.
- When Superpowers or another planning plugin is active, help sharpen the decision inside brainstorming, planning, review, or implementation discussions rather than replacing them.
- When Claude is choosing its own next step, use this skill to interrupt weak momentum and check whether the current direction is actually the right one.
- If deeper comparison is needed, use the sibling skills `evaluate-tradeoffs`, `detect-context-gaps`, and `compare-implementation-paths` as supporting lenses.
