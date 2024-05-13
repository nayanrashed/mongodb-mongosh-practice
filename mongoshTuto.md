### mongoDB-mongosh

- To Enter single data:
  </br>
  `tsx db.test.insertOne({name:"python Master"})`</br>
- To enter multiple data:</br>
  `tsx db.test.insertMany([{ name: "Complete Web Development" }, { name: "Data Anlysis" }])`</br>
- Find data: To Get Single Data</br>
  `tsx db.test.findOne({age:17})`</br>
- Find data: To Get Many Data</br>
  `tsx db.test.find({age:17})`</br>
- Find with field filtering (it will works with findOne)</br>
  `tsx  db.test.find({gender:"Female"},{gender:1})`</br>
- Field Filtering</br>
  `tsx db.test.find({ gender: "Female" }, { name: 1, gender: 1, email: 1, phone: 1 })`</br>
  Or</br>
  `tsx db.test.find({ gender: "Female" }).project({name:1,email:1})`
