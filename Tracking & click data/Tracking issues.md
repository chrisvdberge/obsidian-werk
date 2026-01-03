---
created: 2025-10-31T15:57
updated: 2025-10-31T18:35
tags:
  - tracking
  - click_data
---
- login status in the app is NULL in many cases
```sql 
  select login_status
  from (select * from `kramp-edw-e-commerce-prd`.`presentation_common`.`pres__obt__click_data_master` where webshop_event_date >= date_add(current_date(), interval - 30 day)) dbt_subquery where login_status is null
```

- sql/javascript injections in many dimensions **solved**
```sql
		  with all_values as (
		  
		      select
		          view_type as value_field,
		          count(*) as n_records
		  
		      from (select * from `kramp-edw-e-commerce-prd`.`presentation_common`.`pres__obt__click_data_master` where webshop_event_date >= date_add(current_date(), interval - 30 day)) dbt_subquery
		      group by view_type
		  )
		  
		  select *
		  from all_values
		  where value_field not in (
		      'grid','list'
		  )
```
	- solved by filtering in [[DBT]]

- search_type -> `suggestion_term` instead of `suggestion-term`
	- is this app?

- country_cd is null, veel in de app, maar ook op web
		- op web, vooral in myaccount en op de login page?
	- language_country is null in app
		-
		-