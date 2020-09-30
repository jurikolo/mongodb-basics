# Validations
MongoDB schema validation documentation: [click](https://docs.mongodb.com/v3.6/core/schema-validation/)

* Validation during collection creation
```mongojs
db.createCollection("posts", {
  validator: {
    $jsonSchema: {
      bsonType: "object", 
      required: ["title", "text"], 
      properties: {
        title: {
          bsonType: "string", 
          description: "must be a text"
        }
      }
    }
  }
})
```

NOTE: doesn't work in Amazon DocumentDB as of 30th of September 2020.

* Modify / Add validation to existing collection
```mongojs
db.runCommand({collMod: 'posts',
  validator: {
    $jsonSchema: {
      bsonType: "object", 
      required: ["title", "text"], 
      properties: {
        title: {
          bsonType: "string", 
          description: "must be a text"
        }
      }
    }
  },
  validationAction: "warn"
})
```