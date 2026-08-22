---
name: keep-it-precise
description: Distill source content to the smallest core that must stay unchanged, when the result must stay recognizable and precise. Use when you need both brevity and a distinct signature, and later edits must not corrupt key details like numbers, negations, or unique terms — 当你要简短又不能丢数字/否定词/专有名词时。
---

# Keep It Precise

Extract the minimal set of units that must pass through a source unchanged, when the source must stay recognizable across outputs and its precision is sensitive. The goal is a distinctive, minimal passage — the "precision core" — that carries what cannot be lost and drops what can.

## When this triggers

Trigger only when **all three** are true:

1. The source has real value and needs a high signal that stays consistent across outputs.
2. It must not be misidentified (a signature is needed), without significantly raising token/material cost.
3. Post-hoc decoration would corrupt the content's precision.

Routing: efficiency only → compress (radical compression). Distinctiveness only → visual design. Both AND precision-sensitive → this.

## Step 0: Object definition (mandatory, before anything)

Before any unit scoring, write down the object definition:

```
"The receiver of this source's output must be able to correctly say: this is ______ (one sentence)."
```

The object definition is the single anchor for all scoring. If most units come out +1 (nothing can be dropped), the object definition is too broad — narrow it.

## Precision score (PS) scoring — anchored to the object definition

**PS(unit) = if this unit is deleted, would the receiver change their judgment of the object-definition sentence?**

| Score | Criterion | Handling |
|-------|-----------|-----------|
| +1 (keep) | Deleting it makes the receiver get the object definition wrong | Must pass through |
| 0 (margin) | Deleting it leaves the object definition unchanged, but reads better | Route to the margin (footnote/appendix) |
| -1 (drop) | Deleting it leaves the object definition unchanged and reads simpler | Fold/delete |

Calibration: take 5–10 similar sources as a reference set, mark the units where "deleting it would make the receiver get the object definition wrong", and derive the PS threshold. Then apply the threshold mechanically to later sources of the same type.

**Position does not change protection.** A unit containing transmission-core content keeps its core verbatim even if PS=0 routes it to the margin — "routed to margin" is a position change, not a license to rewrite. Only a unit that is PS=-1 **and** contains no transmission-core content may be folded/deleted.

## Transmission core — verbatim check

- **English**: compare token by token (negations / numbers / unique terms are independent tokens).
- **Chinese**: check against an explicit list (existence check, not token-by-token):
  - Negation / restriction / uniqueness words: 不 / 未 / 无 / 非 / 别 / 勿 / 只 / 仅 / 除非
  - Numbers and units: verify character by character
  - Causal / conditional conjunctions: 如果 / 当 / 因为 / 则 / 才

Any missing item = "substantive distortion" → roll back.

## The precision core's three parts

Only content that is "uniquely identifying information of this source" may pass. Three classes of identifying information, everything else is droppable:

1. **Precision red lines**: negations / numbers / conditions
2. **Unique terms**: source-specific names, API names, proper nouns
3. **Structural signals**: the source's specific organization

```
【Exclusion signature】= only source-unique identifying information passes (the 3 classes above)
【Transmission core】 = technical substance passes verbatim (English token-by-token / Chinese list-check)
【Precision score】 = each passing unit PS=+1; PS=0 → margin (core still protected); PS=-1 → drop (only if no core content)
```

## Minimal example

Source: "Do not ship on Friday unless the release flag is on."

Object definition: the receiver can correctly say what condition gates shipping.

Precision red lines: `not`, `unless`, `Friday`, `release flag`.

Precision core: "Do not ship on Friday unless the release flag is on."

Drop an explanatory sentence such as "This is because Friday deploys are hard to roll back." Deleting it does not change the receiver's answer to the object definition, while deleting any red line does.

## Degradation thresholds

- **Degrades to radical compression**: all units outside the core are PS=-1 → the precision core = full compression.
- **Degrades to visual design**: the signature needs extra design to be recognizable → the precision core = design signature.
- **Precision-core interval**: units outside the core still include PS=+1, and the identifying info is "the path-shape left after exclusion".

## Boundaries

- Do not modify source content directly.
- Do not optimize for single-output token count (optimize for consistent high signal across outputs).
- Do not auto-expand.
- Safety-sensitive content: hard-protect the transmission core.
- Missing any trigger → route.
- No object definition produced → forbidden to enter PS scoring.
- PS decides position only; it never changes transmission-core protection.

## Failure and recovery

| Failure | Detect | Recover |
|---------|--------|---------|
| Precision-core collapse | Exclusion too aggressive, technical substance can't pass | Widen the transmission lane |
| Precision-core inflation | Too many constraints, degrades to design layer | Remove one constraint, watch if PS rises |
| Substantive distortion | Negation/number/condition rewritten | Roll back core, hard gate |
| Signature parasitism | Signature becomes external decoration | Delete signature; if distinctiveness unchanged → cut it |
| Object definition missing | No object definition before PS scoring | Return to Step 0 |
| Object definition too broad | Most units come out PS=+1 | Narrow the object definition |
| Margin block hurts core | PS=0 block rewritten/compressed, terms distorted | Restore block's terms per core rules, keep position in margin |
