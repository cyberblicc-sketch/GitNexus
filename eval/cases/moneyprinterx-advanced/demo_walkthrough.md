# Demo Walkthrough — MoneyPrinterX Advanced with GitNexus

This walkthrough is a canned live demo script for showing how GitNexus can analyze a multi-layer application like `MoneyPrinterX_advanced`.

## Demo objective

Show that GitNexus can:

- index a realistic backend scaffold
- surface architecture without manual reading
- trace runtime processes across layers
- identify safe extension points
- quantify blast radius before edits

## Setup

Extract the uploaded scaffold and run:

```bash
cd MoneyPrinterX_advanced
npx gitnexus analyze --skills --embeddings
```

Optional local web connection:

```bash
gitnexus serve
```

If using the browser UI locally, open the web app and let it auto-detect the GitNexus backend.

---

## Demo flow

### Step 1 — prove the repo is indexed

```text
list_repos()
```

Narration:
- We start by confirming the repo is indexed and available to MCP tools.
- This removes ambiguity when multiple repos are registered.

### Step 2 — recover the top-level architecture

```text
query({ query: "api routers services workflows agents providers compliance models", repo: "MoneyPrinterX_advanced" })
```

Narration:
- This query should recover the main architecture seams quickly.
- We want to see whether GitNexus groups symbols into meaningful processes and layers rather than returning disconnected keyword hits.

Expected takeaway:
- API
- services
- workflows
- agents
- providers
- compliance
- persistence/contracts

### Step 3 — inspect the workflow hub

```text
context({ name: "campaign", repo: "MoneyPrinterX_advanced" })
```

Narration:
- Now we pivot from broad structure into a likely orchestration hub.
- GitNexus should show incoming references, outgoing dependencies, and process membership.

Expected takeaway:
- workflow-centered orchestration
- related services
- planner/writer/scorer adjacency
- policy or approval references nearby

### Step 4 — show the main runtime path

```text
query({ query: "campaign planning drafting scoring approval publishing", repo: "MoneyPrinterX_advanced" })
```

Narration:
- This is the core operator question: how does the system actually run?
- We expect process-grouped results rather than isolated functions.

Expected takeaway:
- request entry
- service coordination
- workflow execution
- planner
- writer
- scorer
- compliance / approval
- provider interaction

### Step 5 — inspect the safety layer

```text
context({ name: "policy", repo: "MoneyPrinterX_advanced" })
context({ name: "approval", repo: "MoneyPrinterX_advanced" })
```

Narration:
- This demonstrates cross-cutting concerns.
- A good graph should show that compliance and approval are not a single isolated file but a dependency seam across workflows and publishing logic.

Expected takeaway:
- policy touches multiple layers
- approval state is central to safe publishing
- these are high-leverage, high-risk change points

### Step 6 — measure blast radius before a change

```text
impact({ target: "policy", direction: "upstream", maxDepth: 4, repo: "MoneyPrinterX_advanced" })
```

Narration:
- Before editing policy logic, we want to know what depends on it.
- This is where GitNexus should outperform manual grep.

Expected takeaway:
- which routers, services, or workflows are exposed to policy changes
- how deep the dependency chain goes
- whether the change is low, medium, or high risk

### Step 7 — find the best extension seam

```text
impact({ target: "factory", direction: "downstream", maxDepth: 4, repo: "MoneyPrinterX_advanced" })
```

Narration:
- Instead of editing orchestration directly, we want to find the safest place to add a real external integration.
- Provider factory and interfaces are likely the correct seam.

Expected takeaway:
- provider abstractions are downstream of workflow logic
- factory is the preferred adapter insertion point
- this avoids rewriting orchestration or contracts

### Step 8 — demo change detection

```text
detect_changes({ scope: "all", repo: "MoneyPrinterX_advanced" })
```

Narration:
- After a hypothetical edit, GitNexus should tell us what processes and symbols are affected.
- This closes the loop from understanding to safe change execution.

---

## Strong close

Suggested summary:

> MoneyPrinterX Advanced is small enough to follow, but rich enough to stress the graph. If GitNexus can recover the architecture, process flow, safety gates, and extension seams here in minutes, it proves the product is doing more than search — it is recovering operational structure.

## Bonus web demo

In the web UI, walk through this order:

1. overview graph
2. cluster or community around workflows
3. select policy / approval-related node
4. inspect dependencies
5. show process trace for campaign execution

## Bonus wiki demo

Use the prompts from `wiki_prompt_pack.md` to generate a short live architecture page after the graph walkthrough.
