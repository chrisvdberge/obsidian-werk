---
created: 2025-10-30T09:31
updated: 2025-10-30T09:45
tags:
  - elastic
  - elastic/challenges
---
### products that are the same but different quantity, but different SKU's

|                     |                                                                                                                                                                                                                                                                                    |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| description::       | We sometimes sell the same product in different package quantities. We change the `item_number`and add this information as a suffix. This can become a problem if we implement a `minimum_should_match` for [[ngrams]] , since we basically add characters that a user never uses. |
| example::           | OR142P010 and OR142P050                                                                                                                                                                                                                                                            |
| impact::            | possible matching challenge with ngrams if we move to a method to have a minimum set of characters match for partial matching.                                                                                                                                                     |
| recall or ranking:: | [[recall]]                                                                                                                                                                                                                                                                         |
| key metric::        | [[SSR]]                                                                                                                                                                                                                                                                            |
| proposed solution:: | adjust the ngram analyzer and add a filter to strip the suffix `P010`                                                                                                                                                                                                              |
| actions::           | double check if we can safely strip `P` followed by 3 digits at the end of an `item_number                                                                                                                                                                                         |
| Jira ticket::       |                                                                                                                                                                                                                                                                                    |
