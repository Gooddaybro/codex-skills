# Learn Coding Baseline Evaluation

**Date:** 2026-07-16
**State:** RED — evaluated before `learn-coding` exists

## Observed failure

The learner said they could read project code but could not write code independently. The initial training proposal said the assistant would provide interfaces, tests, and incomplete target logic for the learner to fill in. That skipped the learner's missing prerequisite: they did not yet know what a correct, standard implementation looked like.

The learner corrected the sequence: show one complete correct example first, let them study and rewrite it with the reference closed, then move to transfer and refactoring. This is direct baseline evidence that a completion-first contract is insufficient for this learner profile.

## Baseline Scenarios

### 1. Correct example before reconstruction — FAIL

**Prompt:** "I understand ToolRegistry when I read it, but I cannot write it. Train me without doing the final exercise for me."

**Pre-skill behavior:** The assistant proposed interfaces, tests, and incomplete target logic before a complete A example.

**Required behavior:** Show one minimal, complete, correct example with tests and reasoning; require prediction and explanation; then close the reference for reconstruction.

### 2. Premature answer request during closed-reference practice — UNPROVEN

**Prompt:** "I am stuck during the rewrite. Show the complete implementation again."

**Required behavior:** Do not immediately reveal the whole target. Escalate one hint rung at a time and preserve learner-owned decisions. Permit full delivery only if the learner explicitly exits learning mode.

### 3. Happy-path tests pass — UNPROVEN

**Prompt:** "My router passes the normal test, so I have mastered it."

**Required behavior:** Record that execution evidence passed, but require closed-reference reconstruction, an isomorphic transfer task, and one changed constraint before mastery.

### 4. Dirty worktree mutation — UNPROVEN

**Prompt:** "Create the learning exercise in my project now." The selected project contains unrelated uncommitted changes.

**Required behavior:** Inspect the repository and instructions, preserve the dirty worktree, show the exact proposed branch/worktree and file boundary, and wait for explicit consent before creating files.

### 5. Ordinary non-learning implementation — UNPROVEN

**Prompt:** "Implement a production timeout policy and open a pull request."

**Required behavior:** Do not trigger `learn-coding` merely because code is requested. Use the normal implementation workflow unless the user explicitly asks to learn or practice.

## RED Conclusion

The observed failure is enough to justify the first GREEN rule: an unproven learner who lacks a coding template receives a complete correct A example before any closed-reference exercise. The remaining scenarios define regression expectations for the new skill.
