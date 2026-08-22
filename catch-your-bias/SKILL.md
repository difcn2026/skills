---
name: catch-your-bias
description: Develop your reasoning like film — reveal bias contamination as a located band with a concrete counter-move, instead of listing bias names. Use when you suspect your current reasoning is tilted but can't pinpoint it — 当你怀疑自己在「找理由支持自己的结论」、觉得推理歪了但说不上来时。
---

# Catch Your Bias

When you suspect your reasoning is tilted, two usual moves fail: reciting a list of bias names ("confirmation bias", "anchoring"…) and vague self-warnings ("be careful"). This skill does neither. It treats your thinking like film: it applies bias-feature probes as developer fluid, and lets the contamination show up in real time as located bands that can be blocked. It does not label you; it locates.

## When this triggers

- Before a high-stakes decision, you need to check whether the current reasoning is contaminated.
- You (or the AI) feel a vague "I might be biased" but cannot locate it.
- Meta-cognitive monitoring fires but only gives anchorless warnings like "be careful".
- A reasoning chain needs a look-back for hidden contamination.
- You are unsure whether something is a normal tradeoff or a bias tilt.

## Input / output

- Input: `thought_sample` (raw thinking flow, at least one complete judgment unit), `context` (optional).
- Output: `contamination_map` (located bands), `stop_bath` (concrete counter-moves), `developed_negative` (the original sample side-by-side with the marks).

## Steps

1. **Take the film (sample)** — cut the smallest complete unit of thinking: one judgment, one tradeoff, one inference. Keep the original wording and order. Never let the user summarize first — summarizing bleaches the bias traces.

2. **Apply the developer (probes)** — apply probes from the bias-feature operator library by contamination spectrum. **Minimal operator library (embedded fallback)**:
   | Operator family | Local cognitive feature it probes (the question) |
   |-----------------|--------------------------------------------------|
   | evidence | Is evidence search symmetric? Are counter-examples missing? "Did you actively look for opposing evidence?" |
   | anchoring | Does the first value/information linger in later reasoning? "If the first number changed, would the conclusion change?" |
   | temporal | Does recency crowd out older causes? Does sunk cost enter the current choice? |
   | social | Does group consensus substitute for independent evidence? "If everyone chose A, would you still choose B?" |
   | emotional | Do emotion load and argument strength move together? Is loss amplified disproportionately? |
   | metacognitive | Does overconfidence, hindsight, or illusion of control leak into the judgment? |

   Probes are not labels; they are detectors of local cognitive features. The full operator library is an external resource synced by the dependency manager; **this embedded version keeps the skill runnable when the library is missing** (degraded path, see counter).

3. **Develop and locate** — record where the probe reacts, as a coordinate, not a category verdict:
   `[segment 2→3] confirmation-bias contamination band, strength 0.72, direction: tilts toward positive examples, counter-example weight down.`

   **Strength scale (honest four-band signal anchoring, not fake precision)** — strength ∈ [0,1], estimated from three observable signals, only four bands:

   | Band | Range | Signals (the more that hold, the higher the band) |
   |------|-------|---------------------------------------------------|
   | none | 0.0–0.2 | probe no reaction; evidence symmetric |
   | weak | 0.2–0.4 | slightly one-sided evidence; counter-examples exist but are waved off |
   | medium | 0.4–0.7 | counter-examples missing; or evidence clearly one-sided; or emotion bound to argument |
   | strong | 0.7–1.0 | counter-examples actively rejected; or conclusion precedes evidence; or an identity stake ("I must be right") is present |

   **What 0.72 means**: it lands in the "strong" band — not because of decimal precision, but because it hit two strong signals at once ("counter-examples rejected" + "conclusion before evidence"). **Strength is band + signal anchoring, not exact measurement; never pretend it is mechanical.**

4. **Fix and map** — combine bands into a `contamination_map`, marking type, strength band, propagation direction, and interactions (e.g. anchoring contamination amplifying confirmation contamination).

5. **Stop-bath** — give each band a concrete counter-move that changes the next cognitive operation, never "be careful":
   - confirmation: force in at least one counter-example with equal search time.
   - anchoring: discard the first reference value, use an external benchmark or interval estimate.
   - emotional: keep the emotion score and the evidence score in separate columns, never merged into one judgment.
   - social: hide the group's answer, give your independent judgment first, then compare.
   - sunk cost: recompute the marginal benefit of the current decision, drop the already-invested resource.

6. **Archive the film** — keep the original sample next to the contamination map, so later you can check whether the development was accurate or over-marked.

## Boundaries

- Do not decide for the user — only locate contamination.
- Do not output a list of bias names as the result; the operator library is only internal developer fluid.
- Do not give empty warnings; there must be coordinates and counter-moves.
- Do not claim bias is fully eliminated; development raises visibility, it is not immunity.
- Do not handle already-summarized, already-abstracted "I think I'm biased" with no original wording.
- Do not collect or transmit the raw thought sample externally, unless the user explicitly allows anonymized archiving.
- **This skill is diagnostic aid, not automatic judgment.** A contamination band is a hypothesis to verify, not a confirmed bias. Development raises visibility; it is not immunity, and not a verdict. When a mark conflicts with the user's self-understanding, the user's feedback wins and the sensitivity is lowered (mark `low_confidence`) — do not force a conviction.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Under-developed | Output has no coordinate, only bias names or "be careful" | Re-sample, require the original judgment turns |
| Over-developed | User says "that's not what I was thinking" | Return to the film comparison, lower probe sensitivity, mark `low_confidence` |
| Empty counter-move | The move is "stay alert" / "be careful" | Replace with a concrete instruction that changes the cognitive operation |
| Sample too short | Sample shorter than one complete judgment | Mark `insufficient_sample`, do not force development |
| Unknown contamination pattern | User reports anomaly, probes no reaction | Mark `unknown_pattern`, route to the ecosystem architect to propose new operators |
| Sample bleached by summary | Input is an abstract conclusion, not raw thinking | Ask for the original wording or the reasoning process, else stop |
| Operator library missing | External bias-feature-operators unavailable | Degrade to the embedded minimal library (six probe families), mark `degraded_operators`, precision limited but not interrupted |
