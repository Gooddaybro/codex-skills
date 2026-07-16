# Project Workspace Boundary

Read this before creating or changing files in a learner's project.

## Discover Before Choosing a Path

Observe:

- repository root and owning subproject;
- nearest `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, and repository instructions;
- current branch, worktree status, and unrelated changes;
- language/build manifests and verified run commands;
- source and test roots;
- existing `learning`, `learn`, `examples`, `learning_demos`, or sample conventions.

If multiple repositories are plausible, inspect only enough to list candidates and ask one blocking repository question. Create nothing until resolved.

## Default: Project-Local Learning Worktree

Use an approved isolated worktree and a non-production learning location. Prefer existing project convention; otherwise propose:

```text
<owning-subproject>/learning/learn-coding/<topic>/
├── reference/   # assistant-owned complete A example
├── exercise/    # learner-owned closed-reference rewrite
├── transfer/    # learner-owned B and changed-constraint work
└── tests/       # verification, fixtures, and runner
```

For Java, an existing `src/test/java/<package>/learning/<topic>/` convention is also valid. In a multi-language repository, place Java work in the Java subproject and Python work in the Python subproject, never at the workspace root by default.

Do not create a new Maven or Gradle module unless the repository already uses a suitable module convention, component scanning would be affected, dependencies must be isolated, or many examples require an independent build. Module creation needs explicit approval.

## Pre-Mutation Preview

Show all fields and wait for explicit approval:

```text
Repository and owning subproject:
Instructions read and their effect:
Current branch and worktree status:
Proposed branch/worktree action:
Exact directories and files:
Minimal run/verify command:
Assistant-owned files:
Learner-owned logic:
Existing changes preserved:
Production source touched: no (default)
```

Agreement to learn a topic is not approval to create files.

## Stage Boundaries

| Stage | Location | Production mutation |
| --- | --- | --- |
| Complete A example | `reference/` | No |
| Closed-reference rewrite | `exercise/` | No |
| B transfer | `transfer/` | No |
| Changed constraint | `transfer/` or existing learning package | No |
| Production migration | approved production path | Second approval required |

The first four stages may read and reuse stable DTOs, interfaces, enums, dependencies, or fixed test data. Replace live models, credentials, slow services, and unstable external systems with deterministic stand-ins whose observable contract is stated.

## Dirty Worktree Guard

If unrelated changes exist, do not switch branches, create a worktree, stash, reset, overwrite, remove files, or otherwise work around them without consent. State the conflict and request the minimum necessary action. Preserve all changes.

Never merge a learning branch automatically.

## Production Migration

Passing isolated exercises permits a migration proposal, not automatic migration. Show a second preview containing:

- exact production files;
- changed interfaces and callers;
- database/API effects;
- tests and rollback path;
- learner-owned implementation;
- learning-branch retention or cleanup options.

Wait for second explicit approval. The learner may keep only the learning branch, request a pull request, or decline production migration.
