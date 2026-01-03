---
created: 2025-10-30T09:31
updated: 2025-10-30T16:21
tags:
  - elastic
  - elastic/challenges
---
- pre-fixes
		- test met uitzetten van de splitter
		- voeg analyzer toe aan index en maak variant query die de andere analyzer gebruikt om te kunnen AB testen
- ### products that are the same but different quantity, but different SKU's

|                     |                                                                                                                                                                                                                                                                 |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| description::       | itemnumbers can have prefixes added to 'industry standard'-itemnumbers for our own convenience. the user will be searching without the prefix. <br>currently we have the `split_character_numbers`filter for this, but this results in a lot of false positives |
| example::           | Searching for 100100 gives a lot of items with 100100 somewhere in the itemnumber                                                                                                                                                                               |
| impact::            | results in a lot of false positives                                                                                                                                                                                                                             |
| recall or ranking:: | [[recall]]                                                                                                                                                                                                                                                      |
| key metric::        | [[precision]]                                                                                                                                                                                                                                                   |
| proposed solution:: | remove the use of this filter in our analyzers                                                                                                                                                                                                                  |
| actions::           | add an analyzer without this filter<br>add this analyzer to a variant query                                                                                                                                                                                     |
| Jira ticket::       | https://kramphub.atlassian.net/browse/FINDTY-1291                                                                                                                                                                                                               |
