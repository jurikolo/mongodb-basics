* Create a DB and enter into
```mongojs
use test
```

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

* Update all documents with extra parameter
```mongojs
db.test.updateMany({}, {$set: {"newKey1" : "newValue1"}})
```