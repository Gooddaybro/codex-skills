# Teaching Playbook

Use this reference when structuring explanations, writing objectives, choosing scaffold level, or repairing mental models. Keep the main loop in `SKILL.md`; this file supplies reusable teaching scripts.

## Why these scripts

They compress classic instructional structures into coach actions:

| Source | Use in this skill |
|---|---|
| Gagné 9 events | Micro-lesson open: hook, objective, activate, present, guide, practice, feedback, assess, transfer |
| Merrill first principles | Problem-centered; activate → demonstrate → apply → integrate |
| Cognitive load / worked examples | Predict before reveal; fade support; one chunk at a time |
| Gradual release | I do / We do / You do / Transfer |
| Bloom revised | Objective verbs and gate height |

## Objective verbs

Prefer high-level verbs tied to evidence:

| Verb | Typical evidence | Gate |
|---|---|---|
| understand | 30s restatement + explain | explain |
| apply | run + predict before run | run, predict |
| analyze | maps, boundary callouts, failure paths | connect, explain |
| evaluate | error classification + corrected model | correction cycle |
| create | closed-reference rebuild or real transfer | reconstruct, transfer |

Bad objectives: "了解 Redis"、"看看这段代码"、"学习一下 LangGraph".

Good objective:

```text
After this topic, the learner can analyze retrieval_grader branch conditions
in the outfit AI service by reconstructing the good/weak/empty paths without
the reference and transferring them to a new weak-evidence business rule.
```

## Micro-lesson templates

### Concept chunk

```text
Hook:
Objective:
Activate (old anchor + difference):
Definition:
Positive example:
Counterexample:
Decision points to watch (2–3):
Learner predict now:
```

### Flow / runtime chunk

```text
Trigger (who calls, when):
Input state:
Decision points in order (3–5 max):
Success output:
Failure / degraded path:
Boundary ownership:
Learner predict now:
```

### Code decision-point card

For each important line or block, fill:

```text
Decision:
Basis:
Wrong choice consequence:
Owning layer (business / infrastructure / boundary):
```

Never narrate an entire file. Select only cards needed for the current objective.

## Scaffold selection

| Signal | Level | Coach does | Learner does |
|---|---|---|---|
| New concept, no evidence | 1 Worked example | Micro-lesson + full minimal example after predict | Predict, restate, explain |
| Can restate, not yet implement | 2 Completion | Plumbing + harness | Target business logic only |
| Can implement with support | 3 Reconstruction | Hide reference; keep requirements | Rebuild core flow |
| Core gates mostly green | 4 Transfer | Change one business constraint | Adapt invariants and decisions |

Fade one step at a time. If the learner thrives, remove more support. If they thrash, step back one level—do not lecture longer.

## Predict-before-reveal ritual

Before showing any complete solution:

1. Give inputs, constraints, and the decision points to watch.
2. Ask for predicted branch/trace, state changes, and output.
3. Only then reveal the worked example.
4. Diff prediction vs reality; classify mismatches with the correction protocol.

Skipping prediction turns the example into passive reading.

## Explanation checklist (learner)

Accept an explanation only if all are present:

- [ ] problem stated in project terms
- [ ] ordered decision points
- [ ] success path
- [ ] failure / degraded path
- [ ] ownership boundary

If any item is missing, ask only for the missing item—do not restart a full lecture.

## Correction language

Prefer mental-model repairs:

```text
You treated this as a [layer A] decision.
In this project it is owned by [layer B] because [reason].
Rewrite only the part that encodes that decision.
```

Avoid:

```text
Just change line 42 to X.
```

unless the user has abandoned learning mode.

## Transfer design

Change **one** meaningful constraint, for example:

- source-of-truth ownership
- ordering policy
- fallback when evidence is weak
- validation boundary
- persistence vs request-scoped state
- failure classification / retry policy

Require pre-code answers:

```text
Invariant that still holds:
Rule that changes:
New trace or state transition:
Why the original is insufficient:
Smallest adaptation:
```

Rename-only scenarios are invalid.

## Turn budget

Default coach turn:

1. name the gate and objective fragment
2. teach at most one chunk
3. request one learner action
4. name required evidence

If the learner returns multiple artifacts at once, evaluate all, but assign only the next single action.

## Session open / close

### Open

```text
Topic:
Objective:
Gates already evidenced:
Start gate:
First learner action:
```

### Close (even if not full pass)

```text
Gates passed:
Gates still open:
Smallest next action:
Review card (if any):
24h / 7d retrieval cue:
```
