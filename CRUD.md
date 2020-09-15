# MongoDB CRUD
## Create DB
* Create a DB and enter into
```mongojs
use test
```

## Create
* Insert one document. Command can be executed multiple times
```mongojs
db.test.insertOne({"key1":"value1", key2:"value2"})
db.test.insertOne({"key1":"value1", key2:"value2"})
db.test.insertOne({"key1":"value1", key2:"value2"})
```

* Insert document with nested object
```mongojs
db.test.insertOne({"key1":"value1", key2:"value2", key3: {"nestedKey1":"netsedValue1", "nestedKey2":"nestedValue2"}})
```

* Insert many documents
```mongojs
db.test.insertMany([{"key1":"value1", key2:"value2"},{"key1":"value1", key2:"value2"}])
```

## Read
* Return all records and pretty print
```mongojs
db.test.find().pretty()
```

* Search for one document
```mongojs
db.test.findOne({"key1" : "value1"})
```

* Search for all the documents with empty filter
```mongojs
db.test.find({})
```

* Search for a document where parameter is greater than some value
```mongojs
db.test.find({"key1" : {$gt : 123}})
```

* Search for all and filter out everything except particular key (_id must be explicitly filtered out)
```mongojs
db.test.find({}, {"key1":1, _id:0})
```

## Update
* Update all documents with extra parameter
```mongojs
db.test.updateMany({}, {$set: {"newKey1" : "newValue1"}})
```

* updateOne() and updateMany() adds / modifies document with provided parameters / values using $set. update() rewrites object with data provided
```mongojs
db.test.update({"key1" : "value1"}, {"theOnlyKey1" : "theOnlyValue1"})
```

* It's recommended to use .replaceOne() instead of .modify()
```mongojs
db.test.replaceOne({"key1" : "value1"}, {"theOnlyKey1" : "theOnlyValue1"})
```

## Delete
* Delete one document
```mongojs
db.test.deleteOne({"key1" : "value1"})
```

* Delete all that match condition
```mongojs
db.test.deleteMany({"newKey1" : "newValue1"})
```

## Read extras
* Return all records as an array
```mongojs
db.test.find().toArray()
```

* Iterate over find() results using [cursor](https://docs.mongodb.com/manual/reference/method/cursor.forEach/)
```mongojs
db.test.find().forEach(<function>)
```

* Last bullet, another example - print each record:
```mongojs
db.test.find().forEach((testDate) => {printjson(testData)})
```