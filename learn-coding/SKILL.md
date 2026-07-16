---
name: learn-coding
description: Use when a learner can read or follow code but cannot implement it independently, relies on copying or complete AI answers, or asks for coding drills, correct worked examples, closed-reference rewriting, Java-first practice, tests, hints, review, timed reconstruction, or transfer exercises.
---

# Learn Coding

## Core Contract

Build independent coding ability, not answer-recognition confidence. For an unproven topic, establish one correct pattern before hiding it, then require reconstruction, transfer, and adaptation.

Default learning-time balance: **60% learner-written code**, 20% relevant project-code reading, 10% principles, and 10% explanation/interview expression. Use the learner's language and give one learner action at a time.

## Boundary With `learn-project`

`learn-project` owns project discovery, concept understanding, architecture maps, and runtime context. `learn-coding` owns deliberate practice: complete examples, closed-reference rewrites, tests, hints, review, isomorphic transfer, and changed constraints.

When both apply, let `learn-project` contextualize the concept, use `learn-coding` to train its implementation, then return to the project for integration and design explanation.

## Before Teaching

Confirm the topic, language, time, repository context, observable pass condition, and existing implementation evidence. Do not accept “I understand it” as coding evidence. Skip a stage only when current evidence proves its ability.

**Required references:**

- Read [exercise ladder](references/exercise-ladder.md) before creating exercises.
- Read [review rubric](references/review-rubric.md) before reviewing code.
- Read [project workspace boundary](references/project-workspace-boundary.md) before repository mutation.
- Read [Java AI four-week profile](references/java-ai-four-week-profile.md) for the Java-first AI interview program.

## Mandatory Ladder

For an unproven topic:

```text
diagnose -> complete A example -> predict/run/explain -> close reference
-> rewrite -> compare/correct -> rewrite again -> B isomorphic transfer
-> changed constraint -> project transfer -> interview explanation
```

The complete A example must be minimal, correct, runnable, tested, and reasoned. Separate reusable structure from business rules. Ask the learner to predict important flow or state before running it.

For reconstruction, hide implementation but retain requirements, interfaces, inputs, failure behavior, tests, and run command. The learner writes from a blank file, corrects precise mismatches, then rewrites once more with the reference closed. One memorized rewrite is not transfer.

For B, preserve the principle but change a real business decision. Renaming entities is not transfer. Then add one changed constraint such as missing data, duplicate input, timeout, retry, concurrency, a new type, tracing, or source-of-truth ownership.

## Answer-Reveal Policy

| Stage | Complete answer |
| --- | --- |
| First A example and explanation | Required and visible |
| First/second reconstruction | Hidden |
| Post-attempt comparison | May be shown, then close it again |
| B isomorphic transfer | Hidden by default |
| Changed constraint | Hidden by default |
| Learner explicitly exits learning mode | Allowed; do not claim mastery |

Escalate one hint rung per attempt:

```text
question -> constraint -> relevant API reminder -> flow -> pseudocode -> minimal code fragment
```

The assistant may own the A reference, fixtures, adapters, interfaces, runner, and harness. The learner owns reconstruction and transfer decisions: routing, order, state, validation, business rules, failure policy, and refactoring. Do not leak those decisions through tests, comments, fixtures, helper names, or early pseudocode.

## Repository Mutation Safety

Before creating files, inspect the selected repository, instructions, Git status, build commands, and learning conventions. Prefer an approved isolated learning worktree and a non-production learning location.

Show the complete pre-mutation preview from the workspace reference and wait for explicit approval. Keep A, reconstruction, B, and changed-constraint files outside production source. Obtain **second approval** before production migration.

Never switch, stash, reset, overwrite, remove, or work around unrelated dirty changes. Never merge a learning branch automatically.

## Review and Passing Standard

Review correctness and decisions before style. Classify the mismatch, repair the smallest underlying gap, and require the learner to rewrite the affected part.

A topic passes only when the learner can:

1. run and explain A;
2. reconstruct with the reference closed;
3. solve B without copying A;
4. handle one changed constraint and add verification;
5. explain the design, failure behavior, and project position.

Passing tests alone means code runs, not that independent coding ability passed.

## Red Flags

Stop if you are about to:

- give only incomplete scaffolding before showing a correct pattern;
- reveal B or the changed-constraint solution at the first difficulty;
- accept one memorized rewrite or happy-path test as mastery;
- call a renamed scenario transfer;
- create files before mutation approval;
- place initial exercises in production source;
- overwrite dirty work or migrate without second approval;
- take back learner-owned decisions because completing them is faster.

State the current stage, one learner action, evidence to return, and exact run command when files exist. Reveal the next artifact only at its decision point.
