---
created: 2025-11-25T20:08
updated: 2025-11-25T20:11
tags:
  - sql
  - dbt
---
`stg__navigation__category_childredn__latest.sql`
```sql
select * from

{{
ref(
"dbt_data_team_data_ingestion",
"ksd__navigation__category_children__latest",
)
}}
```


`prep__dim__navigation_hierarchy.sql`
```sql
with recursive

all_p_c as (

select p.category_id, child.category_id as child_category_id

from

{{ ref("stg__navigation__category_children__latest") }} p,

unnest(children_details) as cd,

unnest(cd.value.children) as child

where true

group by all

),

  

parents as (select category_id from all_p_c group by all),

  

top_level as (

select category_id, child_category_id as child

from all_p_c

where category_id not in (select child_category_id from all_p_c)

group by all

),

  

category_hierarchy as (

-- Base case: from top-level roots

select

r.category_id as category_id,

a.child_category_id as path,

1 as level,

array[r.category_id, a.child_category_id] as full_path

from top_level r

join all_p_c a on r.category_id = a.category_id

  

union all

-- Recursive case: from children to leaves

select

t.category_id,

a.child_category_id as path,

t.level + 1 as level,

array_concat(t.full_path, [a.child_category_id]) as full_path

from category_hierarchy t

join all_p_c a on t.path = a.category_id

)

select

-- p.category_id,

full_path[safe_offset(0)] as level1_id,

full_path[safe_offset(1)] as level2_id,

full_path[safe_offset(2)] as level3_id,

full_path[safe_offset(3)] as level4_id,

full_path[safe_offset(4)] as level5_id,

full_path[safe_offset(5)] as level6_id,

full_path[safe_offset(6)] as level7_id,

full_path[safe_offset(7)] as level8_id,

from category_hierarchy ch

left join parents p on ch.path = p.category_id

where true and p.category_id is null

group by all
```