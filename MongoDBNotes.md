**MongoDB**

* A database is a structered way to store data and access data
NoSQL database not use always related tables of data Ex:- lbrary cards 
Data in mongoDB is stored as a documents stored in the form of collection of documents mongodb is NoSQL document database.
* Document - a way to organize and store data as a set of field-value pairs.

* A document schema is a JSON object that allows you to define the shape and content of documents and embedded documents in a collection. ... Document schemas follow the same JSON schema specification as document validation in the MongoDB server.
* Field - a unique identifier for a datapoint.

* Value - data related to a given identifier.

* Collection - an organized store of documents in MongoDB, usually with common fields between documents. There can be many collections per database and many documents per collection.

* Replica Set - a few connected machines that store the same data to ensure that if something happens to one of the machines the data will remain intact. Comes from the word replicate - to copy something.

* Instance - a single machine locally or in the cloud, running a certain software, in our case it is the MongoDB database.

* Cluster - group of servers that store your data.
* schema -A document schema is a JSON object that allows you to define the shape and content of documents and embedded documents in a collection. ... Document schemas follow the same JSON schema specification as document validation in the MongoDB server.

**JSON**
JavaScript standard object notation 
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/03airaq82dewlmx7ovdt.png)

**BSON**
binary JSON
optimized for speed flexibility space high performance
* Data in MongoDB stored in BSON format both internally and over the network.
* In mongoDB data is stored in BSON but viewed in JSON because it is more human reable than binary BSON format.

**Export JSON**
* mongoimport
* mongoexport

**Export JSON**
* mongorestore
* mongodump

**URI string**
* uniform resource identifier 
* srv establishes the secure collection

**Namespace - The concatenation of the database name and collection name is called a namespace.**

* We looked at the sample_training.zips collection and issued the following queries:
In collectons filters this things done in mongodb atlas 
   Ex * {"state": "NY"}
      * {"state": "NY", "city": "ALBANY"}

**In local system using mongodb community edition server**
* For connecting `mongo "mongodb+srv://sandbox-jbc3i.mongodb.net/test" --username m001-student`

show dbs (for showing/getting databases in cmd/shell)

use sample_training

show collections

db.zips.find({"state": "NY"})
db.zips.find({"state": "NY"}).count()

db.zips.find({"state": "NY", "city": "ALBANY"})

db.zips.find({"state": "NY", "city": "ALBANY"}).pretty()
**Practice excercise command**
* db.inspections.find().count()

**get a random document from the collection:**

* db.inspections.findOne();

**Insert random document Query**
```js 
db.inspections.insert({
...         "_id" : ObjectId("56d61033a378eccde8a8357b"),
...         "id" : "11201-2015-ENFO",
...         "certificate_number" : 9278356,
...         "business_name" : "TEN KESEF II, INC.",
...         "date" : "Feb  3 2015",
...         "result" : "No Violation Issued",
...         "sector" : "Misc Non-Food Retail - 817",
...         "address" : {
...                 "city" : "BROOKLYN",
...                 "zip" : 11234,
...                 "street" : "FLATBUSH AVE",
...                 "number" : 5352
...         }
... })
```

**Find Document with pretty()**
* db.inspections.find({"id" : "10021-2015-ENFO", "certificate_number" : 9278806}).pretty()

**Inserting new documents**
* db.inspections.insert([ { "test": 1 }, { "test": 2 }, { "test": 3 } ]) array of documents.

**If i missspelled database name in insert query in mongodb then i will not get error infact new that missspelled name database created in collections**

**MQL -mongo query lanagauge**
* updateOne() or updateMany()
* findOne() or find() 
* finding the all documents in the zips collection where the city field is equal to "HUDSON".
* db.zips.find({ "city": "HUDSON" }).pretty()
* $inc MQL insert operator db.zips.updateMany({ "city": "HUDSON" }, { "$inc": { "pop": 10 } })
* db.zips.updateOne({ "zip": "12534" }, { "$set": { "pop": 17630 } }) set used set update specified value 
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/wg7ioqn2do2r5r7o42h9.png)
* $push 
``` js
db.grades.updateOne({ "student_id": 250, "class_id": 339 },
                    { "$push": { "scores": { "type": "extra credit",
                                             "score": 100 }
                                }
                     })
                     
 ```
                 
  ![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/s3nx7ygeyxmtwzyw2ub4.png)
   
**Deleting documents in mongoDB**
* db.inspections.deleteMany({ "test": 1 }) /(test 1 is the id )
* when we delete all collections in mongodb database When the database is empty it no longer exists.
* deleting database collections using db.inspection.drop()
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/c9moft0tpntsb5ruuad7.png)

**Comparison operators in mongodb**
* $eq =Equal to  || $neq=not equal to
* $gt greater than || $lt=less than 
* $get greater than equal to || $lte = less than equal to
* {"tripduration":{"$lte":70},"usertype":{"$ne":"Subscriber"}}
* mongo shell query db.trips.find({ "tripduration": { "$lte" : 70 },
                "usertype": { "$ne": "Subscriber" } }).pretty()
* db.zips.find({ "pop": { "$lt": 1000 }}).count()
**Logical Operators**
* $and match all of the specified query clauses
* $or atleast one of the query clause is matched 
* $nor fail to match both query clauses 
* $not negates the query requirement
* nor operation {$nor:[{result:"No Violation Issued"},{result:"Violation Issued"},{result:"Pass"},{result:"fail"}]}
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/a5skkbhhvee7sklqxzx8.png)
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/61rhyh9vbpz8vlo2grnv.png)                

* db.routes.find({ "$and": [ { "$or" :[ { "dst_airport": "KZN" }, { "src_airport": "KZN" }] },{ "$or" :[ { "airplane": "CR2" },{ "airplane": "A81" } ] }]}).count()
* db.inspections.find({ result:"Out of Business","sector":"Home Improvement Contractor - 100" }).count() quiz chapter4                                     
* my wrong answer query db.companies.find({ "$and": [ { "$or": [ { "founded_year": 2004 }, { "founded_month": 10 } ] },{ "$or": [ { "category_code": "web" },{ "category_code": "social" }]}]}).count()
* $expr it allows to use aggregation of expressions within the query langauge expression allows varibles and conditionals 
* {"$expr":{"$eq":["$start station id","$end station id"]}}
* $ denotes the use of operator ||$ addresses the particular field
* db.trips.find({"$expr":{"$eq":["$end station id","$start station id"]}}).count()
* db.companies.find({"$expr":{"$eq":["$permalink","$twitter_username"]}}).count() //quiz question answer
* $size operator for matching size or finding particular element of that size exact size 
* $all return all documents in which specified array field contains regardless of there order.
* db.listingsAndReviews.find({ "reviews": { "$size":50 },"accommodates": { "$gt":6 }})
* db.listingsAndReviews.find({"property_type":"House","amenities":"Changing table"}).count() 
* db.grades.find({ "class_id": 431 },{ "scores": { "$elemMatch": { "score": { "$gt": 85 } } } }).pretty()  //macthing specific element in array
* db.grades.find({ "scores": { "$elemMatch": { "type": "extra credit" } } }).pretty()
* db.companies.find({ "offices": { "$elemMatch": { "city": "Seattle" } }}).count()
* db.trips.findOne({ "start station location.type": "Point" }) //we can use dot to deep dive into the documents collection.
* db.companies.find({ "relationships.0.person.first_name": "Mark", "relationships.0.title": { "$regex": "CEO" } }, { "name": 1 }).count()
* db.trips.find({ "start station location.coordinates": { "$lt": -74 }}).count()
* db.inspections.find({ "address.city": "NEW YORK" }).count() final chapter 4 quiz answer      
* db.listingsAndReviews.aggregate([ { "$project": { "address": 1, "_id": 0 }}, { "$group": { "_id": "$address.country" }}]) aggreation frameworks in specific order 
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/74ll21di7vlprdisn3ou.png)
* db.listingsAndReviews.aggregate([{ "$project": { "address": 1, "_id": 0 }},{ "$group": { "_id": "$address.country","count": { "$sum": 1 } } } ])
* db.listingsAndReviews.aggregate([{ "$project": { "room_type": 1, "_id": 0 }},{ "$group": { "_id": "$room_type" } } ])   
* sort in mongodb db.zips.find().sort({"pop":1}).limit(1).pretty()                                                                
* db.zips.find().sort({ "pop": -1 }).limit(1)
* db.zips.find().sort({ "pop": -1 }).limit(10).pretty() //top 10 zip codes by population 
* db.zips.find().sort({ "pop": 1, "city": -1 })
* db.trips.find({ "birth year": { "$ne":"" } },{ "birth year": 1 }).sort({ "birth year": -1 }).limit(1)
* db.trips.createIndex({ "birth year": 1 }) // indexing is for accessing faster faster the data 
* db.trips.createIndex({ "start station id": 476, "birth year": 1 })
* Data modeling - a way to organize fields in a document to support your application performance and querying capabilities.


              
                                  
                                                
                               
                                 
                   
                 
              
            
                                   
                                  
                          
                                     
         
