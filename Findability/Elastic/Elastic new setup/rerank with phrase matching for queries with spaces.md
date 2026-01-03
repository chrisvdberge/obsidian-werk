---
created: 2025-10-30T09:31
updated: 2025-10-30T16:53
tags:
  - elastic
  - elastic/challenges
---
### use rerank with phrase matching to favour adjecancy of tokens

|                     |                                                                                                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| description::       | we have many cases where the search query will result in multiple tokens. These can match across different fields and if they do, they'll outrank documents where the match is in one field |
| example::           | search query `100-100-620`<br>search query `bolt 22x55mm`                                                                                                                                   |
| impact::            | better rankings                                                                                                                                                                             |
| recall or ranking:: | [[ranking]]                                                                                                                                                                                 |
| key metric::        | [[NDCG]]                                                                                                                                                                                    |
| proposed solution:: | If search_query has space then use rerank with phrase matching<br>for full query see below;                                                                                                 |
| actions::           |                                                                                                                                                                                             |
| Jira ticket::       |                                                                                                                                                                                             |
```json
"rescore": {
  "window_size": 800,
  "query": {
    "rescore_query": {
      "match_phrase": {
        "item_description.standard": {
          "query": "{{search_query}}",
          "slop": 1,
          "boost": 2.0
        }
      }
    },
    "query_weight": 1.0,
    "rescore_query_weight": 1.0
  }
}
```