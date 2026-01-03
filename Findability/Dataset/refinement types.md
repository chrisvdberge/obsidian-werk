---
created: 2025-11-09T18:15
updated: 2025-11-09T18:17
tags:
  - findability/dataset
---
```sql
with refinements as (select search_query,refinement_queries, query_type, sum(is_refined) as refinements, sum(refinements_success_count) as refinement_success from `kramp-edw-e-commerce-prd.presentation_common.pres__obt__searches_mapped_master`
where search_event_date >= "2022-01-01"
-- and webshop_visit_id = -8936834073787585006

-- and query_type = 'item'

-- and zero_results = 1

group by all

order by refinements desc

),

  

all_searches as (select search_query, sum(searches) as searches, sum(success) as success from `kramp-edw-e-commerce-prd.presentation_common.pres__obt__searches_mapped_master`

where search_event_date >= "2022-01-01"

group by search_query

)

select refinements.search_query, refinement_queries,

  

CASE

WHEN

REGEXP_REPLACE(LOWER(refinement_queries), r'\s+', '') =

REGEXP_REPLACE(LOWER(refinements.search_query), r'\s+', '')

AND ARRAY_LENGTH(SPLIT(REGEXP_REPLACE(LOWER(refinement_queries), r'\s+', ' '), ' ')) >

ARRAY_LENGTH(SPLIT(REGEXP_REPLACE(LOWER(refinements.search_query), r'\s+', ' '), ' '))

  

then 'spelling - space addition'

  

WHEN REGEXP_REPLACE(LOWER(refinement_queries), r'[\-]', '') =

REGEXP_REPLACE(LOWER(refinements.search_query), r'[\-]', '')

AND REGEXP_CONTAINS(refinement_queries, r'\-')

AND NOT REGEXP_CONTAINS(refinements.search_query, r'\-') then 'spelling - hyphen addition'

  

-- normalize: remove spaces only for equality check

WHEN REGEXP_REPLACE(LOWER(refinement_queries), r'\s+', '') =

REGEXP_REPLACE(LOWER(refinements.search_query), r'\s+', '')

-- but ensure refined has fewer spaces than original (local removal allowed)

AND (

LENGTH(refinements.search_query) - LENGTH(REGEXP_REPLACE(refinements.search_query, r'\s+', ''))

) >

(

LENGTH(refinement_queries) - LENGTH(REGEXP_REPLACE(refinement_queries, r'\s+', ''))

)

  

then 'spelling space removal'

  

WHEN REGEXP_REPLACE(LOWER(refinement_queries), r'[\-]', '') =

REGEXP_REPLACE(LOWER(refinements.search_query), r'[\-]', '')

AND REGEXP_CONTAINS(refinements.search_query, r'\-')

AND NOT REGEXP_CONTAINS(refinement_queries, r'\-')

THEN 'spelling - hyphen removal'

  

WHEN STARTS_WITH(LOWER(refinement_queries), CONCAT(LOWER(refinements.search_query), ' '))

AND REGEXP_CONTAINS(

SUBSTR(LOWER(refinement_queries), LENGTH(refinements.search_query) + 2),

r'^[a-z\s\-]+$'

)

AND NOT REGEXP_CONTAINS(

SUBSTR(LOWER(refinement_queries), LENGTH(refinements.search_query) + 2),

r'\d'

)

THEN 'specification - functional'

  

WHEN query_type = 'term'

AND ENDS_WITH(LOWER(refinement_queries), LOWER(refinements.search_query))

AND LENGTH(refinement_queries) > LENGTH(refinements.search_query)

AND REGEXP_CONTAINS(

SUBSTR(

LOWER(refinement_queries),

1,

LENGTH(refinement_queries) - LENGTH(refinements.search_query)

),

r'^\p{L}+$' -- prefix is letters only (no digits, no spaces)

)

THEN 'specification - functional prefix'

  
  

WHEN query_type = 'term'

AND STARTS_WITH(LOWER(refinement_queries), CONCAT(LOWER(refinements.search_query), ' '))

AND REGEXP_CONTAINS(

SUBSTR(LOWER(refinement_queries), LENGTH(refinements.search_query) + 2),

r'\d' -- any digit in the added suffix

)

THEN 'specification - attribute'

  

WHEN

EDIT_DISTANCE(

REGEXP_REPLACE(LOWER(refinements.search_query), r'[\s\-]', ''),

REGEXP_REPLACE(LOWER(refinement_queries), r'[\s\-]', '')

) BETWEEN 1 AND 2

AND refinements.query_type = 'term'

THEN 'spelling - term misspelling'

  

WHEN

EDIT_DISTANCE(

REGEXP_REPLACE(LOWER(refinements.search_query), r'[\s\-]', ''),

REGEXP_REPLACE(LOWER(refinement_queries), r'[\s\-]', '')

) = 1

AND refinements.query_type = 'item'

THEN 'spelling - item 1 character change'

  
  

WHEN query_type = 'item'

and starts_with(refinement_queries, refinements.search_query)

then 'specification - item_id extension'

  

when query_type = 'item'

and starts_with(refinements.search_query, refinement_queries)

then 'generalization - item_id shortening'

  

when query_type = 'item'

and edit_distance(refinements.search_query, refinement_queries) > 1

then 'differentation - different item_id'

  

WHEN query_type = 'term'

AND ENDS_WITH(LOWER(refinements.search_query), LOWER(refinement_queries))

AND LENGTH(refinements.search_query) > LENGTH(refinement_queries)

AND REGEXP_CONTAINS(

SUBSTR(

LOWER(refinements.search_query),

1,

LENGTH(refinements.search_query) - LENGTH(refinement_queries)

),

r'^\p{L}+(?:-\p{L}+)*$' -- prefix is letters only (optional internal hyphens)

)

THEN 'generalization - functional prefix removed'

WHEN query_type = 'term'

AND STARTS_WITH(LOWER(refinements.search_query), CONCAT(LOWER(refinement_queries), ' '))

AND REGEXP_CONTAINS(

SUBSTR(

LOWER(refinements.search_query),

LENGTH(refinement_queries) + 2

),

r'^[\p{L}\-]+$' -- suffix is letters (and optional hyphens)

)

THEN 'generalization - functional suffix removed'

  

WHEN query_type = 'term'

AND STARTS_WITH(LOWER(refinements.search_query), CONCAT(LOWER(refinement_queries), ' '))

AND REGEXP_CONTAINS(

SUBSTR(

LOWER(refinements.search_query),

LENGTH(refinement_queries) + 2

),

r'\d' -- any digit in the removed suffix

)

THEN 'generalization - numeric suffix removed'

  

WHEN query_type = 'term'

AND STARTS_WITH(LOWER(refinement_queries), refinements.search_query)

  

THEN 'specification - term completion'

  

WHEN query_type = 'term'

AND STARTS_WITH(

LOWER(refinements.search_query),

CONCAT(LOWER(refinement_queries), ' ')

)

AND REGEXP_CONTAINS(

SUBSTR(

LOWER(refinements.search_query),

LENGTH(refinement_queries) + 2

),

r'^[\p{L}\s\-]+$' -- suffix can be multiple tokens (letters/spaces/hyphens only)

)

THEN 'generalization - functional suffix removed'

  

WHEN query_type = 'term'

AND REGEXP_CONTAINS(

refinement_queries,

r'^[a-z0-9\-\_\/\.]{4,}$'

)

-- AND REGEXP_CONTAINS(refinement_queries, r'[a-z]')

AND REGEXP_CONTAINS(refinement_queries, r'(?:\D*\d){3,}')

THEN 'differentation - term to item'

  

WHEN query_type = 'term'

AND ARRAY_LENGTH(SPLIT(LOWER(refinements.search_query), ' ')) > 1

AND ARRAY_LENGTH(SPLIT(LOWER(refinement_queries), ' ')) > 1

AND EXISTS (

SELECT 1

FROM UNNEST(SPLIT(LOWER(refinements.search_query), ' ')) AS w

WHERE w IN UNNEST(SPLIT(LOWER(refinement_queries), ' '))

)

AND LOWER(refinements.search_query) != LOWER(refinement_queries)

THEN 'context_substitution'

  

-- normalize to collapse multiple spaces

WHEN query_type = 'term'

AND ENDS_WITH(

REGEXP_REPLACE(LOWER(refinement_queries), r'\s+', ' '),

CONCAT(' ', REGEXP_REPLACE(LOWER(refinements.search_query), r'\s+', ' '))

)

AND LENGTH(refinement_queries) > LENGTH(refinements.search_query)

AND REGEXP_CONTAINS(

-- take everything before the last " space + original "

SUBSTR(

REGEXP_REPLACE(LOWER(refinement_queries), r'\s+', ' '),

1,

LENGTH(REGEXP_REPLACE(LOWER(refinement_queries), r'\s+', ' ')) -

LENGTH(REGEXP_REPLACE(LOWER(refinements.search_query), r'\s+', ' ')) - 1

),

r'^[\p{L}\s\-]+$' -- prefix is letters/spaces/hyphens only (no digits)

)

THEN 'specification - functional'

  

WHEN query_type = 'term'

-- single token, letters only (unicode)

AND REGEXP_CONTAINS(LOWER(refinements.search_query), r'^\p{L}+$')

AND REGEXP_CONTAINS(LOWER(refinement_queries), r'^\p{L}+$')

AND EXISTS (

SELECT 1

FROM UNNEST([3,4,5,6,7,8,9,10,11,12]) AS n

WHERE

-- same suffix (the compound head) of length n

SUBSTR(LOWER(refinements.search_query), LENGTH(refinements.search_query) - n + 1) =

SUBSTR(LOWER(refinement_queries), LENGTH(refinement_queries) - n + 1)

-- ensure both have prefixes before that head

AND LENGTH(refinements.search_query) > n

AND LENGTH(refinement_queries) > n

-- prefixes are different (so it’s a substitution, not identity)

AND SUBSTR(LOWER(refinements.search_query), 1, LENGTH(refinements.search_query) - n) <>

SUBSTR(LOWER(refinement_queries), 1, LENGTH(refinement_queries) - n)

-- guard: if head length is only 3, require prefix length >= 3 on both sides

AND (

n >= 4 OR (

n = 3

AND LENGTH(refinements.search_query) - n >= 3

AND LENGTH(refinement_queries) - n >= 3

)

)

)

  

THEN 'synonym - compound head substitution'

  

WHEN query_type = 'term'

AND REGEXP_CONTAINS(LOWER(refinements.search_query), r'^[\p{L}\-]+$')

AND REGEXP_CONTAINS(LOWER(refinement_queries), r'^[\p{L}\-]+$')

AND EXISTS (

SELECT 1

FROM UNNEST([3,4,5,6,7,8,9,10,11,12]) AS n

WHERE

-- compare after removing hyphens

SUBSTR(REGEXP_REPLACE(LOWER(refinements.search_query), r'-', ''), 1, n) =

SUBSTR(REGEXP_REPLACE(LOWER(refinement_queries), r'-', ''), 1, n)

-- both have non-empty tails after the shared prefix

AND LENGTH(REGEXP_REPLACE(refinements.search_query, r'-', '')) > n

AND LENGTH(REGEXP_REPLACE(refinement_queries, r'-', '')) > n

-- tails differ → an actual substitution, not identity

AND SUBSTR(REGEXP_REPLACE(LOWER(refinements.search_query), r'-', ''), n+1) <>

SUBSTR(REGEXP_REPLACE(LOWER(refinement_queries), r'-', ''), n+1)

-- guard: if shared prefix is short (n=3), require both tails ≥3 chars

AND (

n >= 4 OR (

LENGTH(REGEXP_REPLACE(refinements.search_query, r'-', '')) - n >= 3

AND LENGTH(REGEXP_REPLACE(refinement_queries, r'-', '')) - n >= 3

)

)

)

THEN 'synonym - compound tail substitution'

  

WHEN

-- Same characters ignoring spaces and hyphens

REGEXP_REPLACE(LOWER(refinement_queries), r'[\s\-]+', '') =

REGEXP_REPLACE(LOWER(refinements.search_query), r'[\s\-]+', '')

-- Hyphens increased …

AND (LENGTH(refinement_queries) - LENGTH(REPLACE(refinement_queries, '-', '')))

>

(LENGTH(refinements.search_query) - LENGTH(REPLACE(refinements.search_query, '-', '')))

-- …while spaces decreased

AND (LENGTH(refinement_queries) - LENGTH(REGEXP_REPLACE(refinement_queries, r'\s+', '')))

<

(LENGTH(refinements.search_query) - LENGTH(REGEXP_REPLACE(refinements.search_query, r'\s+', '')))

THEN 'spelling - space-hyphen replacement'

  

WHEN

-- Same characters ignoring spaces and hyphens

REGEXP_REPLACE(LOWER(refinement_queries), r'[\s\-]+', '') =

REGEXP_REPLACE(LOWER(refinements.search_query), r'[\s\-]+', '')

-- Hyphens decreased …

AND (LENGTH(refinement_queries) - LENGTH(REPLACE(refinement_queries, '-', '')))

<

(LENGTH(refinements.search_query) - LENGTH(REPLACE(refinements.search_query, '-', '')))

-- …while spaces increased

AND (LENGTH(refinement_queries) - LENGTH(REGEXP_REPLACE(refinement_queries, r'\s+', '')))

>

(LENGTH(refinements.search_query) - LENGTH(REGEXP_REPLACE(refinements.search_query, r'\s+', '')))

THEN 'spelling - hyphen-space replacement'

  

WHEN query_type = 'term'

AND REGEXP_CONTAINS(LOWER(refinements.search_query), r'^\p{L}+$')

AND REGEXP_CONTAINS(LOWER(refinement_queries), r'^\p{L}+$')

AND LOWER(refinements.search_query) != LOWER(refinement_queries)

-- normalized edit distance: "very different"

AND SAFE_DIVIDE(

EDIT_DISTANCE(LOWER(refinements.search_query), LOWER(refinement_queries)),

GREATEST(LENGTH(refinements.search_query), LENGTH(refinement_queries))

) >= 0.5

THEN 'synonym - candidate single token'

  

WHEN query_type = 'term'

AND NOT REGEXP_CONTAINS(LOWER(refinements.search_query), r'\d')

AND NOT REGEXP_CONTAINS(LOWER(refinement_queries), r'\d')

AND ARRAY_LENGTH(SPLIT(LOWER(refinements.search_query), ' ')) <= 2

AND ARRAY_LENGTH(SPLIT(LOWER(refinement_queries), ' ')) <= 2

-- no shared token between original and refined

AND NOT EXISTS (

SELECT 1

FROM UNNEST(SPLIT(LOWER(refinements.search_query), ' ')) AS w

WHERE w IN UNNEST(SPLIT(LOWER(refinement_queries), ' '))

)

THEN 'synonym - candidate phrase'

  

WHEN query_type = 'term'

AND ENDS_WITH(

REGEXP_REPLACE(LOWER(refinements.search_query), r'\s+', ' '),

CONCAT(' ', REGEXP_REPLACE(LOWER(refinement_queries), r'\s+', ' '))

)

AND LENGTH(refinements.search_query) > LENGTH(refinement_queries)

AND REGEXP_CONTAINS(

SUBSTR(

REGEXP_REPLACE(LOWER(refinements.search_query), r'\s+', ' '),

1,

LENGTH(REGEXP_REPLACE(LOWER(refinements.search_query), r'\s+', ' ')) -

LENGTH(REGEXP_REPLACE(LOWER(refinement_queries), r'\s+', ' ')) - 1

),

r'^[\p{L}\s\-]+$' -- dropped prefix is letters/spaces/hyphens only (no digits)

)

THEN 'generalization - functional prefix with space removed'

  
  

END as refinement_type,

sum(refinements.refinements) as refinements,

sum(refinements.refinement_success)/sum(refinements.refinements) as refinement_SSR,

sum(a.success)/sum(a.searches) as original_query_SSR,

sum(b.success)/sum(b.searches) as refinement_query_SSR,

sum(a.searches) as searches_original_query,

sum(a.success) as success_original_query,

sum(refinement_success) as refinement_success,

sum(b.searches) as searches_refinement_query,

sum(b.success) as success_refinement_query

from refinements

left join all_searches a
on refinements.search_query = a.search_query
left join all_searches b
on refinements.refinement_queries = b.search_query
group by all
-- having refinement_queries = 'pompe adblue'
-- having refinement_type = 'specification - term completion'
having refinement_type like 'synonym %'
order by refinements desc
```