---
created: 2025-10-30T09:31
updated: 2025-10-31T17:29
tags:
  - elastic
  - elastic/challenges
---
###  lumen specifications

|                     |                                                                                                                                                                                                 |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| description::       | `lm` is not recognized as a unit, and 3.040lm gets tokenized into `304` and `3040l` by [[word_edge_ngram]] analyzer. [[standard analyzer]] produces `3040lm`<br>we don't have `3040` as a token |
| example::           |                                                                                                                                                                                                 |
| impact::            | if users are using lumen values we might not match the correct documents                                                                                                                        |
| recall or ranking:: | [[recall]]                                                                                                                                                                                      |
| key metric::        | [[SSR]]                                                                                                                                                                                         |
| proposed solution:: |                                                                                                                                                                                                 |
| actions::           | might be solved if we account for units and store values as integers                                                                                                                            |
| Jira ticket::       |                                                                                                                                                                                                 |
