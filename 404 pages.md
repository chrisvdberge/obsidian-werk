---
created: 2026-04-13T06:53
updated: 2026-04-13T06:54
---
Marketing 404s: 
```sql
select 
m.webshop_event_date,
--  m.webshop_visit_id, 
-- m.page_path
 count(m.webshop_visit_id) as visits
-- *
from `kg-data-e-commerce-prd`.`presentation_common`.`pres__obt__click_data_master` as m
left join
    pollution as p
    on m.webshop_visit_id = p.webshop_visit_id
where p.webshop_visit_id is null and m.webshop_event_date >= "2026-01-01"
and m.content_name = "404"
and page_path like '%utm_source%'
group by all
order by 1 asc
```
![[Scherm­afbeelding 2026-04-13 om 06.54.02.png]]