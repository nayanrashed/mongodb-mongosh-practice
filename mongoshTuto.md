### mongoDB-mongosh

-	To Enter single data:
```db.test.insertOne({name:"python Master"})```
-	To enter multiple data:
```db.test.insertMany([{ name: "Complete Web Development" }, { name: "Data Anlysis" }])```
-	Find data: To Get Single Data
```db.test.findOne({age:17})```
-	Find data: To Get Many Data
```db.test.find({age:17})```
-	Find with field filtering (it will works with findOne)
``` db.test.find({gender:"Female"},{gender:1})```
-	Field Filtering
```db.test.find({ gender: "Female" }, { name: 1, gender: 1, email: 1, phone: 1 })```
Or
``` db.test.find({ gender: "Female" }).project({name:1,email:1})```

