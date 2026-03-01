# MongoDB
A document-based NoSQL database. It stores data in BSON (Binary JSON) format.
" No rows, no columns — just JSON structure." 

| Feature | MySQL (SQL) | MongoDB (NoSQL) |
| :--- | :--- | :--- |
| **Structure** | Table | Collection |
| **Record** | Row | Document |
| **Data Unit** | Column | Field |
| **Schema** | Fixed schema | Flexible schema |
| **Relationships** | JOINs common | Embedding preferred |
| **Data Design** | Normalization | Denormalization |

### DDL - CREATE,SHOW,USE (here no use table,we can directly access)

    Show dbs -list the available dbs
  
    Use <db name> - create new db if not existing 
   
    Db - tells the current db
 
    Show collections - list the collections inside the db
 
    db.createCollection("users") - create collection inside db

    db.dropDatabase() - drop the db

    db.<collection name>.drop() - drop the collection 

    db.users.deleteMany({}) - act as truncate (here no auto resent value similar no sql. mdb is not sequence based it use Globally unique identifier system)
