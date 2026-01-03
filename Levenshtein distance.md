---
created: 2025-11-03T11:41
updated: 2025-11-16T08:36
tags:
  - statistics
---
## The original Levenshtein idea

Levenshtein distance measures **how many single-character edits** are needed to transform one string into another.  
Each edit can be:

- **Insertion** (add a character)  
- **Deletion** (remove a character)
- **Substitution** (replace one character with another)

So the distance between `"kitten"` and `"sitting"` is 3 (`k→s`, add `i`, add `g`).

## Formula I use
I use a normalized formula, where we normalize by dividing by the string length. 

```js
var strlen = Math.max(a.length, b.length);
return 1.0 - (matrix[b.length][a.length] / strlen);
```

## used in SQL
this formula is available in #GBQ as a #UDF[[levenshtein distance UDF]]
