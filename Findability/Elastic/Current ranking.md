---
created: 2025-11-03T20:38
updated: 2025-11-04T09:11
tags:
  - elastic
  - findability
---
## fields + analyzers
- brand_cleaned.
		- word_edge_ngram <-> word_edge_ngram
		- standard <-> standard
		- no_stemming <-> no_stemming
		- no_decompound <-> no_decompound
	
- item_description_no_brand.
	- word_edge_ngram <-> word_edge_ngram_no_synoms
	- standard <-> standard_no_synonyms
	- no_stemming <-> no_stemming_no_synonyms
	- no_decompounding <-> no_decompounding_no_synonyms

- external_item_id
	- word_edge_ngram <-> word_edge_ngram (no ngram filter!)

- item_id
	- word_edge_ngram <-> word_edge_ngram (no ngram filter!)
	
- functional_name
	- word_edge_ngram <-> word_edge_ngram_no_synonyms
	- standard <-> standard_no_synonyms
	- no_stemming <-> no_stemming_no_synonyms
	- no_decompounding <-> no_decompounding_no_synonyms
	
- ud_search.ids.eans.
	- no_splitting <-> standard

- ud_search.ids.supplier_item_number
	- standard <-> standard
	- no_splitting <-> standard
	
- ud_search.ids.competitor_item_number
	- standard <-> standard
	- no_splitting <-> standard
	
- ud_search.ids.replaces
	- no_splitting <-> standard
	
- ud_search.ids.external_item_id
	- standard <-> standard
	- no_splitting <-> standard
	- edge_ngram <-> standard

## Scores
### ud.search.ids.external_item_id
- standard - 100.0
- no_splitting - 100.0
- edge_ngram - 100.0
- word_edge_ngram - 100.0
### ud.search.ids.replaces
- no_splitting - 80.0

### ud.search.ids.oe_number
- standard - 75.0
- no_splitting - 75.0

### ud.search.ids.supplier_item_number
- standard - 75.0
- no_splitting - 75.0

### ud.search.ids.competitor_item_number
- standard^75.0",
- no_splitting^75.0",

### ud.search.ids.eans
- no_splitting^80.0

### ud.search.ids.merchandising_associations_alternatives
- standard - 75.0
- no_splitting - 75.0
### ud.search.text.brand_cleaned
- standard - 70.0
- no_stemming^70.0",
- no_decompound^70.0",
- word_edge_ngram^70.0",
### ud.search.text.sales_category_name
- standard - 50.0
### ud.search.text.interacted_search_terms_interaction_365d_global_success
- normalized_keyword^80.0",
### ud.search.text.item_description_no_brand
- standard_no_synonyms^60.0
- no_stemming_no_synonyms^60.0
- no_decompound_no_synonyms^60.0",
- word_edge_ngram_no_synonyms^60.0",

### ud.search.text.variant_description.
- standard - 60.0
- word_edge_ngram - 60.0