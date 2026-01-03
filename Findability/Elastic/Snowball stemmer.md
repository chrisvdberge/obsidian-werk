---
created: 2025-11-04T09:27
updated: 2025-11-04T09:29
tags:
  - elastic
  - findability
  - elastic/resources
---

## 🧩 1. What “stemming” means

**Stemming** is a linguistic normalization process that reduces words to a common **base form** (the _stem_).  
The goal is to make small grammatical variants match the same root.

Example (English):

`run, running, runs → run engineer, engineering, engineered → engineer`

So if a user searches “running”, they’ll also find documents with “run”.

This improves **recall** — users don’t have to type the exact grammatical form used in your product text.

---

## 🧠 2. What _Snowball_ is

**Snowball** is a specific stemming algorithm family — developed by **Martin Porter**, who also wrote the original _Porter stemmer_ in 1980.

- It’s more modern and configurable than the original Porter stemmer.
    
- It supports many languages.
    
- It’s the default stemmer type used in Elasticsearch when you define `"type": "snowball"`.
    

In Lucene/Elasticsearch, you’ll often see analyzers like:

`"filter": [   "lowercase",   { "type": "snowball", "language": "English" } ]`

This adds a **Snowball stemmer** for English, which knows about common suffixes (`-ing`, `-ed`, `-ly`, etc.) and trims them intelligently.

---

## 🌍 3. Supported languages

Snowball has stemming rules for many major languages, for example:

- English
- Dutch
- German
- French
- Spanish
- Italian
- Russian
- Norwegian
- Swedish
- Danish
- Finnish
- … and others
    

Each has its own rule set (e.g., Dutch removes _-en_, _-tje_ endings).

Example (Dutch):

`werkt, werkten, werkte → werk machines, machientje → machin`

So your Dutch search for `"machines"` would also match `"machientje"` (“little machine”).