---
name: know-what-evidence-allows
description: Decide what a piece of evidence lets you say and do — before you over-claim. Use when the user hands you a correlation and wants to predict, explain, intervene, or attribute cause.
---

# Know What Evidence Allows

Most debates about correlation and causation ask "is this correlation or causation?" — a question about what the world is. This skill asks a different question: **what does this evidence allow you to do?** It does not compute a correlation coefficient and it does not draw a causal graph. It couples five parameters — evidence level, conclusion type, confounder status, action cost, reversibility — into a license level, and outputs what is allowed, what is blocked, and what is missing to move up.

## When this triggers

- The user presents an X–Y association and asks to predict, explain, intervene, attribute, or take an irreversible action.
- The system must decide "can we say because" or "can we decide from this data".
- The evidence level clearly does not match the conclusion being claimed, but the user hasn't noticed.

## Input parameters

| Parameter | Candidate values |
|-----------|------------------|
| `evidence_level` | `covariation` / `intervention` / `counterfactual` / `layered` |
| `goal_type` | `predict` / `explain` / `intervene` / `attribute` |
| `confounder_status` | `ignored` / `modeled` / `controlled` / `unknown` |
| `action_cost` | `low` / `medium` / `high` |
| `reversibility` | `reversible` / `semi_reversible` / `irreversible` |

## The license ladder

| Level | Evidence level | Confounder status | Cost / reversibility | Allowed | Blocked |
|-------|---------------|-------------------|----------------------|---------|---------|
| `FROZEN` | covariation | unknown / suspected | any | describe "they move together" only | external prediction, attribution, action |
| `L0` | covariation | uncontrolled but reviewable | low / reversible | internal prediction, reversible probe | public causal claim, irreversible action |
| `L1` | covariation + domain/temporal/dose constraints | controlled or negligible | medium / semi-reversible | prediction, A/B test, rollback-able intervention | "because" claims, irreversible action |
| `L2` | intervention / natural experiment | explicitly modeled | medium-high / semi-reversible | average causal effect, "because", medium-cost action | individual counterfactual attribution |
| `L3` | counterfactual / structural model | identified and controlled | high / irreversible | individual explanation, irreversible decision, policy | nothing absolutely blocked; uncertainty must be recorded |

## Steps

1. **Pin the evidence level** — covariation, intervention, or counterfactual. If you can't tell, downgrade to `FROZEN`.

2. **Read the goal type** — predict, explain, intervene, or attribute.

3. **Read cost and reversibility** — higher cost and lower reversibility demand a higher license. Low-cost reversible actions may probe at a low evidence level; high-cost irreversible actions require `L2` or `L3`.

4. **Downgrade for confounders** — if `confounder_status` is `unknown` or `ignored`, treat the evidence as `covariation` even if intervention data exists. If confounders are explicitly modeled and controlled, allow the evidence level to recover.

5. **Issue the license** — output the level, allowed conclusions, blocked conclusions. If the goal needs a higher license than the evidence supports, do not downgrade the license to please the user; give the minimal upgrade path instead.

6. **Give the upgrade path** — e.g. `L0`→`L1`: add temporal, dose, or domain-mechanism constraints; `L1`→`L2`: run a do(X) intervention, natural experiment, instrument, or regression discontinuity; `L2`→`L3`: build a counterfactual or structural model.

## Walkthrough example

**Input**: a team finds that "share of users using dark mode" correlates with "next-day retention" (r = 0.31), and wants to permanently set dark mode as the default and publicly announce "dark mode improves retention".

**Parameter collection**:
- `evidence_level = covariation` (observational correlation, no intervention)
- `goal_type = intervene` (change the product) and `attribute` (publicly claim "because")
- `confounder_status = unknown` (dark-mode users may be heavier users, who retain better anyway)
- `action_cost = high` (permanent default change affecting all users)
- `reversibility = semi_reversible` (revertible, but with churn and reputation cost)

**Decision**:
1. covariation + unknown confounders → ceiling is `L0`/`FROZEN`
2. goal needs intervene + attribute, high cost, semi-reversible → needs `L2`+
3. ceiling (L0) is far below requirement (L2) → **deny, do not downgrade**

**Output**:
```json
{
  "license": "FROZEN",
  "can_say_because": false,
  "allowed_actions": ["describe_covariation"],
  "blocked_actions": ["default_theme_change", "public_causal_claim", "irreversible_action"],
  "confounder_status": "unknown",
  "minimal_upgrade": "Run an A/B test (randomly assign dark/light default, control for heavy-user mixing) → if the intervention group's retention rises significantly with confounders modeled, upgrade to L2"
}
```

The skill does not say "correlation is not causation" (a warning about the world), and it does not decide for the team. It **revokes the license for the irreversible action at the current evidence level** and hands back the single upgrade path.

## Output format

```json
{
  "license": "...",
  "can_say_because": false,
  "allowed_actions": [...],
  "blocked_actions": [...],
  "confounder_status": "...",
  "minimal_upgrade": "..."
}
```

## Boundaries

- Do not compute a correlation coefficient or build a causal graph; do not replace statistical software.
- Do not replace domain-expert judgment; only decide the license level for the given evidence.
- When the evidence level is unclear, the goal is unclear, or the action is high-cost and irreversible, default to denying a high-level license.
- Do not change the license level to satisfy user preference; only more evidence or a different action design can raise it.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Slips into "correlation = causation" | Output is only yes/no with no license level | Force return to the license ladder, require level + cost |
| Causal license with uncontrolled confounders | confounder unknown/ignored but L2+ output | Auto-downgrade to L0/FROZEN, mark `confounder_frozen` |
| High-cost action on covariation only | action_cost=high and evidence=covariation | Block irreversible action, require intervention/counterfactual evidence |
| Prediction over-demanded causal evidence | goal=predict but counterfactual required | Allow L0/L1 prediction license, mark "predicts, does not explain" |
| Goal type unreadable | goal_type missing | Default to highest-risk handling, issue FROZEN/L0 only |
| Confounders controlled but level not restored | modeled confounders still treated as covariation | Allow upgrade to L1/L2, note the control method |
