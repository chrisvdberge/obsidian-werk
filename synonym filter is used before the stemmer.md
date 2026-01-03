---
created: 2025-12-15T11:47
updated: 2025-12-15T11:56
---

this means some synonyms don't get 'hit'/generated; 

## example
### `onderbroeken`
- we have a synonym for `onderbroek => boxer shorts`
- but `onderbroeken` gets stemmed to `onderbroek` only *after* we generated the synonyms. 
- this causes a spelling suggestion to be triggered for `onderbroeken` => `onderbroek`

## solution
- meervoud aan [[synonyms]] toevoegen, huidige setup van analyzer is correct. 
- 