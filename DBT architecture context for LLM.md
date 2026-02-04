---
created: 2026-02-03T10:58
updated: 2026-02-03T11:00
---

## SPOKES – Per-Subdomain Layers
Each spoke represents one **subdomain** (e.g., Sales, Purchasing, Inventory) and has the same internal structure.
### 1 Staging (SPOKE)
- **Goal:** Adapt HUB data to the needs of a specific subdomain.
- **Characteristics:**
  - Performs **soft transformations**:
    - Light renaming
    - Type casting
    - Basic filtering
    - Domain-specific shaping without heavy business logic
  - Reads from HUB via **cross-project references** (e.g., dbt cross-project refs).
  - Retains a relatively “source-close” structure but tailored to the subdomain.
- **Reference:** https://kramphub.atlassian.net/wiki/spaces/BI/pages/6566805505
### 2 Enriched & Integrated
This is where the **Integrated Data Model (IDM)** for the subdomain lives.
- **Overall Goal:** Create a consistent, historized, and integrated domain model.
#### 2.1 Enriched
- **Goal:** Cleanse and enrich data per **source system**.
- **Characteristics:**
  - Source-by-source modeling.
  - Adds:
    - Data quality rules
    - Derivations
    - Enrichments
  - Still reflects the structure of the originating system, but improved and standardized.
#### 2.2 Integrated
- **Goal:** Combine enriched datasets into a **single coherent domain model**.
- **Characteristics:**
  - Integrates multiple sources into unified entities (e.g., unified customer, product, order).
  - Supports:
    - Historical tracking (slowly changing dimensions, record versioning, etc.).
    - Complex relationships and keys.
  - Modeled using:
    - **Data Vault** concepts (hubs, links, satellites) where appropriate.
    - **3rd Normal Form (3NF)** for clarity and relational integrity.
- **Reference:** https://kramphub.atlassian.net/wiki/spaces/BI/pages/6395922713
---
## 3. Presentation Layers (SPOKE)
Purpose: Provide **consumer-ready models**, typically in **star schema** form, optimized for analytics and BI tools.
There are three presentation sub-layers with different visibility and sharing semantics.
### 3.1 Presentation Common
- **Goal:** Share domain data that is **safe and useful for all subdomains**.
- **Characteristics:**
  - Public data products / data sets.
  - Accessible across the entire DWH landscape.
  - Often contains:
    - Standard dimensions (e.g., calendar, geography).
    - Widely-used facts (e.g., global sales metrics).
### 3.2 Presentation Prep
- **Goal:** Provide a **private working area** inside a domain.
- **Characteristics:**
  - Not visible to other domains.
  - Not directly exposed to end consumers.
  - Used to:
    - Prepare transformations using another domain’s published data.
    - Stage data before publishing final models into Presentation Common or Presentation \<Sub Domain\>.
  - Acts as a sandbox / internal prep area.
---
## Data Flow & Governance Rules
- **Flow Direction:** Always **left → right**:
  1. Sources → HUB Landing
  2. HUB Landing → HUB Staging → HUB Intermediate → HUB Kramp Sub Domains
  3. HUB → SPOKE Staging
  4. SPOKE Staging → Enriched → Integrated → Presentation
- **No Backflow:** Data must not flow from right to left or skip layers in non-approved ways.
- **Inter-Domain Sharing:**
  - Only via **Presentation layers** (Common or targeted subdomain presentations).
  - No direct consumption of another domain’s Enriched/Integrated layers.
- **Implementation Notes:**
  - dbt Cloud ensures no circular dependencies in Presentation.
  - Orchestration must enforce the left-to-right sequencing.
---
## Quick Layer Cheat Sheet

| SPOKE | Staging             | Domain-specific soft transforms of HUB data         | Internal within subdomain |
| ----- | ------------------- | --------------------------------------------------- | ------------------------- |
| SPOKE | Enriched            | Source-specific enriched domain data                | Internal within subdomain |
| SPOKE | Integrated          | Unified domain model (IDM), historized & integrated | Internal within subdomain |
| SPOKE | Presentation Common | Shared, public analytical models                    | All domains               |
| SPOKE | Presentation Prep   | Private working area, pre-publication               | Internal within subdomain |
