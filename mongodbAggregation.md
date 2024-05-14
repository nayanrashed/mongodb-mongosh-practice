- mongoDB Aggregation Operator
- $match

```tsx
db.test.aggregate([
  //stage 1
  { $match: { gender: "Male", age: { $lt: 30 } } },
  //stage 2
  { $project: { name: 1, gender: 1, age: 1 } },
]);
```

- To add fields: $addFields. (it does not modify actual doc.)

```tsx
db.test.aggregate([
  //stage 1
  { $match: { gender: "Male" } },
  //stage 2
  { $addFields: { course: "level-2" } },
]);
```

- To make new doc with aggregate by using $out

```tsx
db.test.aggregate([
  //stage 1
  { $match: { gender: "Male" } },
  //stage 2
  { $addFields: { course: "level-2", eduTech: "Programming Hero" } },
  //stage 3
  { $project: { course: 1 } },
  //stage 4
  { $out: "course-stodent" },
]);
```

here $project is used to select the fields. we can add more than one fields. To select all the field we can remove $project stage.

- To merge the aggregated data with existing data we can use $merge

```tsx
db.test.aggregate([
  //stage 1
  { $match: { gender: "Male" } },
  //stage 2
  { $addFields: { course: "level-2", eduTech: "Programming Hero" } },
  //stage 3
  { $project: { course: 1, eduTech: 1 } },
  //stage 4
  { $merge: "test" },
]);
```

- $group

```tsx
db.test.aggregate([
  //stage-1
  { $group: { _id: "$address.country" } },
]);
```

- group with count

```tsx
db.test.aggregate([
  //stage-1
  { $group: { _id: "$address.country", count: { $sum: 1 } } },
]);
```

- group with $push

```tsx
db.test.aggregate([
  //stage-1
  {
    $group: {
      _id: "$address.country",
      count: { $sum: 1 },
      showMeName: { $push: "$name" },
    },
  },
]);
```

- To get full document using $push of groups

```tsx
db.test.aggregate([
  //stage-1
  {
    $group: {
      _id: "$address.country",
      count: { $sum: 1 },
      showMeName: { $push: "$$ROOT" },
    },
  },
]);
```

- using project

```tsx
db.test.aggregate([
  //stage-1
  {
    $group: {
      _id: "$address.country",
      count: { $sum: 1 },
      fullDoc: { $push: "$$ROOT" },
    },
  },
  //stage-2
  {
    $project: {
      "fullDoc.name": 1,
      "fullDoc.email": 1,
      "fullDoc.phone": 1,
    },
  },
]);
```

- group with different operator

```tsx
db.test.aggregate([
  {
    $group: {
      _id: null,
      totalSalary: { $sum: "$salary" },
      maxSalary: { $max: "$salary" },
      minSalary: { $min: "$salary" },
      avgSalary: { $avg: "$salary" },
    },
  },
]);
```

- Substrauction in Group

```tsx
db.test.aggregate([
  {
    $group: {
      _id: null,
      totalSalary: { $sum: "$salary" },
      maxSalary: { $max: "$salary" },
      minSalary: { $min: "$salary" },
      avgSalary: { $avg: "$salary" },
    },
  },
  {
    $project: {
      totalSalary: 1,
      maxSalary: 1,
      minSalary: 1,
      averageSalary: "$avgSalary",
      rangeB2nMaxMin: { $subtract: ["$maxSalary", "$minSalary"] },
    },
  },
]);
```
- To work with elements of array and object we have to extract them. so we need to use $unwind
```tsx
db.test.aggregate([
    //stage-1
    { $unwind: "$friends" },
    //stage-2
    { $group: { _id: "$friends", count: { $sum: 1 } } }
])
```
```tsx
db.test.aggregate([
    //stage-1
    { $unwind: "$interests" },
   //stage-2
   {
       $group:{_id:"$age", interestsPerAge:{$push:"$interests"}}
   }
])
```
- Bucket in MongoDB
```tsx
db.test.aggregate([
    //stage-1
    {
        $bucket: {
            groupBy: "$age",
            boundaries: [20, 40, 60, 80],
            default: "Over 80",
            output: {
                count: {
                    $sum: 1
                },
                nameList: { $push: "$name" }
            }
        }
    },
    //stage-2
    {
        $sort: { count: -1 }
    },
    //stage-3
    {
        $project: { count: 1 }
    }
])
```
```tsx
db.test.aggregate([
    //stage-1
    {
        $bucket: {
            groupBy: "$age",
            boundaries: [20, 40, 60, 80],
            default: "Over 80",
            output: {
                count: {
                    $sum: 1
                },
                nameList: { $push: "$name" }
            }
        }
    },
    //stage-2
    {
        $sort: { count: -1 }
    },
    //stage-3
    {
        $limit: 3
    },
    //stage-4
    {
        $project: { count: 1 }
    }
])
```
- $facet is used to create multiple pipe Line
```tsx
db.test.aggregate([
    {
        $facet: {
            //Pipe Line-1
            "friendsCount": [
                //stage-1
                { $unwind: "$friends" },
                //stage-2
                { $group: { _id: "$friends", count: { $sum: 1 } } }
            ],
            //Pipe Line-2
            "educationCount": [
                //stage-1
                { $unwind: "$education" },
                //stage-2
                { $group: { _id: "$education", count: { $sum: 1 } } },
            ],
            //Pipe Line-3
            "skilCount": [
                //stage-1
                { $unwind: "$skills" },
                //stage-2
                { $group: { _id: "$skills", count: { $sum: 1 } } }
            ]
        }
    }
])
```
- LookUP
```tsx
db.orders.aggregate([
    {
        $lookup: {
            from: "test",
            localField: "userId",
            foreignField: "_id",
            as: "client"
        }
    }
])
```
- search and text intexing
```tsx
db.getCollection("massive-data").createIndex({about:"text"})
```
```tsx
db.getCollection("massive-data").find({$text:{$search:"dolor"}})
```
