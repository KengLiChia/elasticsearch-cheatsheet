# Chapter 2
Topics covered as follows:
-  Basics on queries and aggregations

## Queries 
Queries retrieve documents that match the criteria

### Retrieve information about documents in an index
```
GET name-of-index/_search
```
The above would show a default of 10 results and max of 10,000 hits. 

### Get the exact total number of hits 
To get an exact total number of hits, you may use the following query. 
```
GET name-of-index/_search
{
 "track_total_hits": true
}
```

### Search for data within a specific time range
```
GET name-of-index/_search
{
  "query": {
    "range": {
      "field: {
        "gte": "2023/09/07",
        "lte": "2023/09/08",
        }
      }
    }
}
```

## Aggregations
An aggregation summarizes your data as metrics (e.g. average), statistics, and other analytics. 

### Analyze the dataset to show categories.
```
GET name-of-index/_search
{
  "aggs": {
      "aggs-name": {
        "terms": {
            "field": Name the field you want to aggregate here
            "size": Indicate how many buckets you want to returned here
          }
        }
    }
}
```

### A combination of query and aggregation request
### Search for the most significant term in a category
```
GET name-of-index/_search
{
  "query": {
    "match": {
        "Enter category": Enter the category value e.g. ENTERTAINMENT
      }
    },
    "aggs": {
      "aggs-name": {
        "significant_text": { 
            "field": Enter the name of field you searching for e.g. headline
          }
        }
    }
}
```
The above would search for headlines that are under category.

### Increase Precision   
```
GET name-of-index/_search
{
  "query": {
    "match": {
      "Enter the field you want to search": {
        "query": Enter search terms
        "operator": "and" // Use "and" for precision or "or" for broader results
      }
    }
  }
}
``        
```
GET name-of-index/_search
{
  "query": {
    "match": {
      "field": {
        "query": enter search terms,
        "minimum_should_match": 2
        }
      }
  }
}
