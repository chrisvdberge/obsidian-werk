---
created: 2025-10-30T09:21
updated: 2025-10-30T09:22
tags:
  - elastic
---
### sales_category lowest level still has non-relevant words
- description:: lowest category sometimes has non-relevant words. mostly because there could be levels missing in the [[make_model]] structure and there is an `apcComposedProduct` linked to a make directly 
- example::  100100
```json
"ud.search.text.sales_category_name": [
	"Meststrooiers",
	"Kruisstukken standaard"
],	  
```
- impact::
- key metric:: [[precision]]
- proposed solution:: [ ]wait for [[PH700]] and new structure and re-evaluate
- Jira ticket:: 