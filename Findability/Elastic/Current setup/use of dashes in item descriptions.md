---
created: 2025-10-30T09:31
updated: 2025-12-15T10:28
tags:
  - elastic
  - elastic/challenges
---
### different uses of dashes in item descriptions

|                     |                                                                                                                                                                                                              |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| description::       | We have many different uses of dashed in our item descriptions. Handling this correctly so we match the user query is a challenge. Simply interpreting it as a space or removing it is not the best solution |
| example::           |                                                                                                                                                                                                              |
| impact::            | missed recall and wrong recall                                                                                                                                                                               |
| recall or ranking:: | [[recall]] and [[ranking]]                                                                                                                                                                                   |
| key metric::        | [[SSR]]                                                                                                                                                                                                      |
| proposed solution:: |                                                                                                                                                                                                              |
| actions::           | investigate further                                                                                                                                                                                          |
| Jira ticket::       |                                                                                                                                                                                                              |

More info: 
	- `1-1/2"` -> should be space
		- meant to be `1,5"` so remove in product data
-
	- `o-ring` -> in text for pre-fix
		- way of writing, can stay like this
		- user might write it like this as well
		- replace dash ?
		- 
	- `D30-50-300 C-serie` -> model and separator for specs (cylinders)
		- probably needs to stay like this
		- industry standard so user might search like this (check!)
		- keep dash
		-
	- `AT-PA` -> technical specification
		- desired or not?
		- keep?
	- `A20-30` or `P25-35` -> ?
		- R701900 Arm II A20-30 P25-35 LI
	- `AZPF-11-004RCN20MB` typenumber
		- keep dash
	- `WB10120 Slang- en kabelbrug zwart`
		- "samentrekking met koppelteken"
			- vermijden in de product data