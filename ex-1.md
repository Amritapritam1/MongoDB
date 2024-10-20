<!----MongoDB--->
**MongoDB is a document database and canbe installed locally or hosted in 
the cloud.//a database is an organized collection of structured information 
  or data typically stored in a computer system.
**It stores data in a type of JSON format called BSON.
**A record in MongoDB is a document, which is a data structure 
  composed of key value pairs similar to the structure of JSON objects.
<!----MongoDB Document---->
Records in a MongoDB database are called documents, and the field values 
may include numbers, strings, booleans, arrays, or even nested documents.

{
	title: "Post Title 1",
	body: "Body of post.",
	category: "News",
	likes: 1,
	tags: ["news", "events"],
	date: Date()
}
Example--
Find all documents that have a category of "news".
db.posts.find( {category: "News"} )

********************SQL VS Document databases*******************
SQL databases are considered relational databases. They store related data
in separate tables. When data is needed, it is queried from multiple tables 
to join the data back together.


****MongoDB is a document database which is often referred to as a non-relational
database. This does not mean that relational data cannot be stored in 
document databases. It means that relational data is stored differently.
A better way to refer to it is as a non-tabular database.
****MongoDB stores data in flexible documents. Instead of having multiple 
tables you can simply keep all
of your related data together. This makes reading your data very fast.
*********You can still have multiple groups of data too. In MongoDB, instead of 
tables these are called collections.
******************Local vs Cloud database*************
MongoDB can be installed locally, which will allow you to host your own 
MongoDB server on your hardware. This 
requires you to manage your server, upgrades, and any other maintenance.

***********************Creating a cluster**************
************************Query ApI*********************
The MongoDB Query API is the way you will interact with your data.
The MongoDB Query API can be used two ways:

1.CRUD Operations
2.Aggregation Pipelines


***************MongoDB Query API Uses
#### You can use the MongoDB Query API to perform:

# Adhoc queries with mongosh, Compass, VS Code, or a MongoDB driver for the programming language you use.
# Data transformations using aggregation pipelines.
# Document join support to combine data from different collections.
# Graph and geospatial queries.
# Full-text search.
# Indexing to improve MongoDB query performance.
# Time series analysis.

*******************MongoDB Create DB***************


***************MongoDB mongosh Creation***********
Create Collection using mongosh
There are 2 ways to create a collection.

***Method 1
You can create a collection using the createCollection() database method.

Example
db.createCollection("posts")
***Method 2
You can also create a collection during the insert process.

Example
We are here assuming object is a valid JavaScript object containing post data:

db.posts.insertOne(object)

*************************MongoDB Insert*************
Insert Documents
There are 2 methods to insert documents into a MongoDB database.

*****insertOne()
To insert a single document, use the insertOne() method.

This method inserts a single object into the database.

db.posts.insertOne({
  title: "Post Title 1",
  body: "Body of post.",
  category: "News",
  likes: 1,
  tags: ["news", "events"],
  date: Date()
})
***********insertMany()
To insert multiple documents at once, use the insertMany() method.

This method inserts an array of objects into the database.

Example
db.posts.insertMany([  
  {
    title: "Post Title 2",
    body: "Body of post.",
    category: "Event",
    likes: 2,
    tags: ["news", "events"],
    date: Date()
  },
  {
    title: "Post Title 3",
    body: "Body of post.",
    category: "Technology",
    likes: 3,
    tags: ["news", "events"],
    date: Date()
  },
  {
    title: "Post Title 4",
    body: "Body of post.",
    category: "Event",
    likes: 4,
    tags: ["news", "events"],
    date: Date()
  }
])
*********************MongoDb Find()****************
Find Data
There are 2 methods to find and select data from a MongoDB collection, find() and findOne().

find()
To select data from a collection in MongoDB, we can use the find() method.

This method accepts a query object. If left empty, all documents will be returned.

Example
db.posts.find()
findOne()
To select only one document, we can use the findOne() method.

This method accepts a query object. If left empty, it will return the first document it finds.

Note: This method only returns the first match it finds.

Example
db.posts.findOne()
**********************Querying Data*************
To query, or filter, data we can include a query in our find() or findOne() methods.

Example
db.posts.find( {category: "News"} )
*******************Projection*************
Both find methods accept a second parameter called projection.

This parameter is an object that describes which fields to include in the results.

Note: This parameter is optional. If omitted, all fields will be included in the results.

Example
This example will only display the title and date fields in the results.

db.posts.find({}, {title: 1, date: 1})
Notice that the _id field is also included. This field is always included unless specifically excluded.

We use a 1 to include a field and 0 to exclude a field.

Example
This time, let's exclude the _id field.

db.posts.find({}, {_id: 0, title: 1, date: 1})
Note: You cannot use both 0 and 1 in the same object. The only exception is the _id field. You should either specify the fields you would like to include or the fields you would like to exclude.

Let's exclude the date category field. All other fields will be included in the results.

Example
db.posts.find({}, {category: 0})
We will get an error if we try to specify both 0 and 1 in the same object.

Example
db.posts.find({}, {title: 1, date: 0})
************************MongoDB Update****************
# Update Document
To update an existing document we can use the updateOne() or updateMany() methods.

The first parameter is a query object to define which document or documents should be updated.

The second parameter is an object defining the updated data.

# updateOne()
The updateOne() method will update the first document that is found matching the provided query.

Let's see what the "like" count for the post with the title of "Post Title 1":

Example
db.posts.find( { title: "Post Title 1" } ) 
Now let's update the "likes" on this post to 2. To do this, we need to use the $set operator.

Example
db.posts.updateOne( { title: "Post Title 1" }, { $set: { likes: 2 } } ) 
Check the document again and you'll see that the "like" have been updated.

Example
db.posts.find( { title: "Post Title 1" } ) 
#### Insert if not found
If you would like to insert the document if it is not found, you can use the upsert option.

Example
Update the document, but if not found insert it:

db.posts.updateOne( 
  { title: "Post Title 5" }, 
  {
    $set: 
      {
        title: "Post Title 5",
        body: "Body of post.",
        category: "Event",
        likes: 5,
        tags: ["news", "events"],
        date: Date()
      }
  }, 
  { upsert: true }
)
****updateMany()
The updateMany() method will update all documents that match the provided query.

Example
Update likes on all documents by 1. For this we will use the $inc (increment) operator:

db.posts.updateMany({}, { $inc: { likes: 1 } })
*************************MongoDb delete************
*** Delete Documents
We can delete documents by using the methods deleteOne() or deleteMany().

These methods accept a query object. The matching documents will be deleted.

**** deleteOne()
The deleteOne() method will delete the first document that matches the query provided.

Example
db.posts.deleteOne({ title: "Post Title 5" })
**** deleteMany()
The deleteMany() method will delete all documents that match the query provided.

Example
db.posts.deleteMany({ category: "Technology" })
*********************MongoDB Query Operators***************
MongoDB Query Operators
There are many query operators that can be used to compare and reference document fields.

Comparison
The following operators can be used in queries to compare values:

$eq: Values are equal
$ne: Values are not equal
$gt: Value is greater than another value
$gte: Value is greater than or equal to another value
$lt: Value is less than another value
$lte: Value is less than or equal to another value
$in: Value is matched within an array
Logical
The following operators can logically compare multiple queries.

$and: Returns documents where both queries match
$or: Returns documents where either query matches
$nor: Returns documents where both queries fail to match
$not: Returns documents where the query does not match
Evaluation
The following operators assist in evaluating documents.

$regex: Allows the use of regular expressions when evaluating field values
$text: Performs a text search
$where: Uses a JavaScript expression to match documents
*******************MongoDB update Operators ************
There are many update operators that can be used during document updates.

Fields
The following operators can be used to update fields:

$currentDate: Sets the field value to the current date
$inc: Increments the field value
$rename: Renames the field
$set: Sets the value of a field
$unset: Removes the field from the document
Array
The following operators assist with updating arrays.

$addToSet: Adds distinct elements to an array
$pop: Removes the first or last element of an array
$pull: Removes all elements from an array that match the query
$push: Adds an element to an array
****************MongoDB Aggregations***********
Aggregation operations allow you to group, sort, perform calculations, analyze data, and much more.

Aggregation pipelines can have one or more "stages". The order of these 
stages are important. 
Each stage acts upon the results of the previous stage.
db.posts.aggregate([
  // Stage 1: Only find documents that have more than 1 like
  {
    $match: { likes: { $gt: 1 } }
  },
  // Stage 2: Group documents by category and sum each categories likes
  {
    $group: { _id: "$category", totalLikes: { $sum: "$likes" } }
  }
])
# $group
# $limit
# $project
# $sort
# $match
# $addfields
# $count
# $lookup
# $out
****************************MongoDBindexing/search**********
Indexing & Search
MongoDB Atlas comes with a full-text search engine that can be used to search for documents in a collection.
To use our search index, we will use the $search operator in our aggregation pipeline.

Example
db.movies.aggregate([
  {
    $search: {
      index: "default", // optional unless you named your index something other than "default"
      text: {
        query: "star wars",
        path: "title"
      },
    },
  },
  {
    $project: {
      title: 1,
      year: 1,
    }
  }
])
************************MongoDB validation************
Schema Validation
By default MongoDB has a flexible schema. This means that there is no strict schema validation set up initially.

Schema validation rules can be created in order to ensure that all documents in a collection share a similar structure.

Schema Validation
MongoDB supports JSON Schema validation. The $jsonSchema operator allows us to define our document structure.

Example
db.createCollection("posts", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: [ "title", "body" ],
      properties: {
        title: {
          bsonType: "string",
          description: "Title of post - Required."
        },
        body: {
          bsonType: "string",
          description: "Body of post - Required."
        },
        category: {
          bsonType: "string",
          description: "Category of post - Optional."
        },
        likes: {
          bsonType: "int",
          description: "Post like count. Must be an integer - Optional."
        },
        tags: {
          bsonType: ["string"],
          description: "Must be an array of strings - Optional."
        },
        date: {
          bsonType: "date",
          description: "Must be a date - Optional."
        }
      }
    }
  }
})
This will create the posts collection in the current database 
and specify the JSON Schema validation requirements for the collection.



