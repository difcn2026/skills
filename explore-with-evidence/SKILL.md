---
name: explore-with-evidence
description: Explore an unclear build direction one small step at a time, capturing evidence after each step to decide the next. Use when you need correctness but can't write tests up front, and the answer matters too much to throw away. Evidence, not guesswork, picks the next step — 当你需要深读/理解/排查一个机制、方向不明且答案太重要不能随便试时。
---

# Explore With Evidence

Navigate development through a series of **small steps** with **parallel verification**, guided by intent. Each step changes state and produces evidence about the feasibility of that change; the evidence confirms the direction or turns it. Evidence steps are the scaffolding for recording and redirecting — navigation judgment is driven by the evidence chain, not invented by the executor.

## Positioning (scaffolding, not navigation judgment)

Evidence steps make an experienced developer steadier, but cannot make an inexperienced one able to navigate. The key judgments ("minimal step", "attribution class") cannot be produced by mechanism alone — they must be driven by the **evidence chain**:

| Step | Who carries it | Mechanism |
|------|---------------|-----------|
| Where to go (minimal step) | **The unknown the last evidence exposed** | Evidence-chain-driven, not the executor picking freely |
| Which class (deviation attribution) | Each class's executable next step | Pick the "executable and minimal" class |
| Record and redirect | Evidence-step mechanism | step / evidence / state-judgment / turn |

**Invariant**: evidence steps do not navigate for the executor; they guarantee the executor **has evidence to stand on at every step, and leaves a trace at every step**.

## When this triggers

1. You need to build a system with correctness requirements, but correctness cannot be stated as test assertions before starting.
2. You hold a malleable intent ("make an accessible cascading selector") that can't generate testable expected values.
3. The product needs both exploration speed and reproducible knowledge accumulation.
4. Can't use test-first development (intent can't turn into up-front tests); can't use a throwaway build (the answer matters too much to throw away wholesale).

## Atomic step unit

Each step is an indivisible three-part atomic unit ("simultaneous" is the ideal; "tight sequence" is the reality):

```
① Act   (make the smallest directional change)
② Evidence (immediately capture evidence of where the state went)
③ Judge  (immediately judge: moved / didn't move / moved backward)
```

## Choosing the minimal step (evidence-chain-driven)

Don't ask "what is the smallest thing" (no standard). Ask instead:

> **After the last step's evidence, what is the most direct next unknown the evidence exposed?**
>
> - First step: the most direct unknown the intent exposes.
> - Later steps: the most direct unknown the previous evidence exposes.
>
> **Minimal step = the smallest change that answers "the most direct next unknown".**

Example:
```
Intent: restore a rate limiter's normal blocking decision → most direct unknown = "what value does the limiter read vs its threshold" → step1 = add logging
Step1 evidence: score=79 > threshold 56 → exposed unknown = "why is the score climbing" → step2 = trace the score's source
(each step is pointed to by the previous evidence, not picked freely by the executor)
```

## Deviation attribution (hypothesis testing, not classification)

Don't directly judge "which class this deviation belongs to". Ask instead:

> **"If I attribute it to class X, what should the next step test?"** — each class maps to one executable next step:

| Attribution class | Executable next step |
|-------------------|------------------------|
| Domain constraint | Check domain rules/docs: "is this a rule the domain already has?" |
| User requirement | Ask the user / check requirements: "does the user really want this?" |
| Platform limit | Check platform capability boundary: "is this something the platform can't do?" |
| Intent error | Restate the intent: "if I swap in a different intent, does the deviation vanish?" |

**Pick the "executable and minimal" class's next step, and run it to test whether the attribution is right.** Attribution is no longer a "judgment" but "a hypothesis testable by the next step".

## Deviation magnitude (three tiers)

| Tier | Definition | Handling |
|------|-----------|----------|
| 0 | Same direction, fine-tune | Absorb autonomously |
| 1 | Same direction, significant | Autonomous, mark for attention |
| 2 | Overturns a core assumption | Bring in external confirmation |

Convergence = two consecutive steps with deviation tier decreasing or staying at 0.

## Turn judgment

| Turn direction | Trigger condition |
|----------------|------------------|
| Turn to spec | ≥3 steps verify the same direction, and deviation tier converges |
| Turn to discard | Answer absorbed, or 2 consecutive steps with no convergence |

Turning to spec does **not claim completeness** (covers only the paths walked); turning to discard does **not lose the conclusion** (only the trace).

## Core loop (seven steps)

1. **State intent** (a movable destination).
2. **Choose minimal step** (evidence-chain-driven: the most direct unknown the previous evidence exposed).
3. **Execute atomic step** (act → evidence → judge).
4. **Attribute deviation** (four-class hypothesis test: pick the executable-and-minimal next step).
5. **Update intent** (per the test result).
6. **Decide turn** (≥3 steps + tier convergence → spec; answer absorbed / no convergence → discard).
7. **Repeat**.

## Minimal example

```
Intent: restore a rate limiter's normal blocking decision

Step1: add logging (intent's most direct unknown = read value vs threshold)
  Evidence: score=79, threshold=56 → judge: moved backward
  Attribution hypothesis: intent error (limiter misconfigured) → next step: trace the score's source
  Tier: 2 (overturns a core assumption) → bring in external confirmation (check config version)

Step2: trace the score's source (step1's evidence exposed this unknown)
  Evidence: the score comes from a config-version / threshold mismatch → judge: moved (root cause located)
  Attribution: confirmed (version mismatch) → tier: 0
  Convergence: 2 → 0 ✅
```

## Failure routing

| What's missing | Route |
|----------------|-------|
| Intent can turn into up-front tests | → test-first development |
| One-shot problem, speed > knowledge | → a throwaway build |
| Intent too vague | → clarify intent first |

## Distinguishing from kept-artifact building (build-incrementally)

Both this skill and build-incrementally grow an artifact in small verified steps, but they solve different problems. Route on the nature of the artifact:

| Question | Answer → this skill | Answer → build-incrementally |
|----------|--------------------|--------------------|
| Is the final artifact meant to be **kept** (delivered, referenced, shipped)? | No — it turns to spec or is discarded | Yes — verification stays attached to each slice |
| Is there a **falsifiable next step** to probe (debug / locate / diagnose)? | Yes | No |
| Does the artifact's **structure converge** (no more modules added/removed/renamed)? | Not applicable | Yes — that's its maturity signal |

Rule of thumb: **this skill probes a chain of evidence to navigate toward an answer; build-incrementally writes a kept artifact one verified slice at a time.** If the product is a trail of evidence toward a root cause / a shape still being discovered → this skill. If the product is a deliverable that must be right and kept → build-incrementally.

## Boundaries

- Do not write tests in advance.
- Do not skip steps to build a complete throwaway build.
- Do not treat deviation as error (deviation is information).
- Do not use when intent is too vague.
- Do not turn to spec and claim completeness.
- Do not substitute for test-first development / a throwaway build.
- Do not navigate for the executor — evidence steps provide the evidence-chain scaffolding; navigation is driven by the evidence chain plus the executor's domain experience.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Verification drift | State-judgment unrelated to intent | Return to a stable evidence step, restate intent |
| Purely decorative step | Evidence can't judge the three states | Delete the step |
| Intent lock | Consecutive tier-2 treated as "another bug" | Pause; accumulated tier-2 = intent failed, restate |
| Premature turn (spec) | Turned spec's assumption wrong next time | Mark "malleable", re-open on deviation accumulation |
| Premature turn (discard) | Same exploration repeated later | Delay the turn (unless 3 consecutive steps give the same answer) |
| Tier-2 without confirmation | Assuming autonomously when overturning a core assumption | Tier-2 immediately brings in external confirmation |
| Evidence chain broken | Previous step's evidence exposed no new unknown | Return to the previous intent, restate |
