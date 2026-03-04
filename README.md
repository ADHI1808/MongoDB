# MongoDB
A document-based NoSQL database. It stores data in BSON (Binary JSON) format.
" No rows, no columns — just JSON structure." . MongoDB is schema-less

| Feature | MySQL (SQL) | MongoDB (NoSQL) |
| :--- | :--- | :--- |
| **Structure** | Table | Collection |
| **Record** | Row | Document |
| **Data Unit** | Column | Field |
| **Schema** | Fixed schema | Flexible schema |
| **Relationships** | JOINs common | Embedding preferred |
| **Data Design** | Normalization | Denormalization |

### DQL - display all, condition(and,or)

note:consider collection with 1000 data ,using find() wont display all !,insted it will split parts of data know as cursor.(i.e parts of whole data). we can use "find().toArray()" to get all

#### functions:
{
1

    .limit(n) -> used to limit the find()
2

    .skip(n) -> skips the 1st n nimbers from find()
3

    .sort({c name:1}) -> accending if 1
    .sort({c name:-1}) -> descending if -1
4

    
}

    db.collection.findOne() ->1st data if no condition applied 

    db.collection.find(
    {condition},
    {projection}
    )

    ex
    db.students.find(
    { age: { $gt: 18 } },   // condition
    { name: 1, age: 1, _id: 0 }   // projection
    )

1 display all data
 
    db.students.find()
2 display particular column(field) note- value 1=include,0=exclude. below will display name,age,address

    db.students.find({}, { name: 1, age: 1, _id: 0, address: 1 })
3 =,>,<

     db.students.find({ age: 21 })

     db.students.find({ age: { $gt: 18 } })

     db.students.find({ age: { $lt: 18 } })

Note: to access nested data we use string for condition ex:
{
  _id: 1,
  name: "Adhi",
  age: 21,
  address: {
    city: "Trichy",
    state: "Tamil Nadu",
    pincode: 620001
  }
}

    db.student.find({"address.city":"Trichy"})

4 and, or
and
    
    db.students.find({
    age: { $gt: 18 },
    department: "CSE"
    })
or

    db.students.find({
    $or: [
    { age: 18 },
    { age: 21 }
    ]
    })

    
### DDL - CREATE,SHOW,USE (here no use table,we can directly access) No ALTER Command
Because MongoDB allows:
JSON
{ name: "A" }
{ name: "B", age: 21 }
{ name: "C", city: "Chennai" }
Same collection, different fields. No problem.

    Show dbs -list the available dbs
  
    Use <db name> - create new db if not existing 
   
    Db - tells the current db
 
    Show collections - list the collections inside the db
 
    db.createCollection("users") - create collection inside db

    db.dropDatabase() - drop the db

    db.<collection name>.drop() - drop the collection 

    db.users.deleteMany({}) - act as truncate (here no auto resent value similar no sql. mdb is not sequence based it use Globally unique identifier system)


To create with condition 
  
    db.createCollection("students", {
    validator: {
    $jsonSchema: {
    bsonType: "object",
    required: ["name", "age"],
    properties: {
    name: { bsonType: "string" },
    age: { bsonType: "int" }}}}})
      
    
    
#### altering field 1) add field,2) remove field,3) modify,4) rename collection
1    

    db.students.updateMany(
    {},
    { $set: { age: 0 } }
    )
2

    db.students.updateMany(
    {},
    { $unset: { age: "" } }
    )
3 

    db.students.updateMany(
    {},
    [{ $set: { age: { $toString: "$age" } } }]
    )
Note: {} → no condition (select every document)

4

    db.<oldCollectionName>.renameCollection("<newCollectionName>")

### DML - Insert & InsertMany(_id is automatically generated, also we can custom),update,delete & deleteMany

Insert

    db.students.insertOne({
    name: "Adhi",
    age: 21,
    department: "CSE"
    })
    
InsertMany

    db.students.insertMany([
    { name: "Bala", age: 22 },
    { name: "Charan", age: 20 }
    ])

Delete 

     db.students.deleteOne({ name: "Adhi" })

DeleteMany (gt,gte,lt,lte,eq,ne)

    db.students.deleteMany({ age: { $gt: 20 } })

#### Update - 1)updateOne, 2)updateMany, 3) increment, 4)rename field update statement {which document},{what to change}

1 

    db.students.updateOne(
    { name: "Adhi" },          // condition (WHERE)
    { $set: { age: 22 } }      // new value (SET)
    )

2

    db.students.updateMany(
    { age: { $gt: 20 } },
    { $set: { status: "Senior" } }
    )

3

    db.students.updateOne(
    { name: "Adhi" },
    { $inc: { age: 1 } }
    )

4

    db.students.updateMany(
    {},
    { $rename: { "<old field>": "<new field>" } }
    )


# Operations 

1. comparison(gt,lt,gtq,ltq,eq,ne,in,between)


    db.students.find({
    age: { $gt: 18 },
    department: "CSE"
    })
    
    only 18,24,25
    db.students.find({
    age: {$in:[18,24,25]}},
    department: "CSE"
    })
    
    between 12-18
    db.students.find({
    age: {$gt:12,$lt:20},
    department: "CSE"
    })