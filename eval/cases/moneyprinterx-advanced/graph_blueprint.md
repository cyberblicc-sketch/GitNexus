# Graph Blueprint — MoneyPrinterX Advanced

This file defines the **graph model expectations** GitNexus should infer when indexing the MoneyPrinterX Advanced scaffold.

## Layered dependency blueprint

```mermaid
flowchart LR
    subgraph API
      R1[auth router]
      R2[projects router]
      R3[campaigns router]
      R4[workflows router]
      R5[assets router]
      R6[approvals router]
    end

    subgraph Services
      S1[auth service]
      S2[projects service]
      S3[campaigns service]
      S4[workflows service]
      S5[assets service]
      S6[approvals service]
      S7[events service]
    end

    subgraph Workflow
      W1[campaign workflow]
    end

    subgraph Agents
      A1[planner]
      A2[writer]
      A3[scorer]
    end

    subgraph Safety
      C1[policy]
    end

    subgraph Providers
      P1[factory]
      P2[mock provider]
      P3[provider base]
    end

    subgraph Data
      D1[models]
      D2[schemas]
      D3[repository]
      D4[database]
    end

    R1 --> S1
    R2 --> S2
    R3 --> S3
    R4 --> S4
    R5 --> S5
    R6 --> S6

    S3 --> W1
    S4 --> W1
    S6 --> C1
    W1 --> A1
    W1 --> A2
    W1 --> A3
    W1 --> P1
    P1 --> P2
    P1 --> P3

    S1 --> D1
    S2 --> D1
    S3 --> D1
    S4 --> D1
    S5 --> D1
    S6 --> D1
    S7 --> D1
    S1 --> D2
    S2 --> D2
    S3 --> D2
    S4 --> D2
    S5 --> D2
    S6 --> D2
    W1 --> D3
    D3 --> D4
```

## Process hypotheses

### Process: campaign execution
- campaign router receives request
- campaigns service validates and persists state
- workflows service starts run
- campaign workflow invokes planner
- campaign workflow invokes writer
- campaign workflow invokes scorer
- compliance policy evaluates publishability
- approvals service records approval state
- events service emits lifecycle events

### Process: approval gate
- router or workflow requests approval
- approvals service creates approval object
- compliance policy checks risk
- workflow branches on approval result
- events service records approval event

### Process: provider resolution
- workflow requests provider
- provider factory selects active implementation
- agent or workflow calls provider interface
- result returns into schema / model boundary

## Best GitNexus queries

```text
query({ query: "campaign workflow planner writer scorer approval provider" })
```

```text
context({ name: "create_campaign" })
```

```text
impact({ target: "policy", direction: "upstream" })
```

```text
impact({ target: "factory", direction: "downstream" })
```

```text
query({ query: "event emission workflow run status" })
```

## What a strong graph result looks like

A strong result should reveal:

- the API layer as entry points
- services as coordination hubs
- workflow as the densest orchestration region
- compliance as a cross-cutting concern
- providers as late-bound dependencies
- models / schemas / repository as the persistence backbone
