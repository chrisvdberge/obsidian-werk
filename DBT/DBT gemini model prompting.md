---
created: 2025-11-25T17:10
updated: 2025-11-25T17:12
tags:
  - dbt
  - findability
  - sql
---

onboard model as source
```json
- name: findability_sources
	tags: ["findability"]
	project: kramp-webanalytics-prd
	dataset: findability
	description: additional data used for mappings in findability
	tables:
		- name: gemini__2_5__pro
```

then simply query it 
```sql
with

queries as (

select

search_query,

search_query_id,

sum(searches) as searches,

row_number() over (order by sum(searches) desc) - 0 as rn

from {{ ref("pres__obt__searches_mapped_master") }}

where

search_event_date >= "2024-01-01"

and query_type = "term"

-- and zero_results = 1

-- and (search_query like '%nettoyant%' or search_query like '%bremsen%')

and query_type_detail <> "kramp product number"

and search_query not in (

select distinct search_query

from {{ this }}

where search_query is not null

)

group by all

order by searches desc

limit 100

offset 0

),

  

llm_output as (

select *, ml_generate_text_llm_result as response

from

ml.generate_text(

model {{ source("findability_sources", "gemini__2_5__pro") }},

(

select

'''

You are a data extraction assistant. Given an input, return a structured JSON response with these fields:

{

"input": "the original input",

"translation": "translated input to English",

"type": "product/manufacturer/brand/technical specification",

"description": "Short description",

"functional_name": "Functional name"

}

The input is provided as a list of multiple inputs. You should return an array with JSON objects for each input.

Return only a valid JSON object, with no extra text, explanations, or formatting. Do not add phrases like "Here is the JSON you requested."

Do not include any additional text, formatting, or markdown. Do not add markdown json format for every response.

  

The input will be search queries that are used on a b2b ecommerce website in the agricultural machinery business. If they are brands or product number no translation is needed. Please translate the input to English in the other cases.

Just state if you are not sure or if you dont know any of the requested information. You can say 'Unknown' in those cases.

  

Here are some examples:

  

input: "nettoyant freins 20ml"

output: {

"input": "nettoyant freins 20ml",

"translation": "brake cleaner 20ml",

"type": "product",

"description": "brake cleaner",

"functional name": "brake cleaners"

}

  

input: "knorr"

output: {

"input": "knorr",

"translation": "knorr",

"type": "manufacturer",

"description": "manufacturer of braking systems",

"functional_name": "braking systems"

}

  

input: "100100"

output: {

"input": "100100",

"translation": "100100",

"type": "product",

"description": "cross journal",

"functional_name": "cross journal"

}

  

input: "worteldoek"

output: {

"input": "worteldoek",

"translation": "root canvas",

"type": "product",

"description": "geotextile to prevent plant root growth",

"functional_name": "geotextiles"

}

  

input: "kabelbinder"

output: {

"input": "kabelbinder",

"translation": "cable tie",

"type": "product",

"description": "cable tie",

"functional_name": "cable ties"

}

  

input: "m20"

output: {

"input": "m20",

"translation": "M20",

"type": "technical specification",

"description": "thread size",

"functional_name": "fasteners"

}

  

input: "topstang"

output: {

"input": "topstang",

"translation": "top link",

"type": "product",

"description": "top link",

"functional_name": "top links"

}

  

input: "maaimes"

output: {

"input": "maaimes",

"translation": "mowing blade",

"type": "product",

"description": "blades for agricultural mowers",

"functional_name": "mowing blades"

}

input: "rc12yc"

output: {

"input": "rc12yc",

"translation": "rc12yc",

"type": "product",

"description": "spark plug",

"functional_name": "spark plugs"

}

  

input: "42411243800"

output: {

"input": "42411243800",

"translation": "42411243800",

"type": "product",

"description": "Stihl blower air filter",

"functional_name": "air filters"

}

input: "PGLO1018"

output: {

"input": "PGLO1018",

"translation": "PGLO1018",

"type": "product",

"description": "swage coupling with o-ring, L-series cutting ring adapter",

"functional_name": "couplings"

}

  

'''

|| "input: ["

|| string_agg('"' || replace(search_query, '"', '') || '"')

|| "]" as prompt

from queries

),

  

struct(

0.2 as temperature,

8192 as max_output_tokens,

true as flatten_json_output

)

)

),

  

responses as (

  

select

-- response,

json_value(item, '$.input') as input,

json_value(item, '$.translation') as translation,

json_value(item, '$.type') as type,

json_value(item, '$.description') as description,

safe_cast(

json_value(item, '$.functional_name') as string

) as functional_name

  

from llm_output, unnest(json_extract_array(response)) as item

)

  

select

search_query_id,

search_query,

-- response,

translation,

type,

description,

functional_name

from responses

left join queries on input = search_query
```