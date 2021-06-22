# MongoDB

#### What is MongoDB?

- It is a document-oriented database program
- Unlike a SQL database, it doesn't use the SQL language to manage it's data.
- It is a non relational database.
- It does not use tables.
- It uses JavaScript to read/write and update data in a JSON way.
- The benefits also come with cons, as you can rapidly develop it also can be easily mismanaged if not properly understood. 
- https://docs.mongodb.com/manual/

A document modal looks like the bellow.

```json
{
    "_id" : "13434",
    "value1" : "sfsd"
    "value2" : "sfsd"
}
```

---

### Useful Commands

1. `help`
2. `show dbs`
3. `use recipes`
4. `show collections`
5. `db.createCollection('recipes')`
6. `db.help()`
7. `db.recipes.find({ ... })`
8. `db.collection.insertOne/insertMany({ ... })`

---

# Install and use

*on Mac*

Follow https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/ to install.

To start the service : `brew services start mongodb-community@4.4`

To stop the service : `brew services stop mongodb-community@4.4`



*on Windows*

Follow : https://www.youtube.com/watch?v=FwMwO8pXfq0&ab_channel=CodeJavaCodeJava

In command prompt

To start the services after following above  `mongod`

Then to open the client `mongo`

---

### How To

Once you first set up mongo you can view the shell by typing `mongo` in your terminal. 

Afterwards the initial command you may want to run is `help`. This will show you a list of all of the shell commands.

From here you can see some key commands such as `show dbs` which shows you the list of databases.

If you want to use or create a database you type `use ...` the ellipses is replaced with either a new db name or an existing db.

To then add an item to the collection you use `db.nameOfDb.insertOne({yourData: "goes here", or: "here"})`

To see all of the items saved in the collection we use `db.name.find()`

To search for an item you do so like `db.name.find({ title: /cake/ })` a regular expression to search the title. You can also search with a string if you know it all.

To delete all the items in the collection you use `db.name.deleteMany({})` 

To refine your deleting you can use `db.name.deleteMany({name: /cake/})`

---

# Use Mongo With NodeJS

First of all we need a driver to connect our MongoDB, this can be found here https://docs.mongodb.com/drivers/

 then `npm install mongodb` in the folder with your project. 

At the top of the project you need:

```js
const mongodb = require('mongodb');
const MongoClient = mongodb.MongoClient;
const url = 'mongodb://localhost:27017';
const dbName = 'recipes'	// or whatever your db name is
```

All of the above code will simply set up a local instance of using mongo db with the exact url needed. 

After the above you need to get into the code and add the below (This is using the recipes example)

```js
async function all() {								// convert to async function
    const client = new MongoClient(url); 			// connect to the mongo db client
    try{								// try because it is a promise 
		await client.connect();						// wait for the connection
		const db = client.db(dbName);				// get to the database
		const collection = db.collection('recipes') // get to the actual collection
		const results = await collection.find({})	// search all in the db collection
		return results.toArray();		// return the collection results as an array
    } finally{
		await client.close();			// just a catcher
    }
}
```

We can then do the exact same thing for the find. The id passed in is the string found in `_id` and it is an object ID so you have the parse it through `mongo.ObjectId()`

```js
async function find(id) {
    const client = new MongoClient(url)
    try {
        await client.connect();
        const db = client.db(dbName);
        const collection = db.collection('recipes');
        const results = await collection.find({ _id: mongodb.ObjectId(id) }); // only real change
		return results.toArray();
    } finally {
        await client.close();
    }
}
```

And the create:

```js
async function create(recipe) {
    const client = new MongoClient(url)
    try {
        await client.connect();
        const db = client.db(dbName);
        const collection = db.collection('recipes');
        const result = await collection.insertOne(recipe);
        return result
    } finally {
        await client.close();
    }
}
```

Finally update: 

```js
async function update=(id, attrs) {
    const client = new MongoClient(url)
    try {
        await client.connect();
        const db = client.db(dbName);
        const collection = db.collection('recipes');
        const filter = {_id: mongodbObjectId(id)}; // to clean the result
        const recipe = { $set: attrs } // we $set the value and attrs
        const result = await collection.findOneAndUpdate(filter, recipe);
        // above is a new command ot find and update one item
        return result
    } finally {
        await client.close();
    }
}
```



Although this works if we want to make it more dry we want to pull out some things to make it a function.

```js
let db, collection; // just to clean the codde

(async function() {
	const client = new MongoClient(url)
	await client.connect();
	db = client.db(dbName);
	collection = db.collection('recipes');    
})(); // immediately invoked function
// wrapping the function in round brackets automatically runs it when the file is run. The file is run once then close. This is why it will work well in this situation.

async function all() {															
	const results = await collection.find({})	
	return results.toArray();
}
```

