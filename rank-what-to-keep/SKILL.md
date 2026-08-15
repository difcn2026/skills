---
name: rank-what-to-keep
description: Rank mutually-exclusive options without scoring them — by carrying each defeated option into its winner, so the final choice makes every sacrifice worth it. Use when you must keep only one of several candidates but cannot score them.
---

# Rank What to Keep

When several options are mutually exclusive and none can be scored, two usual moves fail: scoring them anyway (fake precision) and comparing "which one hurts less to lose" (ignoring what the losers become). This skill does neither. It ranks not the options, but **the composite beings that carry the weight of everything they defeated**. The winner is not "the most important" — it is the one whose survival makes every sacrifice worth it.

## When this triggers

- You face ≥3 mutually-exclusive candidates and must rank them.
- You cannot assign any candidate an "intrinsic importance" score — scoring would only manufacture false precision.
- You can sense "the cost of giving up each candidate" but cannot put an absolute value on it.
- What you really want to ask is: "which one should survive, so that the others' sacrifice wasn't wasted?"

## The core mechanism

When candidate W beats candidate S in a comparison, S does not disappear. S is **inscribed** onto W:

```
W ← W + S
```

W is no longer the original W. It becomes "W at the cost of S". The next round compares not tasks, but **composite beings carrying chains of sacrifice**.

## Steps

1. **Build a no-property pool** — put all candidates in. No pre-scoring, no intrinsic properties. Candidates have only identities: A, B, C, D…

2. **First-round pairing** — take one pair, ask the single comparison question:
   > "If you could keep only one, which would you be less sorry to give up?"
   The one you're less sorry to give up = loser S. The other = winner W. S is inscribed onto W:
   ```
   W₁ = W + [S]
   ```

3. **Next round: compare beings, not tasks** — the sacrifice-carrying W₁ returns to the pool. Continue pairing, but the question changes:
   > "Two beings exist — whose continued existence wastes less?"
   What is compared is not "task A vs task B" but "B carrying A vs D carrying C".

4. **Iterate inscription** — each round, the loser is inscribed whole (including its own sub-chain) into the winner:
   ```
   winner = winner + [loser + loser's entire sub-chain]
   ```

5. **Stop and produce** — stop when one being remains, or a preset round cap is reached. The output is not a ranked table, not an opportunity-cost ledger, but a **sacrifice genealogy** — a nested elimination tree.

## The ranking basis: sacrifice inertia

A being's sacrifice inertia = its own chain depth + the weight of each being it sacrificed.

**"Weight" defined (operational)**: a sacrificed being's weight = the length of the sacrifice chain it had already accumulated before being sacrificed (i.e., how many others it had itself sacrificed).

```
B₂ = B + [A (weight 0), C₁ (weight 1)]
C₁ = C + [D (weight 0)]
A  = A (no chain, weight 0)
D  = D (no chain, weight 0)

Sacrifice inertia:
A  = 0 + 0 = 0
D  = 0 + 0 = 0
C₁ = 1 (chain depth 1) + 0 = 1
B₂ = 2 (chain depth 2) + (A's 0 + C₁'s 1) = 3
```

**Ranking**: B₂ (3) > C₁ (1) > A (0) = D (0).

- Deepest = B₂, the final survivor, carrying every sacrifice.
- Next = C₁, the being directly sacrificed by the final survivor.
- Shallow = A, D — early-sacrificed, chain-less candidates.

## Output shape: the sacrifice genealogy

```
B₂  ===  B + [ A, C₁ ]
  C₁ ===  C + [ D ]
  A   ===  A (no chain)
  D   ===  D (no chain)
```

No candidate is deleted. They are sacrificed, but continue to exist inside the ranking as inscriptions. This is the fundamental difference from a plain elimination bracket — **a bracket discards losers; sacrifice inscription turns losers into the winner's structure.**

**Every output must end with this mandatory note (never omit it):**
> ────────────────────────────────
> This ranking measures sacrifice inertia (a path-dependent product),
> not intrinsic importance. It answers "whose survival keeps past sacrifices
> from being wasted", not "who is objectively more important".
> Do not use it as evidence of who is "more important".
> ────────────────────────────────

## Worked example

A product manager faces five feature candidates (A/B/C/D/E), cannot score them, must ship one.

- A vs E: less sorry to give up E → E inscribed into A.
- B vs D: less sorry to give up D → D inscribed into B.
- C vs A₁ (A carrying E): whose existence wastes less? C loses → C inscribed into A₁. A₂ = A + [E, C].
- B₁ vs A₂: whose existence wastes less? B₁ loses → B₁ (carrying D) inscribed into A₂. A₃ = A + [E, C, B+[D]].

A₃ tops the ranking — not because it is "most important", but because it carries the most sacrifice: giving it up would waste the sacrifices of E, C, B, and D all at once.

**That is sacrifice inertia.**

## Boundaries

- Do not predict the future; this handles only the current ranking.
- Do not require candidates to have intrinsic properties; if you can score objectively, a scoring matrix is more appropriate — but this skill does not assume that objectivity exists.
- Not for binary choices; with only two candidates, a direct opportunity-cost comparison is simpler.
- Do not auto-execute; the ranking needs human confirmation — sacrifice inertia is path-dependent, not objective truth.

## Counter (recovery table)

| Failure | Detect | Recover |
|---------|--------|---------|
| Sacrifice chain overload | Chain depth > 5, unreadable | Extract a "sacrifice summary" — keep only the heaviest sacrifice per level |
| Initial-pairing bias | Final ranking over-sensitive to initial pairing | Run 2–3 paths with different initial pairings, take the stable intersection |
| Comparison fatigue | >10 candidates, comparisons explode | Cluster first, then inscribe within clusters |
| Sacrifice inertia misused | "accumulated sacrifice" treated as "intrinsic importance" | Emphasize: sacrifice inertia is path-dependent, not an objective property of the candidate |
