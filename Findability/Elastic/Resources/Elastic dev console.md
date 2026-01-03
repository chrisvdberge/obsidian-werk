---
created: 2025-11-18T15:38
updated: 2025-11-18T15:41
tags:
  - elastic/resources
---


### check tokens produced for given analyzer
```json
GET /kramp-sherlock-item-nl/_analyze
{
"analyzer": "search_text--standard_index_analyzer",
"explain": false,
"text": "motorolie 5w40"
}
```

### check matching for given field
```json
GET kramp-sherlock-item-en/_explain/HZ100000473 { "query": { "function_score": { "query": { "bool": { "must": [ { "multi_match": { "fields": [ "ud.search.ids.supplier_item_number.edge_ngram" ], "operator": "and", "query": "100-100-224", "type": "cross_fields" } } ] } } } } }
```
