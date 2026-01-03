---
created: 2025-10-30T09:31
updated: 2025-10-31T11:33
tags:
  - elastic
  - elastic/challenges
---
### item descriptions that have negative words are matching in wrong scenarios

|                     |                                                                                                                           |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| description::       | we have many item descriptions that have text like "without glue" . These items will now match when you search for `glue` |
| example::           | search query: glue                                                                                                        |
| impact::            | pollution of search results                                                                                               |
| recall or ranking:: | [[recall]] and [[ranking]]                                                                                                |
| key metric::        | [[SSR]] and [[NDCG]]                                                                                                      |
| proposed solution:: | ?                                                                                                                         |
| actions::           | investigate a solution other than LLM/agents                                                                              |
| Jira ticket::       |                                                                                                                           |
![[Scherm­afbeelding 2025-10-09 om 08.49.05.png]]