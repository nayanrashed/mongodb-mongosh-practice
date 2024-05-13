### mongoDB-mongosh

- To Enter single data:
  </br>
  ```tsx
  db.test.insertOne({ name: "python Master" });
  ```
- To enter multiple data:</br>
  ```tsx
  db.test.insertMany([
    { name: "Complete Web Development" },
    { name: "Data Anlysis" },
  ]);
  ```
- Find data: To Get Single Data</br>
  ```tsx
  db.test.findOne({ age: 17 });
  ```
- Find data: To Get Many Data</br>
  ```tsx
  db.test.find({ age: 17 });
  ```
- Find with field filtering (it will works with findOne)
  ```tsx
  db.test.find({ gender: "Female" }, { gender: 1 });
  ```
- Field Filtering
  ```tsx
  db.test.find(
    { gender: "Female" },
    { name: 1, gender: 1, email: 1, phone: 1 }
  );
  ```
  Or
  ```tsx
  db.test.find({ gender: "Female" }).project({ name: 1, email: 1 });
  ```

### Operator

- Equal: $eq

```tsx
db.test.find({ age: { $eq: 12 } });
```

- Not Equal: $ne

```tsx
db.test.find({ age: { $eq: 12 } });
```

- Gt with sort

```tsx
db.test.find({ age: { $gt: 30 } }).sort({ age: -1 });
```

- Gte with sort

```tsx
db.test.find({ age: { $gte: 30 } }).sort({ age: -1 });
```

- lt with

```tsx
db.test.find({ age: { $lt: 30 } });
```

- lte with sort

```tsx
db.test.find({ age: { $lte: 30 } }).sort({ age: -1 });
```

- Implicit and with sort ascending order

```tsx
db.test.find({ age: { $gt: 18, $lt: 30 } }, { age: 1 }).sort({ age: -1 });
```

```tsx
db.test
  .find({ gender: "Female", age: { $gt: 18, $lt: 30 } }, { age: 1 })
  .sort({ age: -1 });
```

- $in and $nin

```tsx
db.test
  .find(
    { gender: "Female", age: { $in: [18, 20, 22, 24, 26, 28] } },
    { age: 1 }
  )
  .sort({ age: -1 });
```

```tsx
db.test
  .find(
    {
      gender: "Female",
      age: { $in: [18, 20, 22, 24, 26, 28, 30, 31] },
      interests: "Cooking",
    },
    { name: 1, age: 1, interests: 1 }
  )
  .sort({ age: -1 });
```

```tsx
db.test
  .find(
    {
      gender: "Female",
      age: { $nin: [18, 20, 22, 24, 26, 28, 30, 31] },
      interests: { $in: ["Cooking", "Gaming"] },
    },
    { name: 1, age: 1, interests: 1 }
  )
  .sort({ age: -1 });
```

- Implicit $and:

```tsx
db.test.find({ age: { $en: 15, $lte: 30 } });
```

- $and:

```tsx
db.test
  .find({
    $and: [{ gender: "Female" }, { age: { $ne: 15 } }, { age: { $lte: 30 } }],
  })
  .project({ age: 1 });
```

- $or

```tsx
db.test
  .find({
    $or: [
      { interests: "Traveling" },
      { interests: "Cooking" },
      { gender: "Female" },
    ],
  })
  .project({ name: 1, interests: 1 });
```

```tsx
db.test
  .find({
    $or: [{ "skills.name": "JAVASCRIPT" }, { "skills.name": "PYTHON" }],
  })
  .project({ name: 1, skills: 1 });
```

- Implicit $or

```tsx
db.test
  .find({
    "skills.name": { $in: ["JAVASCRIPT", "PYTHON"] },
  })
  .project({ name: 1, skills: 1 });
```

- $exists

```tsx
db.test.find({ age: { $exists: true } });
```

- $type

```tsx
db.test.find({ age: { $type: "string" } });
```

```tsx
db.test.find({ company: { $type: "null" } });
```

- $size

```tsx
db.test.find({ friends: { $size: 4 } });
```

- Match

```tsx
db.test.find({ "interests.2": "Cooking" }).project({ interests: 1 });
```

```tsx
db.test.find({ "skills.name": "JAVASCRIPT" }).project({ skills: 1 });
```

- $all

```tsx
db.test
  .find({ interests: { $all: ["Travelling", "Gaming", "Cooking"] } })
  .project({ interests: 1 });
```

- $elemMatch

```tsx
db.test
  .find({
    skills: {
      $elemMatch: {
        name: "JAVASCRIPT",
        level: "Intermidiate",
      },
    },
  })
  .project({ skills: 1 });
```

- Update Operator
- $set

```tsx
db.test.updateOne(
  { _id: ObjectId("6406ad63fc13ae5a40000065") },
  {
    $set: {
      age: 80,
    },
  }
);
```

```tsx
db.test.updateOne(
  { _id: ObjectId("6406ad63fc13ae5a40000065") },
  {
    $set: {
      interests: ["Gaming", "Writing", "Reading"],
    },
  }
);
```

- To add an element to an Array

```tsx
db.test.updateOne(
  { _id: ObjectId("6406ad63fc13ae5a40000065") },
  {
    $addToSet: {
      interests: "Cooking",
    },
  }
);
```

- To add more than one element

```tsx
db.test.updateOne(
  { _id: ObjectId("6406ad63fc13ae5a40000065") },
  {
    $addToSet: {
      interests: { $each: ["Driving", "Watching"] },
    },
  }
);
```

- To add duplicate entry

```tsx
db.test.updateOne(
  { _id: ObjectId("6406ad63fc13ae5a40000065") },
  {
    $push: {
      interests: { $each: ["Driving", "Watching"] },
    },
  }
);
```
