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

* Create compound index:
```mongojs
db.collection.createIndex({"Key1.EmbeddedKey2": 1, "Key3": -1})
```

NOTE: Sequence of elements in compound index does matter. User can benefit from both compound search and from FIRST element search.

* You can benefit from indexes for sorting results. Say there was previous ocmpound index implemented. Then following will use indexes:
```mongojs
db.collection.explain().find({"Key1.EmbeddedKey2": {$gte: 5}}).sort({"Key3": -1})
```

## Index configuration
* Enable uniqueness of element:
```mongojs
db.collection.createIndex({"Key1": 1}, {unique: true})
```

* Enable partial index, e.g. you want to index documents where certain field matches criteria:
```mongojs
db.collection.createIndex({"Key1": 1}, {partialFilterExpression: {"Key1": {$gte: 50}}})
```

* Partial index can be against another field. Say we want to index by age but only documents where animal is Kraken:
```mongojs
db.collection.createIndex({"Age": 1}, {partialFilterExpression: {"Animal": "Kraken"}})
```

* To create unique index but allow null value, e.g. parameter can be omitted in a document, use partial index:
```mongojs
db.collection.createIndex({"Key1": 1}, {unique: true, partialFilterExpression: {"Key1": {$exists: true}}})
```

* Remove record from DB after some amount of time:
```mongojs
db.collection.createIndex({"TimestampKey1": 1}, {expireAfterSeconds: 10})
```

## Other
* Remove index:
```mongojs
db.collection.dropIndex({"Key1": 1})
```