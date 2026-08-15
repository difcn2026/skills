---
name: compress-to-budget
description: Compress content to fit a strict budget (token count, one screen, a size limit) while staying recognizable. Use when you must cut to a specific limit AND keep the result distinct from competitors. Distill to the semantic core without losing the signature.
---

# Compress To Budget

Distill content to its irreducible semantic core, and crystallize a unique signature in the smallest token carrier, so the form carries both semantic value and efficiency. Form is neither value nor noise — form is the topology of meaning: nodes carry substance, connections carry relation, arrangement carries signature.

## When this triggers

Trigger only when **both** signals appear together:

1. **A quantifiable budget constraint** (an explicit number: ≤ 200 tokens / one screen / within 150px).
2. **An explicit distinctiveness requirement** (needs a recognizable signature: distinct from competitors / has a memory point).

Missing either one → route to a failure path (pure compression / pure design / just do it).

## Domain boundary (draw the line honestly)

Testability of this distillation has a hard boundary. Be honest about it:

| Content type | How it's judged | Example |
|-------------|-----------------|---------|
| **Concrete semantics** | ✅ Mechanical (deletion test / restore test is checkable) | numbers, entities, states, config items (`¥299`, "paid") |
| **Abstract semantics** | ⚠️ Human-assisted (deletion test degrades to subjective; needs a human, state it honestly) | methodology, concepts, claims ("verification and generation share one source") |
| **Signature elements** | Don't pretend to carry semantics — only "unique within batch + not restorable" | symbols, colors, layout |

**Invariant**: this approach works mechanically on concrete semantics; for abstract semantics it honestly degrades to human-assisted — it never pretends to be mechanical. A signature is a signature, not a semantic carrier.

**Three-stream routing (how to tell which stream a fragment falls into):** apply this test *before* running any loop step.

| Stream | One-line test | If it falls here |
|--------|--------------|-----------------|
| **Mechanical** | "If I delete this, another fragment can show a *fact* went missing (a number, an entity, a state)." | Run the deletion/restore test mechanically |
| **Human-assisted** | "This is a claim/concept/methodology; deleting it loses a *stance*, not a *fact*, and no other fragment proves a fact went missing." | Say honestly: this step is human-assisted |
| **Signature** | "Deleting it changes nothing semantically, but the output stops being recognizable, and no other element can restore that recognition." | Treat as distinctiveness only, never as a semantic carrier |

A fragment that can't clearly pass one of the three tests is almost always human-assisted — do not pretend it's mechanical.

**Mixed fragments: split before you route.** A fragment can contain both a fact and a stance at once (e.g. "¥199 is a good deal" — "¥199" is a fact, "is a good deal" is a stance). Do not route the whole fragment into one stream:

1. Split the fragment at the fact/stance boundary.
2. The fact part (a number, an entity, a state — deletable into a provable fact gap) → **mechanical** stream.
3. The stance part (a claim, a value judgment, an opinion — deletable into only a changed opinion) → **human-assisted** stream.

Test for the split point: "if I delete this part, does a *provable fact* go missing (mechanical), or does only the *speaker's stance* change (human-assisted)?"

## Core loop (six steps)

### 1. Semantic distillation (deletion test on four information classes)

Ask per element: **"If I delete X, which class of information is lost?"**
- Losing an **entity** (who/what), **relation** (how connected), **attribute** (what value), or **constraint** (what limit) → keep.
- Losing none of the four → delete.

Minimal example:
```
"Verification and generation are two views of one action"
  delete "verification and generation" → loses entity → keep
  delete "one action" → loses relation → keep
  delete "two views" → loses attribute → keep
  delete "of" → loses none → delete
```
(Note: this example is abstract semantics — the assignment of the four classes still needs a human; state honestly that this step is human-assisted for abstract content.)

### 2. Constraint injection
Budget number + distinctiveness requirement → crystallization conditions (usable form vocabulary, token budget).

### 3. Semantic-core growth + anti-force-fit check
Map the semantic core onto form elements. **Anti-force-fit check**: for every claim "form F carries semantics S", ask "if I swap in a different form F', does the semantic contrast change? If unchanged = force-fit, delete it or demote to neutral decoration."

**Force-fit signals (a check, not a vibe).** Any one of these means the claim "F carries S" is likely force-fit — delete F or demote it to neutral decoration:

1. **Needs explanation to justify** — you have to write more than one sentence to explain why F carries S. A real semantic carrier is obvious on sight.
2. **The explanation is removable** — strip the justification sentence and the meaning of the surrounding text is unchanged → F carried nothing.
3. **Swap leaves contrast unchanged** — substitute a different form F′ and the semantic distinction you claimed still reads the same → F was decoration.

Minimal example:
```
Claim: "the amber color of this badge carries the constraint 'caution'."
Signal 1 fires: explaining why amber = caution takes a sentence.
Signal 2 fires: delete "amber" → "the badge carries the constraint 'caution'" — meaning unchanged.
Signal 3 fires: swap amber for a red badge → "caution" still reads.
→ amber is force-fit decoration, not a semantic carrier. Demote it.
```

### 4. Negative-space verification
Restore test (can the semantics be restored after removal) + **within-batch registry comparison** (after removal, is it still distinguishable from the other outputs in this batch).

### 5. Semantic fidelity audit
Verify that not/never/no/only, exact numbers, and locked cores were not wrongly deleted.

### 6. Density report
Per-element semantic contribution + signature contribution (checkable judgments: deletion test + anti-force-fit check + restore test).

## Signature judgment

A signature is pure distinctiveness — it does not need to carry semantics:

| Signature condition | Criterion (checkable) |
|--------------------|----------------------|
| Unique within batch | Distinguishable from other outputs in this batch |
| Not restorable | After removal, the signature cannot be restored by other elements |

**Minimal batch definition**: ≥ 2 outputs serve as each other's registry; with a single output, signature judgment **degrades to user confirmation** (state it honestly).

## Semantic density metric

Semantic density = elements carrying semantic distinction / total elements.

"Carrying semantic distinction" is judged by the **deletion test** (loses one of the four classes). Signature elements are not counted in semantic density (they carry distinctiveness, not semantics).

## Failure routing

| What's missing | Route |
|----------------|-------|
| Budget only, no distinctiveness | → pure compression |
| Distinctiveness only, no budget | → pure design |
| Neither | → just do it |
| Abstract semantics with no human available | → don't pretend mechanical; return to human-assisted flow |

## Boundaries

- Do not change core semantics — only presentation density and distinctiveness.
- Do not force a signature onto content with no semantics.
- Do not sacrifice accessibility.
- Do not handle narrative/emotional content.
- Do not auto-deploy — semantic core extraction needs human confirmation.
- Locked cores (legal/safety) are not compressed.
- Abstract semantics: honestly state human-assisted, never pretend mechanical.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Key semantics wrongly deleted | Fidelity audit finds a missing information class | Roll back, add the missing item to locked |
| Signature hides semantics | Readability test fails | Weaken signature, re-verify semantic contrast |
| Force-fit semantics | Anti-force-fit: swapping form leaves semantics unchanged | Delete or demote to neutral decoration |
| Output still redundant | Density report shows "no-semantics + no-signature" elements | Delete, re-run negative-space verification |
| Distinctiveness insufficient | Indistinguishable from other batch outputs | Re-pick signature, verify within-batch uniqueness |
| Abstract mistaken for mechanical | Deletion test disagrees with human judgment | Return to human-assisted, mark as abstract content |
