---
created: 2025-10-30T09:10
updated: 2025-10-30T09:11
tags:
  - elastic
---
```json
{
  "kramp-item-nl-2025-09-04": {
    "settings": {
      "index": {
        "max_ngram_diff": "14",
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "mapping": {
          "nested_objects": {
            "limit": "50000"
          },
          "total_fields": {
            "limit": "5000"
          }
        },
        "refresh_interval": "30s",
        "number_of_shards": "1",
        "provided_name": "kramp-item-nl-2025-09-04",
        "similarity": {
          "default": {
            "type": "boolean"
          }
        },
        "creation_date": "1757003534587",
        "analysis": {
          "filter": {
            "search_ids--min_length_4": {
              "type": "length",
              "min": "4"
            },
            "search_ids--edge_ngram_filter": {
              "type": "edge_ngram",
              "min_gram": "3",
              "max_gram": "25"
            },
            "suggestions_shingle_filter": {
              "max_shingle_size": "3",
              "min_shingle_size": "2",
              "type": "shingle"
            },
            "search_text--remove_empty_filter": {
              "type": "length",
              "min": "1"
            },
            "search_text--edge_ngram_filter": {
              "type": "edge_ngram",
              "min_gram": "3",
              "max_gram": "25"
            },
            "search_ids--partnumber_pattern_filter": {
              "type": "pattern_capture",
              "preserve_original": "true",
              "patterns": [
                "^7500(.*)",
                "^0+(.*)"
              ]
            },
            "search_text--alphanumeric_filter": {
              "pattern": "[^0-9a-zA-Z]",
              "type": "pattern_replace",
              "replacement": ""
            },
            "search_ids--split_letter_number": {
              "split_on_numerics": "true",
              "split_on_case_change": "false",
              "type": "word_delimiter_graph",
              "preserve_original": "true",
              "stem_english_possessive": "false"
            },
            "search_text--keyword_marker_filter": {
              "type": "length"
            },
            "search_text--language_normalize_filter": {
              "type": "length"
            },
            "search_text--make_model_synonym_filter": {
              "type": "synonym_graph",
              "synonyms": [
                "df => deutz-fahr",
                "international => case - ih",
                "fiatagri => fiat",
                "fiat agri => fiat",
                "jd => john deere",
                "nh => new holland",
                "mb => mercedes benz",
                "mf => massey ferguson",
                "db => david brown",
                "case => case, david brown",
                "mercedes => mercedes, mb trac"
              ]
            },
            "search_text--language_stemmer_filter": {
              "type": "stemmer",
              "language": "dutch"
            },
            "search_text--elision_filter": {
              "type": "length"
            },
            "search_text--unique_filter": {
              "type": "unique",
              "only_on_same_position": "true"
            },
            "search_text--synonym_filter": {
              "type": "synonym_graph",
              "synonyms_path": "analysis/nl/synonyms.txt"
            },
            "search_text--ngram_filter": {
              "type": "ngram",
              "min_gram": "1",
              "max_gram": "15"
            },
            "search_text--decompound_filter": {
              "type": "dictionary_decompounder",
              "word_list_path": "analysis/nl/dictionary.txt",
              "min_subword_size": "5"
            },
            "search_text--stop_filter": {
              "type": "length"
            },
            "search_ids--alphanumeric_filter": {
              "pattern": "[^0-9a-zA-Z]",
              "type": "pattern_replace",
              "replacement": ""
            }
          },
          "char_filter": {
            "search_text--vbelt_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(^|\s)(SPZ|SPA|SPB|SPC|XPZ|XPA|XPB|XPC|3V|5V|8V|3VX|5VX|8VX|ZX|AX|BX|CX)(?:\s|\-)*(\d+[\,\.]?\d*)""",
              "type": "pattern_replace",
              "replacement": "$1$2$3 $2 $3 "
            },
            "search_text--grams_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(\d+[\,\.]?\d*)(gr|g)(?:\s|$|\-|\.)""",
              "type": "pattern_replace",
              "replacement": "$1gr $1g "
            },
            "search_text--single_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(?<!\S)(\d+[\,\.]?\d*)\s*(cm|mm|µm|nm|m|ml|cl|dl|l|gr|g|kg|mg|v|ah|a|w)(?:\s|$|\-)""",
              "type": "pattern_replace",
              "replacement": "$1$2 "
            },
            "search_text--triple_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(?<!\S)(\d+[\,\.]?\d*)[x-](\d+[\,\.]?\d*)[x-](\d+[\,\.]?\d*)\s*(cm|mm|µm|nm|m|ml|cl|dl|l|gr|g|kg|mg|v|ah|a|w)?(?:\s|$|\-)""",
              "type": "pattern_replace",
              "replacement": "$1$4 $2$4 $3$4 "
            },
            "search_text--double_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(?<!\S)(\d+[\,\.]?\d*)[x-](\d+[\,\.]?\d*)(?![x\-\d\,\.])\s*(cm|mm|µm|nm|m|ml|cl|dl|l|gr|g|kg|mg|v|ah|a|w)?(?:\s|$|\-)""",
              "type": "pattern_replace",
              "replacement": "$1$3 $2$3 "
            },
            "search_text--motoroil_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(?:(sae)\s*(\d{2,4}))(?:\s|$)""",
              "type": "pattern_replace",
              "replacement": "$1$2 "
            },
            "search_text--plug_specification_charfilter": {
              "type": "mapping",
              "mappings": []
            },
            "search_text--iso_metric_screw_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(?<!(?:[^\s]))(M|DIN)(?:\s*)(\d+[\,\.]?\d*)[x-]?""",
              "type": "pattern_replace",
              "replacement": "$1$2 $2 "
            },
            "search_text--existing_to_no_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(?<!\S)((\d+[,.]?\d)(cm|mm|µm|nm|m|ml|cl|dl|l|gr|g|kg|mg|v|ah|a|w))(?:\s|$|-)""",
              "type": "pattern_replace",
              "replacement": "$1 $2 "
            },
            "search_text--normalize-decimal-separators": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(\d+),(\d+)""",
              "type": "pattern_replace",
              "replacement": "$1.$2"
            },
            "search_text--battery_specification_charfilter": {
              "flags": "CASE_INSENSITIVE",
              "pattern": """(?<!\S)(\d+[\,\.]?\d*)(v|ah|w)(\d+[\,\.]?\d*)(v|ah|w)?(?:\s|$|\-)""",
              "type": "pattern_replace",
              "replacement": "$1$2 $3$4 $1 $3 "
            }
          },
          "normalizer": {
            "sort_string_normalizer": {
              "filter": [
                "lowercase",
                "asciifolding"
              ],
              "type": "custom"
            }
          },
          "analyzer": {
            "search_text--simple_ngram_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--make_model_synonym_filter",
                "search_text--stop_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators"
              ],
              "type": "custom",
              "tokenizer": "keyword"
            },
            "search_text--word_edge_ngram_no_filters_index_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--edge_ngram_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators"
              ],
              "type": "custom",
              "tokenizer": "whitespace"
            },
            "suggestions_terms_analyzer": {
              "filter": [
                "lowercase"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--no_decompound_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--synonym_filter",
                "search_text--stop_filter",
                "search_text--language_normalize_filter",
                "search_text--keyword_marker_filter",
                "search_text--language_stemmer_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--simple_ngram_index_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--ngram_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators"
              ],
              "type": "custom",
              "tokenizer": "keyword"
            },
            "search_ids--standard_search_analyzer": {
              "filter": [
                "lowercase",
                "asciifolding",
                "search_ids--alphanumeric_filter"
              ],
              "type": "custom",
              "tokenizer": "keyword"
            },
            "suggestions_phrase_reverse_analyzer": {
              "filter": [
                "lowercase",
                "reverse"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_ids--edge_ngram_index_analyzer": {
              "filter": [
                "lowercase",
                "asciifolding",
                "search_ids--alphanumeric_filter",
                "search_ids--partnumber_pattern_filter",
                "search_text--unique_filter",
                "search_ids--split_letter_number",
                "search_ids--edge_ngram_filter"
              ],
              "type": "custom",
              "tokenizer": "keyword"
            },
            "search_text--word_edge_ngram_no_filters_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--make_model_synonym_filter",
                "search_text--stop_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators"
              ],
              "type": "custom",
              "tokenizer": "whitespace"
            },
            "search_ids--no_splitting_index_analyzer": {
              "filter": [
                "lowercase",
                "asciifolding",
                "search_ids--alphanumeric_filter",
                "search_ids--partnumber_pattern_filter"
              ],
              "type": "custom",
              "tokenizer": "keyword"
            },
            "search_text--standard_no_synonyms_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--language_normalize_filter",
                "search_text--keyword_marker_filter",
                "search_text--language_stemmer_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--no_stemming_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--synonym_filter",
                "search_text--stop_filter",
                "search_text--language_normalize_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--standard_index_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--decompound_filter",
                "search_text--language_normalize_filter",
                "search_text--keyword_marker_filter",
                "search_text--language_stemmer_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--existing_to_no_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--word_edge_ngram_index_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--alphanumeric_filter",
                "search_text--decompound_filter",
                "search_text--edge_ngram_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--existing_to_no_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "whitespace"
            },
            "suggestions_phrase_analyzer": {
              "filter": [
                "lowercase",
                "suggestions_shingle_filter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--no_decompound_index_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--language_normalize_filter",
                "search_text--keyword_marker_filter",
                "search_text--language_stemmer_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--existing_to_no_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--no_stemming_index_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--decompound_filter",
                "search_text--language_normalize_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--existing_to_no_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--normalized_keyword_index_analyzer": {
              "filter": [
                "trim",
                "lowercase",
                "asciifolding"
              ],
              "type": "custom",
              "tokenizer": "keyword"
            },
            "search_text--word_edge_ngram_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--synonym_filter",
                "search_text--stop_filter",
                "search_text--alphanumeric_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "whitespace"
            },
            "search_text--standard_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--synonym_filter",
                "search_text--stop_filter",
                "search_text--language_normalize_filter",
                "search_text--keyword_marker_filter",
                "search_text--language_stemmer_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_ids--standard_index_analyzer": {
              "filter": [
                "lowercase",
                "asciifolding",
                "search_ids--alphanumeric_filter",
                "search_ids--partnumber_pattern_filter",
                "search_ids--split_letter_number",
                "search_ids--min_length_4"
              ],
              "type": "custom",
              "tokenizer": "keyword"
            },
            "search_text--no_decompound_no_synonyms_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--language_normalize_filter",
                "search_text--keyword_marker_filter",
                "search_text--language_stemmer_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            },
            "search_text--word_edge_ngram_no_synonyms_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--alphanumeric_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "whitespace"
            },
            "search_text--no_stemming_no_synonyms_search_analyzer": {
              "filter": [
                "search_text--elision_filter",
                "lowercase",
                "asciifolding",
                "search_text--stop_filter",
                "search_text--language_normalize_filter",
                "search_text--unique_filter",
                "search_text--remove_empty_filter"
              ],
              "char_filter": [
                "search_text--normalize-decimal-separators",
                "search_text--iso_metric_screw_specification_charfilter",
                "search_text--single_specification_charfilter",
                "search_text--double_specification_charfilter",
                "search_text--triple_specification_charfilter",
                "search_text--motoroil_specification_charfilter",
                "search_text--grams_specification_charfilter",
                "search_text--vbelt_specification_charfilter",
                "search_text--battery_specification_charfilter",
                "search_text--plug_specification_charfilter"
              ],
              "type": "custom",
              "tokenizer": "standard"
            }
          }
        },
        "number_of_replicas": "1",
        "uuid": "3wO_t2niTT6ON2kV7oP4aQ",
        "version": {
          "created": "8505000"
        }
      }
    }
  }
}```