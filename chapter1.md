# Chapter 1 
Topics covered as follows:
- Getting information about clusters and nodes 
- Performing CRUD operations with Elasticsearch and Kibana
  
## Getting information about cluster and nodes
Cluster > Node (instance) > Index (similar documents) > Shards (data)
### Get information about cluster
```
GET _cluster/health
```
### Get information about nodes
```
GET _nodes/stats
```

## Performing CRUD operations 
### CREATE 
### Create Index
```
PUT name-of-index
```
### Index Document (POST - without ID)
```
POST name-of-index/_doc
{
  "field": "value"
}
```
 ### Index Document (PUT - with ID)
 ```
PUT name-of-index/_doc/id-you-want-to-assign
{
  "field": "value"
}
```
### Create Endpoint
```
PUT name-of-index/_create/id-you-want-to-assign
{
  "field": "value"
}
```
This API prompts if a document with the same ID already exists, compared to _doc.
### READ
### Read Document
```
GET name-of-index/_doc/id-you-want-to-read
```
### UPDATE
### Update Document 
```
POST name-of-index/_doc/id-you-want-to-update
{
  "doc":{
    "field": "new-value"
    "field": "new-value"
  }
}
```
### DELETE
### Delete Document
```
DELETE name-of-index/_doc/id-you-want-to-delete
