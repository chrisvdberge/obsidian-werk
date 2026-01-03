---
created: 2025-11-16T07:56
updated: 2025-11-16T08:00
tags:
  - elastic/challenges
  - elastic
---

- light_french vs french #stemmer:
	- french: relais -> rel
	- light_french: relais -> relai
	- 
	- example:
		- 4RD933332371 not matching with `relais 12v`
			- token is `relai`
			- users are using `relais`
			- ![[Scherm_afbeelding_2025-02-20_om_11.49.59_1740048704589_0.png]]