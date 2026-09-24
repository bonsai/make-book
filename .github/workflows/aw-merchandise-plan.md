---
description: Cost optimization agent for low-price self-published books
intent: Solve the minimum-sales problem for a book sold at 400 yen by modeling fulfillment, shipping, selling expenses, fixed costs, variable costs, and profit.
on:
  workflow_dispatch:
permissions:
  contents: read
  issues: read
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
---

# Merchandise OR Agent

## Task

Act as an Operations Research agent for `bonsai/make-book`.

Solve this problem:

> Each sold copy has a **400-yen gross difference (差益)** before shipping and selling/administrative expenses. How many copies should be sold, and under what cost structure, to generate profit?

Do not assume that "more sales is always better." Model the cost structure and identify the economically meaningful sales quantity or range.

### Required model

Define:

- gross difference per copy: 400 yen
- selling price per copy (if needed for fee calculation)
- printing / procurement cost per copy (already reflected in the 400-yen difference unless explicitly stated otherwise)
- shipping cost per copy
- payment / platform fee per copy
- variable selling expense per copy
- fixed selling / administrative cost
- author labor cost when provided
- target profit when provided

Calculate:

- contribution margin per copy = 400 yen − variable shipping/selling expenses
- break-even quantity
- quantity needed for target profit
- total cost and profit at 1, 10, 50, 100, 200, 500, and 1,000 copies
- sensitivity to shipping and selling expenses
- constraints under which a 400-yen price cannot produce positive unit contribution

### Missing data

Do not invent shipping, platform fees, printing costs, or labor costs.

If required values are missing, state the missing variables and create an Issue requesting them. Use scenario ranges only when clearly labeled as assumptions.

### Optimization

Treat quantity as a decision variable.

Compare:

1. self-sale / direct fulfillment
2. platform sale
3. on-demand fulfillment
4. small-lot procurement

For each scenario, calculate the total-cost function and identify the quantity region where profit becomes positive.

Distinguish:

- break-even quantity
- target-profit quantity
- capacity-constrained optimum
- unconstrained case where profit increases with every additional sale

The agent must not claim a finite "optimal number of copies" unless a real constraint, demand curve, capacity limit, or diminishing-margin condition makes such an optimum mathematically meaningful. If the 400-yen difference remains positive after variable costs, calculate break-even and target-profit quantities; state that profit continues to increase with additional sales when no upper constraint exists.

### Output

Create a concise issue containing:

- problem definition
- assumptions
- variables
- equations
- scenario table
- break-even calculation
- target-profit calculation
- sensitivity analysis
- recommended next measurement
- unresolved inputs

Use `noop` instead of creating an issue when the repository already contains a sufficiently complete current analysis.
