---
name: find-right-skill
description: 'Find the right skill when the user asks "is there a skill for X" or "how do I do X" and X is ambiguous or unfamiliar. Search and question in one motion: each found skill becomes a question, each answer reshapes the search, until the user decides to accept, adapt, or create.'
---

# Find Right Skill

The user believes they need a skill. That belief is a design tree they have not yet drawn. The ecosystem is the evidence you will use to question that tree.

Do not search in order to recommend. Do not interview in order to clarify. Search and interview are one motion: each skill you find becomes a question you ask, each answer the user gives reshapes what you search next. The goal is not to find a skill. The goal is to locate where the user's real need sits inside the skill ecosystem — then hold them there until they decide whether to **accept**, **adapt**, or **create**.

## When this triggers

- User asks "is there a skill for X" where X could be named wrongly, too broadly, or is absent from the mainstream
- User asks "how do I do X" where X is a capability with contested philosophies (e.g. testing, design, performance)
- Any time a plain skill search alone would return an answer without exposing the design decision behind the request
- Any time Socratic questioning alone would ask questions the user cannot answer because they don't know what already exists in the ecosystem

## The focus loop

Search and questioning run every round as a single entangled act, not sequential steps.

**1. Map the frontier.** Start from the user's statement. Before you search, draw one layer of the design tree: the decisions *above* their request. What is X for? What is the adjacent need upstream? What does X compete with? These are not questions yet — they are search targets.

**2. Illuminate.** Search the ecosystem for each frontier node in parallel: a skill-search command, the leaderboard, stars, source reputation. Treat every result — presence, absence, popularity, philosophy — as evidence, not a recommendation.

**3. Ask at the points of friction.** Where the tree and the ecosystem do not align, there is a decision the user has not made. Ask the frontier questions in a Socratic-questioning format, with recommendations that point at the friction, not the smoothest answer:

```
❓ **Q1** — **<title>**: The ecosystem has X (185K installs, mainstream philosophy). Your stated need sits slightly beside it. Either you haven't named your real need, or you've found a genuine edge. Which is it?

➡️ <recommended answer>
```

**4. Re-shape and repeat.** The user's answers settle frontier nodes. New nodes appear. Restart the loop: new frontier → new searches → new frictions. Later rounds search differently because earlier answers did not just clarify need — they re-named it.

## The illuminate primitive

This is the core operation. A search result is never shown to the user as a verdict. It is *used against* the frontier node that generated it:

- **Exact match, high installs, reputable source** → Ask: "You may have been shaped by the ecosystem. Is this skill your need, or just the most visible name for it?" If the answer is "it's fine," you have exposed an untested assumption — the user must answer it either way.
- **Near match, wrong philosophy** → Ask: "There is a mainstream answer, but it optimizes for a different value. Which of those values is actually yours?" This is not a quality question. Install count is not trust here; it is a measure of how much pressure the ecosystem will put on the user to conform.
- **No match** → Ask: "The ecosystem lacks this. Either your request is misnamed, or it is a real gap. If you can't tell which, I will search the adjacent branches and show you the shape of what *does* exist. That shape is your evidence."
- **Many contested matches** → Stop recommending. Show the user the *map*: who built each skill, what design philosophy it embodies, how the ecosystem is split. Then ask: "Your position in this split is a decision you've been avoiding. Which side are you on — and on what basis?"

The user cannot answer these from introspection alone. They need the ecosystem as a mirror. That is why this skill is neither pure search nor pure interview: the search creates the mirror; the interview holds them still in front of it.

## Fiction vs. Decision

Facts are the ecosystem. You gather them. Never ask the user "what exists out there."

Decisions are the user's. Never answer them for the user. Showing a search result and saying "you should use this" is answering their decision.

The third category — **friction facts** — is what this skill alone produces. A friction fact is a discrepancy between the user's stated need and the ecosystem's shape. You do not resolve it. You put it before the user as a question. Only they can resolve it; you can only make the resolution impossible to avoid.

## Termination

The loop ends when no frontier node remains unilluminated — every branch of the user's design tree has been held against the ecosystem and a discrepancy was either resolved or accepted as real.

At that point, produce one final frame. It is neither a recommendation list nor a shared-understanding statement. It is the **niche verdict**:

- **Accept**: the ecosystem's shape aligns with the user's need. The user adopts a mainstream skill with full awareness of the alignment, not because search ranked it first.
- **Adapt**: the user needs an existing skill but must modify it, choose a non-default variant, or accept a partial mismatch. The user leaves knowing exactly where the adaptation occurs — one branch of the tree could be met by the ecosystem; another branch is the user's own divergence.
- **Create**: the user's need is a genuine gap. They now know what surrounds the gap, what designs failed to produce a match, and why their request was misnamed or genuinely new. They leave with the shape of the thing to build.

Ask for confirmation before acting on any of these. The session ends when the user can name their choice and defend it against someone who wasn't there.

## Minimal example

User: "Is there a skill for code review?"

Do not return the first search result. Map one layer up: the user wants pull requests reviewed without depending on a human bottleneck. Adjacent branches include static analysis, test generation, and review automation.

Search those branches. Suppose the mainstream result is a GitHub-only review skill with high installs. Put the friction in front of the user:

```
The mainstream skill assumes GitHub-only workflows. Your stated need sits beside it.
Either you are willing to adopt GitHub-specific automation, or you need a review
workflow that keeps working in GitLab. Which is the real requirement?
```

Use the answer to reshape the next search. End with an accept, adapt, or create verdict, and require the user to state what they gained and gave up.

## Boundaries

- Do not recommend a skill as a substitute for the decision. A high-install skill is not evidence of fit; it is evidence of pressure. Present it as such.
- Do not allow the session to end at "that looks good." Verify the alignment claim: what value is being traded away by choosing the mainstream option? What edge is claimed by rejecting it? The user must be able to state what they gain and what they give up.
- Do not answer your own frontier questions. A friction fact you resolve silently is a decision stolen from the user.
- Do not keep searching when no further search can change the frontier. If new queries only return repeats, the remaining uncertainty lies in the user, not the ecosystem. Ask directly.

## Failure modes

| Symptom | Diagnosis | Recovery |
|---------|-----------|----------|
| User accepts every recommendation without friction | You stopped questioning. You are in plain-search mode, not question mode | Reopen the design tree on the decision you just rushed past. Ask what was traded away. |
| Session never progresses, searches keep branching | You are treating the ecosystem as the source of decisions instead of evidence. You are in pure-questioning mode with extra steps | Stop searching. Return to the user's latest answer and ask: what did it decide? Then re-search only on that. |
| User says "I don't care, just install anything" | They are refusing to own the decision | Do not install. Name the choice they are avoiding: choose the mainstream and absorb its philosophy, or fight it. Explain that "anything" means outsourcing a design decision they will have to live with. |
| The ecosystem has a perfect match and the session still feels empty | The real decision was upstream of the skill request, outside the ecosystem entirely | Ask what X is for, one layer up. Search that. The skill request was a proxy. |

## It works when

- A search result becomes a question, not an answer
- The user disagrees with at least one recommendation — because you pushed at a real friction
- Later searches differ from earlier ones because the user re-named what they needed
- The final verdict — accept, adapt, create — is a decision the user has made, not one you made for them
- The user leaves knowing not just which skill they chose, but where their need sits in the ecosystem and why the shape was what it was
