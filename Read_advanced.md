[Official documentation](https://docs.mongodb.com/v3.6/reference/operator/query/)

# Commands
* db.collection.findOne()
* db.collection.find() - compared to findOne(), returns cursor

# Query operators
## Comparison operators
* equality
```mongojs
db.collection.find({"Key" : "Value"})
```

the same as
```mongojs
db.collection.find({"Key" : {$eq : "Value"}})
```

* not equal
```mongojs
db.collection.find({"Key" : {$ne : "Value"}})
```

* less than ($lt) or "less or equal to" ($lte)
* greater than ($gt) or "greater or equal to" ($gte)

* search by embedded document
```mongojs
db.collection.find({"key.embeddedKey.anotherEmbeddedKey" : {$gt : "Value"}}).pretty()
```

* search for documents where entry exists in array
```mongojs
db.collection.find({"Key" : "Value"})
```

* search for documents where array is exactly as you search for
```mongojs
db.collection.find({"Key" : ["Value1", "Value2"]})
```

* search for several matching values
```mongojs
db.collection.find({"Key" : {$in : ["Value1", "Value2"]}})
```

* search for documents where key is not one of matching values
```mongojs
db.collection.find({"Key" : {$nin : ["Value1", "Value2"]}})
```

## Logical operators
* $and
```mongojs
db.collection.find({$and: [{"Key" : {$lt : "Value1"}}, {"Key2" : "Value2"}]})
```

New version of the same $and query, but doesn't work in old versions / JS parsers, so better use full form
```mongojs
db.collection.find({"Key" : {$lt : "Value1"}, "Key2" : "Value2"})
```

* $not. Return documents that does not match the condition
```mongojs
db.collection.find({"Key" : {$not: {$eq: "Value"}}})
```

* $nor. Return documents that doesn't match all the conditions
```mongojs
db.collection.find({$nor: [{"Key" : {$lt : "Value1"}}, {"Key" : {$gt : "Value2"}}]})
```

* $or. Return documents that match any of conditions
```mongojs
db.collection.find({$or: [{"Key" : {$lt : "Value1"}}, {"Key" : {$gt : "Value2"}}]})
```
