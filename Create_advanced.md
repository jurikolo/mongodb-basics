# Commands
* insertOne()
* insertMany()
* insert()
* mongoimport

## Insert
* insertOne()
    ```mongojs
    db.collectionName.insertOne({"Key" : "Value"})
    ```

* insertMany()
    ```mongojs
    db.collectionName.insertMany([{"Key1" : "Value1"}, {"Key2" : "Value2"}])
    ```
    
    It's possible to configure ordering. FALSE will insert all the documents, 
        while TRUE (which is default), will stop on first error, say if document duplicates:
    ```mongojs
    db.collectionName.insertMany([{"Key1" : "Value1"}, {"Key2" : "Value2"}], {ordered: false})
    ```

* insert()
    ```mongojs
    db.collectionName.insert({"Key" : "Value"})
    ```
    
    can insert multiple objects as well (uses BulkWrite):
    ```mongojs
    db.collectionName.insert([{"Key1" : "Value1"}, {"Key2" : "Value2"}])
    ```
    
    NOTE: insert() doesn't return ObjectId
    
## Import
[Official documentation](https://docs.mongodb.com/v3.6/reference/program/mongoimport/)
```mongojs
mongoimport --db users --collection contacts --file contacts.json --drop
```
    
## Other
* Write concern ([docs](https://docs.mongodb.com/v3.6/reference/write-concern/))
