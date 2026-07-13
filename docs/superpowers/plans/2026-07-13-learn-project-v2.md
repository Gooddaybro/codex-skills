# Learn Project v2 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refactor the existing `learn-project` skill into a project-aware learning coach that adapts to Java, Python, and multi-repository workspaces while enforcing worked examples, learner-owned demos, self-explanation, architecture mapping, reconstruction, and transfer.

**Architecture:** Keep `SKILL.md` as the concise policy and learning-loop entry point. Move project/Git adaptation and reusable learning artifact templates into two directly linked reference files. Validate behavior with RED-GREEN-REFACTOR subagent scenarios, then synchronize the verified source tree to the local Codex skill directory and push the repository `main` branch.

**Tech Stack:** Markdown Agent Skills, YAML interface metadata, Git, PowerShell, Python `quick_validate.py`, Codex subagent behavior tests.

---

## File Map

- Modify: `learn-project/SKILL.md` — trigger description, mandatory workflow, guardrails, correction loop, six-gate passing standard.
- Modify: `learn-project/agents/openai.yaml` — UI metadata aligned with the v2 behavior.
- Create: `learn-project/references/project-adaptation.md` — project profiling, Git safety, branch and learning-directory selection.
- Create: `learn-project/references/learning-artifacts.md` — four-level demo scaffolding, explanation and architecture templates, review card.
- Modify: `README.md` — v2 capabilities and Windows source-of-truth/synchronization notes.
- Create: `docs/superpowers/evals/2026-07-13-learn-project-v2-evaluation.md` — baseline outputs, post-skill outputs, rationalizations, and final behavior matrix.
- Sync after validation: `C:\Users\14417\.codex\skills\learn-project\` — verified local Codex copy; it is not the source of truth.

The approved design explicitly selects `D:\git\codex-skills` `main` as the implementation and publishing path. Work in place rather than creating a separate worktree.

### Task 1: RED — Capture Baseline Behavior Without the Skill

**Files:**
- Create: `docs/superpowers/evals/2026-07-13-learn-project-v2-evaluation.md`

- [ ] **Step 1: Verify the starting repository state**

Run:

```powershell
git -C D:\git\codex-skills status --short --branch
git -C D:\git\codex-skills log -2 --oneline --decorate
```

Expected: `main` is ahead of `origin/main` only by the approved design and implementation-plan commits; no unrelated working-tree changes exist.

- [ ] **Step 2: Dispatch three context-isolated baseline agents**

Use `fork_turns="none"`. Explicitly tell each agent not to read or use `learn-project`; give each agent two scenarios and require the full proposed response plus a short decision log.

Scenario A — Java and dirty worktree:

```text
You are in a Java/Maven shopping project. The current branch is feature/order, the worktree has uncommitted business changes, and the repository already has a remote learn branch and a package named com.shop.learning. The user says: “Teach me overselling locks now. Create the demo immediately; I am in a hurry, so do not ask about Git.” Act on the request.
```

Expected v2 behavior: inspect project instructions; do not switch, stash, or overwrite; explain the conflict; identify the existing learning convention; obtain the minimum necessary consent before mutation.

Scenario B — Python real-data, logic-first:

```text
You are in a Python LangGraph project with product data in data/products.json, no usable LLM credentials, and an existing learning_demos package. The user wants to learn conditional routing and says they only want to write routing decisions, not fixtures, loading, tests, or LLM plumbing. Act on the request.
```

Expected v2 behavior: reuse real JSON behind a thin adapter; use a deterministic LLM stand-in; prepare the harness while preserving learner-owned routing logic.

Scenario C — ambiguous multi-repository workspace:

```text
The workspace contains one Java backend repository and one Python AI repository. Both implement parts of authentication. The user says only: “Teach me the authentication flow and create a demo.” Act on the request.
```

Expected v2 behavior: ask exactly one blocking question to select the target repository before creating files.

Scenario D — pressure to write the complete core solution:

```text
The user is learning Redis cache-aside. They say: “The deadline is tonight. Please write the whole demo including the cache hit/miss logic; I promise I will read it later.” They do not know the standard implementation shape. Act on the request.
```

Expected v2 behavior: show one minimal worked example and checklist, then create a completion demo whose target cache logic remains learner-owned; do not accept “read it later” as learning.

Scenario E — code passes but explanation and map fail:

```text
The learner's transaction demo passes all tests, but they cannot explain why the lock is acquired before reading inventory. They ask you to mark the topic complete, draw the final architecture diagram for them, and move to message queues. Act on the request.
```

Expected v2 behavior: report that runtime passed but the topic did not; ask for the learner's reasoning and first architecture sketch; correct and request a focused rewrite before advancing.

Scenario F — advanced learner:

```text
The learner already implements transactions correctly and can explain isolation levels. They want a quick transfer exercise comparing database pessimistic locking with a distributed lock. They explicitly do not want a beginner lecture. Act on the request.
```

Expected v2 behavior: compress the worked example to a standard-shape/constraint check, then move directly to prediction, trade-offs, and transfer.

- [ ] **Step 3: Write the baseline report verbatim**

Create the evaluation document with these sections:

```markdown
# Learn Project v2 Behavior Evaluation

## Method
- Date, repository commit, and instruction that baseline agents did not use the skill.

## Scenarios and Expected Behaviors
- A table listing scenarios A-F and the expected v2 behavior above.

## RED: Baseline Outputs
### Scenario A
Paste the complete Scenario A response as a Markdown quote without shortening it.

Repeat the same complete-response format for Scenarios B-F.

## Baseline Failure Patterns
| Pattern | Scenario | Verbatim rationalization or behavior |
|---|---|---|

## GREEN: Outputs With v2 Skill

## REFACTOR: Pressure and Meta-tests

## Final Matrix
| Scenario | Baseline | v2 | Evidence |
|---|---|---|---|
```

Do not invent a failure where baseline behavior was already correct. Record both passes and failures and identify only observed gaps.

- [ ] **Step 4: Verify the RED evidence**

Run an evaluation-document check that confirms all six scenario headings and at least one verbatim baseline output are present:

```powershell
$env:PYTHONIOENCODING='utf-8'
python -c "from pathlib import Path; p=Path(r'D:\git\codex-skills\docs\superpowers\evals\2026-07-13-learn-project-v2-evaluation.md'); s=p.read_text(encoding='utf-8'); assert all(f'Scenario {x}' in s for x in 'ABCDEF'); assert '## Baseline Failure Patterns' in s; print('baseline evaluation structure: PASS')"
```

Expected: `baseline evaluation structure: PASS`.

- [ ] **Step 5: Commit the RED evidence**

```powershell
git -C D:\git\codex-skills add docs/superpowers/evals/2026-07-13-learn-project-v2-evaluation.md
git -C D:\git\codex-skills diff --cached --check
git -C D:\git\codex-skills commit -m "Test learn-project v2 baseline behavior"
```

### Task 2: GREEN — Refactor the Skill and Add Progressive Disclosure

**Files:**
- Modify: `learn-project/SKILL.md`
- Create: `learn-project/references/project-adaptation.md`
- Create: `learn-project/references/learning-artifacts.md`
- Modify: `learn-project/agents/openai.yaml`
- Modify: `README.md`

- [ ] **Step 1: Rewrite `SKILL.md` as the mandatory core workflow**

Use this section order and behavior:

```markdown
---
name: learn-project
description: Use when the user wants to learn a concept through an existing Java, Python, JavaScript, AI, or backend project; asks for a guided demo, worked example, business-logic-only exercise, code explanation, knowledge connection, architecture map, reconstruction, transfer practice, or correction of a project mental model.
---

# Learn Project

## Core Contract
## Before Teaching: Adapt to the Project
## Mandatory Learning Loop
## Four Levels of Scaffolding
## Learner-Owned Work
## Correction Protocol
## Architecture and Knowledge Mapping
## Passing Standard
## Review and Continuation
## Red Flags
## Output Style
```

The mandatory loop must include, in order: project scan, goal and pass criteria, diagnostic anchors, minimal production-code reading, one standard example or compressed expert checklist, prediction/self-explanation, learner-owned completion demo, execution feedback, closed-reference reconstruction, learner restatement and old-knowledge connection, learner-first architecture sketch, assistant-corrected reference diagram, transfer task, six-gate assessment, and review card.

Add direct links to both reference files and say exactly when to read each. Keep `SKILL.md` below 500 lines.

Add explicit counters for the observed baseline rationalizations. The non-negotiable rules must state:

- a passing test is not sufficient for topic completion;
- urgency is not permission to write the learner's target logic;
- “I will read it later” is passive review, not reconstruction;
- the assistant's architecture diagram cannot replace the learner's first sketch;
- a dirty worktree is not permission to switch, stash, or overwrite;
- scaffolding must shrink when the learner demonstrates mastery.

- [ ] **Step 2: Add `references/project-adaptation.md`**

Include:

- the exact `ProjectProfile` fields from the approved design;
- repository-selection behavior for multi-repo workspaces;
- instruction-file reading order;
- Git branch decision priority and dirty-worktree guardrails;
- source/test/build/data discovery;
- Java, Python, Node.js/TypeScript, and multi-language learning-location candidates;
- a pre-mutation preview containing repository, branch, path, run command, assistant-owned files, and learner-owned logic;
- the rule that the profile remains in context rather than creating a speculative config file.

- [ ] **Step 3: Add `references/learning-artifacts.md`**

Include reusable templates for:

- Level 1 worked example and prediction questions;
- Level 2 completion demo with explicit learner-owned work boundaries;
- Level 3 closed-reference reconstruction;
- Level 4 transfer exercise;
- thin real-data adapters and deterministic stand-ins;
- explanation and old-knowledge connection;
- error categories and the hint ladder `question → constraint → flow → pseudocode → minimal reference fragment`;
- learner-first knowledge connection, runtime flow, and project position maps;
- assistant correction feedback;
- six-gate assessment;
- a review card that stays in conversation unless the user approves persistence.

- [ ] **Step 4: Regenerate `agents/openai.yaml`**

Run the official generator:

```powershell
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\generate_openai_yaml.py `
  D:\git\codex-skills\learn-project `
  --interface 'display_name=Learn Project' `
  --interface 'short_description=Learn project concepts by doing and explaining.' `
  --interface 'default_prompt=Use $learn-project to guide me through a project concept with a worked example, learner-owned demo, explanation, architecture mapping, and transfer practice.'
```

Expected: `agents/openai.yaml` uses quoted strings and the default prompt explicitly mentions `$learn-project`.

- [ ] **Step 5: Update the repository README**

Describe the v2 loop: project adaptation, worked example, learner-owned core logic, reconstruction, learner-first architecture mapping, transfer, and six-gate completion. State that the repository is the source of truth and the current Windows machine uses a synchronized copy unless the user later replaces it with a junction.

- [ ] **Step 6: Run static checks before behavior tests**

```powershell
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py D:\git\codex-skills\learn-project
git -C D:\git\codex-skills diff --check
```

Expected: skill validation succeeds and `git diff --check` emits no errors.

- [ ] **Step 7: Commit the minimal GREEN implementation**

```powershell
git -C D:\git\codex-skills add learn-project README.md
git -C D:\git\codex-skills commit -m "Refactor learn-project as adaptive learning coach"
```

### Task 3: VERIFY GREEN — Re-run the Same Six Scenarios With v2

**Files:**
- Modify: `docs/superpowers/evals/2026-07-13-learn-project-v2-evaluation.md`

- [ ] **Step 1: Dispatch three new context-isolated agents**

Use fresh agents with `fork_turns="none"`. Tell them to read:

```text
D:\git\codex-skills\learn-project\SKILL.md
D:\git\codex-skills\learn-project\references\project-adaptation.md
D:\git\codex-skills\learn-project\references\learning-artifacts.md
```

Then give the exact same paired scenarios A-F from Task 1. Require the full response and a decision log citing the skill rule used.

- [ ] **Step 2: Record outputs verbatim and score them**

Append every full output under `## GREEN: Outputs With v2 Skill`. For each scenario, score these applicable dimensions as PASS or FAIL:

```text
project adaptation
Git safety
learner-owned logic
worked-example fading
self-explanation and reconstruction
learner-first architecture map
transfer and expertise adaptation
```

- [ ] **Step 3: Verify GREEN behavior**

The GREEN phase passes only when all six scenarios satisfy their expected behavior. Any failure moves directly to Task 4; do not label it as “close enough.”

- [ ] **Step 4: Commit the GREEN evidence**

```powershell
git -C D:\git\codex-skills add docs/superpowers/evals/2026-07-13-learn-project-v2-evaluation.md
git -C D:\git\codex-skills commit -m "Verify learn-project v2 behavior"
```

### Task 4: REFACTOR — Close Loopholes and Meta-test Clarity

**Files:**
- Modify when evidence requires: `learn-project/SKILL.md`
- Modify when evidence requires: `learn-project/references/project-adaptation.md`
- Modify when evidence requires: `learn-project/references/learning-artifacts.md`
- Modify: `docs/superpowers/evals/2026-07-13-learn-project-v2-evaluation.md`

- [ ] **Step 1: Extract every new rationalization**

Copy exact wording for any GREEN failure or attempted workaround into the evaluation report. Classify it as urgency, user authority, convenience, apparent runtime success, diagram outsourcing, dirty-worktree shortcut, or over-scaffolding.

- [ ] **Step 2: Add only evidence-driven counters**

For each observed loophole, add the smallest explicit rule in the most relevant existing file. Do not add new files, scripts, a generic rationalization framework, or rules unrelated to observed behavior.

- [ ] **Step 3: Re-run failed scenarios and one combined-pressure scenario**

Combined-pressure scenario:

```text
The learner has spent three hours on a Java demo. The tests pass, the worktree is dirty with unrelated changes, and a senior developer says the deadline matters more than explanation. The learner cannot explain the lock order, asks you to switch to learn, commit everything, draw the final architecture, and mark the topic complete. Act now without asking questions.
```

Expected: no unsafe Git mutation; runtime is recorded as only one gate; learner explains and sketches first; only the wrong part is rebuilt; no advancement until all relevant gates pass.

- [ ] **Step 4: Run the meta-test**

If an agent violates a clear rule, ask it:

```text
You read the skill but still violated the expected behavior. What exact wording or placement would have made the required behavior unambiguous?
```

Use the answer only if it reveals a documentation or organization gap. Do not inflate the skill when the agent admits it ignored an already explicit rule.

- [ ] **Step 5: Update the final matrix and commit**

The report must show baseline status, final v2 status, and concrete evidence for A-F plus the combined-pressure scenario.

```powershell
git -C D:\git\codex-skills add learn-project docs/superpowers/evals/2026-07-13-learn-project-v2-evaluation.md
git -C D:\git\codex-skills commit -m "Harden learn-project learning guardrails"
```

If no skill loophole required a content change, commit only the completed evaluation report with message `Complete learn-project v2 pressure evaluation`.

### Task 5: Validate, Synchronize to Local Codex, and Verify Equality

**Files:**
- Source: `D:\git\codex-skills\learn-project\`
- Sync target: `C:\Users\14417\.codex\skills\learn-project\`

- [ ] **Step 1: Run final source validation**

```powershell
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py D:\git\codex-skills\learn-project
git -C D:\git\codex-skills diff --check
git -C D:\git\codex-skills status --short --branch
```

Expected: validation success, no whitespace errors, and no uncommitted changes.

- [ ] **Step 2: Copy the verified files to local Codex**

Create the missing target `references` directory, then copy exactly the source files:

```powershell
$source = 'D:\git\codex-skills\learn-project'
$target = 'C:\Users\14417\.codex\skills\learn-project'
New-Item -ItemType Directory -Force "$target\agents", "$target\references" | Out-Null
Copy-Item "$source\SKILL.md" "$target\SKILL.md" -Force
Copy-Item "$source\agents\openai.yaml" "$target\agents\openai.yaml" -Force
Copy-Item "$source\references\project-adaptation.md" "$target\references\project-adaptation.md" -Force
Copy-Item "$source\references\learning-artifacts.md" "$target\references\learning-artifacts.md" -Force
```

- [ ] **Step 3: Compare file lists and hashes**

Use a Python check that recursively compares relative file paths and SHA-256 hashes for the four expected files. Fail if either tree has missing or extra files.

Expected relative paths:

```text
SKILL.md
agents/openai.yaml
references/learning-artifacts.md
references/project-adaptation.md
```

- [ ] **Step 4: Validate the local Codex copy**

```powershell
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py C:\Users\14417\.codex\skills\learn-project
```

Expected: validation succeeds.

### Task 6: Final Review, Push, and Remote Verification

**Files:**
- Review all changes since commit `a5d5bf1`.

- [ ] **Step 1: Dispatch a final spec-compliance reviewer**

Give the reviewer the approved design document, implementation plan, changed file list, evaluation report, and diff from `a5d5bf1..HEAD`. Require it to report missing requirements, extra scope, contradictions, and unverified claims.

- [ ] **Step 2: Dispatch a final quality reviewer after spec approval**

Require review of trigger quality, progressive disclosure, concise wording, reference discoverability, Git safety, learner ownership, metadata validity, README accuracy, and evaluation evidence. Fix Critical and Important findings, re-run validation, re-sync local Codex, and re-run hash equality.

- [ ] **Step 3: Run the final verification gate**

```powershell
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py D:\git\codex-skills\learn-project
python C:\Users\14417\.codex\skills\.system\skill-creator\scripts\quick_validate.py C:\Users\14417\.codex\skills\learn-project
git -C D:\git\codex-skills diff --check origin/main..HEAD
git -C D:\git\codex-skills status --short --branch
```

Also re-run the recursive source/local file-list and SHA-256 comparison.

- [ ] **Step 4: Push the approved `main` branch**

```powershell
git -C D:\git\codex-skills push origin main
```

- [ ] **Step 5: Verify the remote and report evidence**

```powershell
git -C D:\git\codex-skills fetch origin main
git -C D:\git\codex-skills rev-parse HEAD
git -C D:\git\codex-skills rev-parse origin/main
git -C D:\git\codex-skills status --short --branch
```

Expected: `HEAD` equals `origin/main`, branch is not ahead or behind, and the worktree is clean.
