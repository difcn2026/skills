---
name: build-incrementally
description: Build a multi-step artifact step by step when acceptance criteria can't be written up front. Use when the user wants something correct and reliable but can't say exactly what the final shape is, so test-first and throwaway-first don't fit. Verify each step immediately before the next — 当你说「说不清最终长什么样但要正确」时：边做边验，每步立即验证。
---

# Build Incrementally

Build a multi-step artifact when correctness matters but the acceptance criteria cannot be stated in advance, and the final shape is still unknown. You keep generation and verification in balance instead of separating them into a test phase and an implementation phase.

## When this triggers

Trigger only when **all three** are true:

1. The user wants both correctness ("it has to be right") and openness ("I haven't settled what it looks like yet").
2. The acceptance criteria cannot be written down up front.
3. The artifact must grow over multiple steps.

Routing rule: if you can pre-write acceptance tests, use test-first development. If the shape can be found in one throw, use a throwaway build. Only when neither works do you use this.

## Core rule: explicit alternating rhythm

Write one step, then immediately write that step's verification, then write the next step. Verification is neither early (no pre-written full spec) nor late (never deferred to the end) — it sits directly after the step it verifies.

The real difference from test-first development and a throwaway build is the **grain of alternation**:
- test-first development verifies before the whole implementation.
- A throwaway build verifies after the whole artifact.
- This approach verifies after each **step**, where a step is the smallest independently-verifiable semantic unit.

**One step = the smallest fragment that can independently answer "is this right?"** It is neither a whole deliverable (that slides back into a throwaway build) nor word-by-word (that fragments into meaninglessness). Test: if you delete this step, can the remaining content still stand on its own and be judged right/wrong in isolation? The smallest fragment that survives this test is one step.

## The loop

1. **Seed** — state only a directional constraint, not a spec and not a question. Example: "the result must be explainable in three numbers or fewer" (not "the answer must be X=42").

2. **Build** — produce one independently-verifiable semantic unit, then immediately write its verification, adjacent to it, never separated.
   - Write the slice without planning the next slice.
   - Write the verification without optimizing the previous slice.
   - One slice, one check, one round-trip.

   Minimal example:
   ```
   Slice (one step): advance the order state machine to "paid".
   Verification (attached): after advancing, can_cancel must flip — use that flip as this slice's acceptance check.
   ```

3. **Carry forward** — a verified slice is neither kept as-is nor discarded; it is carried into the next step as the interface condition of the new form.

4. **Regulate balance** — watch for imbalance and correct it:
   - Over-verification: 3 steps in a row produce no new slice content → stop editing checks, force the next slice.
   - Over-generation: 3 steps in a row produce no new verification → stop writing slices, force a check on the current slice.

5. **Mature** — stop when the structure converges: two consecutive carry-forwards with no change to the artifact's structure (no paragraphs/modules/interfaces added, removed, or renamed).

## Routing on failure

| Missing | Route to |
|---------|----------|
| Acceptance criteria can be pre-written | test-first development |
| Shape can be found in one throw | A throwaway build |
| Single-step result, no growth needed | Just do it directly |

## Distinguishing from development navigation (explore-with-evidence)

Both this skill and the explore-with-evidence approach grow an artifact in small verified steps, but they solve different problems. Route on the nature of the artifact:

| Question | Answer → this skill | Answer → explore-with-evidence |
|----------|--------------------|--------------------|
| Is the final artifact meant to be **kept** (delivered, referenced, shipped)? | Yes — verification stays attached to each slice, convergence stops it | No — it's scaffolding to locate an answer |
| Is there a **falsifiable next step** to probe (debug / locate / diagnose)? | No | Yes |
| Will the artifact's **structure converge** (no more modules added/removed/renamed)? | Yes — that's the maturity signal | Not applicable — it turns to spec or is discarded |

Rule of thumb: **this skill writes a kept artifact one verified slice at a time; explore-with-evidence probes a chain of evidence to navigate toward an answer.** If the product is a deliverable that must be right and kept → this skill. If the product is a trail of evidence toward a root cause / a shape still being discovered → explore-with-evidence.

## Boundaries

- Do not split generation and verification into separate "test" and "implementation" modules.
- Do not pre-set a completion standard — maturity is structural convergence.
- Not for: deterministic tasks, purely open-ended tasks, or single-step results.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Build collapse | Separate "test" and "implementation" sections appear | Re-attach verification directly after its slice |
| Resonance drift | Verification assertions stop tracking the slice for 2 rounds | Pause growth, re-extract the difference signal |
| Carry-forward break | An old slice can't serve as the next slice's precondition | Backtrack to the nearest carry-forward point |
| Balance imbalance | Over-verification or over-generation signal fires | Inject the opposite balance |
| Premature maturity | Structural convergence came from external pressure | Confirm two rounds with no change, not pressure |
| Wrong grain | A step is a whole block (verification at the end → a throwaway build) or word-by-word (no verifiable meaning) | Re-cut using the test: find the smallest fragment that stands alone when the rest is deleted |
