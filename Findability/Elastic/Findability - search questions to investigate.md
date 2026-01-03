---
created: 2025-11-20T20:48
updated: 2025-11-21T08:45
tags:
  - elastic
  - findability
---
### `trillingsdemper 30mm`
#### problem
- no results, should have many

#### cause
- attribute values are `30.0` and/or `30.0 mm`
- no match between 30.0 and 30

#### solution
- analyzer for attributes should replace .0 