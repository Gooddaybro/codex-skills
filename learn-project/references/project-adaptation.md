# Project Adaptation

Use this reference before any project mutation and whenever repository, language, path, or Git state is ambiguous.

## ProjectProfile

Build this profile in conversation context only; do not create a configuration file:

- `repository_root`
- `project_instructions`
- `current_branch`
- `worktree_status`
- `languages_and_frameworks`
- `build_and_run_commands`
- `source_roots`
- `test_roots`
- `existing_learning_locations`
- `existing_learning_branch`
- `architecture_and_business_docs`
- `usable_real_data_sources`

Treat every field as observed context, not a reason to add infrastructure.

## Repository and Instruction Selection

If several repositories are plausible and the target is ambiguous:

1. Inspect only enough to list candidate roots and their distinguishing manifests.
2. Ask exactly one blocking question that selects the repository.
3. Create nothing until the answer resolves the target.

Within the selected repository, read instructions in this order:

1. the nearest applicable `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md` for each affected path;
2. root-level instruction documents;
3. root README, architecture/business documents, and build manifests;
4. conventions in the nearest existing source, tests, examples, or learning directory.

When instructions conflict, the closest applicable project instruction governs its scope.

Before selecting or finalizing any branch or learning path:

1. List the applicable instruction files actually read, or state that none were found.
2. Summarize the relevant constraints and their effect on the branch or path choice.
3. Only then apply the branch and learning-location priorities below.

Branch or path selection cannot be finalized from prompt facts alone until this instruction check is recorded.

## Git Decision and Dirty Guard

Choose a learning branch by priority:

1. an explicit project instruction;
2. the current branch when it is an existing learning branch;
3. an existing `learn` branch or semantic equivalent;
4. otherwise propose `learn` and ask before creating or switching.

Reading-only learning may remain on the current branch. Before any branch action, explain its effect.

If the worktree is dirty, do not switch branches, create a worktree, stash, reset, overwrite, or remove existing work. State what blocks the proposed action and ask for the minimum consent or user action required. Preserve all existing changes.

## Discovery

Inspect the smallest useful set of files:

- Git root, branch list, status, and recent project conventions;
- language and framework manifests;
- source and test roots;
- existing `learn`, `learning`, `learning_demos`, `examples`, tutorial, or sample locations;
- documented build, run, and test commands plus the smallest command that verifies the topic;
- architecture and business-flow documents;
- reusable database, JSON, API, knowledge-file, vector-store, fixture, or candidate-data entry points.

Prefer documented commands. If none exist, infer conservatively from manifests and label the inference before use.

## Candidate Learning Locations

| Project shape | Candidate locations |
|---|---|
| Java with Maven | Existing learning/example package; otherwise a proposed `learning` package under the current package/source root |
| Java with Gradle | Existing example package or the applicable source set and package hierarchy |
| Python | Existing `learning_demos/`, `learn/`, examples package, or a small package beside related tests |
| Node.js or TypeScript | Existing `examples/`, `learn/`, sample app, or a minimal demo beside related tests |
| Multi-language repository | The subproject that owns the concept, never the workspace root by default |

Reuse a project convention before proposing a new location. Do not hard-code one layout across languages.

## Data and Dependency Choice

Prefer a thin adapter over copied fake data when a usable real source exists. The adapter should expose only the input required by the learning target and keep the important business causality visible.

Use a deterministic stand-in only when a dependency is nondeterministic or distracting, including live LLM output, unstable external services, unavailable credentials, or slow integrations. State what behavior is preserved and what is replaced.

## Pre-Mutation Preview

Before creating or changing any project file, show all of these fields:

- **Repository:** selected root
- **Instructions read and effect:** applicable instruction files actually read (or none found), relevant constraints, and their effect on branch and path selection
- **Branch/action:** current branch and any proposed Git action
- **Path:** exact demo or learning location
- **Run/verify command:** smallest expected command
- **Assistant-owned files:** adapter, fixture, runner, harness, or other plumbing
- **Learner-owned logic:** exact target decisions the learner must implement
- **Existing changes preserved:** dirty paths or existing learning work that will not be overwritten

Wait until the user explicitly starts implementation after seeing this preview. Approval to learn a topic alone is not approval to mutate the project.
