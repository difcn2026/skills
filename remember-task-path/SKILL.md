---
name: remember-task-path
description: Remember the path a task took and replay it for similar future tasks to save tokens. Use when the same type of task repeats and each repetition should cost less than the first. Compress a run into an entry anchor plus decision markers, and re-verify each step while replaying.
---

# Remember Task Path

Compress a completed task run into a **path triple**: `[entry anchor] → [decision-path markers] → [cost and result]`. When a similar task arrives, hit the entry anchor first, then replay the path while re-verifying each step as you go. You remember the path, and recall the next step.

## When this triggers

Any **one** of these signals triggers a recall attempt:

1. On task arrival, the **entry anchor** matches a path already in the ledger (task type + first module/file touched).
2. During execution, token consumption deviates ≥ 30% from baseline (baseline = the first direct-run measurement).
3. After a task completes, the compressed path structure is ≥ 0.7 similar to a ledger path.

## Entry anchor matching (the core mechanism)

The entry anchor is two fields available **at task start** (you don't need to finish the run to get them):

```
entry anchor = ( task type , first module/file touched )
e.g. a service alert → ( diagnose , rate-limit-config )
```

**Anchor tolerance (the "first file" field may drift).** The same task type may not always touch the *same* first file — e.g. a diagnosis run sometimes starts at the config file, sometimes at a cached snapshot. Matching rule:

- Exact match on `task type` is required.
- The `first module/file` field is a strong hint, not a hard key: if it drifts, fall back to matching on `task type + key resource identity` (the object the task is really about, e.g. "the rate-limiter", not "which file was opened first").
- If the fallback also can't disambiguate, treat it as **no hit** and run direct — do not force a match.

A false anchor hit is already contained by the first-node verification (first replay node fails → immediate direct run), so tolerance only widens recall; it never risks leading down a wrong path silently.

Matching flow:

1. Task arrives → extract the entry anchor → find candidate paths with the same anchor in the ledger.
2. Hit found → enter **replay mode**, without committing to complete it.
3. **Before each node executes, verify**: "Does this node still hold for the current task?"
   - Holds → continue replaying that node.
   - Doesn't → **exit replay immediately, switch to direct run** (walk the rest yourself).
4. Result: the recall decision is *before-the-fact* (entry anchor), path completeness is *verified as you go* — no more "matches too late".

## Quality state (process signal, not verdict)

Every task gets an objective positive/negative signal, so diagnosis/exploration tasks can self-heal too:

| State | Criterion (process signal, objective) | Self-heal action |
|-------|---------------------------------------|------------------|
| `walked-through` | Reached path exit + produced a reviewable conclusion + no fallback triggered | ✅ Raise this path's recall priority |
| `diverged` | Fallback / retry / stuck / manual intervention triggered mid-run | ✅ Mark `diverged`, lower priority |

The "success" of a diagnosis/exploration task is **not** "the result is absolutely correct" (can't be auto-scored) — it's "**walked through, didn't get stuck, produced a reviewable conclusion**". That is objectively observable, and self-healing works in both directions.

## Savings — a sort weight, not a gate

Savings = baseline − actual. This drifts when task difficulty drifts, so it is **not a hard gate for ledger admission**, only a sort weight.

```
Ledger admission hard condition (process-signal-driven):
  → quality state = walked-through (path completed, no fallback)
Sort weight (soft signal, only for priority among same-anchor paths):
  → measured savings = baseline − actual (reference only, not admission)
```

**Invariant**: the first path never saves; savings start from the second run. Whether it saves does not decide whether it's admitted — only whether it sorts earlier or later.

## Core loop (three streams)

**Stream A — entry match + verify-as-you-go**
1. Task arrives → extract entry anchor → find same-anchor candidates.
2. Hit → replay mode, verify each node before executing, switch to direct run if a node fails.
3. No hit → direct run, record baseline.

**Stream B — path compression**
1. Task completes → trace → identify key decision points → compress to path markers `[entry]→[locate]→[reuse]→[verify]→[exit]`.
2. Quality state = `walked-through` → admitted; `diverged` → not admitted (or kept as a counter-example).

**Stream C — cost audit + recall self-heal**
1. After replay, measure actual tokens + quality state.
2. `diverged` → re-compress.
3. `walked-through` and tokens below baseline → raise priority (savings as soft weight).

## Where correctness comes from

**Memory IS recall** — a path is both remembered as valid (`walked-through`) and audited as economical (measured savings > 0). Double verification closes the loop.

## Failure exits

| Failure | Detect | Recover |
|---------|--------|---------|
| Stale path | A replay node fails verification / state `diverged` | Switch to direct run from that node; two consecutive `diverged` → remove from recall table |
| False anchor hit | Same anchor but path diverges quickly | First replay node fails → immediate direct run, cost is contained |
| Ledger becomes a token burden | Retrieval cost > average single-run savings | Thin the ledger to top-200 |
| Savings inflation | 3 consecutive replays with actual tokens ≥ baseline | Zero that path's savings weight (keep it, only lower priority) |

**Ultimate fallback**: any path with two consecutive `diverged` → removed from the recall table; that anchor's tasks return to direct run.

## Degradation thresholds

| Parameter | Value |
|-----------|-------|
| Structural similarity hit threshold | **0.7** (on false hits, raise by 0.05, up to 0.9) |
| Ledger capacity | **top-200** |
| Token deviation trigger | ≥ **30%** |
| Priority lowering | one `diverged` ×0.5; two consecutive → remove from table |

## Safety boundaries

- Path markers never write raw keys / tokens / user data — only location anchors + decision type.
- The path ledger is append-only; `diverged` lowers priority, never deletes.
- Only admit `walked-through` paths (`diverged` paths not admitted, or kept as counter-examples).
- Replay skips only redundant reasoning — it never skips permissions, credentials, or input validation.

## Input / output

**Input**: task entry anchor, execution trace, first direct-run baseline, quality state (walked-through / diverged).
**Output**: `path_ledger.jsonl` (path triples + measured savings history + quality state), recall decision `recall`/`no_recall`, path health report.
