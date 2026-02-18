---
created: 2026-02-17T13:12
updated: 2026-02-17T19:41
---

| version                                             | change type                    | slot milliseconds | slot time             |
| --------------------------------------------------- | ------------------------------ | ----------------- | --------------------- |
| original                                            |                                | 1,016,505,062     | 282 u, 21 min, 45 sec |
| page_path -> content_name                           | shorter strings in like filter | 887,657,681       | 246 u, 34 min, 17 sec |
| having -> where statement                           | having -> where                | 867,342,371       | 240 u, 55 min, 42 sec |
| customer_cd like 'C%' -> login_status = 'logged in' | like filter to exact filter    | 840,809,854       | 233 u, 33 min, 29 sec |
