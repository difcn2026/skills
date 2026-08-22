---
name: decide-whether
description: Decide whether to do something when the user is genuinely torn. Turn an unresolved yes-or-no decision into one reusable one-line rule. Use when the user says "should I do this", "I don't know whether to", or is stuck between two choices — 或说「要不要做」「该不该做」「拿不准」时。
---

# Decide Whether

Help a user settle an unresolved "whether to do this" decision into a reusable one-line principle. You do not make the decision for them; you apply pressure until they arrive at their own integrative statement, then compress it.

## When this triggers

Only when the user's **goal itself** is undecided ("I don't know whether I should do this") and they show genuine tension about it. Before doing anything, classify their state by inference — do not ask unless you cannot infer:

| User state | Inference basis | Action |
|-----------|-----------------|--------|
| Goal undecided | No explicit goal + visible tension | Enter the decision, make the encounter |
| Goal decided, means undecided | They recently stated a priority/stand ("I definitely want to…") | Do NOT enter this flow; assist execution instead |
| Already integrated | They already said "I used to think… but seeing… so…" | Skip to closure directly |

**Infer first, ask only as a fallback.** If you can't tell from what they've already said whether the undecided part is the goal or the means, ask one question: "Is the part you haven't decided the *whether to do it*, or the *how to do it*?" Never interrupt someone who is clearly mid-execution with this question.

## The decision file structure

A decision is stored in four fields:

```
DECISION::core      → the compressed one-line principle
DECISION::trigger   → when this decision may be reopened
DECISION::reopen    → the first action when reopening
DECISION::trace     → ≤3 encounter traces: absorbed / rejected / restated
```

Minimal example:
```
DECISION::core    → "Tool value is intrinsic (emerges from the work); reach is a natural result of value being realized, not the motive."
DECISION::trigger → When I'm about to promote a tool and start wondering "should I chase reach?"
DECISION::reopen  → First ask: did this tool's value grow on its own, or did I force it for reach?
DECISION::trace   → ①absorbed: quantity trades for probability; ②rejected: none; ③restated: "reach is not the production motive, it's the payout."
```

## The five actions

0. **Pre-route** — classify (infer-first, ask-as-fallback), then check whether an integrative statement already exists. If it does, skip actions 2–3 and go straight to closure.

1. **Align** — place the user's internal stance next to the external gap side by side. Don't interrogate, don't lecture.

2. **Make encounter** — apply pressure only to the undecided goal layer. Treat already-decided goals as facts; never reverse-pressure them.

3. **Hold tension** — when the user leans:
   - toward the external → push back with "Then what is the decision you haven't made?"
   - toward the internal → push back with "How did this external evidence change how you feel?"

4. **Identify the rule** — the user states, without prompting, a new formulation that integrates inside and outside. That is the rule. Compress it to one core line.

5. **Close the decision** — produce the four-part decision file at session end.

## Authorized reopening

Reopening a decision requires the user's explicit authorization. Other skills may read only the `core` line; reading `trace`/`reopen` requires the user present and confirming.

## Routing

- Goal decided, means undecided → assist execution, do not enter this flow.
- Purely internal problem → fall back to Socratic questioning.
- Purely external problem → fall back to explaining/fact-finding.

## Boundaries

- Do not make the decision for the user.
- Do not provide a single external authority as the answer.
- Do not generate multi-file courses.
- Do not persist mid-session; settle once, at the end.
- Do not write raw data / secrets / full external resource text into the decision file.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Decision won't settle | 3 rounds of pressure, user still swings | Cut a smaller decision surface; still failing → drop to Socratic questioning / direct instruction and return |
| Goal/means misread | User reacts "I already decided that" | Stop making the encounter, switch to execution assist |
| Decision breaks | Later: "I understood it before, can't recall now" | Rewrite the trigger |
| Tension imbalance | User deflects or goes emotional ("I don't know") | Withdraw external pressure, switch to an instructing posture |
| Decision turns dogmatic | User applies core without checking context | Inject a "re-decide" reminder |
| Decision misused | A guard finds the decision rule cited as external fact | Mark "a decision rule is not a fact record" |
| Mechanical question interrupts execution | You ask "is your goal decided?" to someone who already decided | Stop asking; infer and assist. Record the inference so you don't re-ask |
