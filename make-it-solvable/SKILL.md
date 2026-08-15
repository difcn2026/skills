---
name: make-it-solvable
description: Turn a vague request into a solvable unit — a boundary and a solution that take shape together. Use when the user says "help me improve X" and you're unsure whether to think it through first or just start solving.
---

# Make It Solvable

When a request is vague, two failures are common: endless clarifying questions (define-then-solve paralysis) and blind attempts that miss the mark (jump-to-solve thrash). This skill takes a third path: it does not wait for the boundary to be complete, and it does not solve blindly. It gives a minimal trial solution first, lets the boundary show itself, and forges boundary and solution against each other until they form a "solvable unit" — a boundary that explains why the solution works, and a solution that verifies the boundary is drawn correctly.

## When this triggers

Enter the classification gate when **any** of these holds:

1. The request says "help me do X", but at least two of {goal, constraint, acceptance criterion} are missing.
2. The same request has already produced 3+ rounds of questions with no boundary output.
3. A solution was already offered and the user said "that's not it".

**Decision rule**: all three of goal/constraint/acceptance present → already defined, solve directly. Two or more missing → boundary state, enter the forge loop. No request structure at all → symptom state, give a minimal trial solution to surface the boundary.

## The three states (classification gate)

| State | Basis | Action |
|-------|-------|--------|
| Already defined | goal, constraint, acceptance all observable | Solve directly; do not forge a boundary |
| Boundary state | two of three missing | Enter the forge loop |
| Symptom state | no request structure | Minimal trial solution first, then surface the boundary |

## The forge loop

```
trial solution → reverse-engineer boundary → compress boundary → re-solve inside → coupling check → output / loop back
```

- **Trial solution surfaces the boundary**: don't wait for a complete boundary; give a minimal solution draft as raw material.
- **Solve inside the boundary**: re-solve within the boundary so the solution takes shape inside it.
- **Solvability takes shape**: boundary and solution forge each other until they form a solvable unit.

Minimal example of a trial solution:
```
Request: "help me improve our retention" (goal vague, no constraint, no acceptance)
Trial solution (not an answer, forging raw material):
"Assume the bottleneck is the signup flow — first list the drop-off rate of each step and find the step that leaks most."
```
This trial solution implies a boundary: scope = signup funnel, metric = drop-off rate, constraint = don't touch the backend yet.

## Steps

1. **Classify** — the three states above. If already defined, jump to step 7.

2. **Trial solution** — give a minimal solution draft to surface the boundary.

3. **Reverse-engineer the boundary** — pull the implied goal/constraint/acceptance out of the trial solution. Record them as candidate boundaries.

4. **Compress the boundary** — shrink candidate boundaries to the smallest solvable set. If a contradiction can't be removed, mark "incomplete symptom", request one key missing signal (at most once), then force-continue.

5. **Re-solve inside** — produce a solution within the compressed boundary. If it overflows the boundary, return to step 3. If it fits, go to step 6.

6. **Coupling check** (mechanical):
   - Boundary→solution direction: translate each boundary line into one sentence of "why this solution works" — every line must translate.
   - Solution→boundary direction: trace each key action of the solution to "which boundary line it falls under" — no action may fall outside.
   - Both pass → solvable unit holds. Either fails → return to step 3.

7. **Output the solvable unit** — the boundary and the solution together, marked clearly that the boundary is a working hypothesis that new evidence can overturn.

## Loop limit

The step 5↔6 loop is capped at **3 rounds**. After 3 rounds without coupling, stop and output: the candidate boundary forged so far, the list of conflict points, and the explicit conclusion "current information is insufficient to form a solvable unit". Do not fake solvability.

## Routing

| Situation | Route |
|-----------|-------|
| Already defined | Solve directly; this skill is not needed |
| Endless questions (define-paralysis) | Use this skill: force a trial solution to surface the boundary |
| Solution with no boundary (jump-thrash) | Return to step 1, add classification and boundary reverse-engineering |
| 3 failed coupling rounds | Output "not currently solvable", hand back to the user for one key signal |

## Boundaries

- Do not skip the classification gate and start solving (jump-to-solve).
- Do not ask endlessly for a perfect boundary; the boundary must be reverse-engineered from a trial solution, not only questioned (define-paralysis).
- Do not treat the forged boundary as permanent truth; it is a working hypothesis.
- Do not decide for the user; the solvable unit needs user confirmation before execution.
- Do not forge a boundary when the request is already defined; solve directly.
- Do not fake solvability; when the boundary can't be compressed and the user can't supply a key signal, say "not currently solvable".

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Slips into jump-to-solve | Output has only a solution, no boundary | Force return to step 1 |
| Slips into endless questions | 3+ questions with no trial solution or boundary | Force a trial solution from current information |
| Boundary won't compress | Candidate boundaries contradict and can't be reduced | Mark "incomplete symptom", request one key signal (once) |
| Coupling check fails | Boundary translation or action trace fails | Return to step 3; after 3 rounds, output "not solvable" |
| Solvability faked | Boundary and solution both pass but user rejects | Re-compress the boundary, or downgrade to "experimental solution" |
