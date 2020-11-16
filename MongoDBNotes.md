**MongoDB**

* A database is a structered way to store data and access data
NoSQL database not use always related tables of data Ex:- lbrary cards 
Data in mongoDB is stored as a documents stored in the form of collection of documents mongodb is NoSQL document database.
* Document - a way to organize and store data as a set of field-value pairs.

* Field - a unique identifier for a datapoint.

* Value - data related to a given identifier.

* Collection - an organized store of documents in MongoDB, usually with common fields between documents. There can be many collections per database and many documents per collection.

* Replica Set - a few connected machines that store the same data to ensure that if something happens to one of the machines the data will remain intact. Comes from the word replicate - to copy something.

* Instance - a single machine locally or in the cloud, running a certain software, in our case it is the MongoDB database.

* Cluster - group of servers that store your data.

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
show dbs

use sample_training

show collections

db.zips.find({"state": "NY"})
db.zips.find({"state": "NY"}).count()

db.zips.find({"state": "NY", "city": "ALBANY"})

db.zips.find({"state": "NY", "city": "ALBANY"}).pretty()
