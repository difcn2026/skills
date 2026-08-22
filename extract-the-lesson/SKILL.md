---
name: extract-the-lesson
description: Turn a hard-won lesson into something that will actually resurface later. Use when a post-incident review or retrospective produced conclusions that everyone already forgot by the next project — 当复盘结论写了又忘、同一个错反复犯、说不清「下次什么时候该想起它」时。
---

# Extract the Lesson

Two habits quietly waste most hard-won lessons. One keeps digging into what happened — more facts, more detail, a fuller record of the past. The other keeps lifting the lesson upward — a cleaner rule, a more general principle. Both treat the lesson as a property of the past, so both stop at "here is what we learned." This skill takes the lesson to be neither a fact nor a rule but an **interface to the future**: a lesson only exists if, at the moment it matters again, you can pull it back out. The work here is not to extract more — it is to **bind every lesson to a recall signal**: a specific, observable sign that says "now is when you need this."

## When this triggers

Enter when **any** of these holds:

1. The same root-cause sentence keeps reappearing across reviews ("it was a communication problem again") without any new mechanism being named.
2. New and old lesson write-ups overlap heavily in their cause/lesson wording, but no one can say what to do differently next time.
3. A lesson was written down, but no one can say **when** it should have come to mind.
4. You notice the same failure pattern recurring in two or more different-looking situations.

The four signals above are **candidate** triggers. Before acting, verify they are the *same* failure: write each as two fields — **trigger condition** (what pre-state caused it) and **failure mechanism** (how it unfolded). Only when *both* fields match are two events the same lesson. Overlapping keywords alone do not make two events the same failure.

## Steps

### 1. Extract the lesson content (X)

From the material, pull out each candidate lesson in the form: **"When [condition], do / do-not [action], because [reason]."** If you can only produce a description ("the project ran late, everyone was exhausted") and not a condition–action–reason, the material is not yet a lesson — go back and gather more facts first.

### 2. Identify the recall signal (Y) — the core step

For each lesson X, ask not "what is this lesson?" but **"what sign, when it appears, should bring this lesson back?"**

A recall signal must satisfy three conditions:

| Condition | Meaning | Counter-example → fixed |
|-----------|---------|------------------------|
| **Observable** | The sign is directly checkable in the future scene, no extra inference needed | "when we become complacent again" → "when the team has gone 3 straight days with no objection raised" |
| **Early** | The sign appears **before** the failure, not after | "after the project fails" → "when the project plan lists no risks at all" |
| **Actionable** | When the sign appears, there is still time to act | "once the contract is signed" → "the first time the contract draft is discussed" |

### 3. Bind X ↔ Y into a recall unit

```
recall unit = {
  lesson (X):       [one executable sentence],
  recall signal (Y):[observable, early, actionable],
  binding strength: [strong / medium / weak],
  false-positive risk: [when Y appears but X does not apply],
  false-negative risk: [when X applies but Y does not appear]
}
```

**Binding strength** — score three factors, each 1–5, then take the **lowest** score (a binding is only as reliable as its weakest dimension):

| Factor | 1 (weak) | 3 (medium) | 5 (strong) |
|--------|----------|------------|------------|
| Causal distance | signal and lesson are 3+ inference steps apart | 1–2 steps apart | the signal *is* the lesson's direct trigger |
| Observability | needs introspection to detect | needs a simple observation (count / check a record) | literally matchable (page count, record count, empty-or-not) |
| Times verified | 0 | 1 | 2 or more |

Any factor at 1 → binding strength must not be marked "strong."

### 4. Deploy the recall interface

Place the recall unit where the signal will actually be met:

| Method | When the signal is… | Example |
|--------|--------------------|---------|
| Environment trigger | detectable in a physical/digital environment | add to a code-review checklist: "if the PR has no tests, recall 'untested code gets reworked'" |
| Process checkpoint | at a fixed node of a process | add to kickoff: "if the risk list is empty, recall 'a zero-risk plan is the biggest risk'" |
| Human agreement | something a person must notice and report | agree that "anyone who sees 3 days with no objection may interrupt and recall 'silence is how things rot'" |

### 5. Verify and decay-manage

After each recall, record: did the signal fire in time? Was the binding accurate? Has the signal degraded (no longer observable / no longer meaningful)? Adjust the binding strength or update the signal. A recall unit's lifecycle is: create → deploy → recall → verify → strengthen / fix / retire.

**Minimal example** (a full walk-through):

```
Input: Project Alpha slipped 6 weeks. The team spent 4 weeks building features
"that looked important but no user asked for." The 80-page spec listed no user
interview. The PM said "we thought the requirements were clear." Nobody objected
at kickoff.

Step 1 — extract X:
  Lesson: when the spec is long but zero user interviews were done, do not start
  building, because document length has nothing to do with requirement clarity.

Step 2 — identify Y:
  Ask: when, in the future, should this lesson come to mind?
  Answer: at a kickoff where the spec is long and the interview count is zero.
  Signal Y: at project kickoff, spec pages > 20 AND user-interview count = 0.

Step 3 — bind:
  binding strength = strong (causal distance 5, observability 5, verified 1 → lowest = 1 …
  wait, lowest is 1 because verified only once). Corrected: binding = weak (1),
  because it has been verified only once. Re-score after the next kickoff.

Step 4 — deploy: process checkpoint — add to the kickoff checklist:
  "user-interview count = ? (if 0, recall unit #1)"

Step 5 — verify: at the next kickoff, if the signal fires and the team pauses to
interview, upgrade binding strength from weak to medium.
```

(Note how the example itself catches a scoring mistake — this is the binding-strength rule doing its job: one unverified lesson must not be marked strong.)

## Boundaries

- Do not replace a full retrospective — if the material lacks enough facts to extract a lesson, do the review first.
- Do not boil it down into a bare rule — if a lesson cannot be put in one executable sentence, sharpen it first.
- Do not handle signal-less lessons — if no observable, early, actionable signal exists, mark the lesson `unbindable`; this usually means it is too vague or not really a lesson.
- Do not guarantee recall — the unit binds and deploys; whether a human notices the signal is still on the human (see "Human agreement").
- Do not monitor more than 7 active recall units in one scene — more than 7 means the signals are too fine-grained; abstract upward.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Slipped back into a retrospective | Output is only "we learned X", no Y | Return to Step 2, force a Y for every X |
| Slipped back into over-generalizing | Output is only "the rule is X", no Y | Same — force a Y |
| Signal not observable | Y needs extra inference to judge | Rewrite Y until it can be directly checked |
| Signal too late | Y appears after the failure | Ask "what sign appears *before* this one?" |
| Binding over-strong | False-positive risk ignored, Y mechanically fires X | Add the false-positive condition, lower the strength |
| Signal degraded | Verification finds Y no longer fires or no longer means anything | Update the signal or retire the unit |
| Recall units piling up | Active units > 7 in one scene | Abstract upward: merge similar signals or group by scene |
| Different failures merged | Two events only share a keyword, treated as one lesson | Re-check trigger-condition AND failure-mechanism fields; split into separate units |
