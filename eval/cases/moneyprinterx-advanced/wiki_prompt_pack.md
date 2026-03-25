# Wiki Prompt Pack — MoneyPrinterX Advanced

Use this pack after indexing the extracted `MoneyPrinterX_advanced` repo with GitNexus.

## Goal

Generate a repository wiki that demonstrates GitNexus' ability to:

- recover layered architecture
- identify workflow processes
- separate contracts from orchestration
- explain approval and compliance gating
- expose provider seams and extension points

## Recommended prep

From the extracted repo root:

```bash
npx gitnexus analyze --skills --embeddings
```

Then optionally generate the built-in wiki:

```bash
gitnexus wiki
```

Use the prompts below to validate or enrich the result.

---

## Prompt 1 — system overview

```text
Using the GitNexus graph for MoneyPrinterX_advanced, generate a system overview wiki page.
Explain the main architecture layers, the primary runtime path from HTTP router to workflow execution, and the role of models, schemas, providers, and compliance policy.
Return sections for Overview, Main Layers, Core Runtime Path, and Extension Points.
```

## Prompt 2 — process map

```text
Using GitNexus graph context for MoneyPrinterX_advanced, write a process-oriented wiki page for campaign execution.
Show the likely sequence from request entry to service coordination, workflow orchestration, planner, writer, scorer, compliance checks, approval state, and event emission.
Return a concise narrative plus a mermaid flowchart.
```

## Prompt 3 — compliance and approval

```text
Using the graph, generate a wiki page explaining how approval and compliance function as cross-cutting concerns in MoneyPrinterX_advanced.
Highlight which layers reference policy, which components should remain stable, and what changes would have the largest blast radius.
Return sections for Safety Boundaries, Dependency Hotspots, and Refactor Guidance.
```

## Prompt 4 — provider architecture

```text
Explain the provider abstraction in MoneyPrinterX_advanced using GitNexus graph data.
Focus on where the factory belongs in the execution flow, which modules depend on provider contracts, and the safest insertion point for a real external adapter.
Return sections for Provider Role, Dependency Structure, and Recommended Integration Pattern.
```

## Prompt 5 — codebase map

```text
Create a codebase map wiki page for MoneyPrinterX_advanced from the GitNexus graph.
Group the repository into API, services, workflows, agents, providers, compliance, models, schemas, and core platform.
For each area, explain what it is for, what it depends on, and what depends on it.
```

---

## Expected wiki outcomes

A strong GitNexus-backed wiki should show:

- routers as entry points
- services as coordination hubs
- workflows as orchestration centers
- planner/writer/scorer as agent subgraph
- policy and approval as cross-cutting graph edges
- providers as late-bound integration seams
- models/schemas as contract and persistence boundaries

## Evaluation notes

The generated wiki is good if it helps answer these questions quickly:

- Where do requests enter the system?
- What triggers campaign execution?
- Where does human approval sit?
- Which modules are safest to extend?
- Which changes have the highest blast radius?
