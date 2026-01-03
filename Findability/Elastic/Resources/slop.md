---
created: 2025-10-30T16:57
updated: 2025-10-30T16:59
tags:
  - elastic
  - elastic/documentation
  - slop
---
In a [[phrase query]], Elasticsearch normally requires the **exact same terms in the exact same order** and **adjacent** (no gaps).

Example:

Query `"eye bolt"`  
→ will only match `"eye bolt"` exactly (tokens must be consecutive).

If the doc says:

- `"eye heavy duty bolt"` → ❌ no match (because there’s one token gap).
- `"bolt eye"` → ❌ no match (wrong order).    

`slop` relaxes that strictness by allowing:
- **Gaps** between the words, and/or
- **Swapped order** within a small distance (depending on analyzer).

---
## ⚙️ 2. How it works numerically

`slop` = maximum **edit distance** between word positions in the phrase.
- `slop: 0` → strict adjacency (default).
- `slop: 1` → allow up to one word gap or a minor reordering.
- `slop: 2` → up to two gaps or distance between phrase tokens ≤ 2.
- etc.

So with `slop: 1`, the query `"eye bolt"` would match:

|Text|Match?|Why|
|---|---|---|
|`"eye bolt"`|✅|exact|
|`"eye heavy bolt"`|✅|one gap allowed|
|`"eye stainless steel bolt"`|❌|two gaps (needs `slop ≥ 2`)|
|`"bolt eye"`|✅ sometimes, if token order is close enough and analyzer keeps both tokens||