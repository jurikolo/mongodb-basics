[Official documentation](https://docs.mongodb.com/v3.6/reference/operator/update/)

# Commands
## updateOne()
* $set. Update record with id 12345 with new value for Key1:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$set: {"Key1": "Value2"}})
```

* $inc. Increment value by X (could be negative to reduce the value):
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$inc: {"Key1": 5}})
```

* $min. Update the value of the field to X **only if** X is lower than current value
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$min: {"Key1": 5}})
```

* $max. Update the value of the field to X **only if** X is greater than current value
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$max: {"Key1": 5}})
```

* $mul. Multiply the value of the field by X. For example, multiply by 10%:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {mul: {"Key1": 1.1}})
```

* $unset. Remove parameter from object:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$unset: {"Key1": ""}})
```

* upsert. Update a record if it exists or add if it's missing. This example below, when object is missing, it will add Key1 = "Value1":
```mongojs
db.collection.updateOne({"Key1": "Value1"}, {$set: {"Key2": "Value2", "Key3": 3}}, {upsert: true})
``` 

## updateMany()
* $set. Update several records that match criteria with new parameter (or override if it exists):
```mongojs
db.collection.updateMany({"Key1": "Value1"}, {$set: {"Key2": "Value2"}})
```

* $rename. Rename parameter name. For example, rename all objects parameter Key1 to Key2:
```mongojs
db.collection.updateMany({}, {$rename: {"Key1": "Key2"}})
```