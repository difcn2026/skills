---
name: find-the-real-cause
description: Find which step actually changed the outcome by contrasting the real outcome with near-miss alternatives. Use when a retrospective insists "it was inevitable" or "if only…", and you need to locate the true leverage point.
---

# Find the Real Cause

After something goes wrong, two traps await: "I knew it all along" (hindsight) and "if only that one step had been different" (unanchored speculation). This skill takes a third path. It does not explain why the outcome was inevitable, and it does not fantasize about what could have been. It treats the actual outcome as a contrast agent: it generates near-miss alternative outcomes, runs them down the same causal path, and uses their differences to light up which node actually moved the outcome — while dismantling the illusion that the outcome had to happen.

## When this triggers

Enter when **any** of these signals appears:

1. Text contains inevitability markers: "I knew it", "it was bound to happen", "the only choice", "obvious in hindsight".
2. Text contains unanchored what-if markers: "if only we had…", "if that step had been different".
3. The same outcome has 2+ conflicting attributions (different people tell the same story with different "key causes").
4. You need to locate "which step truly changed the outcome" but cannot run an experiment.

**Decision rule**: if you can run an experiment, run it — this skill is not needed. If you only have a narrative and it carries inevitability or what-if markers, use this skill.

## The three phases

1. **Break inevitability** — generate alternative outcomes to break the "single path" illusion.
2. **Light up the differences** — multiple outcomes illuminate path nodes, revealing outcome sensitivity.
3. **Locate the leverage point** — from sensitivity differences, find the branch point and discard narrative pseudo-causes.

## Phase 1 — Specimen and alternatives

1. Anchor the actual outcome E₀ — record "what is known, what happened". Do not explain.
2. Expose the narrative — record the user's inevitability narrative in full. Do not argue.
3. Generate alternatives E₁, E₂, E₃ — each satisfies a "minimal intervention" constraint: shares ≥70% of the causal path with E₀, differing only at one branch point. At least 3. If you cannot generate 3 such alternatives, mark the specimen unfit.

**Minimal example** (what an alternative looks like):
```
E₀ (actual): the project slipped, because requirements froze in week 3.
Narrative: "unclear requirements make slippage inevitable — nobody could avoid it."

Alternatives (minimal intervention, differing only at the "requirements-freeze timing" branch):
E₁: requirements froze in week 2 → slippage compressed to 1 week.
E₂: requirements froze in week 3, but devs built interfaces in parallel → slippage offset.
E₃: requirements froze in week 4, but one low-priority module was cut → same slippage, smaller scope.
(E₁/E₂/E₃ share ≥70% of the path with E₀ — team, stack, and scope are unchanged.)
```

## Phase 2 — Illuminate the differences

4. **Rebuild the common path P** (operational):
   - List every node that appears in E₀ **and** all alternatives (team, stack, scope, requirements, development, testing, release…).
   - Drop nodes that appear only in E₀ or only in one alternative.
   - What remains is the common path P — taken from the intersection of the four outcomes, not copied from the narrative.

5. Measure node sensitivity — what value does each node take in E₀, E₁, E₂, E₃? Does the outcome change when the node changes?

6. **Difference weighting** (honest three-level, not fake precision):
   - `high`: the node takes different values in ≥2 outcomes, and the outcome changes with it.
   - `medium`: the node differs in ≥2 outcomes, but the outcome shifts only slightly.
   - `low`: the node is the same across all outcomes (an accompaniment), or it changes but the outcome does not.
   - The basis is a node-value vs outcome-change pairing table, not a feeling.

## Phase 3 — Image and locate

7. Draw the causal image — a path profile with each node marked high/medium/low. High-sensitivity nodes = branch points (key-cause candidates); low-sensitivity nodes with narrative weight = narrative pseudo-causes.

8. Rule on inevitability — if E₀ were truly "the only possible outcome", the alternatives should be unimaginable or wildly unstable. In fact they are imaginable and share 70% of the path, so "inevitable" is downgraded to "accidentally realized".

9. Locate the intervention point — sort branch points by sensitivity and mark "the next move belongs here".

## High-sensitivity claims must be falsifiable

**Every node marked `high` must carry a falsifiable counterfactual test sentence** (form: "if this node took the opposite value, the outcome should become ____ — this is a prediction to test, not an assertion"):
- Can you write a specific "opposite value → outcome change" sentence? → keep it `high`.
- Cannot (you can only repeat "it's high because it matters")? → downgrade to `medium`.

Why: the typical symptom of motivated reasoning is an unfalsifiable assertion — you can assert "requirements were the root cause" but cannot say "what happens if requirements don't change". Requiring a falsifiable test sentence exposes the pseudo-high.

## Boundaries

- Do not predict; alternatives are cognitive instruments, not futures the skill can realize.
- Do not remove uncertainty; "this node is sensitive" ≠ "changing it will definitely change the outcome".
- Do not give a single root cause; a key cause is a branch point, structural and pairing-dependent, not a hero cause.
- Do not replace experiment; when experiment is possible, use experiment.
- Do not chase exhaustive alternatives; take only 3–5 minimal-intervention ones.
- Safety boundary: the untrusted input is the user's self-consistency motive — pretending to run the skill while defending the narrative. Phase 1 forces the narrative out; Phase 3 forces the inevitability ruling. If the user refuses to generate alternatives, block execution.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Slips into hindsight | Narrative treated as "the only correct" story, alternatives refused | Block: "you are treating the realized outcome as the only imaginable one." Still refusing → mark specimen unfit |
| Slips into unanchored fantasy | Alternatives share <30% of path with E₀ | Reject the alternative; require the branch point within the last 70% of the path |
| Cause still hindsight-picked | All key causes come from the original narrative, no node marked pseudo-cause | Re-run phases 2–3; force at least one narrative cause through other-outcome testing |
| Pseudo-cause slips in | Node unchanged in most outcomes yet marked a branch point | Remove it, mark "accompaniment" |
| Too few alternatives | Only 1 alternative generated | Add more; difference-illumination needs ≥2 alternatives (3 outcomes total) |
| Sensitivity uncomputable | Nodes identical or fully divergent across outcomes | Return to step 4, rebuild the common path |
