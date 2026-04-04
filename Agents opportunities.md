---
created: 2026-02-13T10:58
updated: 2026-04-03T08:56
---
## DBT coding agent
- OpenCode
- DBT MCP
## Analyst Agent
### first version
- opencode
- parquet file with metrics
- duckdb

### second version
- opencode
- DBT MCP

### final version
- langchain?
- connected through Slack/Teams
- DBT MCP

## Search specialist
### First version
- custom GPT

### Second/Final version
- langchain?
- Tools: 
	- connected through Elastic API and/or MCP
- Interface: connected through Slack/Teams

Every `@laplace` session follows this flow. Morpheus bookends the work to keep

`findings.md` current and shared across all installations.

  

```mermaid

flowchart TD

U([User question]) --> L["@laplace"]

  

L -->|sync-in| M_IN["@morpheus — sync-in"]

M_IN -->|git pull + curate| FIN[(findings.md)]

FIN -->|read| L

  

L -->|decomposes & delegates| D["@descartes — dbt analyst"]

L -->|decomposes & delegates| A["@argus — relevance engineer"]

L -->|decomposes & delegates| LN["@linnaeus — product specialist"]

L -->|decomposes & delegates| Q["@qualia — UX researcher"]

  

D -->|data findings| L

A -->|config findings| L

LN -->|catalog findings| L

Q -->|UX findings| L

  

L -->|synthesise + write new findings| FOUT[(findings.md)]

  

FOUT -->|sync-out| M_OUT["@morpheus — sync-out"]

M_OUT -->|git commit + push| R[(remote)]

  

L --> ANS([Signal · Diagnosis · Recommendation])

```

  

`@morpheus` can also be invoked directly or via `/curate-findings` to run a standalone

curation and sync cycle outside of a `@laplace` session.

```mermaid

sequenceDiagram

actor User

participant Laplace as @laplace

participant Morpheus as @morpheus

participant Agents as @descartes · @argus · @linnaeus · @qualia

participant Git as Remote git

  

User->>Laplace: asks findability question

  

Laplace->>Morpheus: sync-in

Morpheus->>Git: git pull --rebase

Git-->>Morpheus: latest findings

Morpheus->>Morpheus: curate findings.md

Morpheus-->>Laplace: pull confirmed, findings current

  

Laplace->>Laplace: read findings.md

Laplace->>Agents: delegate scoped sub-questions

Agents-->>Laplace: domain findings

  

Laplace->>Laplace: synthesise · diagnose · recommend

Laplace->>Laplace: write new findings to findings.md

  

Laplace->>Morpheus: sync-out

Morpheus->>Git: git commit + push

Morpheus-->>Laplace: pushed

  

Laplace-->>User: Signal · Diagnosis · Recommendation

```
