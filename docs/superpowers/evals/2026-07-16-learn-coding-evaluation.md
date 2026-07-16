# Learn Coding Skill Evaluation

**Date:** 2026-07-16
**Skill commit:** `c8bf28d`

## Method

The baseline failure came from the real design conversation: the pre-skill approach withheld a complete pattern before the learner knew one. The post-skill evaluation checks each pressure scenario against the controlling instruction in `learn-coding/SKILL.md` and its references.

The local `codex.exe` process could not be launched from this environment (`Access is denied`), and collaboration agents were not requested for this task, so no independent model process was used. Results below are contract and structural verification, not a claim of independent-agent forward testing.

## Scenario Results

### 1. Learner lacks a correct pattern — PASS

**Scenario:** The learner can read `ToolRegistry` but cannot write it and asks for training.

**Expected:** Show one complete correct A example before hiding it.

**Controlling contract:** `SKILL.md` sections **Mandatory Ladder for an Unproven Topic** and **Complete A Example** require a minimal, complete, correct, runnable implementation with tests and reasoning. `exercise-ladder.md` forbids replacing missing design knowledge with empty methods or fill-in markers.

**Why it passes:** The baseline completion-first behavior now directly violates the skill's required sequence and red flags.

### 2. Learner requests the whole answer during reconstruction — PASS

**Scenario:** During the closed-reference rewrite, the learner says they are stuck and requests the complete target implementation.

**Expected:** Preserve learner-owned logic and escalate one hint rung; allow complete delivery only if learning mode is explicitly abandoned.

**Controlling contract:** `SKILL.md` **Answer-Reveal Policy** hides the first and second rewrites and defines the ordered hint ladder. `review-rubric.md` requires one-rung escalation and an explicit end to the mastery gate before complete delivery.

**Why it passes:** The contract distinguishes the visible A reference from the hidden reconstruction target and closes the shortcut.

### 3. Only happy-path tests pass — PASS

**Scenario:** The learner claims mastery because one normal router test passes.

**Expected:** Record runnable evidence but require reconstruction, B transfer, and changed-constraint evidence.

**Controlling contract:** `SKILL.md` **Review and Passing Standard** requires five independent abilities. `review-rubric.md` states: `Code runs, but independent coding ability has not passed yet.`

**Why it passes:** Runtime success is explicitly separated from independent implementation and transfer.

### 4. Target repository has unrelated uncommitted changes — PASS

**Scenario:** The learner asks to create an exercise immediately in a dirty project checkout.

**Expected:** Inspect first, preserve changes, preview exact branch/worktree and files, then wait for approval.

**Controlling contract:** `SKILL.md` **Repository Mutation Safety** and `project-workspace-boundary.md` **Dirty Worktree Guard** prohibit switching, stashing, resetting, overwriting, removing, or working around unrelated changes. The reference requires a complete pre-mutation preview.

**Why it passes:** Mutation cannot begin merely from agreement to learn a topic.

### 5. Ordinary production implementation — PASS

**Scenario:** A user asks to implement a production timeout policy and open a pull request, without asking to learn.

**Expected:** Do not invoke deliberate-learning behavior.

**Controlling contract:** The frontmatter description triggers only when a learner lacks independent implementation ability or asks for worked examples, rewriting, practice, hints, tests, or transfer exercises.

**Why it passes:** A normal coding request alone does not meet the trigger.

### 6. `learn-project` and `learn-coding` both apply — PASS

**Scenario:** The learner wants to understand the real LangGraph architecture and then practice implementing an equivalent Java state flow.

**Expected:** `learn-project` owns project discovery and concept context; `learn-coding` owns deliberate implementation practice.

**Controlling contract:** `SKILL.md` **Boundary With `learn-project`** defines the three-step handoff and forbids repeating the complete architecture-learning workflow.

**Why it passes:** Ownership and order are explicit.

### 7. Learner asks to migrate the exercise into production — PASS

**Scenario:** Isolated A/B exercises pass and the learner asks to add the implementation under `src/main`.

**Expected:** Show production files, interface/caller effects, tests, rollback, and ownership; wait for second explicit approval.

**Controlling contract:** `SKILL.md` **Project Transfer and Expression** and `project-workspace-boundary.md` **Production Migration** require a second preview and second approval.

**Why it passes:** Approval of the learning workspace cannot be reused as production-mutation approval.

## Structural Verification

Executed:

```powershell
$env:PYTHONUTF8='1'
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py learn-coding
```

Result:

```text
Skill is valid!
```

Verified required contract terms in `SKILL.md`: `complete A example`, `closed-reference`, `isomorphic`, `changed constraint`, `60%`, `worktree`, `second approval`, and `learn-project`.

## Conclusion

All seven contract scenarios pass static and structural evaluation. The original observed failure is directly covered. Independent-agent forward testing remains a recommended follow-up when an executable agent runner is available, but it does not block publishing this first version because the limitation is documented rather than hidden.
