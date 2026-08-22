---
name: negotiate-the-constraints
description: Resolve a conflict between goals and hard constraints by negotiating at the constraint layer, not by watering down the solution. Use when you face "I want A and B but…" with hard limits — 当你既要 A 又要 B 但有硬限制、不想把解打折时。
---

# Negotiate the Constraints

When a problem has multiple goals and hard limits, two usual moves fail: picking a point on the Pareto frontier (ignoring structural conflict) and finding any feasible solution (ignoring the goals). This skill redefines "solution" as **feasible frontier + unsatisfiable-core diagnosis**. It first separates constraints into three layers (hard / negotiable boundary / soft goal), then builds a frontier for the soft goals inside the hard region; when the hard constraints themselves conflict, it does not return "no solution" — it outputs the minimal unsatisfiable core and a constraint-reclassification proposal. **It moves compromise from the solution space to the constraint layer.**

## When this triggers

Enter when **any** of these holds:

1. The input has ≥2 quantifiable goals and ≥1 hard constraint (check: two "maximize/minimize" goals + one "must/cannot/red-line" constraint).
2. The statement contains a "want A and B but…" structure.
3. Optimization has hit a constraint boundary, or the feasible region is empty ("no solution" already returned).

**Decision rule**: goals with no constraints, or constraints with no goals → degenerate problem, this skill is not needed. Both present and in conflict → use this skill.

## Steps

### 1. Separate the constraints (three tests)

Split by non-negotiability. **The tests (not a feeling)**:

| Layer | Test | Pass condition |
|-------|------|----------------|
| `H` hard | Violating it causes **irreversible harm** (safety / legal / physical / ethical red line)? | yes → H |
| `N` negotiable boundary | Default-fixed, but reclassifiable when the H layer conflicts? | yes → N |
| `S` soft goal | Quantifiable, discountable, enters the frontier ("as good as possible", not "must")? | yes → S |

**The test question**: relax this constraint by 10% — does irreversible harm follow? Yes → H; no but needs renegotiation → N; it should just be optimized anyway → S.

**Minimal example**:
```
Problem: self-driving "safety vs performance".
Constraints/goals → layers:

- "collision fatality rate must be below human drivers" → relaxing 10% causes irreversible harm (deaths) → H
- "response latency ≤ 200ms" → relaxing 10% (220ms) isn't fatal but needs negotiation → N
- "top speed as high as possible" → quantifiable, discountable → S
- "ride comfort as high as possible" → quantifiable, discountable → S
- "cost per mile as low as possible" → quantifiable, discountable → S
```

**H-layer hard rule (mandatory mechanism statement)**: every `H` constraint must state the **mechanism** of its irreversible harm — the specific physical law, regulation, or safety standard it violates — not a consequence description:
- Acceptable: "violates GDPR Article 32 (security of processing)".
- Not acceptable: "would cause a data-leak problem" (a consequence, not a mechanism).
- A constraint that cannot state a mechanism → **auto-downgrade to `N`**, it may not stay in H.
Why: the essence of inflating a commercial line into a "safety line" is reasoning backwards from consequence to mechanism. Requiring the specific statute/law/standard blocks the fabricated line at the first step. A commercial decision ("must use our own chip") cannot state a safety-mechanism clause → auto-downgrades to N.

### 2. Structural diagnosis: H-layer unsatisfiable-core check
Run conflict detection on the H layer alone. Non-empty feasible region → step 3. Empty → step 5.

### 3. Build the feasible frontier
Inside the H layer's feasible region, optimize the S layer — producing a frontier clipped by the hard constraints (neither unconstrained optimum nor pure feasible set).

### 4. Monitor boundary events
When the optimization path touches an H boundary, record "which soft goal hit which hard constraint" — these are negotiation inputs marking which constraints are the active limits.

### 5. Output the minimal unsatisfiable core
If the H layer's feasible region is empty, compute the minimal unsatisfiable core (smallest conflicting subset of non-negotiable constraints) and output:
- The conflicting H subset.
- Each conflicting constraint's **reclassification feasibility rating** (honest three-level):
  - `high`: the constraint is a policy/organizational choice, not a physical/legal/safety hard line (e.g. "must use our own chip" is actually a business decision).
  - `medium`: a technical alternative exists to bypass it (e.g. "latency ≤200ms" can be bypassed with edge computing).
  - `low`: the constraint is a physical/legal/safety hard line with no alternative (e.g. "collision fatality rate").
- If all conflicting H's are un-reclassifiable → return `infeasible-core` and stop; do not fabricate a pseudo-solution.

**Minimal example** (unsatisfiable core):
```
H-layer conflict: "zero emissions" (environmental hard line) ∧ "range 1000km" (if also judged H) ∧ "cost ≤ X" (financial, if H).
→ currently unsatisfiable together.

Minimal unsatisfiable core = {zero emissions, range 1000km} (cost only amplifies).
Reclassification ratings:
- "range 1000km": technical alternative (battery tech / range extender) → medium, downgradable to N
- "zero emissions": environmental regulation hard line → low, not reclassifiable
→ Proposal: downgrade "range 1000km" from H to N to open the feasible region.
```

### 6. Generate the negotiation protocol
Merge boundary events (step 4) and the unsatisfiable core (step 5) into reclassification proposals (which N to promote to H, which H to demote to N). All reclassification needs human confirmation. Compromise moves from solution-space discounting to constraint-layer renegotiation.

## Boundaries

- Do not auto-reclassify any `H` constraint — propose only, never decide.
- Do not return an "approximate solution" or "softened hard constraint" when the H layer is empty.
- Do not ignore the S layer — a feasible solution is not the endpoint; optimize within it.
- Do not handle goal-less or constraint-less degenerate problems.
- Do not treat `N` as default-negotiable — `N` is a bargaining chip, not a soft goal.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| H empty and all H un-reclassifiable | Core check finds no downgradable item | Return `infeasible-core`, stop, no pseudo-solution |
| Feasible frontier collapses to a point | Feasible region too small, frontier goals < 2 | Prompt to adjust N boundaries or re-examine H scope |
| Too many boundary events | Optimization keeps touching H | Pause, output the event list, propose reclassification negotiation |
| Reclassification rejected | Human confirmation refused | Fall back to the original H/N/S split, keep the frontier or core |
| Soft goal misjudged as hard | User says a constraint shouldn't be H | Record the misjudgment, adjust the split heuristic (not auto-fixed this run) |
| Frontier coincides with unconstrained Pareto | H layer has no clipping effect | Prompt that a real hard constraint may be missing, avoid slipping into plain multi-objective optimization |
