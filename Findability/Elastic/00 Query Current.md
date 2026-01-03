---
created: 2025-10-30T09:12
updated: 2025-10-31T17:31
tags:
  - elastic
---
```json
{
  "_source": {
    "includes": [
      "ud.display.item_id",
      "score.*",
      "ud.aggs.string.variant_id",
      "ud.aggs.string.brand",
      "ud.sort.string.item_id",
      "ud.score.normalized_interacted_item_boosting_interaction_90d_language"
    ]
  },
  "aggregations": {
    "all": {
      "aggregations": {
        "term-suggestion": {
          "filters": {
            "filters": {
              "magneet": {
                "bool": {
                  "filter": [
                    {
                      "terms": {
                        "ud.aggs.string.assortment_id": [
                          "base_FR"
                        ]
                      }
                    },
                    {
                      "terms": {
                        "ud.aggs.string.market": [
                          "FR"
                        ]
                      }
                    }
                  ],
                  "must": [
                    {
                      "multi_match": {
                        "fields": [
                          "ud.search.text.description.word_edge_ngram",
                          "ud.search.text.brand_cleaned.word_edge_ngram",
                          "ud.search.text.attribute_values.word_edge_ngram",
                          "ud.search.text.variant_description.word_edge_ngram",
                          "ud.search.text.external_item_id.word_edge_ngram",
                          "ud.search.text.description.standard",
                          "ud.search.text.item_description_only_spec.standard",
                          "ud.search.text.brand_cleaned.standard",
                          "ud.search.text.attribute_values.standard",
                          "ud.search.text.variant_description.standard",
                          "ud.search.text.external_item_id.standard",
                          "ud.search.text.oe_number.standard",
                          "ud.search.text.supplier_item_number.standard",
                          "ud.search.text.competitor_item_number.standard",
                          "ud.search.ids.eans.no_splitting",
                          "ud.search.text.attribute_search_names.standard",
                          "ud.search.ids.merchandising_associations_alternatives.standard",
                          "ud.search.ids.external_item_id.edge_ngram",
                          "ud.search.ids.replaces.no_splitting",
                          "ud.search.ids.supplier_item_number.edge_ngram",
                          "ud.search.ids.competitor_item_number.edge_ngram",
                          "ud.search.ids.attribute_search_names.edge_ngram",
                          "ud.search.text.sales_category_name.standard"
                        ],
                        "operator": "and",
                        "query": "magneet",
                        "type": "cross_fields"
                      }
                    }
                  ],
                  "must_not": [
                    {
                      "term": {
                        "ud.aggs.string.replaced_in_country": {
                          "value": "FR"
                        }
                      }
                    }
                  ]
                }
              }
            }
          }
        }
      },
      "global": {}
    }
  },
  "from": 0,
  "post_filter": {
    "bool": {}
  },
  "query": {
    "function_score": {
      "functions": [
        {
          "field_value_factor": {
            "field": "ud.score.normalized_interacted_item_boosting_interaction_90d_language",
            "missing": 0.8
          }
        },
        {
          "filter": {
            "terms": {
              "ud.aggs.string.brand": [
                "Gopart",
                "Kramp"
              ]
            }
          },
          "weight": 1.03
        }
      ],
      "query": {
        "bool": {
          "filter": [
            {
              "terms": {
                "ud.aggs.string.assortment_id": [
                  "base_FR"
                ]
              }
            },
            {
              "terms": {
                "ud.aggs.string.market": [
                  "FR"
                ]
              }
            }
          ],
          "must": [
            {
              "multi_match": {
                "fields": [
                  "ud.search.text.description.word_edge_ngram",
                  "ud.search.text.brand_cleaned.word_edge_ngram",
                  "ud.search.text.attribute_values.word_edge_ngram",
                  "ud.search.text.variant_description.word_edge_ngram",
                  "ud.search.text.external_item_id.word_edge_ngram",
                  "ud.search.text.description.standard",
                  "ud.search.text.item_description_only_spec.standard",
                  "ud.search.text.brand_cleaned.standard",
                  "ud.search.text.attribute_values.standard",
                  "ud.search.text.variant_description.standard",
                  "ud.search.text.external_item_id.standard",
                  "ud.search.text.oe_number.standard",
                  "ud.search.text.supplier_item_number.standard",
                  "ud.search.text.competitor_item_number.standard",
                  "ud.search.ids.eans.no_splitting",
                  "ud.search.text.attribute_search_names.standard",
                  "ud.search.ids.merchandising_associations_alternatives.standard",
                  "ud.search.ids.external_item_id.edge_ngram",
                  "ud.search.ids.replaces.no_splitting",
                  "ud.search.ids.supplier_item_number.edge_ngram",
                  "ud.search.ids.competitor_item_number.edge_ngram",
                  "ud.search.ids.attribute_search_names.edge_ngram",
                  "ud.search.text.sales_category_name.standard"
                ],
                "operator": "and",
                "query": "magneet",
                "type": "cross_fields"
              }
            }
          ],
          "must_not": [
            {
              "term": {
                "ud.aggs.string.replaced_in_country": {
                  "value": "FR"
                }
              }
            }
          ],
          "should": [
            {
              "bool": {
                "should": [
                  {
                    "multi_match": {
                      "fields": [
                        "ud.search.ids.external_item_id.standard^100.0",
                        "ud.search.ids.external_item_id.no_splitting^100.0",
                        "ud.search.ids.external_item_id.edge_ngram^100.0",
                        "ud.search.text.external_item_id.word_edge_ngram^100.0",
                        "ud.search.ids.replaces.no_splitting^80.0",
                        "ud.search.ids.oe_number.standard^75.0",
                        "ud.search.ids.oe_number.no_splitting^75.0",
                        "ud.search.ids.supplier_item_number.standard^75.0",
                        "ud.search.ids.supplier_item_number.no_splitting^75.0",
                        "ud.search.ids.competitor_item_number.standard^75.0",
                        "ud.search.ids.competitor_item_number.no_splitting^75.0",
                        "ud.search.ids.eans.no_splitting^80.0",
                        "ud.search.ids.merchandising_associations_alternatives.standard^75.0",
                        "ud.search.ids.merchandising_associations_alternatives.no_splitting^75.0",
                        "ud.search.text.brand_cleaned.standard^70.0",
                        "ud.search.text.brand_cleaned.no_stemming^70.0",
                        "ud.search.text.brand_cleaned.no_decompound^70.0",
                        "ud.search.text.brand_cleaned.word_edge_ngram^70.0",
                        "ud.search.text.sales_category_name.standard^50.0",
                        "ud.search.text.interacted_search_terms_interaction_365d_global_success.normalized_keyword^80.0",
                        "ud.search.text.item_description_no_brand.standard_no_synonyms^60.0",
                        "ud.search.text.item_description_no_brand.no_stemming_no_synonyms^60.0",
                        "ud.search.text.item_description_no_brand.no_decompound_no_synonyms^60.0",
                        "ud.search.text.item_description_no_brand.word_edge_ngram_no_synonyms^60.0",
                        "ud.search.text.variant_description.standard^60.0",
                        "ud.search.text.variant_description.word_edge_ngram^60.0"
                      ],
                      "minimum_should_match": "0",
                      "operator": "or",
                      "query": "magneet",
                      "tie_breaker": 0.2,
                      "type": "best_fields"
                    }
                  }
                ]
              }
            }
          ]
        }
      }
    }
  },
  "size": 200,
  "sort": [
    {
      "_score": {
        "order": "desc"
      }
    },
    {
      "ud.sort.string.brand": {
        "order": "asc",
        "unmapped_type": "keyword"
      }
    },
    {
      "ud.sort.string.item_id": {
        "order": "asc",
        "unmapped_type": "keyword"
      }
    }
  ],
  "suggest": {
    "phrase-suggestion": {
      "text": "magneet",
      "phrase": {
        "field": "ud.suggestions.phrase",
        "collate": {
          "query": {
            "source": {
              "bool": {
                "filter": [
                  {
                    "terms": {
                      "ud.aggs.string.assortment_id": [
                        "base_FR"
                      ]
                    }
                  },
                  {
                    "terms": {
                      "ud.aggs.string.market": [
                        "FR"
                      ]
                    }
                  }
                ],
                "must": [
                  {
                    "multi_match": {
                      "fields": [
                        "ud.search.text.description.word_edge_ngram",
                        "ud.search.text.brand_cleaned.word_edge_ngram",
                        "ud.search.text.attribute_values.word_edge_ngram",
                        "ud.search.text.variant_description.word_edge_ngram",
                        "ud.search.text.external_item_id.word_edge_ngram",
                        "ud.search.text.description.standard",
                        "ud.search.text.item_description_only_spec.standard",
                        "ud.search.text.brand_cleaned.standard",
                        "ud.search.text.attribute_values.standard",
                        "ud.search.text.variant_description.standard",
                        "ud.search.text.external_item_id.standard",
                        "ud.search.text.oe_number.standard",
                        "ud.search.text.supplier_item_number.standard",
                        "ud.search.text.competitor_item_number.standard",
                        "ud.search.ids.eans.no_splitting",
                        "ud.search.text.attribute_search_names.standard",
                        "ud.search.ids.merchandising_associations_alternatives.standard",
                        "ud.search.ids.external_item_id.edge_ngram",
                        "ud.search.ids.replaces.no_splitting",
                        "ud.search.ids.supplier_item_number.edge_ngram",
                        "ud.search.ids.competitor_item_number.edge_ngram",
                        "ud.search.ids.attribute_search_names.edge_ngram",
                        "ud.search.text.sales_category_name.standard"
                      ],
                      "operator": "and",
                      "query": "{{suggestion}}",
                      "type": "cross_fields"
                    }
                  }
                ],
                "must_not": [
                  {
                    "term": {
                      "ud.aggs.string.replaced_in_country": {
                        "value": "FR"
                      }
                    }
                  }
                ]
              }
            }
          }
        },
        "direct_generator": [
          {
            "field": "ud.suggestions.phrase",
            "suggest_mode": "always"
          },
          {
            "field": "ud.suggestions.phrase-reverse",
            "post_filter": "suggestions_phrase_reverse_analyzer",
            "pre_filter": "suggestions_phrase_reverse_analyzer",
            "suggest_mode": "always"
          }
        ]
      }
    },
    "term-suggestion": {
      "text": "magneet",
      "term": {
        "field": "ud.suggestions.terms",
        "suggest_mode": "popular"
      }
    }
  },
  "timeout": "5000ms",
  "track_total_hits": true
}```