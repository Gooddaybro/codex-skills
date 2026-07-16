# Review Rubric

Use this reference after each learner attempt.

## Review Order

1. Observable behavior and test evidence.
2. Control flow, state, and business decisions.
3. Failure behavior and boundaries.
4. Decomposition and naming.
5. Style.

Do not rewrite the whole solution when a focused correction is enough.

## Error Categories

| Category | Meaning |
| --- | --- |
| syntax/API | Language syntax or library/API usage is missing or incorrect |
| control flow/order | Branching, sequencing, loops, or early exits are wrong |
| data/state | Input modeling, mutation, returned state, or persistence is wrong |
| business rule | Domain decision does not match the requirement |
| system boundary | Ownership, dependency direction, failure policy, or integration boundary is wrong |
| testing/observability | Verification misses important behavior or evidence |
| decomposition | Responsibilities or interfaces make the flow hard to change or test |
| prerequisite | A smaller concept must be repaired before continuing |
| oversight | Learner understands the rule but omitted it accidentally |

## Correction Record

Use:

```text
Observed mismatch:
Learner's expected behavior and reason:
Category:
Correct model:
Smallest learner-owned rewrite:
Verification to rerun:
```

Ask why before prescribing the fix. Repair the mental model, then have the learner rewrite the smallest affected area.

## Hint Ladder

Escalate one rung per attempt:

```text
question -> constraint -> relevant API reminder -> flow -> pseudocode -> minimal code fragment
```

Do not jump rungs because giving the solution is faster. If the learner explicitly abandons learning mode, state that the mastery gate is ending before providing complete target code.

## Evidence Gates

| Gate | Required evidence |
| --- | --- |
| run | A agreed verification command succeeds |
| explain | Learner explains flow, order, state, reason, and failure behavior |
| reconstruct | Learner rebuilds the core logic with reference closed |
| transfer | Learner solves B with a genuinely different business decision |
| adapt | Learner handles one changed constraint and adds verification |
| position | Learner identifies the real project owner, callers, dependencies, and boundary |

Passing only `run` means: `Code runs, but independent coding ability has not passed yet.`

## Review Card

```text
Topic and language:
Current ladder stage:
Evidence passed:
One corrected mistake:
Weakest category:
Closed-reference entry point:
Next transfer or changed constraint:
Interview explanation to retrieve:
```

Keep the review card in chat unless the user approves persistence or the repository has an existing learning-log convention.
