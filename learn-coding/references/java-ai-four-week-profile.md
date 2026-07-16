# Java AI Four-Week Profile

Use this profile for a learner preparing for Java AI application interviews who can read project code but lacks independent implementation practice.

## Default Rhythm

Use roughly two hours per study day:

| Day | Work |
| --- | --- |
| Monday | 30 minutes of principles, then A example prediction, run, and explanation |
| Tuesday | Project-code location, then first closed-reference rewrite |
| Wednesday | Blank-file second rewrite and focused review |
| Thursday | B isomorphic transfer with tests |
| Friday | Changed constraint, refactor, and timed retrieval |
| Weekend | Project-integrated exercise and interview explanation |

Each week produces at least four focused Java exercises, one project-integrated exercise, tests for every exercise, one timed reconstruction, one changed constraint, and one concise design explanation.

Python supports reading and small RAG/Agent changes. It must not displace Java-first coding unless the learner explicitly changes the profile.

## Week 1: Architecture and Fact Boundaries

**Principles:** Java versus AI responsibility, database source of truth, request contracts, synchronous response versus SSE/MQ, failure ownership.

**Java exercises:**

1. Validate a recommendation request DTO and return structured validation errors.
2. Filter AI-proposed product IDs against Java-owned candidates and stock facts.
3. Design a sealed or typed success/error result contract.
4. Convert internal progress events into stable SSE event payloads.

**Integrated exercise:** Trace one Java -> Python -> Java recommendation request and implement a boundary validator that prevents generated price or stock facts.

**Interview follow-ups:** Why not let the model determine price? When choose SSE over MQ? What happens when the AI service times out?

## Week 2: RAG

**Principles:** chunking, embedding, Top-K retrieval, threshold rejection, citations, grounding, recall/precision trade-off, structured facts versus semantic knowledge.

**Java exercises:**

1. Split documents with stable IDs and overlap rules.
2. Select Top-K scored chunks with deterministic tie-breaking.
3. Reject results beyond a distance threshold and return an explicit unsupported outcome.
4. Assemble accepted evidence into a cited response context without losing metadata.

**Integrated exercise:** Reproduce the project's `top_k=3` and threshold decision with fixed scores, then explain why zero false accepts can be preferred over maximum positive recall.

**Python support:** Read the real retriever/evaluation path and make only a small parameter or evaluation-case change after the Java logic is understood.

**Interview follow-ups:** Why not put inventory in a vector database? How measure retrieval quality? How prevent hallucination after weak retrieval?

## Week 3: Agent

**Principles:** pipeline versus Agent, ReAct, tool calling, explicit state, conditional transitions, stop conditions, short-term versus long-term memory, multi-Agent boundary.

**Java exercises:**

1. Route a user request to one declared intent with an unknown outcome.
2. Implement `ToolRegistry` registration, lookup, execution, and duplicate handling.
3. Apply immutable or controlled state updates across Agent steps.
4. Enforce maximum steps and stop reasons to prevent loops.

**Integrated exercise:** Implement a deterministic Java Agent loop that mirrors the project's important LangGraph nodes and emits trace events for each transition.

**Python support:** Trace node, edge, conditional route, and checkpoint behavior in the real LangGraph code.

**Interview follow-ups:** When is a pipeline enough? Why explicit state? How handle tool failure? Why not use multiple Agents for every task?

## Week 4: Engineering and Interview Closure

**Principles:** timeout, retry, rate limiting, circuit breaking, idempotency, streaming contracts, trace/token/success metrics, evaluation, prompt injection, tool authorization.

**Java exercises:**

1. Implement a bounded retry policy that distinguishes retryable failures.
2. Implement a simplified circuit-breaker state transition with deterministic time.
3. Record trace events without leaking sensitive prompt or credential data.
4. Run deterministic evaluation cases and aggregate route, fallback, and pass metrics.

**Integrated exercise:** Wrap the recommendation call with timeout/fallback, trace it, run evaluation cases, and explain the safe failure behavior.

**Interview follow-ups:** What do you monitor? How distinguish model failure from retrieval failure? How authorize tools? What project trade-off would you change at larger scale?

## Four-Week Exit Evidence

The learner must independently reconstruct one Week 1 boundary component, one Week 2 retrieval component, one Week 3 Agent component, and one Week 4 reliability component. Then they explain one end-to-end request, one failure path, one measured trade-off, and one production limitation.
