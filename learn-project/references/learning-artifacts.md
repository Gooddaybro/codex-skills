# Learning Artifacts

Use these templates when preparing examples, demos, maps, assessments, and review cards. Keep each artifact focused on one concept or core flow. For how to teach each level, see [teaching-playbook.md](teaching-playbook.md).

## Level 0: Micro-Lesson and Objective

Before Level 1, assistant fills and shows:

```text
Hook (project pain in 1 sentence):
Objective (one Bloom-style observable action):
Old-knowledge anchor (similar + different):
Definition:
Positive example:
Counterexample:
Decision points to watch (2–3):
Boundary / failure mode (exactly one):
```

Learner returns before any full solution reveal:

```text
30-second restatement:
Predicted branch/trace for the upcoming example:
Predicted state changes:
What I am still unsure about:
```

Do not open Level 1 reveal until prediction is present (experts may compress, not skip prediction entirely unless that gate is already evidenced).

## Level 1: Worked Example and Prediction

Assistant provides **after** learner prediction:

```text
Problem and production mapping:
Input and expected output:
Minimal standard implementation:
Reasoning for each important decision (decision-point cards only):
Constraint and pitfall checklist:
Minimal run command:
Prediction vs reality diff prompts:
```

Before running, learner provides (or updates):

```text
Predicted branch/trace:
Predicted state changes:
Expected output:
Reason for the order:
```

Compare prediction with evidence. A demonstrated expert may receive only the standard shape, constraints, and checklist before proceeding—still after a prediction or an already-proven predict gate.

## Level 2: Core-Logic Completion

Define ownership before presenting the demo:

```text
Assistant supplies: input adapter, deterministic dependencies, interfaces, runner, and verification harness
Learner implements: target routing, ordering, state updates, validation, business rules, or tool orchestration
Verification observes: output, trace, state, and one important failure path
```

Mark the implementation boundary in code with instructional markers:

```text
LEARNER_WORK_START: target business decisions only
LEARNER_WORK_END
```

Do not place the target algorithm in comments, tests, fixtures, or helper names. Plumbing must not hide the business cause-and-effect the learner is meant to explain.

## Level 3: Closed-Reference Reconstruction

Close or hide the worked implementation. Retain only:

```text
Behavioral requirement
Interface or function signature
Inputs and expected observations
Business constraints and failure behavior
Run/verification command
```

The learner reconstructs the full core flow and then explains which decisions were recovered from principles rather than memory of syntax.

## Level 4: Real Transfer

Change one meaningful business condition, such as source-of-truth ownership, ordering, fallback policy, state persistence, validation boundary, or failure policy.

Learner answers before coding:

```text
Invariant that still holds:
Rule that changes:
New trace or state transition:
Reason the original implementation is insufficient:
Smallest adaptation:
```

A variable, type, or entity rename without a changed decision is not transfer.

## Explanation Artifact

Accept only when complete:

```text
Problem in project terms:
Decision points in order:
Success path:
Failure / degraded path:
Ownership boundary:
```

## Review Card (after pass)

```text
Topic:
Objective:
Core decision points:
Common pitfall:
One closed-reference prompt (24h):
One transfer prompt (7d):
Gates evidenced:
```

## Real Data and Deterministic Dependencies

Thin-adapter record:

```text
Real source used:
Minimal input exposed to the learner:
Production boundary preserved:
Setup hidden by the adapter:
```

Deterministic-stand-in record:

```text
Dependency replaced:
Why nondeterminism or setup distracts from the topic:
Observable contract preserved:
Fixed responses or failure modes used for verification:
```

Prefer the thin adapter when real data is practical. Use the stand-in only for unstable, slow, credentialed, or nondeterministic dependencies.

## Explanation and Old Anchor

Learner explains:

```text
Problem solved:
Input origin:
Core flow and decision order:
Why that order matters:
Failure behavior:
Production-code location:
Old knowledge anchor:
Same:
Different:
Likely confusion:
```

Treat a weak old anchor as a prerequisite gap, repair it narrowly, and ask for a corrected restatement.

## Error Classification and Hint Ladder

Classify each mismatch as one of:

- syntax/API
- control flow/order
- data/state
- business rule
- system boundary
- architecture
- prerequisite
- oversight

Use this correction record:

```text
Observed mismatch:
Learner's reason:
Error category:
Correct mental model:
Learner-owned rewrite boundary:
Recheck evidence:
```

Escalate one rung at a time: **question -> constraint -> flow -> pseudocode -> minimal reference fragment**. Never jump to the whole target solution while learning mode remains active.

## Learner-First Maps

Ask for three separate drafts.

### Knowledge connection map

```text
Old anchor -> shared idea -> new concept
Prerequisite -> new concept
New concept -> neighboring concept most likely to be confused
Label each similarity and difference.
```

### Runtime flow map

```text
Show input/request -> decisions -> data or state changes -> output.
Include the important failure or fallback path and the direction of every edge.
```

### Project position map

```text
Show the owning component or layer, upstream caller, downstream dependency, and system boundary.
Do not mix runtime steps with component containment.
```

Assistant feedback:

```text
Correct:
Omitted:
Wrong direction:
Mixed layer:
Revision request:
```

The learner revises before the assistant supplies a reference Mermaid diagram. Ask the learner to explain the material difference between the two versions.

## Six-Gate Assessment

| Gate | Required evidence |
|---|---|
| Run | Minimal verification succeeds |
| Predict | Pre-run trace, branch, or state prediction matches important behavior |
| Explain | Own-words account covers problem, flow, order, reason, and failure behavior |
| Connect | Old anchor includes a valid similarity and difference |
| Reconstruct | Core flow is rebuilt with the reference closed |
| Transfer | Changed business condition is handled by adapting the correct principle |

Record each gate as **pass** or **not yet**, with one evidence sentence. If only run passes, use: `Demo runs, but the topic has not passed yet`.

## Review Card

```text
Topic:
One-sentence model:
Core flow:
Old anchor, similarity, and difference:
Key pitfall:
One corrected mistake:
Closed-reference reconstruction entry point:
Transfer question:
Weak or not-yet gate:
```

Keep the card in chat unless the user approves persistence or an existing project convention explicitly provides a learning log. Do not create a file, reminder, or background task by default.
