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
and each row represents an entry. MongoDB is also schemaless which means 
that documents can have different keys in them. 

## Installation and setup
### mac installation 
--Installing with HomeBrew--   
The easiest way to install MongoDBon a Mac is with HomeBrew.  HomeBrew is 
a package mananger for macs. To download HomeBrew, go to [http://brew.sh/](http://brew.sh/).
Then from your terminal you will type the command `$ brew install mongodb`.     

--Installing from a tar file--  
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

--Running MongoDB--  
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
```bash
list of available commands
> help

prints the names of the databases on the database server which the console is connected
> show dbs

switches to db_name
> use db_name

prints list of collections in the selected database
> show collections

deletes collection
> db.collection_name.drop();

deletes database
> db.dropDatabase();
```

## CRUD operations
```bash
finds all items matching query
> db.collection_name.find(query)

finds one item that matches query
> db.collection_name.findOne(query)

adds a document to the collection_name collection
db.collection_name.insert(document)

saves a document in the collection_name collection--a shorthand for upsert(no _id) or insert(with _id)
> db.collection_name.save(document)

updates items that match query in the collection_name collection with data object values
> db.collection_name.update(query, {$set: data})

removes all items from collection_name that matches query criteria
> db.collection_name.remove(query)
```

## MongoDB and Node

## Hosting a MongoDB server in the cloud

## Additional Resources
[MongoDB download](https://www.mongodb.com/download-center#community)  
[Installation instructions for OS X](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)  
[MongoDB University](https://university.mongodb.com/)