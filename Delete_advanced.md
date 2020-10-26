* Delete one record:
```mongojs
db.collection.deleteOne({_id: ObjectId(12345)})
```

* Delete all records that match certain criteria:
```mongojs
db.collection.deleteMany({"Key1": "Value1", "Key2": {$gte: 5}})
```

* Delete all records in collection:
```mongojs
db.collection.deleteMany({})
```

* Remove collection:
```mongojs
db.collection.drop()
```

* Remove database (you need to be inside that database):
```mongojs
db.dropDatabase()
```