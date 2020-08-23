# mongodb-tutorial
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
## show database
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> show dbs
admin  0.000GB
local  3.769GB
```
## create database
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> use first-test
switched to db first-test
```
## insert one values to database
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.insertOne({ name :"steffy",age :23})
{
	"acknowledged" : true,
	"insertedId" : ObjectId("5f421b5e684950ade1ce944f")
}
```
## show all the database
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> show dbs
admin       0.000GB
first-test  0.000GB
local       3.781GB
```
## show collections ie tables
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> show collections
users
```
## show values stored in collections ie tables
```
MongoDB Enterprise atlas-ojbtmw-shard-0:PRIMARY> db.users.find()
{ "_id" : ObjectId("5f421b5e684950ade1ce944f"), "name" : "steffy", "age" : 23 }
```
## insert multiple values to database
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
