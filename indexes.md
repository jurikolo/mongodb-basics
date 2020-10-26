# Indexes

* [explain()](https://docs.mongodb.com/v3.6/reference/method/cursor.explain/). To investigate the query, add explain() after collection name, but before the operation:
```mongojs
db.collection.explain().find({})
``` 

* More details can be retrieved by passing executionStats in explain():
```mongojs
db.collection.explain("executionStats").find({})
``` 