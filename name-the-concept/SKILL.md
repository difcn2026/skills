---
name: name-the-concept
description: Turn an "I understand it but can't say it" into a name you can actually reuse. Use when you keep saying "there's this thing…", "sort of…", "I can't quite put it into words" — and the idea stays unusable because it has no handle.
---

# Name the Concept

An idea you can gesture at but not name is not yet a concept — it is a pre-concept: it has structure but no interface, substance but no form. Two habits keep it stuck there. One reaches for a better label, as if the idea were already finished and only needed prettier packaging. The other keeps abstracting, waiting until the idea is "clean enough" to deserve a name. Both assume a name is something you attach *after* the concept is done. This skill inverts that: **a name is the interface through which an idea becomes usable, and naming is the act of birth** — the pre-concept crosses over into a real, callable concept the moment it gets its name.

## When this triggers

Enter when **any** of these holds:

1. Language signal — you describe an understanding with hedges: "sort of", "roughly", "some kind of", "I can't quite say", "it feels like".
2. Structure signal — you can give several instances or phenomena, but cannot say what they *are* in common.
3. Call-failure signal — you keep trying to use this understanding to explain something new, make a judgment, or pass it to someone else, and each attempt circles back to the start.
4. Repetition signal — you keep describing the same thing with different words each time, and it never settles.
5. Explicit request — "help me think it through", "give it a name", "what is this, really".

Do **not** enter when the concept is already clear and you only want a better label (that is a renaming task, not a birthing task).

## Steps

### 1. Diagnose before naming (confirm there is structure)

Have the user describe the thing **without naming it** — no nouns allowed to point at it, only verbs, adjectives, and relations. Then judge stability along three dimensions, each with a mechanical test:

| Dimension | Test question | Stability criterion |
|-----------|---------------|---------------------|
| **Relation** | "Do A and B always act on each other the same way?" | The direction/sign of the relation is consistent across ≥ 2 descriptions |
| **Boundary** | "Can you name a case that is *not* it? Where is the edge?" | The user gives ≥ 1 clear counter-example, and two descriptions' counter-examples do not conflict |
| **Dynamic** | "How does it change? Is there a fixed direction or trigger?" | The change follows the same direction (grows/decays) or same trigger in ≥ 2 tellings |

**Decision**: ≥ 2 of 3 dimensions stable → pre-concept, continue to Step 2. Otherwise it is not yet a pre-concept — go abstract the structure further before naming (this skill does not apply yet).

Output: a "structure sketch" — relation, boundary, dynamic — with **no candidate name yet**. Naming at this step is forbidden; doing so degenerates into "renaming an existing concept."

### 2. Probe for the interface (find the leverage point)

Look for the point where a single word would let the mind grasp the whole structure:

- **Draw the premise arrows** — write relations as "X is the premise of Y". Which relation is pointed to by the most arrows? That is the premise relation.
- **Run the deletion test** — imagine deleting a boundary; which one makes the others collapse? That is the anchor boundary.
- **Find the driver** — which dynamic, when it changes, drags the others with it? That is the driving dynamic.

Among premise relation, anchor boundary, and driving dynamic, pick the one shared by the most dimensions as the **highest-leverage point** — the name lands there.

Then generate 3–5 candidate names, each satisfying: **callable** (usable as subject or object in a sentence), **structure-bearing** (the name compresses the shape, not an arbitrary tag), **distinctive** (no confusion with neighbors), **growable** (an interface, not a locked definition).

### 3. Name to birth (the act itself)

The user picks a candidate (or proposes their own). Then run the **birth test** — all three must pass:

| Test | Must answer with a concrete instance | Walking-through-it (fails) |
|------|--------------------------------------|----------------------------|
| **Call** | *Which* new phenomenon did you explain as "this is a case of X"? | "It can explain things" (no instance) → fail |
| **Pass** | To *whom* did you explain it, and *which words* showed they got it? | "It's explainable" (no audience, no feedback) → fail |
| **Combine** | With *which* concept did you combine it, producing *which* new judgment? | "It combines" (no specific combination) → fail |

All three have concrete instances → the concept is born. Any test lacks an instance → mark `unborn`, return to Step 2 and adjust. This rule does not stop a shortcut, but a shortcut can no longer produce a "born" verdict.

### 4. Aftercare (keep it from slipping back)

Produce a "birth certificate": the name, its structure-bearing note, the three test instances, misuse boundaries (where this name gets confused with neighbors), and an evolution note (how the concept may grow and the name may need to change).

**Minimal example**:

```
User: "I keep feeling there's a thing… when you try really hard to do something,
but the harder you try the worse it gets. It's not nerves, not lack of skill.
The effort itself is blocking you. I don't know what it's called."

Step 1 — diagnose (no naming yet):
  Relation: effort and outcome act inversely — consistent across tellings. ✓
  Boundary: "not nerves" / "not skill deficit" / "not outside interference". ✓
  Dynamic: more effort → more blockage → worse result → more effort (same direction). ✓
  → 3/3 stable → pre-concept, continue.

Step 2 — probe:
  Premise relation: the *inverse* relation between effort and outcome is pointed to
  by the others; it is the leverage point.
  Candidates: effort paradox / over-effort / inverse-effort effect / trying-too-hard trap.

Step 3 — birth test (user picks "effort paradox"):
  Call:   "Learning to swim — the harder I try to float, the more I sink. That's the effort paradox." ✓
  Pass:   "Effort paradox = past a point, the effort itself starts producing the opposite effect." ✓
  Combine: "Effort paradox vs flow: in flow the effort disappears and the result peaks —
           flow is the inverse of the effort paradox." ✓
  → born: effort paradox.

Step 4 — aftercare:
  Misuse boundary: not "laziness" (no effort), not "skill gap", not "nerves".
  Evolution note: may split into cognitive vs physical effort paradox.
```

## Boundaries

- Do not birth something with no structure — if the relation/boundary/dynamic are unstable, send it back for structure first.
- Do not make the final naming decision for the user — candidates may be offered, but the final choice is theirs (the name is their interface, not the tool's).
- Do not re-birth an already-born concept — if the user can already call on the thing cleanly, this skill does not apply.
- Do not promise one-shot success — a name may fail the birth test; failing is part of the process, not an error.
- Do not name someone else's concept — this handles the user's own pre-concept, not "help me understand this existing idea."

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Slipped into renaming | Names appear before the structure sketch is done | Stop, return to Step 1, forbid names until the sketch exists |
| Slipped into defining | After a name, the user fixates on a precise definition instead of testability | Return to Step 3, run the birth test — callability matters, not the definition |
| Naming failed | Call/pass/combine test fails | Return to Step 2, diagnose *why* (missed the leverage point? too narrow? too wide?), generate new candidates |
| Structure unstable | Step 1 shows each telling differs, no stable relation/boundary/dynamic | Judge it not-yet-a-pre-concept, send back for structure first |
| User refuses to name | "I don't want a name, I just want to understand" | Explain: an unnamed thing cannot be called on; not naming = not finishing the understanding. If they still refuse, respect it but mark `unfinished concept` |
| Name locks the concept | After naming, the user rejects any other facet | In Step 4, stress "a name is an interface, not a definition" — interfaces can change, concepts can grow |
