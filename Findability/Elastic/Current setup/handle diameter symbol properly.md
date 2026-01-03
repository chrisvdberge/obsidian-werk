---
created: 2025-10-30T09:31
updated: 2025-10-31T17:35
tags:
  - elastic/challenges
  - elastic
---

### use diameter symbol normalization to prevent 'o'

|                     |                                                                                                                    |
| ------------------- | ------------------------------------------------------------------------------------------------------------------ |
| description::       | we currently normalize the diameter symbol to 'o'. probably a big reason why we have spelling suggestions like `o` |
| example::           |                                                                                                                    |
| impact::            | we never match the diameter symbol, since token is too small (1 char) and gives `o` as spelling suggestion         |
| recall or ranking:: | [[recall]]                                                                                                         |
| key metric::        | [[SSR]]                                                                                                            |
| proposed solution:: | add a char filter to replace the diameter symbol by `diameter`                                                     |
| actions::           |                                                                                                                    |
| Jira ticket::       |                                                                                                                    |

```json
 "char_filter": {
        "dia_only_when_number_after": {
          "type": "pattern_replace",
          "flags": "CASE_INSENSITIVE",
          "pattern": "(?<!\\p{L})[Øø]\\s*(\\d+(?:[.,]\\d+)?)\\b",
          "replacement": " diameter $1 "
        }
      },
```