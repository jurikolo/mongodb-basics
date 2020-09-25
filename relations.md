# Relations
There are 2 types of relations available:
* embedded
* references

## Embedded
* One to one relationship 
```mongojs
db.test.insertOne({"key1":"value1", key2:"value2", key3: {"nestedKey1":"nestedValue1", "nestedKey2":"nestedValue2"}})
```

* One to many relationship
```mongojs
db.persons.insertOne({Name: "Jurijs", age: 34, cars: [{Brand: "Ford", Model: "C-Max"}, {Brand: "Renault", Model: "Thalia"}]})
```

## References
* One to one relationship
```mongojs
db.persons.insertOne({Name: "Jurijs", age: 34})
db.cars.insertOne({Brand: "Ford", Model: "C-Max", owner: ObjectId("123")})
```

* One to many relationship
```mongojs
db.persons.insertOne({Name: "Jurijs", age: 34, cars: ["jurikolo_car_1", "jurikolo_car_2"]})
db.cars.insertOne({Brand: "Ford", Model: "C-Max", _id: "jurikolo_car_1"})
db.cars.insertOne({Brand: "Renault", Model: "Thalia", _id: "jurikolo_car_2"})
```