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

## Intro to Aggregation framework

another way to query data in MongoDB.

everything we know how to do using MQL can also be done using aggregation.

aggregation framework allows to analyze data in real time.

- create an aggregation pipeline that consists of one or more stages
- each stage transform the document and passes the output to the next stage
- output from one stage is passed as a input to the next stage
- can get results to end-users faster and save you from a lot of scripting.

### What are aggregations?

Aggregations basically groups the data from multiple documents and operates in many ways on those grouped data in order to return one combined result.

### What differenciate it from MQL

#### $group

an opeator that takes the incoming stream of data, and siphons it into multiple distinct reservoirs.

## Studio 3T

**Studio 3T** provides a GUI and IDE for accessing and modifying MongoDB databases and their documents.

## Update Operators

Enable us to modify data in the database.

example: `$inc`, `$set`, `$unset`

## Query Operators

Provide additional ways to locate data within the database.

### Comparisons

comparison operators specifically allow us to find data within a certain range.

if no comparison operators specified, `$eq` will be used by default.

### Logical

- `$and`
- `$or`
- `$nor` Fail to match both given clauses
- `$not` negate the query requirement

### expressive

allows the use of aggregation expressions within the query language.

allows us to use variables and conditional statements.

allows for more complex queries and for comparing fields within a document.

## MQL and aggregation syntax

```
// MQL
{ <field>: { <operator> : <value> } }
// Aggregation
{ <operator>: { <field> , <value> } }
```

## Array Operators

### $push

- allows us to add element to an array
- turns a field into an array if it was previously a different type.

### $all

return all elements that contains at least all elements that is specified in the array argument.

### $size

matches an array with the number of elements specified by the argument.

## Projection

- the second argument in `find()`.
- describing specifically which fields we're looking for.
- use 1 to field you want to include, and 0 to exclude
- if using 1s then youre going to get the field which you specified and an \_id field
- if using 0s, get all field except field with 0

## $elemMatch

- Matches documents that contain an array field with at least one element that matches the specified query criteria.
- Projects only the array elements with atleast one element that matches the specified criteria

## Index

In a database ― special data structure that stores a small portion of the collection's data set in an easy to traverse form.

imporve performance in our database.

## Data modeling

a way to organize fields in a document to support your application performance and querying capabilities.

## Upsert

- the third argument of update query.
- is set false by default.
- update will happen if theres a match, insert when no match.

## Aggregation framework

### Syntax

arguments:

1. array of stage
2. options

File Path: "$fieldName" ― used to access the value of a field in a document
System Variable: "$$UPPERCASE" ― System Level Variables. need to be uppercase
user Variable: "$$lowercase" ― user level variable. must be lowercase

### Structures and Syntax Rules

- Piplines are always an array of one or more stages
- Stages are composed of one or more aggregation operators or expressions
- Expressions may take a single or an array of arguments.

### $match

- filter documents that matched.
- should come early in a pipline
- uses standard MongoDB read operation query syntax as `find()`.
- cannot use `$where` operator
- if using `$text` operator, it must be on the first stage
- does not allow for projection

### $project

- Once we specified one field to retain, we must specify all fields we want to retain. (`_id` is the only exception)
- beyond removing and retaining field, it let us add new fields
- can be used as many times as required
- can be used to reassign values to existing field names and to derive entirely new fields.

### $addFields

- add fields to a document.
- only allows you to modify the incoming pipeline with new field or to modify existing fields.

### $geoNear

Output documents in order of nearest to farthest from a specific point.

- the collection can have only one 2dsphere index
- if using 2dsphere, the distance is returned in meters
- if using legacy coordinates, returned in radians
- $geoNear must be the first stage in an aggregation pipeline

### Cursor-like stages

similar to cursor method in MQL.

- sort
- skip
- limit
- counts

### allowDiskUse

- to allow handling larger data set
- because operation like `sort()` are limited to 100 megabytes of RAM by default, `allowDiskUse` will allow for more than 100mb

### $sample

will select a set of random documents in a collection, in one of two ways.

### $group

- `_id` is where to specify what incoming documents should be grouped on
- can use all accumulator expressions within $group
- $group can be used multiple times within a pipeline
- It may be necessary to sanitize incoming data

#### Accumulator expressions

- $sum, $avg, $max, $min, $stdDevPop, $stdDevSam
- Expressions have no memory between documents
- May still have to use $reduce or $map for more complex calculations

### $unwind

- Deconstruct an array field from the input documents to output a document for each element.
- only works on array values
- using Unwind on large collections with big documents may lead to performance issues.

### $lookup
