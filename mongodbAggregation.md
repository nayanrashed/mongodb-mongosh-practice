-	mongoDB Aggregation Operator
- $match
```tsx
db.test.aggregate([
    //stage 1
    { $match: { gender: "Male", age: { $lt: 30 } } },
    //stage 2
    { $project: { name: 1, gender: 1, age: 1 } }
])
```

- To add fields: $addFields. (it does not modify actual doc.)
```tsx
db.test.aggregate([
    //stage 1
    { $match: { gender: "Male" }},
    //stage 2
    { $addFields: { course: "level-2" } }
])

```
- but we can make new doc with aggregate by using $out
```tsx
db.test.aggregate([
    //stage 1
    { $match: { gender: "Male" } },
    //stage 2
    { $addFields: { course: "level-2", eduTech: "Programming Hero" } },
    //stage 3
    { $project: { course: 1 } },
    //stage 4
    { $out: "course-stodent" }
])
```
here $project is used to select the fields. to select all the field we can remove $project stage