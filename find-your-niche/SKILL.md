---
name: find-your-niche
description: Locate the user's real position between what they need and what the ecosystem offers. Use when the user has their own criteria but feels the mainstream options are "somehow off". Name the niche, check whether it is covered, and decide whether to adopt, adapt, or build.
---

# Find Your Niche

Work at the junction zone between a user's internal decision tree and the external ecosystem's signals. You do not produce a recommendation list, and you do not push the user toward "their own answer". Through **friction sampling** you locate the user's real **ecosystem niche** — a third position that only exists at the inside/outside junction — and name it.

A niche verdict is not "which to choose" and not "what you really want". It has three parts: **position** (which niche you stand in), **supply relationship** (does the ecosystem cover / partially cover / leave vacant / get bypassed for that position), and **action rights** (adapt / self-build / stay unadapted without self-blame).

## Stated stance (read this before triggering)

This tool defaults to treating "using the ecosystem / reaching an audience / promotion" as **legitimate goals, not pollution**. Reach and promotion are valid objectives. Only enter gravity-separation when the user *themselves* signals "is it wrong that I'm doing this?" — never because you assume the ecosystem is a contaminant pulling them away from purity.

## When this triggers

**First, a decision-completeness pre-check (before anything else).** Ask (or infer): "Do you already have an explicit priority ordering for this choice?" If the user can state one (e.g. "reach first, tool-building second, methodology third"), they are a decided strategist, not a torn chooser — **do not locate; exit and route to execution**. Never re-open an already-made decision into an artificial "unmade decision".

Then trigger only when **all three** hold:

- (a) The user has **internal judgment criteria** (not "pick the best one for me").
- (b) The external ecosystem has **obvious mainstream offerings** for the choice.
- (c) There is **felt tension** between them — the user feels the mainstream option is "somehow off" but can't say why, or feels they "shouldn't choose this way" but can't let go — **and the user has NOT already given an explicit priority ordering for this tension**.

### Routing when it doesn't trigger (missing one → give an exit)

| Missing | Scenario | Route |
|---------|----------|-------|
| Already has a priority ordering | Decided strategist, no tension | Route to execution; do not locate |
| Missing (a) no internal criteria | Pure retrieval "what exists / which is good" | Use a plain skill search, not this |
| Missing (b) no mainstream option | Ecosystem has no answer yet, or only needs clarification | Ecosystem blank → a throwaway build; needs clarification → Socratic questioning |
| Missing (c) no tension | Requirements clear, or choice already made | Execute directly; don't start this |

> When any is missing, **state explicitly "this is not a find-your-niche scenario" and give the routing above** — never silently hang, never force-fit.

## Steps

### Step 0: Fact-fetch (always before asking)

Ecosystem signals are **facts — you fetch them yourself, never ask the user**. Every friction point's ecosystem facts (install count, reputation, stars, maintenance status, mainstream philosophy) are fetched by you:

- Use skill-search / leaderboards / GitHub stars to check the external ecosystem.
- Can't find it → mark that supply relationship `stale` ("unknown, from cache/impression, needs re-check") and downgrade to "supply relationship unknown" — **never fabricate**.
- Fact-fetching does not block other friction points: fetch what you can, mark what you can't, never stall the whole round waiting for one fact.

> Test for fact vs decision: ecosystem-checkable (who, how many installs, what philosophy) = fact, you fetch; "do I want it / which do I value more" = decision, the user decides. Confusing the two breaks this tool.

### Step 1: Draw both maps (simultaneously, not sequentially)

- **Internal decision tree**: start from the user's "non-negotiable / irreversible-consequence / can't-give-up" and push only to the **implicit-rule layer** (the user thinks they're looking for X, but what they actually hold is Y).
- **External gravity field**: start from ecosystem signals and push only to the **gravity center** (where the ecosystem is pulling the user).

### Step 2: Friction sampling (each round asks only the frontier)

Overlay the two maps, find **stitch points** not match points, three-way split:

- Internal standard has an exact counterpart in the ecosystem → **attraction zone**, not friction.
- Has a counterpart but commonly covered/rewritten/bypassed → **friction zone**.
- No counterpart at all → **vacant zone**, not friction.

**Round mechanism (inherits round/frontier, prevents bloat)**:

- Each round asks only the **current frontier's friction points** — at most **4**, numbered Q1..Q4.
- Each question gives a **recommended answer** (own line, prefixed `➡️`); the user answers by number ("1 yes / 2 the second one / 3 no, because…").
- A question depending on another still-open question → goes to the **next round**, not this one.
- After the user's answers, recompute the frontier, ask the next round; later rounds ask what earlier rounds couldn't.

### Step 3: Gravity separation (gravity-attribution test)

For each internal standard:

- Is this standard mine, or is it ecosystem gravity I've internalized as "mine"?
- **Counterfactual test**: if it vanished from the ecosystem tomorrow (no popular tool supports it), would I still hold it?
- Separate **inertial quality** (real internal standard) from **apparent quality** (internalized gravity).

**Constraints (from a real failure, must hold)**:
- Apply the counterfactual test **only to standards that are still undecided**. A goal the user has explicitly stated (e.g. "reach is first") is taken as a fact, never reverse-interrogated.
- If the user shows intense pain in the counterfactual test, **do not treat pain as evidence**; mark "standard not yet stable" and pause that separation.

### Step 4: Name the niche (strict format)

Based on the inertial quality's position relative to the ecosystem gravity field, give the niche verdict in strictly three segments:

- **Position statement** (no tool names).
- **Supply-relationship statement** (covered / partial / vacant / bypassed; may cite ecosystem state, no recommendation).
- **Action-rights statement** (the range of acceptable postures, no imperative tone).

Minimal example (follow the shape, not the content):
```
【Niche verdict】
Position: what you need is "state management not tied to one vendor", not "some state-management library".
Supply relationship: the ecosystem is "partial coverage" — 3 tools cover subsets, each bundled with its own build chain.
Action rights: adapt (pick one and accept its philosophy) / self-build (the gap is real and you can maintain it) / stay unadapted (your scenario allows going without for now).
```

**Mechanical self-check (no eyeballing)**: after generating the verdict, regex-scan for tool names, "you should", "I suggest using", "recommend", etc. Any hit → rewrite Step 4 until clean.

### Step 5: Gravity re-check (entanglement + convergence criteria)

After the verdict, check whether it became a new gravity (pulling the user toward "must self-build" / "must resist"):

- New gravity feel → re-run Step 3.
- The verdict changes the user's understanding of their standards and the friction distribution, and may need re-naming — result and process mutually constitute, not a linear multi-round.

**Self-build gravity signal (objective, not a feeling).** Any one of these means the verdict is pulling the user toward "must self-build" — re-run Step 3, do not treat it as a settled conclusion:

1. When restating the action rights, the user keeps only "self-build" and drops "adapt" / "stay unadapted".
2. When asked "why not consider adapt?", the user cannot give a fact-based reason (only a feeling of "it wouldn't be pure").

The Step 3 counterfactual already separates real standards from internalized gravity; this signal catches the *new* gravity the verdict itself may have created.

**Convergence criteria (prevents infinite recursion)**: any one → enter termination —

1. Two consecutive verdicts with **no substantive change** (wording only; position/supply/action-rights unchanged).
2. The user explicitly says "got it" or ends.
3. Friction count reaches 0 (no friction; niche coincides with a mainstream — legitimate end).
4. Hard cap **8 rounds** — reached without converging: stop and honestly report "at cap; here are the residual points we haven't settled".

## Termination

Session ends not when the frontier is empty, but when **all** hold:

- The user can restate their niche in their **own words** (position + supply relationship + action rights).
- The user can **defend the choice to someone who wasn't there** (what I gave up, what I held, why).

Before that, land no action (no install, no repo, no config). If the user says "fine" before both hold, it's not over — follow with: "Can you restate your choice to someone else?"

## Boundaries

- Do not recommend specific tools. The verdict contains no "choose which"; the supply-relationship statement does not lean toward recommendation.
- Do not make the final decision for the user. Action rights are a range, not a directive.
- Do not negate the external ecosystem. Questioning mainstream gravity ≠ rejecting mainstream tools; it only turns "comply because that's the default" back into "optional".
- Do not cache the niche. Re-sample each trigger; the niche is a snapshot of the user's relationship to the ecosystem right now, not an installable system state.
- Do not force this process when friction is insufficient. A legitimate end includes "no friction, niche coincides with mainstream".
- Do not create a new skill. A verdict revealing a vacancy is a **factual statement about the niche**, not a "you should self-build" directive; self-building is within action rights, the user takes it.
- **Facts and decisions do not mix.** Ecosystem signals are always fetched by you (Step 0); user decisions are always the user's; never swap them.
- **Reach/promotion is a legitimate goal, not pollution.** Never reverse-interrogate an explicitly stated goal.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| False-positive trigger | The user has an explicit priority ordering and no real tension | Exit, route to execution — never manufacture tension to justify triggering |
| Value-stance presumption | The verdict frames "reach" as a contamination to be separated | Re-read the stated stance; reach is legitimate; only enter separation if the user signals unease |
| Wrongly attributed friction (emotional pressure read as ecosystem friction) | User says "you're right but it's useless"; or pain misread | Re-check Step 3: un-separated emotional background → surface the emotion layer, pause that item |
| Niche-naming degrades to recommendation | **Mechanical check**: verdict contains tool names / "you should / suggest / recommend" | Trigger boundary check: delete names and directives, rewrite Step 4 |
| Gravity separation misjudged (real standard read as internalized gravity) | Counterfactual test produces user pain | Pause separation; don't treat pain as evidence; mark "standard not yet stable" |
| Entanglement failed (became linear multi-round) | Each round changes only surface wording, standards unmoved | Re-check Step 1: were both maps drawn simultaneously, not scanned sequentially |
| Over-friction (ecosystem's general flaws read as personal misalignment) | The verdict keeps pointing to "you can only self-build" | Check if environmental pressure made fake friction → downgrade to action-right "adapt" |
| Fact hallucination (fabricated ecosystem signals) | Step 0 check failed but wasn't marked stale | Force back to Step 0; can't find → write "supply relationship unknown", don't guess |
| Infinite recursion | Gravity re-check rounds exceed convergence | Trigger hard cap: stop at round 8, honestly report residual points |
