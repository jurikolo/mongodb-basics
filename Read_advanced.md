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

## Elements
* $exists. Return documents where parameter exists
```mongojs
db.collection.find({"Key": {$exists: true}})
```

Can be extended with logical operators:
```mongojs
db.collection.find({"Key": {$exists: true, $gt: 123}})
```

* $type. Return documents where parameter has specified type
```mongojs
db.collection.find({"Key" : {$type: "string"}})
```

Can be a list of types:
```mongojs
db.collection.find({"Key" : {$type: ["string", "double"]}})
```

## Evaluation
* $regex. Search for regex in a parameter:
```mongojs
db.collection.find({"Key": {$regex: /value/}})
```

* $expr. Search for expression, for example where Key1 value is greater than Key2 value:
```mongojs
db.collection.find({$expr: {$gt: ["$Key1", "$Key2"]}})
```

# Arrays
* Search for documents where embedded document is array of objects and one of parameter equals to "X":
```mongojs
db.collection.find({"Key1.Key2": "X"})
```

* Search for documents where amount of entries in array are 42:
```mongojs
db.collection.find({"Key1": {$size: 42}})
```

* Search for documents where array matches values, but sequence of values doesn't matter:
```mongojs
db.collection.find({"Key1": {$all: ["Value1", "Value2"]}})
```

* Search for documents where embedded document in an array matches particular conditions:
```mongojs
db.collection.find({"Key1": {$elemMatch: {"Key2": "Value2", "Key3": {$gt: 42}}}})
``` 

## Projection
* Projection allows to return only requested parameters for the object. Parameter must have value 1 in find() to be returned:
```mongojs
db.collection.find({}, {"Key1": 1, "Key2": 1, "Key3": 1})
```

* ObjectId is always returned. It has to be explicitly set to 0 in order not to return:
```mongojs
db.collection.find({}, {"Key1": 1, "Key2": 1, "Key3": 1, _id: 0})
```

* Embedded parameters can be projected as well:
```mongojs
db.collection.find({}, {"Key1": 1, "Key2.EmbeddedKey1": 1})
```

* Search for value in array and return only this specific data instead of full array:
```mongojs
db.collection.find({"Key1": "Value1"}, {"Key1.$": 1})
```

* Slice. Limits amount of elements in array output:
```mongojs
db.collection.find({"Key1": "Value1"}, {"Key1": {$slice: 2}})
```

## Other
* .sort(). Sorting. 1 - ascending, -1 - descending:
```mongojs
db.collection.find().sort({"Key1": 1, "Key2": -1})
```

* .skip(). Skip some documents, can be used for pagination:
```mongojs
db.collection.find().skip(10)
```

* .limit(). Limit amount of records returned by cursor:
```mongojs
db.collection.find().limit(10)
```

And now everything at once:
```mongojs
db.collection.find().sort({"Key1": 1, "Key2": -1}).skip(100).limit(10).pretty()
```