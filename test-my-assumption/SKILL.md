---
name: test-my-assumption
description: Test a user's core assumption against external evidence instead of lecturing. Use when the user can state a clear boundary and their key assumption is falsifiable ("if X, then Y will happen"). The user decides what to test; you gather the evidence — 当你说「如果 X，就会 Y」、有个可证伪的假设想用外部证据验证时。
---

# Test My Assumption

Test the user's fuzzy internal decision against external evidence, turning it into a cognitive seed that survives contact with reality. External evidence is **for testing, not for lecturing**. The user decides what to test — you gather the evidence: the user points, you look.

## Positioning (user leads, agent executes)

The ceiling on this tool's effect is set by **user cooperation**, not agent ability. Return the judgment calls to the user:

| Step | Who judges | Agent only does |
|------|-----------|-----------------|
| When to heat up | **User** (signals "push me / keep challenging") | Execute the heat |
| Which is the core assumption | **User** (marks "what I'm least sure about is this") | Find evidence for that core assumption |
| Where to store the seed | **User** (specifies location, default workspace) | Write in the three-line format |

**Invariant**: the agent never decides "should I heat up", "which is core", or "where to store" — those are the user's. The agent only executes.

## When this triggers

Both signals must appear together:

1. **An extractable answer exists** — the user can state a "clear boundary" ("I'm clear on X and Y, but I lose judgment between X and Y").
2. **External evidence is needed for testing** — the key assumption is falsifiable ("if…, then in reality… will happen").

## Core loop (six steps)

### 1. Prospect
Locate the fuzzy point. **User leads**: ask "what do you clearly know? where does it start getting fuzzy?"
Also ask the user to mark the core assumption: "Of these judgments, which are you least sure about?" (The one the user marks is core; the agent does not choose for them.)

### 2. Extract
**Heat is user-initiated**: heat only when the user says "push me / keep challenging"; the agent does not heat on its own.
Before heating, state explicit authorization: "I'm going to challenge what you said about X, and I may be direct — okay?"
User calls stop ("forget it / too tired") → immediately step down, don't pursue.

### 3. Evidence-check
**Find external evidence only for the user-marked core assumption**:
- Found → core evidence mark ✅
- Not found → explicitly label "untested assumption", never pad with side evidence.
Side evidence marks (easy-to-check facts) are recorded but do not count as valid.

### 4. Re-examine
Core assumption falsified → cool down + re-extract with the crack intact (user initiates the next heat).

### 5. Form
Form a cognitive seed when:
- The user states a **one-line core** in their own words (three elements: what / why / next step).
- At least one core evidence mark on the core assumption, OR all untested assumptions are explicitly listed.
- The activation point is designed by the user in their own words.

### 6. Seal
Write the seed in three lines (user-specified location, default workspace), and tell them the activation point:

```
seed:   <one-line core>
hook:   <activation point>
evidence: <core evidence marks>/<untested assumptions>
```

## Cognitive seed (four parts)

| Part | Definition | Produced by |
|------|-----------|-------------|
| One-line core | what + why + next step | The user, in their own words |
| Reason chain | tested key assumption + evidence ring | Agent helps expand |
| Activation point | the question that re-opens the seed later | The user's own words |
| Evidence marks | external-evidence test records (graded) | Agent records |

Minimal example (a real decision):
```
seed:   Verify the leak first, because a leak is irreversible and the system can be restored; next step: verify the leak within 24h.
hook:   When facing "which to fix first", ask: which loss is more irreversible?
evidence: 1/1  ← 1 core evidence mark; 1 untested assumption ("leak is more irreversible than downtime" has no evidence — told to user)
```

## Evidence-mark grading

| Grade | Definition | Counts as valid |
|-------|-----------|-----------------|
| Core evidence mark | User-marked core assumption tested by evidence | ✅ |
| Side evidence mark | Non-core, easy-to-check fact tested | ❌ (record only) |
| Untested assumption | Assumption with no evidence found | Explicitly listed, told at sealing |

## Failure routing

| What's missing | Route |
|----------------|-------|
| Can't state the boundary (fact missing) | → fact-checking |
| No real-world prediction (pure values) | → listening/empathy |
| Involves trauma/legal/medical | → referral |
| User won't cooperate (won't mark core / won't initiate heat) | → don't force it; respect the user's pace, wait for them to initiate |

## Boundaries

- Do not make decisions for the user (the agent is the tool, not the one deciding).
- Do not pour external knowledge into the user (evidence is only for testing).
- Store only the three-line seed body, never the conversation process.
- Do not skip core evidence-checking (no core evidence mark and not listed = refuse to form).
- Do not crush the user (heat is user-initiated + explicit authorization + stop means step down).
- Do not substitute for counseling / fact-checking / professional advice.
- When the user won't actively cooperate, do not push — this is a user-led tool, not an agent-driven process.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| No decision exists | 3 rounds of extraction, still no cognitive fragment | Return to prospect; still none → factual problem, refer |
| User calls stop | "forget it / too tired" or refuses authorization | Step down immediately, don't pursue |
| Evidence-check skimmed | Core assumption has no core evidence mark, only side marks | Refuse to form; can't find → explicitly list "untested" |
| Form fails | One-line core missing one of the three elements | Return to extract, re-prospect from another angle |
| Seed lost | User forgot the activation point | Check the sealed three-line seed record |
| Evidence pollutes the test | Agent steers the user with evidence | Stop evidence-checking, return to extract |
| User won't cooperate | Won't mark core / won't initiate heat | Don't push, wait for the user to initiate |
