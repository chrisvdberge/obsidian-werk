---
created: 2025-12-02T13:20
updated: 2025-12-02T13:21
tags:
  - findability
  - findability/dataset
---
```sql
case
when
request_original_query <> ''
and request_original_query is not null
and lower(request_query) <> lower(request_original_query)
then 1
when request_query is null
then null
else 0

end as spell_suggestion_used,

case

when el.result_item_ids = '[]' and el.suggested_result_item_ids = '[]'

then 1

when el.result_item_ids is null

then null

else 0

end as zero_results,
```