# MoneyPrinterX Advanced in GitNexus

This case study shows how to use **GitNexus** to map, query, and explain the `MoneyPrinterX_advanced` scaffold as a real multi-layer application graph.

## Why this case is useful

MoneyPrinterX Advanced is a compact but realistic backend system with:

- API routers
- service layer
- workflow orchestration
- agents
- provider abstraction
- compliance policy checks
- persistence models
- observability

That makes it a strong graph benchmark for GitNexus because the repo has both **horizontal architecture layers** and **vertical execution flows**.

## Source layout observed

Key areas in the uploaded scaffold:

- `src/moneyprinterx/api/routers/` — HTTP entry points
- `src/moneyprinterx/services/` — business logic
- `src/moneyprinterx/workflows/` — campaign orchestration
- `src/moneyprinterx/agents/` — planner, writer, scorer
- `src/moneyprinterx/providers/` — provider contracts and factory
- `src/moneyprinterx/compliance/` — policy gates
- `src/moneyprinterx/models/` — domain persistence models
- `src/moneyprinterx/schemas/` — typed contracts
- `src/moneyprinterx/core/` — settings, database, security, metrics

## What GitNexus should surface

### Expected clusters

1. **API Surface**
   - auth router
   - projects router
   - campaigns router
   - workflows router
   - assets router
   - approvals router

2. **Application Services**
   - auth service
   - projects service
   - campaigns service
   - assets service
   - approvals service
   - events service
   - workflows service

3. **AI Orchestration**
   - planner agent
   - writer agent
   - scorer agent
   - workflow campaign runner

4. **Safety / Compliance**
   - policy rules
   - approval requirements
   - publish preflight checks

5. **Persistence + Domain**
   - SQLAlchemy models
   - repository storage
   - schema contracts

6. **Platform Core**
   - settings
   - DI container
   - database session
   - security
   - metrics / middleware

## Recommended GitNexus workflow

Run from the extracted MoneyPrinterX Advanced repo root:

```bash
npx gitnexus analyze --skills --embeddings
```

Then use these tool flows.

### 1. List indexed repos

```text
list_repos()
```

### 2. Find the campaign execution path

```text
query({ query: "campaign workflow publish approval policy", repo: "MoneyPrinterX_advanced" })
```

### 3. Inspect the orchestration hub

```text
context({ name: "campaign", repo: "MoneyPrinterX_advanced" })
```

### 4. Measure blast radius before editing approval logic

```text
impact({ target: "approval", direction: "upstream", repo: "MoneyPrinterX_advanced" })
```

### 5. Trace service + router dependencies

```text
query({ query: "router service workflow event policy", repo: "MoneyPrinterX_advanced" })
```

## High-value questions GitNexus should answer well

- Which routers trigger workflow execution?
- Which service emits campaign or approval events?
- Where does policy gating sit relative to publishing?
- Which modules are safe to refactor without breaking orchestration?
- What is the shortest path from HTTP request to provider adapter?
- Which symbols form the approval-critical execution path?

## Success criteria

GitNexus performs well on this case if it can:

- isolate layered architecture cleanly
- group API -> service -> workflow -> provider flows into processes
- expose approval and compliance as a cross-cutting cluster
- identify provider abstraction as the seam for integrations
- show blast radius for changing policy, workflow, or schema contracts
