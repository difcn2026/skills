---
name: update-your-belief
description: Measure how much you should have updated your belief versus how much you actually did, and close the gap step by step. Use when strong new evidence arrives but a belief barely moves.
---

# Update Your Belief

When new evidence arrives, there is a gap between how much you *should* update (what the math says) and how much you *actually* update (what the old belief drags you back to). This skill makes that gap the primary object: measurable, taxable, and calibratable. It does not recite a formula, and it does not just say "don't be anchored". It computes the should-have posterior, elicits the actual posterior, measures the gap, and gives a resistance-aware path to close it.

## When this triggers

- New evidence arrives and a key judgment should update.
- Strong evidence appears but you (or someone) "barely moved".
- A decision needs an old belief calibrated.
- A wrong judgment is being reviewed, and it turns out the failure was not ignorance but slow updating.
- The user says "am I anchored?".

## The core loop

1. **Surface the prior** — elicit three priors at once:
   - `p0_declared`: the stated prior probability.
   - `p0_functional`: the action prior — "what minimum odds would you bet on this, if no new evidence existed?" Convert to probability.
   - `anchor_shadow`: the anchor shadow — "if this evidence completely failed, what old belief would you most comfortably fall back to?"
   - If the three differ by > 0.15, the prior itself is already anchored; record `prior_anchored`.

2. **Compute the should-have posterior** — given likelihood ratio `L = P(E|H) / P(E|¬H)`:
   ```
   p* = p0_functional * L / (p0_functional * L + 1 - p0_functional)
   ```
   If `L` is not precisely obtainable, replace it with an interval `[L_low, L_high]`, yielding a posterior band. This step only answers: where should a rational update land?

3. **Elicit the actual posterior** — through three channels, to avoid relying on a single easily-anchored self-report:
   - `p_verbal`: "what probability would you say now?"
   - `p_action`: "at what minimum odds would you bet on it now?"
   - `p_resource`: "how much reversible resource would you commit if this belief were true?"
   - Take `p_actual = min(p_verbal, p_action, p_resource)` — anchoring usually depresses action, not inflates it. If the three differ by > 0.2, mark `elicitation_discordant` and use the action threshold as the primary measure.

4. **Compute the gap and the anchor tax** — with `p0 = p0_functional`:
   ```
   Δ*       = p* - p0
   Δ_actual = p_actual - p0
   ```
   - If `|Δ*| < 0.05`: evidence too weak, skip the tax, mark `evidence_too_weak`.
   - If `Δ_actual` and `Δ*` point the same way:
     ```
     α = Δ_actual / Δ*
     τ = 1 - α
     ```
     `τ` is the **anchor tax** — the fraction of the should-have update that anchoring rubbed away. `α` is the **update sufficiency** — the fraction of the should-have distance actually traveled.
   - If `Δ_actual` points the other way, or `α < 0`: mark `anchor_lock` (not under-adjusting — locked).
   - If `α > 1.2`: mark `overshoot` (not dragged by the old anchor — yanked by the new evidence's emotional anchor).
   - Output the core triple `(p*, p_actual, τ)`.

5. **Resistance profile** — score five resistance sources 0–1: identity binding, public commitment, sunk cost, threat sensitivity, switching cost. Average < 0.3 = low; 0.3–0.6 = medium; > 0.6 = high.

6. **Calibration strategy** — by resistance and `α`:
   - **low**: adopt `p*` directly; write a one-line pre-commitment ("if I'm still below p* in 24h, mark me recalcitrant").
   - **medium**: use an update staircase — every 24h move one third of the remaining gap from `p_actual` toward `p*`; record `α` each step.
   - **high**: don't force the belief; rewrite action weights so the old belief leaves the key decision function; set a reversal-evidence threshold; mark `strong_anchor`.
   - **anchor_lock**: don't calibrate directly; first unbind identity or lower threat sensitivity, then return to step 1; two consecutive locks → `frozen`, hand to an outside view.
   - **overshoot**: pause; check whether the new evidence carries high emotional weight, recency, or social pressure; pull `p_actual` back toward `p*`.

7. **Log and re-review** — record the update; re-review defaults to 24h later; if `α` has not risen and resistance has not fallen, the strategy failed, enter the counter.

## Walkthrough example

**Scenario**: an engineer strongly believed "refactoring now will slow delivery". New evidence: a comparable team sped up delivery 40% after refactoring.

**Step 1** — surface the prior:
- `p0_declared = 0.75`, `p0_functional = 0.8`, `anchor_shadow = 0.7` → spread 0.1 < 0.15, prior not locked. `p0 = 0.8`.

**Step 2** — should-have posterior, take `L = 5`:
```
p* = 0.8 × 5 / (0.8 × 5 + 0.2) = 4.0 / 4.2 = 0.952
```
Rational update: "will slow delivery" should fall from 0.8 to 0.048.

**Step 3** — actual posterior:
- `p_verbal = 0.6`, `p_action = 0.55`, `p_resource = 0.5` → spread 0.1 < 0.2, consistent. `p_actual = 0.5`.

**Step 4** — gap and tax:
```
Δ*       = 0.048 - 0.8 = -0.752
Δ_actual = 0.5 - 0.8   = -0.3
α = (-0.3)/(-0.752) = 0.40
τ = 0.60
```
**Anchor tax τ = 60%** — the math said update by 0.752, but anchoring rubbed away 60%, and only 40% actually happened.

**Step 5** — resistance: identity 0.7, public commitment 0.6, sunk cost 0.3, threat 0.5, switching 0.4 → average 0.5 → **medium**.

**Step 6** — medium resistance → update staircase:
- Day1: 0.5 → 0.5 + (0.048 − 0.5)/3 ≈ 0.35
- Day2: 0.35 → 0.35 + (0.048 − 0.35)/3 ≈ 0.25
- Day3: … → approaching 0.048, recording α each step.

**Step 7** — log: `{p0: 0.8, L: 5, p_star: 0.048, p_actual: 0.5, alpha: 0.40, tau: 0.60, resistance: medium, strategy: staircase_3day, next_review: 24h}`.

The skill never says "you should update" (empty advice). It computes that **you owe 60% of an update you haven't paid**, and hands back a resistance-aware staircase.

## Boundaries

- Only handle beliefs that are quantifiable or at least ordinally comparable; unquantifiable values are `uncalibratable`.
- Do not replace the domain model or evidence-quality assessment; only calibrate the update magnitude for the given evidence.
- Do not do therapy; resistance analysis is decision-relevant only.
- Do not change the user's external behavior automatically; pre-commitments and action-weight rewrites need user confirmation.
- High-stakes beliefs (medical, legal, major financial) are marked `needs_domain_review` before use.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Belief elicitation distorted | Three channels differ > 0.2 | Use the action threshold as primary, ignore the verbal |
| Likelihood ratio unobtainable | Cannot give L or interval | Use equivalent-evidence-volume method: weak/moderate/strong |
| Update direction reversed | α < 0 or p_actual moves away from p* | Mark `anchor_lock`, switch to high-resistance strategy |
| User refuses a prior | p0 missing | Use default prior set {0.2, 0.5, 0.8}, output a posterior band |
| Over-update | α > 1.2 | Reverse-calibrate, check the new evidence's emotional anchor |
| Strategy ineffective | α not risen after 24h | Downgrade from staircase to action-weight rewrite |
