### mongoDB-mongosh

-	To Enter single data:
```tsx db.test.insertOne({name:"python Master"})```
-	To enter multiple data:
```tsx db.test.insertMany([{ name: "Complete Web Development" }, { name: "Data Anlysis" }])```
-	Find data: To Get Single Data
```tsx db.test.findOne({age:17})```
-	Find data: To Get Many Data
```tsx db.test.find({age:17})```
-	Find with field filtering (it will works with findOne)
```tsx  db.test.find({gender:"Female"},{gender:1})```
-	Field Filtering
```tsx db.test.find({ gender: "Female" }, { name: 1, gender: 1, email: 1, phone: 1 })```
Or
```tsx db.test.find({ gender: "Female" }).project({name:1,email:1})```

