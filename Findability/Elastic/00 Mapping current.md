---
created: 2025-10-30T09:08
updated: 2025-10-30T09:10
tags:
  - elastic
---
```json
{
  "kramp-item-nl-2025-09-04": {
    "mappings": {
      "dynamic_templates": [
        {
          "interacted_search_terms": {
            "path_match": "ud.search.text.interacted_search_terms_*",
            "mapping": {
              "fields": {
                "normalized_keyword": {
                  "analyzer": "search_text--normalized_keyword_index_analyzer",
                  "type": "text"
                }
              },
              "index": false,
              "type": "text"
            }
          }
        },
        {
          "aggs_numeric": {
            "path_match": "ud.aggs.numeric.*",
            "mapping": {
              "coerce": true,
              "ignore_malformed": true,
              "type": "float"
            }
          }
        },
        {
          "aggs_string": {
            "path_match": "ud.aggs.string.*",
            "mapping": {
              "ignore_above": 128,
              "type": "keyword"
            }
          }
        },
        {
          "aggs_bool": {
            "path_match": "ud.aggs.bool.*",
            "mapping": {
              "type": "boolean"
            }
          }
        },
        {
          "aggs_date": {
            "path_match": "ud.aggs.date.*",
            "mapping": {
              "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis",
              "type": "date"
            }
          }
        },
        {
          "aggs_flattened": {
            "path_match": "ud.aggs.flattened.*",
            "mapping": {
              "type": "flattened"
            }
          }
        },
        {
          "scores": {
            "path_match": "ud.score.*",
            "mapping": {
              "type": "float"
            }
          }
        },
        {
          "sort_string": {
            "path_match": "ud.sort.string.*",
            "mapping": {
              "ignore_above": 128,
              "normalizer": "sort_string_normalizer",
              "type": "keyword"
            }
          }
        },
        {
          "sort_numeric": {
            "path_match": "ud.sort.numeric.*",
            "mapping": {
              "coerce": true,
              "ignore_malformed": true,
              "type": "float"
            }
          }
        },
        {
          "sort_nested": {
            "path_match": "ud.sort.nested.*",
            "mapping": {
              "properties": {
                "sortOrder": {
                  "coerce": true,
                  "ignore_malformed": true,
                  "type": "float"
                },
                "id": {
                  "ignore_above": 128,
                  "type": "keyword"
                }
              },
              "type": "nested"
            }
          }
        },
        {
          "display": {
            "path_match": "ud.display.*",
            "mapping": {
              "index": false,
              "type": "text"
            }
          }
        },
        {
          "nested_aggs_numeric": {
            "path_match": "ud.nested.*.aggs.numeric.*",
            "mapping": {
              "coerce": true,
              "ignore_malformed": true,
              "type": "float"
            }
          }
        },
        {
          "nested_aggs_string": {
            "path_match": "ud.nested.*.aggs.string.*",
            "mapping": {
              "type": "keyword"
            }
          }
        },
        {
          "nested_aggs_bool": {
            "path_match": "ud.nested.*.aggs.bool.*",
            "mapping": {
              "type": "boolean"
            }
          }
        },
        {
          "nested_sort_numeric": {
            "path_match": "ud.nested.*.sort.numeric.*",
            "mapping": {
              "coerce": true,
              "ignore_malformed": true,
              "type": "float"
            }
          }
        },
        {
          "nested_sort_string": {
            "path_match": "ud.nested.*.sort.string.*",
            "mapping": {
              "ignore_above": 128,
              "normalizer": "sort_string_normalizer",
              "type": "keyword"
            }
          }
        },
        {
          "disable_other": {
            "path_match": "*",
            "path_unmatch": "ud.*",
            "mapping": {
              "enabled": false,
              "type": "object"
            }
          }
        }
      ],
      "properties": {
        "ud": {
          "properties": {
            "aggs": {
              "properties": {
                "date": {
                  "properties": {
                    "last_upserted_at": {
                      "type": "date",
                      "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis"
                    }
                  }
                },
                "flattened": {
                  "properties": {
                    "facets": {
                      "type": "flattened"
                    }
                  }
                },
                "numeric": {
                  "properties": {
                    "enrichment_level": {
                      "type": "float",
                      "ignore_malformed": true,
                      "coerce": true
                    }
                  }
                },
                "string": {
                  "properties": {
                    "assortment_id": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "brand": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "campaign_id": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "component_ids": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "make_model_model": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "market": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "replaced_in_country": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "sales_category": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "sales_category_STEPWeb": {
                      "type": "keyword",
                      "ignore_above": 128
                    },
                    "variant_id": {
                      "type": "keyword",
                      "ignore_above": 128
                    }
                  }
                }
              }
            },
            "display": {
              "properties": {
                "brand": {
                  "type": "text",
                  "index": false
                },
                "item_description_original": {
                  "type": "text",
                  "index": false
                },
                "item_id": {
                  "type": "text",
                  "index": false
                },
                "replaced_in_country": {
                  "type": "text",
                  "index": false
                },
                "thumbnail": {
                  "type": "text",
                  "index": false
                }
              }
            },
            "nested": {
              "properties": {
                "offers": {
                  "type": "nested"
                }
              }
            },
            "score": {
              "properties": {
                "interacted_item_boosting_interaction_90d_language": {
                  "type": "float"
                },
                "normalized_interacted_item_boosting_interaction_90d_language": {
                  "type": "float"
                }
              }
            },
            "search": {
              "properties": {
                "ids": {
                  "properties": {
                    "attribute_search_names": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "edge_ngram": {
                          "type": "text",
                          "analyzer": "search_ids--edge_ngram_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    },
                    "competitor_item_number": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "edge_ngram": {
                          "type": "text",
                          "analyzer": "search_ids--edge_ngram_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "no_splitting": {
                          "type": "text",
                          "analyzer": "search_ids--no_splitting_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "standard": {
                          "type": "text",
                          "analyzer": "search_ids--standard_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    },
                    "eans": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "no_splitting": {
                          "type": "text",
                          "analyzer": "search_ids--no_splitting_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    },
                    "external_item_id": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "edge_ngram": {
                          "type": "text",
                          "analyzer": "search_ids--edge_ngram_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "no_splitting": {
                          "type": "text",
                          "analyzer": "search_ids--no_splitting_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "standard": {
                          "type": "text",
                          "analyzer": "search_ids--standard_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    },
                    "item_id": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "edge_ngram": {
                          "type": "text",
                          "analyzer": "search_ids--edge_ngram_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "no_splitting": {
                          "type": "text",
                          "analyzer": "search_ids--no_splitting_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "standard": {
                          "type": "text",
                          "analyzer": "search_ids--standard_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    },
                    "merchandising_associations_alternatives": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "no_splitting": {
                          "type": "text",
                          "analyzer": "search_ids--no_splitting_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "standard": {
                          "type": "text",
                          "analyzer": "search_ids--standard_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    },
                    "oe_number": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "no_splitting": {
                          "type": "text",
                          "analyzer": "search_ids--no_splitting_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "standard": {
                          "type": "text",
                          "analyzer": "search_ids--standard_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    },
                    "replaces": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "no_splitting": {
                          "type": "text",
                          "analyzer": "search_ids--no_splitting_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    },
                    "supplier_item_number": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "edge_ngram": {
                          "type": "text",
                          "analyzer": "search_ids--edge_ngram_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        },
                        "no_splitting": {
                          "type": "text",
                          "analyzer": "search_ids--no_splitting_index_analyzer",
                          "search_analyzer": "search_ids--standard_search_analyzer"
                        }
                      }
                    }
                  }
                },
                "text": {
                  "properties": {
                    "attribute_search_names": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        }
                      }
                    },
                    "attribute_values": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "word_edge_ngram": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_search_analyzer"
                        }
                      }
                    },
                    "brand": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "brand_cleaned": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "no_decompound": {
                          "type": "text",
                          "analyzer": "search_text--no_decompound_index_analyzer",
                          "search_analyzer": "search_text--no_decompound_search_analyzer"
                        },
                        "no_stemming": {
                          "type": "text",
                          "analyzer": "search_text--no_stemming_index_analyzer",
                          "search_analyzer": "search_text--no_stemming_search_analyzer"
                        },
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "word_edge_ngram": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_search_analyzer"
                        }
                      }
                    },
                    "competitor_item_number": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        }
                      }
                    },
                    "description": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "standard_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_no_synonyms_search_analyzer"
                        },
                        "word_edge_ngram": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_search_analyzer"
                        },
                        "word_edge_ngram_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_no_synonyms_search_analyzer"
                        }
                      }
                    },
                    "external_item_id": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "word_edge_ngram": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_search_analyzer"
                        }
                      }
                    },
                    "functional_name": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "no_decompound_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--no_decompound_index_analyzer",
                          "search_analyzer": "search_text--no_decompound_no_synonyms_search_analyzer"
                        },
                        "no_stemming_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--no_stemming_index_analyzer",
                          "search_analyzer": "search_text--no_stemming_no_synonyms_search_analyzer"
                        },
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "standard_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_no_synonyms_search_analyzer"
                        },
                        "word_edge_ngram": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_search_analyzer"
                        },
                        "word_edge_ngram_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_no_synonyms_search_analyzer"
                        }
                      }
                    },
                    "interacted_search_terms_interaction_365d_global_success": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "normalized_keyword": {
                          "type": "text",
                          "analyzer": "search_text--normalized_keyword_index_analyzer"
                        }
                      }
                    },
                    "interacted_search_terms_interaction_365d_language_success": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "normalized_keyword": {
                          "type": "text",
                          "analyzer": "search_text--normalized_keyword_index_analyzer"
                        }
                      }
                    },
                    "item_description_no_brand": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "no_decompound": {
                          "type": "text",
                          "analyzer": "search_text--no_decompound_index_analyzer",
                          "search_analyzer": "search_text--no_decompound_search_analyzer"
                        },
                        "no_decompound_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--no_decompound_index_analyzer",
                          "search_analyzer": "search_text--no_decompound_no_synonyms_search_analyzer"
                        },
                        "no_stemming": {
                          "type": "text",
                          "analyzer": "search_text--no_stemming_index_analyzer",
                          "search_analyzer": "search_text--no_stemming_search_analyzer"
                        },
                        "no_stemming_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--no_stemming_index_analyzer",
                          "search_analyzer": "search_text--no_stemming_no_synonyms_search_analyzer"
                        },
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "standard_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_no_synonyms_search_analyzer"
                        },
                        "word_edge_ngram": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_search_analyzer"
                        },
                        "word_edge_ngram_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_no_synonyms_search_analyzer"
                        }
                      }
                    },
                    "item_description_no_spec": {
                      "type": "text",
                      "fields": {
                        "keyword": {
                          "type": "keyword",
                          "ignore_above": 256
                        }
                      }
                    },
                    "item_description_only_spec": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "standard_no_synonyms": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_no_synonyms_search_analyzer"
                        }
                      }
                    },
                    "item_id": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "word_edge_ngram": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_search_analyzer"
                        }
                      }
                    },
                    "oe_number": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        }
                      }
                    },
                    "sales_category_name": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        }
                      }
                    },
                    "supplier_item_number": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        }
                      }
                    },
                    "suppressed_search_terms": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "normalized_keyword": {
                          "type": "text",
                          "analyzer": "search_text--normalized_keyword_index_analyzer"
                        }
                      }
                    },
                    "variant_description": {
                      "type": "text",
                      "index": false,
                      "fields": {
                        "standard": {
                          "type": "text",
                          "analyzer": "search_text--standard_index_analyzer",
                          "search_analyzer": "search_text--standard_search_analyzer"
                        },
                        "word_edge_ngram": {
                          "type": "text",
                          "analyzer": "search_text--word_edge_ngram_index_analyzer",
                          "search_analyzer": "search_text--word_edge_ngram_search_analyzer"
                        }
                      }
                    }
                  }
                }
              }
            },
            "sort": {
              "properties": {
                "nested": {
                  "properties": {
                    "campaign": {
                      "type": "nested",
                      "properties": {
                        "id": {
                          "type": "keyword",
                          "ignore_above": 128
                        },
                        "sortOrder": {
                          "type": "float",
                          "ignore_malformed": true,
                          "coerce": true
                        }
                      }
                    },
                    "components_sorting": {
                      "type": "nested",
                      "properties": {
                        "id": {
                          "type": "keyword",
                          "ignore_above": 128
                        },
                        "sortOrder": {
                          "type": "float",
                          "ignore_malformed": true,
                          "coerce": true
                        }
                      }
                    }
                  }
                },
                "numeric": {
                  "properties": {
                    "interacted_item_boosting_interaction_90d_language": {
                      "type": "float",
                      "ignore_malformed": true,
                      "coerce": true
                    },
                    "normalized_interacted_item_boosting_interaction_90d_language": {
                      "type": "float",
                      "ignore_malformed": true,
                      "coerce": true
                    },
                    "variant_sorting": {
                      "type": "float",
                      "ignore_malformed": true,
                      "coerce": true
                    }
                  }
                },
                "string": {
                  "properties": {
                    "brand": {
                      "type": "keyword",
                      "ignore_above": 128,
                      "normalizer": "sort_string_normalizer"
                    },
                    "item_id": {
                      "type": "keyword",
                      "ignore_above": 128,
                      "normalizer": "sort_string_normalizer"
                    }
                  }
                }
              }
            },
            "suggestions": {
              "type": "text",
              "index": false,
              "fields": {
                "phrase": {
                  "type": "text",
                  "analyzer": "suggestions_phrase_analyzer"
                },
                "phrase-reverse": {
                  "type": "text",
                  "analyzer": "suggestions_phrase_reverse_analyzer"
                },
                "terms": {
                  "type": "text",
                  "analyzer": "suggestions_terms_analyzer"
                }
              }
            }
          }
        }
      }
    }
  }
}```