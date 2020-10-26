# Indexes
## Understand the issue
* [explain()](https://docs.mongodb.com/v3.6/reference/method/cursor.explain/). To investigate the query, add explain() after collection name, but before the operation:
```mongojs
db.collection.explain().find({})
``` 

* More details can be retrieved by passing executionStats in explain():
```mongojs
db.collection.explain("executionStats").find({})
``` 

## Improve DB performance
* Create ascending sorted index:
```mongojs
db.collection.createIndex({"Key1": 1})
```

* Create descending sorted index on embedded document:
```mongojs
db.collection.createIndex({"Key1.EmbeddedKey2": -1})
```