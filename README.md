# MongoDB

MongoDB is a non-relational database also known as a NoSQL database. 
One of the differences between a MongoDB database and a relational
database is that MongoDB stores data in a JSON document as opposed 
to a table. JSON stands for JavaScript object notation and it uses 
key-value pairs to organize data.  This is an example of JSON document:
```javascript
{
	"firstName": "Alberta",
	"lastName": "Williams"
}
```
Here, firstName is a key and Alberta is a value.  A table in a relational
database is organized into columns and rows. Where each column has a key
and each row represents a document. MongoDB is also schemaless which means 
that documents can have different keys in them. 

## Installation and setup
### mac installation 
__Installing with HomeBrew__   
The easiest way to install MongoDBon a Mac is with HomeBrew.  HomeBrew is 
a package mananger for macs. To download HomeBrew, go to [http://brew.sh/](http://brew.sh/).
Then from your terminal you will type the command `$ brew install mongodb`.     

__Installing from a tar file__  
Download MongoDB at [https://www.mongodb.com/download-center#community](https://www.mongodb.com/download-center#community).
From your terminal, navigate to the directory the file was saved to.  If
it was saved to your downloads directory you would type `$ cd ~/Downloads/`.
Then unpack the file by typing the command `$ tar zxvf filname` and replace
filename with the name of the downloaded mongodb file. I recommend moving 
MongoDB to the folder `/usr/local/mongodb`. Next, navigate into
the directory that was created.  

In order to access the MongoDB commands from anywhere on your system, you 
will need to add the mongodb path to the $PATH variable. You can change your
$PATH variable inside your .bash_profile file. This file contains your
enviroment variables.  Open the file from your terminal by typing the command
`$ vi ~/.bash_profile`. You will add mongodb to your $PATH variable like so:
`export PATH=/usr/local/mongodb/bin:$PATH`.  

__Running MongoDB__  
One of the commands you will use is `mongod` which will start your MongodB
server. You will also need to create the directory where the MongoDB server will store its data. By default it is /data/db. To do that from your terminal enter the following commands:  

```bash
$ sudo mkdir -p /data/db
$ sudo chmod 755 /data
$ sudo chmod 755 /data/db
```

The first command creates the directory and the second command gives the account read, write and execute permissions for the directory. To start the
server type the command `mongod`.  A MongoDB server consists of multiple
databases. Each database contains multiple collections.  A collection is 
the equivalent of a table for a relational database. Each collection
contains multiple documents.  A document is the equivalent of a row in a table.


## Using the mongo shell 
The mongo shell is a program that lets us connect to your database from the
terminal. After you have started MongoDB you can start the shell by 
opening another terminal window and type the `mongo' command. Some useful
commands are:  

list of available commands
```bash
> help
```
prints the names of the databases on the database server which the console is connected
```bash
> show dbs
```

`use <database>` switches to <database> or creates the database if it doesn't exist. Example: create a database with the name test.
```bash
> use test
```

### Creating documents

`db.collection_name.insert(document)`  
Adds a document to the collection_name collection. Creates a collection if 
it doesn't exist. Example: create a collection named users in the test database and insert a document.
```bash
> db.users.insert({firstName: "Alberta", lastName: "Williams"})
```
TASK add insert another document with a firstName and lastName property.    

Prints list of collections in the selected database.
```bash
> show collections
```

### Reading documents

`db.collection_name.find()`  
Returns all documents in the collection <collection_name>.  Alternatively,
you can use `db.collection_name.find({}). Example:
Get all of the documents from the users collection.
```bash
> db.users.find()  
```

`db.collection_name.find(filter)`  
Returns all documents in the collection <collection_name> matching the filter.
The filter is an object that has the form `{field: value}`. 
Example: find the document with the first name "Alberta".
```bash
> db.users.find({first: "Alberta"})
```
TASK: find a document with a different first name.  

`db.collection_name.find({field1: value, field2: value})`  
Returns documents from the collection <collection_name> based on more than one field


`db.collection_name.find(filter, projection)`  
Returns the documents from the collection <collection_name> where filter is
the criteria for the doucments to return and projection in an object that 
specifies the fields to return from the document.  Example: find the document with the first name "Alberta" and only show the first name field.
```bash
> db.users.find({first: "Alberta"}, {first: 1, _id:0})
```

The value `1` means the field will be included and a value of `0` means the 
field will be excluded. By default, the `_id` field will be shown.
TASK: 

### Updating documents

`db.collection_name.update(query, update, options)`  
Updates or replaces a document that matches the query. Where update 
is a document with the fields to update. Options is an optional document 
that can include the following fields: `upsert: <boolean>` which will create
a new document if no matching document is found; `multi: <boolean>` which will
update all documents that match the query; `writeConcern: <document>`. Example:
Replace the document with the first name "Alberta" with the document 
{first: "Artificial", last: "Al"}.
```bash
> db.users.update({first: "Alberta"}, {first: "Artificial", last: "Al"})
```
TASK  

`db.collection_name.update(query, {<operator>: {field: value}})`  
Performs the modifies the fields of the docoument matching the query
according to the `<operator>`.  Operators will begin with a `$` symbol.
Example: set the last name field of the document with the name "Articical" 
to "Alien".
```bash
> db.users.update({first: "Artificial"}, {$set: {last: "Alien"}})
```

`db.collection_name.update(query, {$unset: {field: 1}})`  
Removes a field. Example: remove the last name field for the document
that has a first name of "Artificial".
```bash
db.users.update({first: "Artificial"}, {$unset: {last: 1}})
```
TASK: remove the last name field for the user that has thefirst name "Arthur".   

`db.collection_name.update({}, {$set: {field: value}}, {multi: true})`  
Updates all of the documents with the specified field  
TASK: Update all users with the field "admin" and give it the value true.

### Deleting documents

`db.collection_name.remove(query)`  
Deletes a single document that matches that matches query.  
TASK: Remove the user with the first name "Artificial"

`db.collection_name.remove({})`  
Removes all documents 1 by 1.  

`db.collection_name.drop()`  
Deletes the collection with the name collection_name. Example: delete the users
collection in the test database. 
```bash
> db.users.drop();
```

deletes database
```bash
> db.dropDatabase();
```
TASK Delete the test database that you created

## Exercises
TODO

## Additional Resources
[MongoDB download](https://www.mongodb.com/download-center#community)  
[Installation instructions for OS X](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)  
[MongoDB University](https://university.mongodb.com/)