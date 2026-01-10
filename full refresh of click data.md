---
created: 2025-12-21T08:18
updated: 2026-01-08T12:12
---

### Scope
- `enr__cbc__webshop_event__ga4__web__latest
	- `webshop_event_cd`
	- `device_profile_id
	- `device_profile_cd
	- `webshop_visit_id
	- `webshop_visit_cd
- `enr__cbc__device_profile__ga4__web__latest`
	- `device_profile_id
	- `device_profile_cd
- `enr__cbc__device_profile__ga4__app__latest
	- `device_profile_id
	- `device_profile_cd



### dbt ls selection
```
dbt ls --resource-type model --select tag:click+ 
--exclude config.materialized:view 
--exclude config.materialized:ephemeral
--exclude config.materialized:microbatch
--exclude path:models/staging 
--exclude path:models/enriched/slim4 
--exclude path:models/enriched/step 
--exclude path:models/presentation/presentation_common/metrics
```

]