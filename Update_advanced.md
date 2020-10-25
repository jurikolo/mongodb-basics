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

* $push. Add an element to an array, can be a duplicate:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$push: {"ArrayKey1": {"Key1": "Value1", "Key2": 2}}})
```

* $push + $each. Add multiple elements to an array:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$push: {"ArrayKey1": {$each: [{"Key1": "Value1", "Key2": 2}, {"Key3": "Value3", "Key4": 4}]}}})
```

* Same as example above, but sort the resulting array:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$push: {"ArrayKey1": {$each: [{"Key1": "Value1", "Key2": 2}, {"Key1": "Value3", "Key2": 4}], $sort: {"Key2": 1}}}})
```

* $pull. Remove elements from an array that match certain criteria:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$pull: {"ArrayKey1": {"Key1": "Value1"}}})
```

* $pop. Remove last (or first) element from array:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {$pop: {"ArrayKey1": 1}})
```

* addToSet. Add uniqye element to an array, e.g. do not allow duplicates:
```mongojs
db.collection.updateOne({_id: ObjectId(12345)}, {addToSet: {"ArrayKey1": {"Key1": "Value1", "Key2": 2}}})
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

* Update complex array element which matches certain criteria with Key2 value of 2:
```mongojs
db.collection.updateMany({"ArrayKey1": {$elemMatch: {"Key1": "Value1", "Key2": {$gte: 1}}}}, {$set: {"ArrayKey1.$": {"Key1": "Value2", "Key2": 2}}})
```

* Update complex array element which matches certain criteria with new parameter:
```mongojs
db.collection.updateMany({"ArrayKey1": {$elemMatch: {"Key1": "Value1", "Key2": {$gte: 1}}}}, {$set: {"ArrayKey1.$.NewParameter": true}})
```

* $[]. Update all entries in array in documents that match certain criteria:
```mongojs
db.collection.updateMany({"ArrayKey1": {$gte: 1}}, {$inc: {"ArrayKey1.$[].count": 1}})
```

* arrayFilters. Update many elements in array:
```mongojs
db.collection.updateMany({"ArrayKey1.EmbeddedKey1": {$gte: 1}}, {$set: {"ArrayKey1.$[X].NewParameter": 123}}, {arrayFilters: [{"X.EmbeddedKey1": {$gte: 1}}]})
```