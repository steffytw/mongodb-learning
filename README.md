# MongoDB

* MongoDB is a cross-platform document-oriented database program. 
* Classified as a NoSQL database program, MongoDB uses JSON-like documents with optional schemas. 
* MongoDB is developed by MongoDB Inc. 
* MongoDB is great for transactional stores where performance is a concern. 
* Its also great when the data structure is going to evolve over time, as its schema-less operations allow you to update the data on the fly.


## BSON data format
*  The name "BSON" is based on the term JSON and stands for "Binary JSON".
*  BSON is a computer data interchange format.

![image](https://user-images.githubusercontent.com/33021781/125059785-53911f00-e0c9-11eb-9104-868bfc49b601.png)

* MongoDB supports many datatypes. Some of them are −

String − This is the most commonly used datatype to store the data. String in MongoDB must be UTF-8 valid.

Integer − This type is used to store a numerical value. Integer can be 32 bit or 64 bit depending upon your server.

Boolean − This type is used to store a boolean (true/ false) value.

Double − This type is used to store floating point values.

Min/ Max keys − This type is used to compare a value against the lowest and highest BSON elements.

Arrays − This type is used to store arrays or list or multiple values into one key.

Timestamp − ctimestamp. This can be handy for recording when a document has been modified or added.

Object − This datatype is used for embedded documents.

Null − This type is used to store a Null value.

Symbol − This datatype is used identically to a string; however, it's generally reserved for languages that use a specific symbol type.

Date − This datatype is used to store the current date or time in UNIX time format. You can specify your own date time by creating object of Date and passing day, month, year into it.

Object ID − This datatype is used to store the document’s ID.

Binary data − This datatype is used to store binary data.

Code − This datatype is used to store JavaScript code into the document.

Regular expression − This datatype is used to store regular expression.


## Relationship of RDBMS terminology with MongoDB

![image](https://user-images.githubusercontent.com/33021781/125072558-5f381200-e0d8-11eb-9bc7-f8bd719e66f3.png)


## Advantages of MongoDB over RDBMS

* Schema less
* No complex joins
* Ease of scale-out
* Structure of a single object is clear etc

## Why Use MongoDB?

* Document Oriented Storage − Data is stored in the form of JSON style documents.
* Index on any attribute
* Replication and high availability
* Rich queries
* Fast in-place updates etc

## Connection Setup
```
steffy@steffy:~/mongodb-linux-x86_64-ubuntu1804-4.4.0/bin$ mongo "mongodb+srv://cluster0.c2bvg.mongodb.net/<dbname>" --username steffy
MongoDB shell version v4.4.0
Enter password: 
connecting to: mongodb://cluster0-shard-00-02.c2bvg.mongodb.net:27017,cluster0-shard-00-01.c2bvg.mongodb.net:27017,cluster0-shard-00-00.c2bvg.mongodb.net:27017/%3Cdbname%3E?authSource=admin&compressors=disabled&gssapiServiceName=mongodb&replicaSet=atlas-ojbtmw-shard-0&ssl=true
Implicit session: session { "id" : UUID("cbaa33d1-5c84-4e43-8533-08a91615dc33") }
MongoDB server version: 4.2.8
WARNING: shell and server versions do not match
Error while trying to show server startup warnings: user is not allowed to do action [getLog] on [admin.]
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> 
```
## create database
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> use first-test
switched to db first-test
```
## show all the databases
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> show dbs
admin       0.000GB
first-test  0.000GB
local       3.781GB
```
## Drop database
This will delete the selected database
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.dropDatabase()
{ "dropped" : "mydb", "ok" : 1 }
```
## Create Colection
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.createCollection("tests")
{ "ok" : 1 }
```
## Drop Colection
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.tests.drop()
true
```
## insert one value to collections
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.insertOne({ name :"steffy",age :23})
{
	"acknowledged" : true,
	"insertedId" : ObjectId("5f421b5e684950ade1ce944f")
}
```

## show collections ie tables
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> show collections
users
```
## show values stored in collections
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
```
## insert multiple values to collections
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.insertMany({ name :"Thankam"},{name :"Wilson",age :51})
uncaught exception: TypeError: documents.map is not a function :
DBCollection.prototype.insertMany@src/mongo/shell/crud_api.js:307:17
@(shell):1:1
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.insertMany([{ name :"Thankam"},{name :"Wilson",age :51}])
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("5f421e2c684950ade1ce9450"),
		ObjectId("5f421e2c684950ade1ce9451")
	]
}
```
## show values stored in collections ie tables
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
{ "_id" : ObjectId("5f421e2c684950ade1ce9450"), "name" : "Thankam" }
{ "_id" : ObjectId("5f421e2c684950ade1ce9451"), "name" : "Wilson", "age" : 51 }
```
## add some other values
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.insertOne({ name :"Lisa",age :30})
{
	"acknowledged" : true,
	"insertedId" : ObjectId("5f4221ac684950ade1ce9452")
}
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.insertMany([{ name :"Manual",age:27},{name :"Harleen",age :25}])
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("5f4221d6684950ade1ce9453"),
		ObjectId("5f4221d6684950ade1ce9454")
	]
}
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
{ "_id" : ObjectId("5f421e2c684950ade1ce9450"), "name" : "Thankam" }
{ "_id" : ObjectId("5f421e2c684950ade1ce9451"), "name" : "Wilson", "age" : 51 }
{ "_id" : ObjectId("5f4221ac684950ade1ce9452"), "name" : "Lisa", "age" : 30 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9454"), "name" : "Harleen", "age" : 25 }
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find({age:27})
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }

```
## find document with age as 27
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find({age:27})
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }


```

## find document with age greater than 25
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find({age:{$gt :25}})
{ "_id" : ObjectId("5f421e2c684950ade1ce9451"), "name" : "Wilson", "age" : 51 }
{ "_id" : ObjectId("5f4221ac684950ade1ce9452"), "name" : "Lisa", "age" : 30 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }
```

## nested documents in collections
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.insertOne({ name :"Stewart",age :30,address:{street: "t1 indranagar",city:" kolkata"}})

{
	"acknowledged" : true,
	"insertedId" : ObjectId("5f422a2a684950ade1ce9455")
}




MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
{ "_id" : ObjectId("5f421e2c684950ade1ce9450"), "name" : "Thankam" }
{ "_id" : ObjectId("5f421e2c684950ade1ce9451"), "name" : "Wilson", "age" : 51 }
{ "_id" : ObjectId("5f4221ac684950ade1ce9452"), "name" : "Lisa", "age" : 30 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9454"), "name" : "Harleen", "age" : 25 }
{ "_id" : ObjectId("5f422a2a684950ade1ce9455"), "name" : "Stewart", "age" : 30, "address" : { "street" : "t1 indranagar", "city" : " kolkata" } }



```

## find address with street t1 indranagar
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find({"address.street":"t1 indranagar"})
{ "_id" : ObjectId("5f422a2a684950ade1ce9455"), "name" : "Stewart", "age" : 30, "address" : { "street" : "t1 indranagar", "city" : " kolkata" } }
```

## find address with street t1 indranagar, nothing is returned
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find({"address.street":"t1 indranagar"})
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY>
```

## updated age of Lisa ,set to 45
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.update({ name :"Lisa"},{$set:{age:56}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
{ "_id" : ObjectId("5f421e2c684950ade1ce9450"), "name" : "Thankam" }
{ "_id" : ObjectId("5f421e2c684950ade1ce9451"), "name" : "Wilson", "age" : 51 }
{ "_id" : ObjectId("5f4221ac684950ade1ce9452"), "name" : "Lisa", "age" : 45 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9454"), "name" : "Harleen", "age" : 25 }
{ "_id" : ObjectId("5f422a2a684950ade1ce9455"), "name" : "Stewart", "age" : 30, "address" : { "street" : "t1 indranagar", "city" : " kolkata" } }
```

## updated age of lisa without setting it to 56
The name is not there and the age is updated.Here the Id is same.
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.update({ name :"Lisa"},{age:56})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
{ "_id" : ObjectId("5f421e2c684950ade1ce9450"), "name" : "Thankam" }
{ "_id" : ObjectId("5f421e2c684950ade1ce9451"), "name" : "Wilson", "age" : 51 }
{ "_id" : ObjectId("5f4221ac684950ade1ce9452"), "age" : 56 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9454"), "name" : "Harleen", "age" : 25 }
{ "_id" : ObjectId("5f422a2a684950ade1ce9455"), "name" : "Stewart", "age" : 30, "address" : { "street" : "t1 indranagar", "city" : " kolkata" } }

```
## delete age of 56
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.deleteOne({age:56})
{ "acknowledged" : true, "deletedCount" : 1 }
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
{ "_id" : ObjectId("5f421e2c684950ade1ce9450"), "name" : "Thankam" }
{ "_id" : ObjectId("5f421e2c684950ade1ce9451"), "name" : "Wilson", "age" : 51 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9454"), "name" : "Harleen", "age" : 25 }
{ "_id" : ObjectId("5f422a2a684950ade1ce9455"), "name" : "Stewart", "age" : 30, "address" : { "street" : "t1 indranagar", "city" : " kolkata" } }
```


## delete name Thankam
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.deleteOne({ name :"Thankam"})
{ "acknowledged" : true, "deletedCount" : 1 }
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
{ "_id" : ObjectId("5f421e2c684950ade1ce9451"), "name" : "Wilson", "age" : 51 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9453"), "name" : "Manual", "age" : 27 }
{ "_id" : ObjectId("5f4221d6684950ade1ce9454"), "name" : "Harleen", "age" : 25 }
{ "_id" : ObjectId("5f422a2a684950ade1ce9455"), "name" : "Stewart", "age" : 30, "address" : { "street" : "t1 indranagar", "city" : " kolkata" } }

```
