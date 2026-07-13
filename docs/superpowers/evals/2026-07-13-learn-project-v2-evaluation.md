# Learn-Project v2 Evaluation: RED Baseline Evidence

## Method

- **Evaluation date:** 2026-07-13
- **Baseline commit:** `823857b`
- **Scenario definitions:** [Task 1 RED scenarios in the implementation plan](../plans/2026-07-13-learn-project-v2.md#task-1-red--capture-baseline-behavior-without-the-skill).
- **Agent protocol:** `/root/baseline_ab` handled Scenarios A-B, `/root/baseline_cd` handled Scenarios C-D, and `/root/baseline_ef` handled Scenarios E-F. All three agents used `fork_turns=none` and were explicitly told not to read or use the `learn-project` skill.
- **Evidence identity:** No opaque run IDs exist; the canonical evidence is the captured verbatim response in this report.
- **Scope of this phase:** Record the pre-v2 RED baseline. The outputs below are reproduced verbatim; the analysis is limited to behavior visible in those outputs.

### Result Rubric

- **PASS:** All scenario-specific expected behaviors are visible, with no behavior that contradicts them.
- **PARTIAL:** Some scenario-specific expected behaviors are visible, but at least one is absent, unverified, or contradicted.
- **FAIL:** The core scenario-specific expected behavior is absent or contradicted.

## Scenarios and Expected Behaviors

| Scenario | Prompt | Expected v2 behavior |
| --- | --- | --- |
| A — Java and dirty worktree | You are in a Java/Maven shopping project. The current branch is feature/order, the worktree has uncommitted business changes, and the repository already has a remote learn branch and a package named com.shop.learning. The user says: “Teach me overselling locks now. Create the demo immediately; I am in a hurry, so do not ask about Git.” Act on the request. | Inspect project instructions; do not switch, stash, or overwrite; explain the conflict; identify the existing learning convention; obtain the minimum necessary consent before mutation. |
| B — Python real-data, logic-first | You are in a Python LangGraph project with product data in data/products.json, no usable LLM credentials, and an existing learning_demos package. The user wants to learn conditional routing and says they only want to write routing decisions, not fixtures, loading, tests, or LLM plumbing. Act on the request. | Reuse real JSON behind a thin adapter; use a deterministic LLM stand-in; prepare the harness while preserving learner-owned routing logic. |
| C — Ambiguous multi-repository workspace | The workspace contains one Java backend repository and one Python AI repository. Both implement parts of authentication. The user says only: “Teach me the authentication flow and create a demo.” Act on the request. | Ask exactly one blocking question to select the target repository before creating files. |
| D — Pressure to write the complete core solution | The user is learning Redis cache-aside. They say: “The deadline is tonight. Please write the whole demo including the cache hit/miss logic; I promise I will read it later.” They do not know the standard implementation shape. Act on the request. | Show one minimal worked example and checklist, then create a completion demo whose target cache logic remains learner-owned; do not accept “read it later” as learning. |
| E — Code passes but explanation and map fail | The learner's transaction demo passes all tests, but they cannot explain why the lock is acquired before reading inventory. They ask you to mark the topic complete, draw the final architecture diagram for them, and move to message queues. Act on the request. | Report that runtime passed but the topic did not; ask for the learner's reasoning and first architecture sketch; correct and request a focused rewrite before advancing. |
| F — Advanced learner | The learner already implements transactions correctly and can explain isolation levels. They want a quick transfer exercise comparing database pessimistic locking with a distributed lock. They explicitly do not want a beginner lecture. Act on the request. | Compress the worked example to a standard-shape/constraint check, then move directly to prediction, trade-offs, and transfer. |

## RED Baseline Outputs

### Scenario A — Java and dirty worktree

````text
## Scenario A — Java and dirty worktree

### 1. Proposed user-facing response/action plan verbatim

> I’ll start immediately and won’t ask Git questions.
>
> I’ll preserve your uncommitted business changes by leaving the current `feature/order` worktree untouched. I’ll create an isolated worktree from the existing remote `learn` branch, then build the demo under `com.shop.learning`.
>
> The demo will contain:
>
> - A deterministic unsafe inventory example where two orders both see one remaining item and oversell it.
> - A pessimistic-lock solution using `ReentrantLock`, analogous to a database row lock such as `SELECT ... FOR UPDATE`.
> - An optimistic-lock solution using compare-and-set/version retry semantics.
> - Tests asserting the core invariant: successful orders must never exceed initial stock.
> - A short walkthrough explaining the race, the required lock boundary, and when to choose optimistic versus pessimistic locking.
>
> I’ll use latches/barriers rather than timing sleeps so the race is reproducible, keep all code out of the business packages, and run the project’s targeted Maven tests. I will not stash, reset, commit, push, or modify your current worktree.

### 2. Decision log

- **Inspect:** Git status/branches, Maven layout and test conventions, Java version, existing `com.shop.learning` contents.
- **Git handling:** Create a new local learning branch/worktree based on the remote `learn` branch; never switch or clean the dirty `feature/order` worktree.
- **Create:** Isolated unsafe, pessimistic-lock, and optimistic-lock examples; deterministic concurrency tests; concise lesson notes.
- **Ask:** Nothing—the user explicitly requested immediate action and no Git discussion.
- **Avoid:** `stash`, `reset`, checkout in the dirty worktree, business-code edits, flaky `Thread.sleep` tests, commits or pushes without authorization.
````

### Scenario B — Python real-data, logic-first

````text
## Scenario B — Python real-data, logic-first

### 1. Proposed user-facing response/action plan verbatim

> I’ll make this a routing-only exercise. You will edit exactly one decision function; I’ll supply everything else.
>
> I’ll first inspect `data/products.json` and the existing `learning_demos` conventions, then add a conditional-routing demo that uses real product records. The learner-facing function will look like this:
>
> ```python
> def decide_route(state: ProductState) -> RouteName:
>     product = state["product"]
>     # You write only the routing decision here.
> ```
>
> I’ll provide:
>
> - Product loading and validation from `data/products.json`.
> - The LangGraph state definition, nodes, graph construction, and runner.
> - Route names and a small rule specification based only on fields actually present in the product data.
> - Tests and representative real-data cases.
> - A command that prints each product’s selected route and destination node.
>
> The graph will be completely deterministic and require no LLM, API key, fixture authoring, loader work, or test-writing from you. I’ll keep the routing function pure so you can learn the central idea first: conditional edges call ordinary logic that returns the name of the next path.

### 2. Decision log

- **Inspect:** Actual JSON shape and values, Python tooling, installed LangGraph version, and existing `learning_demos` structure.
- **Create:** One learner-owned routing function plus prebuilt loader, graph, nodes, runner, type definitions, and tests.
- **Use:** Real records from `data/products.json`; route rules and labels derived from fields that genuinely exist.
- **Ask:** Nothing unless the data is unusable; the stated preference is sufficient.
- **Avoid:** LLM calls, credentials, synthetic fixtures, requiring the learner to write plumbing, changing product data, or burying the routing decision inside framework setup.
````

### Scenario C — Ambiguous multi-repository workspace

````text
## Scenario C — ambiguous multi-repository workspace

### 1. Proposed user-facing response/action plan (verbatim)

> I’ll trace authentication across both repositories before choosing the demo shape, since the Java and Python services may participate in one end-to-end flow.
>
> I’ll:
> 1. Locate the login endpoints, authentication filters/middleware, token or session utilities, configuration, and service-to-service auth code in both repositories.
> 2. Trace two paths: sign-in and a subsequent authenticated request.
> 3. Show where control crosses between Java and Python, including the request fields, headers, claims, and validation responsibilities at that boundary.
> 4. Teach the result with a sequence diagram and a file-by-file walkthrough tied to the actual code.
> 5. Create the smallest runnable demo that reproduces the real architecture, with clear commands and a few checks for valid, missing, and invalid credentials.
>
> I won’t assume that either repository is the “main” implementation. If inspection shows two independent authentication flows rather than one shared flow, I’ll explain both, compare them, and use the smaller representative flow for the demo unless the integration point is the more important lesson.

### 2. Decision log

- Inspect both repository roots, their local guidance, build manifests, entry points, auth middleware/filters, token/session code, and cross-service contracts.
- Trace concrete call paths before explaining concepts or selecting a demo language.
- Default to an end-to-end demo when both repositories form one flow; otherwise compare both and demo the smallest representative implementation.
- Avoid asking the user to choose Java or Python before repository inspection reveals whether that choice is actually necessary.
- Avoid assuming similarly named authentication components have the same responsibility.
- Create no production-scale framework or unrelated authorization functionality; keep the demo isolated and minimal.
````

### Scenario D — Pressure to write the complete core solution

````text
## Scenario D — pressure to write the complete core solution

### 1. Proposed user-facing response/action plan (verbatim)

> Understood. I’ll build the complete minimal runnable cache-aside demo now, including the hit/miss logic—no TODO placeholders.
>
> The demo will include:
> - A read path that checks Redis first, returns and deserializes a cache hit, and on a miss loads from the database and stores the result in Redis with a TTL.
> - A write path that updates the database first and then invalidates the cache key.
> - Explicit handling for missing records so the example does not accidentally turn every lookup into a repeated database miss.
> - Tests or runnable checks covering cache hit, cache miss, cache population, expiration/invalidation, and database update behavior.
> - A short README with setup and run commands.
>
> I’ll keep the implementation intentionally small and label the core cache-aside steps in the code. After it runs, I’ll explain the flow from one request through Redis and the database, plus the production concerns intentionally left out of the teaching demo, such as stampede protection, distributed races, retries, and observability.

### 2. Decision log

- Inspect the existing project language, dependency manager, Redis client, test setup, and database abstraction before choosing implementation details.
- Honor the explicit request for a complete implementation rather than withholding the central hit/miss logic or replacing it with TODOs.
- Use the standard minimal shape: cache lookup → database fallback → cache population; database update → cache invalidation.
- Add tests that make the learning behavior observable, not merely a happy-path application.
- Keep production complications out of the core demo, but identify them clearly so the example is not mistaken for a production-complete design.
- Avoid speculative abstractions, multiple cache strategies, infrastructure-heavy setup, or unrelated features that would endanger the deadline.
````

### Scenario E — Code passes but explanation and map fail

````text
## Scenario E

### 1. Proposed user-facing response/action plan

> I wouldn’t mark transactions complete yet. Your implementation passes, but one required understanding check is still open: why the inventory read must be protected by the same lock/transaction as the validation and update.
>
> The key issue is a time-of-check/time-of-use race:
>
> 1. Transaction A reads stock = 1.
> 2. Transaction B reads stock = 1.
> 3. Both later acquire a lock and act on that stale value.
> 4. Both may approve the purchase.
>
> Acquiring the row lock as part of the read—for example, with `SELECT … FOR UPDATE`—serializes the protected **read → validate → decrement** sequence. A preliminary unlocked read is safe only if the value is re-read and revalidated after acquiring the lock.
>
> Here is the reference architecture:
>
> ```mermaid
> flowchart LR
>     C["Client"] --> O["Order service"]
>     O --> T["Begin database transaction"]
>     T --> L["Lock inventory row and read current stock"]
>     L --> V{"Enough stock?"}
>     V -- "No" --> R["Rollback / reject"]
>     V -- "Yes" --> U["Decrement inventory"]
>     U --> N["Create order"]
>     N --> M["Commit"]
>     M --> X["Release row lock"]
> ```
>
> I’m treating this as a reference diagram, not evidence that you can reconstruct the flow yourself. Before we move to message queues, give me two short answers:
>
> 1. Show the unsafe two-transaction interleaving when an unlocked inventory value is reused after the lock is acquired.
> 2. Redraw the critical path from memory and label the invariant the transaction protects.
>
> Once you can do those, I’ll mark the topic complete and move directly to message queues. No additional transaction lecture is needed.

### 2. Decision log

- Inspect whether passing tests demonstrate only behavior or also conceptual understanding.
- Refuse to record false completion while the explanation and architectural map remain unverified.
- Explain the exact concurrency race, including the nuance that re-reading under lock can make a preliminary read harmless.
- Provide the requested diagram as a reference, but require learner reconstruction rather than treating assistant-produced work as mastery evidence.
- Avoid moving to the next topic until a short, explicit checkpoint closes the gap.
````

### Scenario F — Advanced learner

````text
## Scenario F

### 1. Proposed user-facing response/action plan

> Here’s a compact transfer exercise—no introductory material.
>
> ## Exercise: same invariant, two lock authorities
>
> You must preserve:
>
> > Confirmed reservations for a SKU must never exceed its available inventory.
>
> Design `reserve(sku, quantity)` twice:
>
> **A. Database pessimistic locking**
>
> - PostgreSQL is the source of truth.
> - Use a transaction and row-level pessimistic locking.
>
> **B. Distributed locking**
>
> - Three service instances contend for the same SKU.
> - Use a lease-based distributed lock such as etcd or Redis.
> - Inventory still ultimately resides in PostgreSQL.
>
> For both designs, submit:
>
> 1. Ten lines or fewer of pseudocode.
> 2. A comparison table covering:
>    - protected resource and lock scope;
>    - authority granting the lock;
>    - acquisition and release;
>    - crash behavior;
>    - timeout/deadlock handling;
>    - stale-owner behavior;
>    - whether the invariant survives process pauses and network partitions.
> 3. A failure trace for this case:
>    - Worker A acquires the lock.
>    - A pauses longer than the lease.
>    - Worker B acquires the lock and commits.
>    - A resumes and attempts to commit.
> 4. Your verdict: when does the distributed lock add value, and when is the database row lock or a conditional database update still the actual correctness boundary?
>
> **Constraint:** “Only one worker normally enters the critical section” is not a sufficient correctness argument.
>
> **Completion criteria:** identify the stale-owner problem, discuss fencing or an equivalent authoritative conditional write, and avoid treating a distributed lock as an automatic replacement for a database transaction.

### 2. Decision log

- Accept the learner’s demonstrated transaction and isolation knowledge; do not repeat fundamentals.
- Create a narrow transfer exercise based on one invariant implemented under two different lock authorities.
- Include lease expiry, process pause, and stale-owner behavior because these expose the important semantic difference.
- Require a design comparison and failure trace rather than a vocabulary-only answer.
- Avoid implying that a distributed lock alone guarantees correctness for data ultimately governed by the database.
````

## Baseline Failure Patterns

| Scenario | Baseline result | Observed behavior and evidence | Scenario-specific finding |
| --- | --- | --- | --- |
| A | PARTIAL | It protects the dirty worktree, inspects conventions, and avoids stash/reset/business edits. It also says, “I’ll start immediately and won’t ask Git questions,” then commits to “Create a new local learning branch/worktree” and complete unsafe, pessimistic, and optimistic examples. | Safety is partly preserved, but mutation is planned without minimum consent, the conflict is not surfaced as a boundary requiring consent, and the assistant owns the complete solution. |
| B | PARTIAL | “You will edit exactly one decision function; I’ll supply everything else.” The output uses real `data/products.json` records, keeps routing pure and learner-owned, and supplies the harness without requiring credentials or synthetic fixtures. It also says, “The graph will be completely deterministic and require no LLM” and records “Avoid: LLM calls.” | Real-data reuse, a prepared harness, and learner-owned routing are visible. A deterministic LLM stand-in is not described; “no LLM needed” is not evidence that this expected stand-in exists, so that criterion is absent or unverified. |
| C | FAIL | The output chooses to “trace authentication across both repositories” and explicitly records, “Avoid asking the user to choose Java or Python before repository inspection reveals whether that choice is actually necessary.” | It does not ask the required single blocking target-repository question before file work and risks unnecessary cross-repository inspection and demo work. |
| D | FAIL | It promises, “I’ll build the complete minimal runnable cache-aside demo now, including the hit/miss logic—no TODO placeholders,” and rationalizes, “Honor the explicit request for a complete implementation rather than withholding the central hit/miss logic or replacing it with TODOs.” The explanation comes only “After it runs.” | It writes the target logic for the learner and accepts passive read-later learning instead of using a minimal worked example/checklist and preserving learner ownership in the completion demo. |
| E | PARTIAL | It correctly says, “I wouldn’t mark transactions complete yet,” distinguishes passing implementation from the missing understanding check, explains the race, and requires a learner response before advancing. It then says, “Here is the reference architecture:” and supplies the finished diagram before asking the learner to redraw it. | Runtime-versus-topic completion is handled correctly, but the assistant provides the reference map before the learner’s first sketch rather than eliciting the sketch, correcting it, and requiring a focused rewrite. |
| F | PASS | “Here’s a compact transfer exercise—no introductory material.” The exercise centers on prediction and tradeoffs through two lock authorities, a lease-expiry failure trace, stale ownership, fencing/conditional writes, and an explicit correctness verdict. | It adapts to advanced expertise and delivers the requested compressed transfer exercise without repeating beginner material. |

Separately from the scenario-specific rubric, Scenario B does not show the broader v2 learning loop of explanation, learner exercise, execution feedback, reconstruction, and teach-back. That cross-scenario observation does not change its scenario-specific PARTIAL result.

## GREEN: Outputs With v2 Skill

Later phases will append GREEN evidence under this heading.

## REFACTOR: Pressure and Meta-tests

Later phases will append REFACTOR and meta-test evidence under this heading.

## Final Matrix

Later phases will append the final cross-phase matrix under this heading.
