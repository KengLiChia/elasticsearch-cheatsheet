# Chapter 3
Topics covered as follows:
- Search for phrase
- Run a match query against multiple fields
- Combined queries

## Search for phrase using the match_phrase query
```
GET name-of-index/_search {
  "query": {
    "match_phrase": {
        "field": {
          "query": Enter phrase
          }
      }
  }
}
```

## Running a match query against multiple fields
The following asks ElasticSearch to query documents that contains the search term "Tomato Pineaaple BaiChoy" in the fields fruits and vegetable. 
```
GET name-of-index/_search {
  "query": {
    "multi_match": {
      "query": "Tomato Pineapple BaiChoy",
      "fields": [
        "fruits",
        "vegetable",
      ]
    }
  }
}
```
To designate one field to carry more weight use "^2"

## Improve precision with phrase type match
```
GET name-of-index/_search {
  "query": {
    "multi_match": {
      "query": "Tomato Pineapple BaiChoy",
      "fields": [
        "fruits",
        "vegetable",
      ],
      "type": "phrase"
    }
  }
}
```
## Combined Queries
### Bool Query
Suppose you have an Elasticsearch index called "products," and you want to search for products that meet the following criteria:

1. The product title must contain the word "laptop."
2. Products with the brand "Dell" should be excluded from the results.
3. The product price should be between $500 and $1000.
4. The product should belong to the category "Electronics
```
GET products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "title": "laptop"
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "brand": "Dell"
          }
        }
      ],
      "should": [
        {
          "match": {
            "description": "gaming"
          }
        },
        {  
          "match": {
            "headline": "video-making"
          }
        }
      ],
      "filter": [
        {
          "range": {
            "price": {
              "gte": 500,
              "lte": 1000
            }
          }
        },
        {
          "term": {
            "category": "Electronics"
          }
        }
      ]
    }
  }
}
```
Should Clause is nice to have and would be prioritize. 
