---
created: 2025-11-18T19:44
updated: 2025-11-18T20:04
tags:
  - elastic
  - elastic/challenges
---
## problem
it tokenizes non-battery specifications as well; 
example: 
`5w40` which is an oil specification. it gets tokenized into `5w` , `40` and `5` because of this filter

```json
GET /kramp-sherlock-item-nl/_analyze

{
"analyzer": "search_text--standard_index_analyzer",
"explain": true,
"text": "motorolie 5w40"
}
```

## example
searching for `motorolie 5w40` gives different results now than searching for `motorolie 5w-40`
## solution
use 2 more stricter char_filters. one for voltage then capacity, the other for first capacity then voltage


```json
"search_text--battery_specification_voltage_capacity_charfilter":
{
  "type": "pattern_replace",
  "flags": "CASE_INSENSITIVE",
  "pattern": "(?<!\\S)(\\d+(?:[.,]\\d+)?)\\s*(v)\\s*(\\d+(?:[.,]\\d+)?)\\s*(a?h|wh)(?=\\s|$|-)",
  "replacement": "$1$2 $3$4 $1 $3 "
}

```

```json
"search_text--battery_specification_capacity_voltage_charfilter":
{
  "type": "pattern_replace",
  "flags": "CASE_INSENSITIVE",
  "pattern": "(?<!\\S)(\\d+(?:[.,]\\d+)?)\\s*(a?h|wh)\\s*(\\d+(?:[.,]\\d+)?)\\s*(v)(?=\\s|$|-)",
  "replacement": "$1$2 $3$4 $3 $1 "
}

```
