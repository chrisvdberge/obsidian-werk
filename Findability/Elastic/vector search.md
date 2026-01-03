---
created: 2025-12-01T08:58
updated: 2025-12-01T20:22
tags:
  - elastic
  - findability
  - "#vector_search"
---
# setup
- 'regular' search should be BM25 for text fields and boolean for id.s-> this is currently the way it is setup, no change needed!
- 
# conclusions
- synonyms still important because of different results
- vector search favours the short/wrong/incomplete item descriptions
## examples
![[Scherm­afbeelding 2025-12-01 om 08.58.25.png]]


# ChatGPT advice on setup
# Single-term–first architecture (practical recipe)


## 1) Router (decide when vectors are allowed)

At query time (after running the same analyzer you use for indexing):

- If `term_count == 1`:
    
    - **If it looks like an ID/partno/brand** → lexical-only (no vectors).
        
    - **Else** → lexical-primary. Call vectors **only if** the lexical head looks weak:
        
        - `hits == 0`, or
            
        - top `_score < S_LO` (empirically choose a percentile threshold), or
            
        - the term is **OOV/rare** (analyzed token not in term stats / very low DF).
            
- If `term_count ≥ 2` → your normal hybrid (`knn` + BM25 + phrase rescore).
    

This policy removes the majority of “1 word → vector over-favoring tiny docs” cases.

## 2) Tune BM25 to reduce short-doc bias (per field)

Use lighter length normalization on name-like fields:

- `item_description_no_brand`, `variant_description` → **BM25(b≈0.25)**
    
- Long `description` → **BM25(b≈0.75)**
    

Result: a single token in a 3-word “name” field no longer crushes a detailed, relevant product.

## 3) Query shape for single-term (lexical-primary)

Prefer **best_fields + dis_max** (not `cross_fields`) so the strongest field “wins” without over-counting duplicates.

`{   "size": 200,   "query": {     "function_score": {       "query": {         "bool": {           "filter": [             /* your assortment/market/replaced filters */           ],           "must": [             {               "dis_max": {                 "tie_breaker": 0.2,                 "queries": [                   { "match": { "ud.search.text.item_description_no_brand.standard": { "query": "<q>" } } },                   { "match": { "ud.search.text.variant_description.standard":       { "query": "<q>" } } },                   { "match": { "ud.search.text.functional_name.standard":          { "query": "<q>" } } },                   { "match": { "ud.search.text.description.standard":              { "query": "<q>" } } }                 ]               }             }           ],           "should": [             /* exact ID/brand boosts, if applicable for this term */           ]         }       },       "functions": [         /* 3a — add gentle verbosity prior */         {           "field_value_factor": {             "field": "ud.meta.length.name_tokens",  /* integer token count of NAME */             "modifier": "log1p",             "missing": 1.0           },           "weight": 0.05         },         /* 3b — business priors (interaction, availability, private label, etc.) */         {           "field_value_factor": {             "field": "ud.score.normalized_interacted_item_boosting_interaction_90d_language",             "missing": 0.8           }         }       ],       "boost_mode": "multiply",       "score_mode": "sum"     }   },   /* 3c — single-term rescore: bias NAME/VARIANT presence (not phrase) */   "rescore": [{     "window_size": 200,     "query": {       "query_weight": 0.6,       "rescore_query_weight": 1.4,       "rescore_query": {         "dis_max": {           "tie_breaker": 0.2,           "queries": [             { "match": { "ud.search.text.item_description_no_brand.standard": { "query": "<q>" } } },             { "match": { "ud.search.text.variant_description.standard":       { "query": "<q>" } } }           ]         }       }     }   }] }`

**Why this helps**

- `dis_max` + low-`b` BM25 curbs the “short stub wins” effect.
    
- A small **verbosity prior** (log1p of NAME token count) breaks ties against ultra-short names without burying concise good results.
    
- The **single-term rescore** amplifies high-quality matches in human-visible fields (NAME/VARIANT), which is what shoppers expect.
    

## 4) Let vectors in only when the text signal is weak

If router says “lexical weak,” add a `knn` block **with the same filters** and a modest `k`:

`"knn": {   "field": "ud.search.embedding_short",   "query_vector": "<q-embedding>",   "k": 64,   "num_candidates": 512,   "filter": { "bool": { "filter": [ /* same filters */ ] } } }`

Then rely on the rescore above (or app-side RRF) to make sure vector-only oddballs don’t jump the queue. Two extra guardrails you can add if needed:

- **Keep-if-lexical**: after the union, drop candidates with zero lexical score (app-side check).
    
- **Cap vector share**: e.g., in top-N, allow max 30–40% to be vector-only for single terms.
    

## 5) Embed cleanly to avoid “token dominance”

For single-term stability:

- Use **`embedding_short`** (NAME + VARIANT + FN, capped lengths) for single-term queries.
    
- **Tag** sections (`[NAME] …`) and limit tokens per section (e.g., 64/64/64) to prevent any one token from dominating the vector.
    
- Strip brand duplication and boilerplate before embedding.
    

## 6) Head-term intent priors (big payoff for agri B2B)

Many single-term queries are **category intents** (“filter”, “lager”, “riem”, “schaar”, “o-ring”). For those:

- Maintain a **head-term → functional_name(s)** map.
    
- If the query equals (or stems to) a known functional_name, add a **constant_score** boost for items with that functional_name and favor **popular** SKUs within it (clicks/sales). This converts “browsey” one-word queries into clean category-like rankings instead of noisy keyword matches.
    

`{ "constant_score": {     "filter": { "terms": { "ud.aggs.string.functional_name": ["O-ring"] } },     "boost": 1.1 }}`

## 7) Monitoring to keep it honest

Track these per **single-term** bucket:

- % zero-result, CTR@1/3/10, add-to-cart rate.
    
- Share of results with **non-zero lexical score** (should stay high).
    
- Median NAME length of top-10 vs. overall (should not collapse to 1–2 tokens).
    
- Head-term list drift (new frequent single tokens → curate functional_name priors).