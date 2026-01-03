---
created: 2025-11-16T08:14
updated: 2025-11-16T08:18
tags:
  - click_data
---
- [ ] find a way to do near real time / intraday tracking of metrics with alerting. #p1 


## possible solutions
- we could use sgtm to send select data to bigquery where we have a view to calculate things. but should be streaming?
- we could simply process intraday click-data with our existing models in DBT
	- copy the models to reflect processing only intraday data
	- setup new pipeline with these models
