---
created: 2025-10-30T19:14
updated: 2025-12-15T09:17
tags:
  - sql
  - gbq
---
- moving average
```sql
AVG(breadcrumb_pct) OVER (ORDER BY UNIX_DATE(date) RANGE BETWEEN 6 PRECEDING AND CURRENT ROW) AS
```
- select median value:
	```sql
	APPROX_QUANTILES(column_name, 2)[OFFSET(1)] AS median
	```
- BYTE type comparisons for hashed id's
	- ```sql
	  id = FROM_BASE64('LCxnsUcFzjCv0hWPKX9c7hXS1FxeHW2OvNZFgeONDgk=')
	  ```

- create #vertex model
	- ```sql
	  	  CREATE OR REPLACE MODEL `kramp-webanalytics-prd.findability.gemini_model`
	  REMOTE WITH CONNECTION `kramp-webanalytics-prd.eu.vertex_ai`
	  OPTIONS (
	    endpoint = 'https://europe-west4-aiplatform.googleapis.com/v1/projects/kramp-webanalytics-prd/locations/europe-west4/publishers/google/models/gemini-1.5-pro-001'
	  );
	  ```
