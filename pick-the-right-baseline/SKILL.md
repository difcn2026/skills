---
name: pick-the-right-baseline
description: Re-select the right reference class before judging an individual case, so vivid detail stops distorting the base rate. Use when a specific case feels typical yet is statistically rare, or when intuition and the base rate pull against each other.
---

# Pick the Right Baseline

When judging an individual case, two errors compete: judging only by the base rate (ignoring the case's specifics) and judging only by the vivid impression (ignoring the base rate). This skill splits the two apart. It keeps base-rate probability at the object level and moves case features to a meta-level: similarity does not directly change the probability — it only re-selects the reference class. Then only diagnostic features may calibrate the probability within the new class; vivid, non-diagnostic features are marked as noise.

## When this triggers

Enter when **any** of these holds:

1. A case feels typical yet is statistically rare ("he looks exactly like X, but X itself is rare").
2. Vivid case detail and the base rate pull against each other ("the detail is vivid" vs "statistically almost impossible").
3. The judge reports only a base rate with no case features (base-rate-only), or only an impression with no base rate (impression-only).

**Decision rule**: if the case clearly belongs to one reference class and its features only calibrate within that class → judge directly, this skill is not needed. If case features and the base rate fight, and reference-class selection is at stake → use this skill.

## The two levels

- **Object level**: candidate reference classes and their base-rate probabilities.
- **Meta level**: case features, vividness, similarity cues.

The two levels must never be multiplied, summed, or merged directly.

## Steps

1. **Separate the levels** — object level and meta level, never combined directly.

2. **Enumerate reference classes** — at least 3 applicable classes, each with a base rate. Fewer than 3 → mark "reference class too narrow", do not synthesize.

3. **Score diagnostic similarity** (operational):
   - **Diagnostic similarity**: based only on features explicitly named in a reference class's definition. Method: count "case features ∩ class definition features", divided by "class definition features total".
   - **Non-diagnostic vividness**: narrative detail, emotional punch, ease of imagining — must **not** enter the next step.

   **Minimal example**:
   ```
   Case: a 40-year-old man, chest pain, 20-year smoker, father died of a heart attack at 50.
   (vivid details: just watched a game, agitated, pale — these are non-diagnostic vividness)

   Candidate reference classes (enumerate ≥3):
   R1 average 40-year-old man (base heart-attack rate 2%)
   R2 40-year-old smoking man (base rate 8%)
   R3 40-year-old smoker with early family history (base rate 20%)

   Diagnostic similarity (match against each class's definition features):
   - vs R1: definition = male, 40 → 2/2 = 1.0
   - vs R2: definition = male, 40, smoker → 3/3 = 1.0
   - vs R3: definition = male, 40, smoker, family history → 4/4 = 1.0
   ("agitated / pale" appear in no class definition → non-diagnostic, dropped)
   ```

4. **Re-select the reference class** — use diagnostic similarity to choose or weight-switch the baseline class among candidates. Output an explicit switching reason. **Never use similarity to directly change the chosen class's base rate.**
   In the example: all three classes score 1.0, but R3's definition is the most specific (adds family history), so switch to R3 — baseline moves from 2% to 20%, with the explicit reason "the case carries R3's unique feature (early family history)".

5. **Calibrate within the baseline** — on the newly selected baseline, only diagnostic features may adjust the probability, bounded by the reference class's internal prior uncertainty (**±50% relative band**: a 20% baseline allows only 10%–30%):
   - Exceeding the band → either the class is wrong or a non-diagnostic feature slipped in; return to step 3.
   - Non-diagnostic vividness must not enter the probability term.
   In the example: R3 baseline 20%; a diagnostic feature (chest pain, if in R3's definition) may nudge up, capped at 30%; "pale/agitated" may not enter.

6. **Structured output** — which class was selected/switched, old vs new baseline, calibrated probability, category judgment, confidence bound, and the features marked as noise.

## Boundaries

- Similarity must never override the base-rate probability directly (representativeness failure).
- Never output a single baseline with no class selection/switch (base-rate failure).
- Not for fully novel cases with no applicable reference class → hand to a human.
- Does not replace high-stakes domain-expert decision; the output is a judgment structure, not a final order.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Similarity leaks across and changes probability | Output probability deviates from baseline beyond the ±50% band | Force return to the new baseline, drop the leaked similarity |
| Base-rate-only or impression-only | No switching reason output, or no diagnostic features used | Block output, re-run the separation |
| Wrong reference class switch | Post-switch calibration scores below the default class | Fall back to the default class, mark "switch failed" |
| Vividness contamination | Non-diagnostic feature appears in the probability term | Delete the feature, downgrade it to noise |
| Reference class too narrow | Fewer than 3 applicable classes | Refuse synthesis, require more candidate classes |
