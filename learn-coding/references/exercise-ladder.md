# Exercise Ladder

Use this reference to construct one focused learning sequence. Keep the target small enough to rewrite in one sitting.

## 1. A Example Package

Provide:

```text
Topic and production mapping:
Behavioral requirement:
Input and expected output:
Complete minimal implementation:
Tests and run command:
Expected trace or state changes:
Reasoning for important decisions:
Reusable structure:
Scenario-specific rules:
One common wrong implementation and why it fails:
```

Before execution, ask the learner for the important branch, order, state change, output, and reason. After execution, reconcile prediction with evidence.

The A example must be complete. Do not replace missing design knowledge with empty methods or fill-in markers.

## 2. Closed-Reference Package

Hide or close the implementation. Retain only:

```text
Requirement
Interfaces or signatures
Inputs and expected observations
Business constraints and failure behavior
Tests
Run command
```

The first rewrite may preserve the A example's scenario. The learner writes the core flow from a blank file. After tests:

1. compare behavior and structure;
2. classify mismatches with the review rubric;
3. ask why the learner expected the wrong behavior;
4. require a focused correction;
5. show the reference only for comparison;
6. close it and require a second rewrite.

Do not claim transfer after memorization.

## 3. B Isomorphic Transfer Package

Preserve the principle and change the scenario. Require at least one new business decision; renaming entities is insufficient.

Before coding, the learner states:

```text
Reusable structure from A:
Business rule that differs:
Expected new flow:
Failure behavior:
Smallest implementation plan:
```

Supply tests for observable behavior, not the internal algorithm. Avoid helper names or fixture arrangements that reveal the decision order.

## 4. Changed-Constraint Package

Choose one constraint that changes design:

- missing or conflicting data;
- duplicate registration or idempotency;
- timeout, retry, or circuit breaking;
- concurrent access;
- new tool or strategy without central modification;
- unified success/error result;
- trace or metric evidence;
- changed source-of-truth ownership.

The learner states:

```text
Invariant that remains:
Rule that changes:
Why the old design is insufficient:
New trace or state change:
Smallest adaptation:
New test:
```

## 5. Solution Leakage Guard

The assistant may provide setup and deterministic dependencies. Keep target decisions learner-owned.

Do not encode the answer in:

- comments inside the learner region;
- test names that state the algorithm;
- fixture ordering that forces one solution;
- one helper per required step;
- pseudocode before the learner reaches that hint rung.

## ToolRegistry Blueprint

### A example

Build a minimal Java flow:

```text
UserRequest -> IntentRouter -> ToolRegistry -> Tool.execute -> ToolResult
```

Include three tools, duplicate-registration rejection, an unknown-tool result, and JUnit tests. Explain why the registry owns lookup while the router owns selection.

### Closed-reference rewrite

Keep `Tool`, `ToolResult`, requirements, and tests. Hide `ToolRegistry` and routing implementation. The learner rebuilds registration, lookup, execution, and failure handling.

### B transfer

Change clothing tools to after-sales tools: refund lookup, logistics lookup, and human handoff. Require the learner to define selection and unknown-intent behavior.

### Changed constraint

Choose one: execution timeout, concurrent lookup, replace-versus-reject registration policy, trace events, or adding a tool without modifying central routing code.
