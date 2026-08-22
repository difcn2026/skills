---
name: calibrate-your-forecast
description: Know how accurate your judgments really are — not by waiting for a long track record, not by trusting your gut. Use when you give a confident prediction and want to make your own blind spot visible after the result lands — 当你说「我 80% 确定」、结果落地后想检验自己到底准不准、或总在没料到的地方翻车时。
---

# Calibrate Your Forecast

Two things are true about your confident judgments, and together they form a trap. One: every prediction *can* be scored — attach a probability, then let the actual outcome settle whether you were right. Two: your subjective confidence is *systematically* higher than your real accuracy, and — this is the trap — **you cannot see this bias from the inside**. The more sure you feel, the more likely you are wrong about *how* sure you are, and the feeling itself hides the error.

The usual advice fails on both ends. "Keep a track record and you'll get calibrated over the long run" only works after hundreds of predictions you never actually log. "Don't be overconfident" is a warning you cannot act on, because the bias is precisely that you don't notice it. This skill closes the gap: **you don't need a long track record, and you don't need self-awareness.** You need to plant three anchors the moment you make a judgment, then perform an autopsy the moment the result lands.

## When this triggers

Enter when **any** of these holds:

1. You state a confidence level — "I'm 80% sure", "this will definitely happen", "no way this fails".
2. You make a prediction whose outcome can be checked against data on a specific date.
3. You keep being wrong in ways you didn't expect, and want to know *why* the surprise keeps happening.
4. Someone (or you) wants to know "how good is my judgment, actually?" — not as a vague feeling, but as a number.

Do **not** enter when the judgment cannot be falsified on a concrete date, or when you already have a long-running scoring system (then you're doing superforecasting, not a single-judgment autopsy).

## Steps

### 1. Plant the anchor (the moment you judge)

When you make a judgment that carries a confidence level, write it down in this exact shape:

```
[Judgment]  [a specific, falsifiable claim]
[Confidence] [0-100%]
[Counterfactual anchor] If I'm wrong, the most likely failure point is: [one concrete, checkable step]
[Surprise budget] If the opposite happens, my surprise should be [0-10]
[Surprise tell] If the opposite happens, my first observable reaction will be: [a checkable behavior, e.g. "open the X report first"]
[Timestamp] [when you judged]
[Backfill date] [when the result lands]
```

Two hard rules:
- The counterfactual anchor must be a **concrete, checkable step** — never "bad luck" or "the market". It must name a specific link you believe is the weak one.
- The surprise tell must be an **observable behavior**, not an emotion. "I'd be very surprised" is the surprise budget's job; the tell is its objective witness. Write something you can check after the fact.

### 2. Perform the autopsy (the moment the result lands)

Look only at what you *wrote down then*, never at what you *think now*. Work through each organ:

```
[Outcome] [what actually happened]
[Organ 1 — probability]  Confidence X% vs outcome:
  - right → record (1, X)
  - wrong → record (0, X)
[Organ 2 — counterfactual anchor]  Did the step you named actually break? (use counterfactual elimination, below)
[Organ 3 — surprise]  Budget [Y]/10 vs actual [Z]/10 (record within 1 hour of the outcome):
  - surprise tell happened: [yes/no]
  - gap: |Y-Z|
[Autopsy verdict] [one sentence: what shape did your blind spot take this time]
```

#### Counterfactual elimination for Organ 2

When the outcome went wrong, don't decide the "real cause" from memory. Mechanically separate it:

```
1. List every candidate cause that could explain the failure (including the one you anchored).
2. For each candidate C, ask: "If C had NOT happened, would the outcome still have failed?"
   - If no (C is necessary, NEC) → C is a real cause
   - If yes (C is only correlated) → C is not the real cause
3. Hit judgment:
   - your anchored step is NEC → hit (h=1)
   - your anchored step is not NEC, but another NEC exists → miss (h=0, blind spot elsewhere)
   - several causes are jointly necessary (no single NEC) → record "jointly necessary"; hit = whether your anchor is inside that set
```

If the failure has no separable causal steps (pure randomness), record `h=NA` and do not force an arbitration.

### 3. Name the blind spot (right after the autopsy)

Give the exposed blind spot a concrete name:

```
[Blind spot type]
  - anchor misalignment: the step you named was not the NEC that actually broke
  - surprise incontinence: actual surprise far exceeded budget — you can't even predict your own reaction
  - probability inflation: your confidence number runs systematically higher than your hit rate
  - anchor absence: you couldn't name any counterfactual step — your judgment has no structure
  - custom: [describe]
[Next intervention] [what specifically you'll do differently on the next judgment]
```

---

## Measuring "how sure I felt" vs "how right I was" — mechanically

No subjective assessment anywhere in this chain.

### Collect

Each autopsy yields one record: `(p, r, h, s)`
- `p` — stated confidence (0–1)
- `r` — outcome right/wrong (0 or 1)
- `h` — anchor hit (0/1/NA; meaningful only when r=0)
- `s` — surprise gap (0–10)

### Compute three mechanical indicators

| Indicator | Formula | Reading |
|-----------|---------|---------|
| **Calibration Bias** | `CB = mean(p) − mean(r)` | positive = overconfident; negative = underconfident; 0 = calibrated |
| **Anchor Hit Rate** | `AHR = sum(h) / count(r=0 and h≠NA)` | of your wrong calls, how often was your named weak point the real cause? low = your blind spot is deeper than you think |
| **Surprise Miscalibration** | `SM = mean(s)` | high = you can't even predict your own emotional reaction |

### Roll up every 10 autopsies

```
[Window] [date range]
[N] [number of judgments]
[Calibration Bias] CB = [value] → > 0.1 = "probability inflation"; < −0.1 = "probability deflation"
[Anchor Hit Rate] AHR = [value] → < 0.5 = "anchor misalignment"; ≥ 0.5 = "anchor effective"
[Surprise Miscalibration] SM = [value] → > 2 = "surprise incontinence"
[Diagnosis] [one sentence: what your bias looks like and what to change next time]
```

### Verify the core assumption ("you can't see your own bias")

```
1. Before any autopsy, ask: "what do you think your calibration bias is?" → record CB_self
2. Run the autopsies, compute the mechanical CB_actual
3. Compute |CB_self − CB_actual|
4. If > 0.1 → the "you can't see it" assumption holds; your estimate of your own bias is itself miscalibrated
5. Record the gap as the Blind Spot Visibility Index (BSVI)
```

---

## Worked example

### Scenario: an analyst predicts "feature X will pass 10k DAU by Sep 14"

#### Plant the anchor (Aug 14)

```
[Judgment] Feature X will exceed 10,000 DAU on 2026-09-14
[Confidence] 80%
[Counterfactual anchor] If wrong, most likely failure: new-user onboarding completion falls below 40%, so new users can't push DAU over 10k
[Surprise budget] 6/10
[Surprise tell] First reaction if it fails: open the growth dashboard and check the "new users" line first
[Timestamp] 2026-08-14
[Backfill date] 2026-09-14
```

#### Autopsy (Sep 14)

```
[Outcome] DAU = 8,200 — failed
[Organ 1] said 80%, wrong → (0, 0.80)
[Organ 2] counterfactual elimination:
  candidate A = onboarding completion (anchored)
  candidate B = next-day retention among existing users dropped
  test A: if onboarding had held ≥40%, would it have passed 10k? → no (retention still dropping) → A not NEC
  test B: if retention had held, would it have passed? → yes → B is NEC
  → anchored A is not NEC, real NEC is B → miss (h=0)
[Organ 3] budget 6/10, actual 8/10, gap 2; surprise tell: yes, I opened the growth dashboard and checked "new users" first
[Verdict] anchor pointed at acquisition, real cause was retention — I'm systematically blind to retention-side decay
```

#### Name the blind spot

```
[Blind spot] anchor misalignment (acquisition ≠ NEC, retention is)
[Next intervention] for growth judgments, the counterfactual anchor must cover BOTH acquisition and retention — never name only one
```

---

## Boundaries

- **Not long-term tracking** — this does a single-judgment autopsy. If you want a calibrated long-run curve, use a full superforecasting scoring system.
- **Not group statistics** — this doesn't answer "are humans systematically overconfident". It answers "what did *this* judgment's bias look like".
- **Not a decision tool** — it doesn't tell you whether to make the call. It shows you what you couldn't see, after you made it.
- **Not for unfalsifiable claims** — if the judgment can't be checked against data on a concrete date, this doesn't apply.
- **No forced arbitration on non-attributable outcomes** — if the failure has no separable causal steps, record `h=NA` and stop.

## Failure modes and recovery

| Failure | Detect | Recover |
|---------|--------|---------|
| Anchor is unfalsifiable | contains "maybe", "roughly", "luck" | reject the anchor, demand a concrete checkable step |
| Memory tampering at autopsy | "what I actually meant was…" | only the written anchor counts, never post-hoc memory |
| Surprise rationalized afterward | "I wasn't *that* surprised" | surprise must be recorded within 1 hour; also cross-check the surprise tell |
| Surprise tell also unreliable | the written tell didn't happen but self-reported surprise is high | treat "did the tell happen" as hard evidence; on conflict mark `surprise_unreliable` and exclude that gap from SM |
| Sample too small | N < 10 | mark `insufficient_data`, keep accumulating, no diagnosis yet |
| Anchor hit rate inflated | anchor written vague enough to almost always "hit" | anchor must contain a quantifiable threshold, else reject |
| Arbitration breaks down | causes are jointly necessary, no single NEC | record "jointly necessary", hit = whether anchor is inside the set; don't force a binary |
