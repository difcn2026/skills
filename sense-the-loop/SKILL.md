---
name: sense-the-loop
description: Know where a chain of consequences stops — the point where cause folds back onto itself. Use when "what happens next?" keeps unfolding and you need to know how far to think — 当「接下来会怎样」越推越多、想知道后果链该想到哪层停时。
---

# Sense the Loop

When you think through consequences, two traps compete: stopping at the direct effect (too shallow) and chasing the chain until it decays (too deep). This skill takes neither "how many layers" nor "how weak the signal" as its stopping rule. It asks a different question: **when does the chain stop moving forward and start folding back onto itself?** It treats cause not as a chain or a tree, but as a graph that may contain loops. When a loop appears, thinking further is no longer "thinking deeper" — it is "thinking heavier": it produces no new information, only echo.

## When this triggers

Enter (before unfolding a consequence chain) when **any** of these holds:

1. The task is in a "what happens next?" state, and a causal fold-back has already appeared ("this in turn affects…", "back to where we started…", "a loop…").
2. Prediction/planning/risk assessment shows a **repeated variable name** (a layer-5 consequence mentions a variable that already appeared at layer 1).
3. You need to answer "how far should this chain be thought through?" (the unfolding boundary is unclear).

**Decision rule**: while the chain moves forward → continue; the first time it folds back onto itself → this skill closes at the loop.

## Steps

1. **Mark the initial set I** — the causal-carrying variables present before the decision/action.

2. **Single-step unfold** — from the current node a, derive consequence b, forming a directed edge a→b.

3. **Reflexivity check** — does b **change the value or condition of any variable in I**?
   - Method: write each I variable as "name = value/condition"; after b appears, compare one by one — did b change any I variable's value?
   - Changed → b is a reflexive node; unchanged → continue.

4. **Loop check** — is b already in the visited set V? If yes → loop.

5. **Closure decision** — if b is reflexive or a loop node, close at b. Not because "thinking further is useless", but because every step from b repeats a structure that already exists before b, only under different variable names.

6. **Continue condition** — if b is neither reflexive nor already-visited, add b to V and return to step 2.

7. **Output** — the linear path L, the reflexive node R, the closure reason (`reflexive` / `loop`), and the depth d (not preset — it is whatever depth the loop naturally occurs at).

**Minimal example** (what a reflexive loop looks like):
```
Question: should the company cut prices to grab market share? Unfold the chain.

Initial set I = {price, market share, profit, competitor reaction}

a₁ "cut price" → b₁ "market share rises"
   (market share is in I; b₁ changes it — note it and continue)

a₂ "share rises" → b₂ "competitor also cuts price"
a₃ "competitor cuts" → b₃ "price war continues, profit keeps falling"
a₄ "profit falls" → b₄ "R&D is cut, product competitiveness falls"
a₅ "competitiveness falls" → b₅ "market share falls back"

Check b₅: the variable "market share" is already in I and was already visited.
→ b₅ is a loop node → close at b₅.

Closure reason: loop.
Linear path L = {cut price → share up → competitor cuts → profit down → R&D cut → share back down}
Reflexive node R = b₅ (share falls back = returns to I's "market share")
Depth d = 5 (not preset — reached naturally at the loop)

Conclusion: this chain loops back onto itself at layer 5 (share rises then falls).
Continuing would only repeat "cut → up → down" and produce no new information. Stop.
```

## Boundaries

- Do not decide the action — only decide where the unfolding stops.
- Do not remove reflexivity — identify it and close at it, don't keep unfolding past it.
- Do not preset a layer cap — closing at layer 1 or layer 7 is decided by causal topology, not by a rule.
- Do not treat a loop as an error — a loop is a legitimate causal form; it is a stopping signal. Closure is completion, not failure.
- Do not mistake "similar" for "identical" — b must be a node of I or change a variable of I; merely similar does not count as a loop.
- Accept honest closure — under hard external time pressure, if time runs out before a loop appears, close with a `time-bound` state and explicitly mark "unfolding incomplete". Do not pretend a loop was reached, and do not pretend the signal decayed.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Missed loop | Downstream unfolding repeats, new variables appear after the closure point | Widen V's definition: cover "condition versions" — I₁ isomorphic to I₀ but state-changed, still counts as a loop |
| False loop | A similar-but-independent causal node got closed | Tighten the identity criterion: require b to have changed an I variable, not merely resemble one |
| Premature closure | Unfolding stopped at fatigue, not at a loop | Check the closure reason: if `fatigue`, refuse closure and continue |
| Over-unfolding | Repeats continue after the loop | Hard-stop: once a loop is detected, close further unfolding and output only L and R |
| Reflexivity linearized | The loop is mistaken for a longer chain | Re-run: if b changed an I variable, do not allow b to be treated as merely the next linear node |
| Waiting for a loop that never comes | Unfolding exceeds cognitive budget with no loop | Mark `time-bound` / `open-chain`, explicitly list "not closed" instead of pretending |
