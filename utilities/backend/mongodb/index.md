# MongoDB

- [MongoDB](#mongodb)
  - [Database Control](#database-control)
  - [Collection Control](#collection-control)
  - [Docuemnt Control](#docuemnt-control)
  - [Update document](#update-document)
  - [delete document](#delete-document)
  - [Aggregation](#aggregation)

## Database Control

```shell
# Switch to my_db
use my_db

# Show all databses
show databases

# Drop database
db.dropDatabase()
```

## Collection Control

```javascript
// Get collection names
db.getCollectionNames()

// Drop a collection
db.users.drop()
```

## Docuemnt Control

```javascript
// Insert a document
db.users.insertOne({name: "foo"})

// Insert many documents
db.users.insertMany([
    {name: "foo"},
    {name: "bar"}
])

// Find all document
db.users.find()
// Find one document
db.users.findOne()
// or
db.users.find().limit(1)

// Sort asc by level
db.users.find().sort({level: 1})
// Sort desc by level
db.users.find().sort({level: -1})

// Skip the first 1 record
db.users.find().skip(1)

// Query users who meet certain criteria
// User with name 'foo'
db.users.find({name: "foo"})
// Regex search, and ignore case
db.users.find({name: {$regex: /\w{0,2}/, $options: 'i'}})
// Get adult user
db.users.find({age: {$gt: 18}})
// Get chinese-speaking user
db.users.find({country: {$in: ['china', 'taiwan']}})
// Get non-korean user
db.users.find({country: {$nin: ['korea']}})
// or
db.users.find({country: {$not: {$in: ['korea']}}})
// Get user with email field
// All users with the "email" field will be retrieved, even if that field is null.
db.users.find({email: {$exists: true}})

// Return only wanted field
db.users.find({name: "foo"}, {_id: 0, name: 1})

// or logic
// Retrive young or old people
db.users.find({$or: [{age: {$gte: 70}}, {age: {$lte: 10}}]})
```

## Update document

```javascript
// Update one record
db.users.updateOne({name: "foo"}, {$set: {name: "bar"}})
// Update many records
db.users.updateMany({name: "foo"}, {$set: {name: "bar"}})
```

## delete document

```javascript
// Delete one document
db.users.deleteOne({name: "foo"})
// Delete many documents
db.users.deleteMany({name: "foo"})
```

## Aggregation

```javascript
db.users.countDocuments()
```
