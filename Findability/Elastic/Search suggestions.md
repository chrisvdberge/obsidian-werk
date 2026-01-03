---
created: 2025-10-02
updated: 2025-10-31T17:34
tags:
  - findability
  - elastic
---

Search suggestions are populated from Redis. This pulls data from GBQ which is combining Snaga functional logging interaction data with Sherlock events data. 
- Snaga functional logging was turned off in october 2024
- Snaga was stopped around may 2025. 
- So no more data as of these dates, making the search suggestions dataset stale
- 
![[Scherm­afbeelding 2025-10-02 om 13.05.31.png]]

[[SSR]] for term suggestions usage has been going down around 90 days after dataset became stale. 

## new setup
a new setup should make use of its own index and be populated by the dataset `pres__obt__search_suggestions`
