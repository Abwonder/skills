# Enterprise Elevation

After the concept is solid, place it in production. Do not bolt this on as
trivia — frame each item as a decision an engineer actually makes. An ADR-style
"we chose X over Y because Z" teaches more than a bullet list.

## Cover at least these five

### 1. At scale
What changes when the thing runs at 1000x? Memory, contention, hot paths,
amortised cost, caching layers. Quantify direction ("this becomes the bottleneck
because..."), never invent numbers.

### 2. Failure modes
What breaks first? Partial failure, timeout, crash, corrupt state, retry storm.
Describe the failure, the blast radius, and the mitigation.

### 3. Security
What is the attack surface the concept creates? Input trust, injection, leakage,
race conditions, least privilege. State the threat and the control.

### 4. Observability
How do you know it is working in production? What to log, what metric captures
it, what alert fires when it degrades, what trace shows the path.

### 5. Tradeoffs (as decisions)
Every real choice is a trade. Present it as a decision with alternatives and a
reason, not a preference:

```
Decision: cache the function vs recreate every render
- Option A: memoize (stable identity, memory retained, dependency bookkeeping)
- Option B: recreate (simpler, no deps to keep honest, may cause re-render churn)
→ Chose A because a child depends on identity stability; accepted the dep risk.
```

## System design / architecture connection

Where does the concept sit in a real system? Draw the boundary in words:

- What owns the state, and what observes it?
- What is the data flow (request → handler → state → render)?
- What is the lifecycle (create → use → teardown)?
- Where does it couple, and how do you decouple it?

A text diagram (boxes + arrows) is better than a paragraph when the concept is
structural. Use monospace ASCII:

```
render(state) ──► new scope ──► new bindings
      ▲                            │
      └────── memoized fn (old scope)  ← stale reference
```

## Standards and patterns to reference (when they apply)

- Name the industry pattern (e.g. memoisation, idempotency, backpressure,
  circuit breaker, single-writer, eventual consistency).
- Reference the relevant principle (SOLID, CAP, CQRS, etc.) only when it actually
  explains the choice — never as decoration.
- If there is an official spec or RFC, cite it once with a deep link.

## Rule

No invented benchmarks, no "in production everyone does X" without a source or a
demonstration. If you cannot support a production claim, say "typical" and mark it
as a heuristic, not a fact.
