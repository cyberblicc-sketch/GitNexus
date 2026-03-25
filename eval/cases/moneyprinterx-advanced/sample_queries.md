# Sample GitNexus Queries — MoneyPrinterX Advanced

Use these after indexing the extracted MoneyPrinterX Advanced project.

## Search the main architecture seams

```text
query({ query: "api routers services workflows agents providers compliance models", repo: "MoneyPrinterX_advanced" })
```

## Find the campaign orchestration process

```text
query({ query: "campaign planning drafting scoring approval publishing", repo: "MoneyPrinterX_advanced" })
```

## Inspect workflow context

```text
context({ name: "campaign", repo: "MoneyPrinterX_advanced" })
```

## Inspect compliance / approval context

```text
context({ name: "policy", repo: "MoneyPrinterX_advanced" })
context({ name: "approval", repo: "MoneyPrinterX_advanced" })
```

## Measure impact before changing safety logic

```text
impact({ target: "policy", direction: "upstream", maxDepth: 4, repo: "MoneyPrinterX_advanced" })
impact({ target: "approval", direction: "upstream", maxDepth: 4, repo: "MoneyPrinterX_advanced" })
```

## Measure provider abstraction blast radius

```text
impact({ target: "factory", direction: "downstream", maxDepth: 4, repo: "MoneyPrinterX_advanced" })
```

## Detect changes after editing workflow files

```text
detect_changes({ scope: "all", repo: "MoneyPrinterX_advanced" })
```

## Rename example

Use dry-run first.

```text
rename({ symbol_name: "policy", new_name: "compliance_policy", dry_run: true, repo: "MoneyPrinterX_advanced" })
```

## Cypher ideas

Find dense workflow-adjacent symbols:

```cypher
MATCH (s)-[r:CodeRelation]->(t)
WHERE toLower(s.filePath) CONTAINS 'workflow' OR toLower(t.filePath) CONTAINS 'workflow'
RETURN s.name, type(r), t.name
LIMIT 50
```

Find cross-cutting safety references:

```cypher
MATCH (s)-[r:CodeRelation]->(t)
WHERE toLower(s.name) CONTAINS 'policy' OR toLower(t.name) CONTAINS 'policy'
RETURN s.name, type(r), t.name, r.confidence
ORDER BY r.confidence DESC
LIMIT 50
```

## Best evaluation prompts for agents

- Explain the shortest path from HTTP router to provider factory.
- Show which modules are most likely to break if approval rules change.
- Summarize the campaign execution flow as a process map.
- Find the safest extension point for adding a real publishing adapter.
- Identify which layers are purely contracts versus orchestration.
