# MongoDb

**MongoDB** is a document database, which is a type of NoSQL database that stores data as individual documents.

provides the flexibility necessary to accomodate varying and evolving data structures.

NoSql means you're storing your data in an organized way but not in rows and columns.

is open-source which available as cloud-based service or as an on-premises software.

**MongoDB Atlas** is an example of the cloud based services.

on-premises comes in 2 editions:

- MongoDB Community Server
- MongoDB Enterprise Server

## How MongoDB stores data

- stores data in BSON(Binary representation of JSON) document.
- `document` is like javaScript Object
- stores groups of document on collections
- collection is like table in sql

## Document

A way to organize and store data as a set of field-value pairs

## Collection

An organized store of documents in MongoDB, usually with common field between documents.

## Atlas

### Clusters

a group of servers that stores your data.

### Replica Set

- a few connected MongoDB instances that store the same data.
- this setup will make sure that the is still available when one of the instances is unavailable

### Instance

a single machine locally or in cloud running a certain software

## Import and Export

for manual backup.

### in JSON

- mongoimport

- mongoexport

### in BSON

- mongorestore
- mongodump

## find()

**cursor** is a pointer to result set of a query

**pointer** is a direct address of the memory location

directives :

- pretty()
- count()

### ObjectId

a 12-byte hexadecimal value which consists of:

- 4-byte(representing seconds since the Unix epoch)
- 5-byte(random value)
- 3-byte(counter, starting with a random value)

the above makeup is only applied from version 3.4 on MongoDB.

#### Odd of Uniqueness

the randomness of the last eight bytes in the current implementation makes the likelihood of the same ObjectId being created pretty small.

## Aggregation framework

aggregation framework allows to analyze data in real time.

- create an aggregation pipeline that consists of one or more stages
- each stage transform the document and passes the output to the next stage
- output from one stage is passed as a input to the next stage
- can get results to end-users faster and save you from a lot of scripting.

### What are aggregations?

Aggregations basically groups the data from multiple documents and operates in many ways on those grouped data in order to return one combined result.

## Studio 3T

**Studio 3T** provides a GUI and IDE for accessing and modifying MongoDB databases and their documents.
