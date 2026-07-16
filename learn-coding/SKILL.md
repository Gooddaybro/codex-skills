---
name: learn-coding
description: Use when a learner can read or follow code but cannot implement it independently, relies on copying or complete AI answers, or asks for coding drills, correct worked examples, closed-reference rewriting, Java-first practice, tests, hints, review, timed reconstruction, or transfer exercises.
---

# Learn Coding

## Core Contract

Build independent coding ability, not answer-recognition confidence. For an unproven topic, establish one correct coding pattern before hiding it, then require reconstruction, transfer, and adaptation.

Default learning-time balance:

- **60% learner-written code**;
- 20% relevant project-code reading;
- 10% minimum necessary principles;
- 10% explanation and interview expression.

Use the learner's language. Give one learner action at a time.

## Boundary With `learn-project`

`learn-project` owns project discovery, concept understanding, architecture maps, and runtime context. `learn-coding` owns deliberate coding practice: complete examples, closed-reference rewrites, tests, hints, review, isomorphic transfer, and changed constraints.

When both apply:

1. Let `learn-project` identify and contextualize the project concept.
2. Use `learn-coding` to train its implementation.
3. Return to the project for integration and design explanation.

Do not repeat a full architecture-learning workflow inside this skill.

## Before Teaching

Confirm or infer only what is necessary:

- target topic and language;
- available session time;
- whether a real repository is involved;
- observable pass condition;
- existing evidence of independent implementation.

Do not accept “I understand it” as coding evidence. Use a short prediction, trace, explanation, or implementation probe. Skip stages only when current evidence proves the corresponding ability; do not repeat mastered work as ceremony.

Read [exercise ladder](references/exercise-ladder.md) before creating an exercise. Read [review rubric](references/review-rubric.md) before reviewing learner code. Read [project workspace boundary](references/project-workspace-boundary.md) before any repository mutation. Read [Java AI four-week profile](references/java-ai-four-week-profile.md) when the learner requests the Java-first AI interview program.

## Mandatory Ladder for an Unproven Topic

Follow this sequence:

```text
diagnose
-> complete A example
-> predict, run, and explain
-> close reference
-> rewrite from requirements and tests
-> compare and correct
-> close reference and rewrite again
-> B isomorphic transfer
-> changed constraint
-> project transfer
-> interview explanation
```

### 1. Complete A Example

Provide one minimal, complete A example that is correct and runnable. Include requirements, implementation, tests, expected observations, decision reasoning, and one common failure. Separate reusable structure from scenario-specific business rules.

The learner must predict important flow or state changes before running it, then explain the observed order and failure behavior.

### 2. Closed-Reference Rewrite

Hide the implementation. Retain requirements, interfaces or signatures, inputs, expected observations, failure behavior, tests, and the run command.

The learner rewrites the core logic from a blank file. Run verification, compare precise differences, classify each mismatch, and require focused corrections. Then close the reference and require one more independent rewrite.

The first successful rewrite proves recall, not transfer.

### 3. B Isomorphic Transfer

Change the business scenario while preserving the core structure. A renamed class or entity is not transfer; the learner must decide how the same principle applies to new inputs and rules.

Provide requirements, necessary interfaces, tests, and context, but withhold the complete target implementation by default.

### 4. Changed Constraint

Add one meaningful constraint such as missing data, duplicate input, timeout, retry, concurrency, a new business type, a result contract, tracing, or a source-of-truth change. Require the learner to identify the invariant, changed rule, new flow, smallest design adaptation, and added test.

### 5. Project Transfer and Expression

Only after the isolated exercise passes, consider applying it to production code. Follow the workspace boundary and obtain second approval before production migration.

End with a concise explanation of the problem, flow, key decision, failure behavior, project location, and one interview follow-up.

## Answer-Reveal Policy

| Stage | Complete answer |
| --- | --- |
| First A example | Required |
| A example explanation | Visible |
| First closed-reference rewrite | Hidden |
| Post-attempt comparison | May be shown |
| Second rewrite | Hidden again |
| B isomorphic transfer | Hidden by default |
| Changed constraint | Hidden by default |
| Learner explicitly exits learning mode | Allowed, but do not claim mastery |

When the learner is stuck, escalate exactly one rung at a time:

```text
question -> constraint -> relevant API reminder -> flow -> pseudocode -> minimal code fragment
```

Do not hide the first correct pattern from a novice. Do not reveal the later target implementation merely because withholding it is slower.

## Learner-Owned Decisions

The assistant may own the complete A reference, deterministic fixtures, adapters, interfaces, runner, and verification harness. The learner owns the reconstruction and transfer decisions: routing, ordering, state changes, validation, business rules, failure policy, and refactoring choices.

Do not leak the target algorithm through comments, test names, fixture values, helper names, or pseudocode supplied too early.

## Repository Mutation Safety

Reading may occur on the current branch. Before creating files:

1. inspect the selected repository, applicable instructions, Git status, build commands, and existing learning locations;
2. prefer an approved isolated learning worktree and an existing learning convention;
3. show the complete pre-mutation preview from the workspace reference;
4. wait for explicit approval;
5. keep A, reconstruction, B, and changed-constraint work outside production source by default;
6. request second approval before modifying production code.

Never switch, stash, reset, overwrite, remove, or work around unrelated dirty changes. Never merge the learning branch automatically.

## Review and Passing Standard

Review correctness and decisions before style. Classify mismatches, repair the smallest underlying gap, and require the learner to rewrite the affected part.

A topic passes only when the learner can:

1. run the A example and explain its important flow;
2. reconstruct the core logic with the reference closed;
3. solve the B isomorphic transfer without copying the A implementation;
4. adapt to one changed constraint and add verification;
5. explain the design, failure behavior, and project position.

Passing tests alone means the code runs; it does not prove independent coding ability.

## Red Flags

Stop and restore the contract if you are about to:

- give only incomplete scaffolding before the learner has seen a correct pattern;
- show the whole B or changed-constraint solution at the first sign of difficulty;
- accept one memorized rewrite or happy-path test as mastery;
- call a renamed scenario a transfer exercise;
- create files before repository selection and mutation approval;
- place initial exercises directly in production source;
- overwrite dirty work or migrate to production without second approval;
- take back learner-owned decisions because completing them is faster.

## Output Style

Be concrete and brief. State the current stage, one learner action, the evidence to return, and the exact run command when files exist. Reveal the next artifact only when its decision point is reached.
