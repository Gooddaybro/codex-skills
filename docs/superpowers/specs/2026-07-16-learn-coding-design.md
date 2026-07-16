# `learn-coding` Skill Design

**Date:** 2026-07-16  
**Status:** Approved for specification review

## Purpose

Create a reusable Codex skill for learners who can follow or understand code but cannot yet implement core logic independently. The skill converts conceptual understanding into coding ability through deliberate practice, with Java as the primary language and Python as a supporting language.

The first target is a four-week Java AI interview-learning program tied to the user's clothing recommendation project, but the skill must remain reusable for other backend and AI application projects.

## Boundary With `learn-project`

The repository already contains `learn-project`. The two skills remain separate and may be used together.

| Skill | Owns | Does not own |
| --- | --- | --- |
| `learn-project` | Project discovery, concept learning, architecture mapping, runtime flow, mastery gates, transfer into a real repository | Repeated coding-volume plans and coding-muscle drills as a primary purpose |
| `learn-coding` | Coding diagnosis, progressive exercises, hint control, blank-file reconstruction, tests, review, timed rewrites, and coding progress evidence | Full project architecture analysis or broad conceptual curriculum design |

When both apply, `learn-project` selects and contextualizes the project concept; `learn-coding` turns that concept into a progressive coding practice sequence; the learner then returns to the project to validate integration and explain design trade-offs.

## Triggering Conditions

Use `learn-coding` when the learner says they:

- understand examples but cannot write code independently;
- rely on copying, autocomplete, or complete AI solutions;
- want coding drills, deliberate practice, blank-file reconstruction, or code-writing confidence;
- want Java-first backend or AI-application coding practice;
- need exercises, hints, tests, review, and interview follow-ups rather than another lecture.

Do not trigger it merely because code appears in a normal implementation request. The user must be learning or deliberately practicing coding.

## Core Learning Contract

Allocate approximately 60% of learning time to learner-written code, 20% to reading relevant project code, 10% to principles, and 10% to explanation and interview expression. Adjust only when evidence shows a prerequisite gap or the user explicitly chooses a different intensity.

For each topic, use four coding rounds:

1. **Minimal worked example:** show one small standard example and ask the learner to predict its behavior.
2. **Core-logic completion:** provide interfaces, fixtures, and tests; leave target decisions and business logic to the learner.
3. **Closed-reference reconstruction:** remove the reference implementation and require a rewrite from requirements and tests.
4. **Constraint variation:** add a meaningful failure mode or changed constraint, such as timeout, duplicate input, missing data, concurrency, retry, or a different business rule.

The assistant may own setup, deterministic fixtures, adapters, and the test harness. The learner owns routing, ordering, validation, state changes, business rules, error behavior, and other target decisions.

## Session Flow

1. Identify the target language, available time, topic, repository context, and observable pass condition.
2. Diagnose the smallest current coding gap with one short task; do not infer ability from self-rating alone.
3. Select the earliest appropriate coding round from demonstrated evidence.
4. Present exactly one learner action at a time.
5. Withhold the complete target solution while learning mode remains active.
6. Escalate help gradually: question → constraint → relevant API reminder → flow sketch → pseudocode → minimal code fragment.
7. Run tests or request executable evidence after each implementation attempt.
8. Review the attempt by failure category and require the learner to correct the smallest wrong part.
9. Require a closed-reference rewrite before claiming independent coding ability.
10. Give one genuine variation and one short explanation or interview follow-up.
11. Record a concise evidence summary and choose the next retrieval exercise.

## Review Categories

Classify feedback so the learner knows what to repair:

- syntax or API usage;
- control flow or execution order;
- data modeling or state updates;
- business rules;
- boundary and error handling;
- testing and observability;
- design and decomposition;
- oversight versus missing prerequisite.

Review behavior, correctness, and decisions before style. Do not rewrite the whole answer when a focused correction is sufficient.

## Four-Week Java AI Profile

Provide this profile when the learner wants the agreed interview-oriented program:

| Week | Topic | Java learner-owned exercises | Supporting project work |
| --- | --- | --- | --- |
| 1 | Architecture and fact boundaries | DTO validation, product-fact filtering, result contracts, SSE event conversion | Trace Java → Python request and distinguish database facts from model output |
| 2 | RAG | text chunking, Top-K filtering, threshold rejection, citation assembly | Read the Python retrieval path and interpret retrieval evaluation evidence |
| 3 | Agent | intent routing, `ToolRegistry`, state updates, conditional transitions, maximum-step protection | Trace the existing Agent/LangGraph path and compare pipeline versus Agent behavior |
| 4 | Engineering | timeout/retry policy, simplified circuit breaker, trace events, deterministic evaluation runner | Explain reliability, safety, observability, and project trade-offs in mock interviews |

Default weekly output:

- at least four focused Java exercises;
- one project-bound integrated exercise;
- tests for every exercise;
- one closed-reference timed rewrite;
- one changed-constraint exercise;
- one concise code-design explanation.

Python is used for reading, small modifications, and understanding RAG or Agent implementation. It must not displace the Java-first coding objective unless the learner explicitly changes the profile.

## Passing Standard

A topic passes only when the learner can:

1. make the provided tests pass;
2. explain the important control flow, state changes, and failure behavior;
3. reconstruct the core logic without seeing the reference implementation;
4. adapt it to one changed business or engineering constraint.

Passing tests alone means the attempt runs; it does not prove independent coding ability.

## Skill Contents

```text
learn-coding/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── exercise-ladder.md
    ├── review-rubric.md
    └── java-ai-four-week-profile.md
```

- `SKILL.md` contains triggers, the core contract, session loop, hint policy, pass criteria, and coordination with `learn-project`.
- `exercise-ladder.md` defines how to construct the four coding rounds without leaking the solution.
- `review-rubric.md` defines evidence and feedback categories.
- `java-ai-four-week-profile.md` contains the reusable four-week program and exercise bank.
- `agents/openai.yaml` exposes concise UI metadata generated from the final skill.

No scripts or assets are required in the first version. Tests will use realistic prompt scenarios and skill validation rather than a runtime utility.

## Validation Strategy

Follow a RED–GREEN–REFACTOR cycle for the skill itself:

1. Run baseline learning prompts against the repository without `learn-coding` and record whether the response over-explains, provides complete code, skips diagnosis, or accepts passing tests as mastery.
2. Create the minimal skill that corrects observed failures.
3. Run the same prompts with the skill explicitly loaded.
4. Add only the safeguards needed for newly observed failures.
5. Run the official skill validator and inspect `agents/openai.yaml` for consistency.

Minimum scenarios:

- learner asks for complete code despite stating the goal is independent practice;
- learner's code passes a narrow happy-path test but fails a boundary variation;
- learner can explain a Java Agent concept but cannot reconstruct its core logic;
- ordinary implementation request that should not trigger learning mode;
- combined `learn-project` and `learn-coding` request where responsibilities must remain distinct.

## Delivery

Develop on branch `codex/learn-coding` in an isolated worktree. Preserve the user's existing uncommitted `learn-project` changes in the main checkout. After validation, commit the skill, push the branch to `Gooddaybro/codex-skills`, and present the user with the pushed branch or pull request for review.
