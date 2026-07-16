# Learn Coding Skill Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build, validate, document, and publish a reusable `learn-coding` Codex skill that uses complete examples, closed-reference rewriting, isomorphic transfer tasks, constraint-driven refactoring, and safe project-local learning worktrees.

**Architecture:** Keep the operational contract concise in `SKILL.md` and move detailed exercise construction, review evidence, workspace mutation boundaries, and the Java AI four-week profile into four focused references. Treat the current conversation as the RED baseline because it exposed the exact failure the skill must prevent: withholding the first correct example from a learner who lacks a coding template.

**Tech Stack:** Agent Skills Markdown/YAML, Python skill-creator validation scripts, Git, PowerShell verification.

---

## File Map

- Create `learn-coding/SKILL.md`: trigger metadata, core contract, routing, answer-reveal rules, mastery gates, and reference-loading instructions.
- Create `learn-coding/agents/openai.yaml`: generated UI metadata.
- Create `learn-coding/references/exercise-ladder.md`: A-example, closed-reference rewrite, B-transfer, and changed-constraint exercise construction.
- Create `learn-coding/references/project-workspace-boundary.md`: project discovery, branch/worktree, learning directory, file ownership, preview, and production migration rules.
- Create `learn-coding/references/review-rubric.md`: error categories, hint ladder, evidence, and review-card format.
- Create `learn-coding/references/java-ai-four-week-profile.md`: Java-first interview curriculum and exercise bank.
- Create `docs/superpowers/evals/2026-07-16-learn-coding-baseline.md`: observed RED behavior and scenario expectations.
- Create `docs/superpowers/evals/2026-07-16-learn-coding-evaluation.md`: post-skill contract evaluation.
- Modify `README.md`: list both skills and provide installation/usage instructions without duplicating the skill bodies.

### Task 1: Capture the RED Baseline

**Files:**
- Create: `docs/superpowers/evals/2026-07-16-learn-coding-baseline.md`

- [ ] **Step 1: Record the observed failing behavior**

Document the actual pre-skill proposal from this conversation: the assistant planned to provide interfaces, tests, and incomplete target logic before establishing a complete correct example. Record the learner's correction that they first need a correct example, then a closed-reference rewrite, then refactoring.

- [ ] **Step 2: Define five contract scenarios**

Record scenarios for: example-first learning, premature answer requests during reconstruction, passing only happy-path tests, dirty-worktree project mutation, and an ordinary non-learning implementation request.

- [ ] **Step 3: Verify RED evidence exists**

Run:

```powershell
Select-String -Path docs/superpowers/evals/2026-07-16-learn-coding-baseline.md `
  -Pattern 'Observed failure','correct example','closed-reference','dirty worktree','non-learning'
```

Expected: all five patterns are returned. The first scenario is marked `FAIL` before the new skill exists.

- [ ] **Step 4: Commit the RED baseline**

```powershell
git add docs/superpowers/evals/2026-07-16-learn-coding-baseline.md
git commit -m "test: capture learn-coding baseline failures"
```

### Task 2: Initialize the Skill Skeleton

**Files:**
- Create: `learn-coding/SKILL.md`
- Create: `learn-coding/agents/openai.yaml`
- Create: `learn-coding/references/exercise-ladder.md`
- Create: `learn-coding/references/project-workspace-boundary.md`
- Create: `learn-coding/references/review-rubric.md`
- Create: `learn-coding/references/java-ai-four-week-profile.md`

- [ ] **Step 1: Run the official initializer**

```powershell
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\init_skill.py learn-coding `
  --path . `
  --resources references `
  --interface "display_name=Learn Coding" `
  --interface "short_description=Build independent coding ability through guided practice" `
  --interface "default_prompt=Use $learn-coding to help me study a coding topic through a correct example, closed-reference rewrite, transfer exercise, tests, and review."
```

Expected: `learn-coding/SKILL.md`, `learn-coding/agents/openai.yaml`, and `learn-coding/references/` are created.

- [ ] **Step 2: Remove initializer placeholders by replacing the generated body**

Write frontmatter exactly as:

```yaml
---
name: learn-coding
description: Use when a learner can read or follow code but cannot implement it independently, relies on copying or complete AI answers, or asks for coding drills, correct worked examples, closed-reference rewriting, Java-first practice, tests, hints, review, timed reconstruction, or transfer exercises.
---
```

The body must route to the four references and contain no template sections or placeholder text.

- [ ] **Step 3: Verify the skeleton has no placeholders**

```powershell
Get-ChildItem learn-coding -Recurse -File | Select-String -Pattern 'TODO|TBD|FIXME|\[Describe|\[Choose'
```

Expected: no matches.

### Task 3: Implement the GREEN Learning Contract

**Files:**
- Modify: `learn-coding/SKILL.md`
- Modify: `learn-coding/references/exercise-ladder.md`
- Modify: `learn-coding/references/project-workspace-boundary.md`
- Modify: `learn-coding/references/review-rubric.md`
- Modify: `learn-coding/references/java-ai-four-week-profile.md`

- [ ] **Step 1: Write the concise core contract**

Require this order for an unproven topic:

```text
diagnose -> complete A example -> predict/run/explain -> close reference -> rewrite
-> compare/correct -> rewrite again -> B isomorphic transfer -> changed constraint
-> project transfer -> interview explanation
```

State that complete code is required for the first A example, hidden for reconstruction, and withheld by default for B/constraint tasks. Require one learner action at a time and approximately 60% learner-written code.

- [ ] **Step 2: Write `exercise-ladder.md`**

Define required artifacts for all four stages, the A/B separation, what tests may reveal, how to prevent answer leakage, how to choose meaningful changed constraints, and a complete `ToolRegistry` exercise blueprint.

- [ ] **Step 3: Write `project-workspace-boundary.md`**

Require instruction and Git discovery, then a pre-mutation preview containing repository, instructions, branch/action, exact path, run command, assistant-owned files, learner-owned logic, preserved changes, and whether production code is touched. Default to a project-local learning directory in an approved isolated worktree. Require a second approval before production migration.

- [ ] **Step 4: Write `review-rubric.md`**

Define error categories, the hint ladder `question -> constraint -> API reminder -> flow -> pseudocode -> minimal fragment`, focused correction, reconstruction evidence, transfer evidence, and a compact review card.

- [ ] **Step 5: Write `java-ai-four-week-profile.md`**

Encode the four weeks: architecture/fact boundaries, RAG, Agent, and engineering. Include at least four Java exercises plus one project-integrated exercise per week, Python-support boundaries, default weekly rhythm, and interview follow-ups.

- [ ] **Step 6: Verify required contract language**

Run:

```powershell
$required = @(
  'complete A example','closed-reference','isomorphic','changed constraint',
  '60%','worktree','second approval','learn-project'
)
$text = Get-Content -Raw learn-coding/SKILL.md
$required | ForEach-Object { if ($text -notmatch [regex]::Escape($_)) { throw "Missing: $_" } }
```

Expected: exit code 0.

- [ ] **Step 7: Commit the minimal skill**

```powershell
git add learn-coding
git commit -m "feat: add learn-coding skill"
```

### Task 4: Validate and Refactor the Skill

**Files:**
- Create: `docs/superpowers/evals/2026-07-16-learn-coding-evaluation.md`
- Modify if needed: `learn-coding/SKILL.md`
- Modify if needed: `learn-coding/references/*.md`

- [ ] **Step 1: Run the official validator**

```powershell
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py learn-coding
```

Expected: the validator reports the skill is valid.

- [ ] **Step 2: Evaluate the five baseline scenarios against the written contract**

For each scenario, cite the exact controlling section and record `PASS` only if the contract selects the intended behavior:

1. show a complete correct A example before the first rewrite;
2. refuse to reveal the target B implementation prematurely and escalate one hint rung;
3. treat happy-path test success as insufficient mastery;
4. stop before mutating a dirty worktree and request minimum consent;
5. do not trigger learning mode for ordinary implementation work.

- [ ] **Step 3: Add combined-skill and production-migration scenarios**

Verify `learn-project` owns project concept/context, `learn-coding` owns deliberate coding practice, and production migration requires a second preview and explicit approval.

- [ ] **Step 4: Close only observed gaps**

If a scenario fails, edit the smallest controlling section and rerun the validator plus the complete scenario table. Do not add speculative features.

- [ ] **Step 5: Commit evaluation and refinements**

```powershell
git add learn-coding docs/superpowers/evals/2026-07-16-learn-coding-evaluation.md
git commit -m "test: validate learn-coding behavior"
```

### Task 5: Document Installation and Usage

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Add `learn-coding` to the repository overview**

Describe it in one short section focused on the example -> rewrite -> transfer -> refactor progression and its boundary with `learn-project`.

- [ ] **Step 2: Generalize installation commands for multiple skills**

Show macOS links and Windows mirror commands for both `learn-project` and `learn-coding`, without making users copy the whole repository into the skills directory.

- [ ] **Step 3: Add explicit usage examples**

Include:

```text
$learn-coding Teach me Java ToolRegistry. Show one complete correct example first, then close it and make me rewrite it.
```

and a combined example using both `learn-project` and `learn-coding`.

- [ ] **Step 4: Verify README references valid paths**

```powershell
Select-String -Path README.md -Pattern 'learn-project','learn-coding','reference','rewrite','transfer'
Test-Path learn-project/SKILL.md
Test-Path learn-coding/SKILL.md
```

Expected: all patterns found; both path checks return `True`.

- [ ] **Step 5: Commit documentation**

```powershell
git add README.md
git commit -m "docs: document learn-coding installation"
```

### Task 6: Final Verification and Publish

**Files:**
- Verify all created and modified files.

- [ ] **Step 1: Run final structural validation**

```powershell
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py learn-project
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py learn-coding
git diff origin/main...HEAD --check
git status --short
```

Expected: both skills valid, no whitespace errors, clean worktree.

- [ ] **Step 2: Inspect the final file inventory**

```powershell
Get-ChildItem learn-coding -Recurse -File | Sort-Object FullName | Select-Object -ExpandProperty FullName
```

Expected: only `SKILL.md`, `agents/openai.yaml`, and the four approved reference files.

- [ ] **Step 3: Review commits and push**

```powershell
git log --oneline origin/main..HEAD
git push -u origin codex/learn-coding
```

Expected: the branch is published to `Gooddaybro/codex-skills`.

- [ ] **Step 4: Create a ready-for-review pull request**

```powershell
gh pr create --repo Gooddaybro/codex-skills --base main --head codex/learn-coding `
  --title "feat: add learn-coding skill" `
  --body "Adds an example-first deliberate coding practice skill with closed-reference rewriting, transfer exercises, project-worktree safety, validation evidence, and Java AI interview training."
```

Expected: GitHub returns the pull request URL.
