# Mongoose

The mongo db driver is production-quality but very low level for application use.

Mongoose is a javascript library that wraps around the MongoDB driver library and gives additional features such as Schemas and Models.

Mongoose helps by making a model of your data in MongoDB - when you place actions on the model, it will mirror the database.

Mongoose brings ActiveRecord-like abstractions to Node.js

## Key Links

https://mongoosejs.com/docs/index.html

https://mongoosejs.com/docs/queries.html

https://mongoosejs.com/docs/validation.html

https://mongoosejs.com/docs/populate.html

## Creating a model

Provides schema definitions for a schema-less document database

A model represents a MongoDB collection

Used for CRUD operations to add/remove/update documents in MongoDB. What is done to the model, will determine what mongoose will do with the corresponding collection.

*Schema*

```js
const recipeSchema = new Schema({
    title: String,
    created_at: { type: Date, default: Date.now }
})
```

From this schema we then create a model from it

Then we Export the model to be used to create instances

*Model*

```js
const Recipe = mongoose.model('Recipe', recipeSchema);
module.exports = Recipe;
```

---

# Step by Step

First thing we want to do in the root director is create a directory called `models`

Then we need to install mongoose `npm install mongoose`

In the models directory we want to create a `db.js` for connectivity `touch models/db.js`

We also want to create the model for our data (singular) `touch models/recipe.js`

Then we can go into the db.js and do the below

```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;	// create Schema

mongoose.connect('mongodb://localhost/recipes', {useUnifiedTopology: true, useNewUrlParser: true}) // connect to mongodb with specified

module.exports = { mongoose, Schema };
```

After we create this we can then jump into our data model. 

```js
const { Schema, mongoose } = require('./db');
// import {Schema, mongoose} from './db'

// first we create the Schema which the model will use
const RecipeSchema = Schema({
	title: { type: String, require: true},
    difficulty: { type: Number, min: 1, max: 5 },
    ingredients: [ String ]
})

// create the Recipe model
const Recipe = mongoose.model('Recipe', RecipeSchema);

module.exports = Recipe;
```

Then in our routes file we convert the '/'

BEFORE

```js
const Recipe = require('./db')
...

router.get('/', async (req, res) => {
    const recipes = await Recipe.all();
    res.json(recipes)
})
```

AFTER

```js
const Recipe = require('../models/recipe')

router.get('/', async (req, res) => {
    const recipes = await Recipe.find({})
    res.json(recipes)
})
```

I'll demonstrate the rest below

```js
const Recipe = require('../models/recipe')

//show all
router.get('/', async (req, res) => {
    const recipes = await Recipe.find({})
    res.json(recipes)
})

//show one
router.get('/:id', async (req, res) => {
    const recipe = await Recipe.findById(req.params.id);
    res.json(recipe);
})

//create one
router.post('/', async (req, res) => {
    try{	// added due to validation of models
    	const recipe = await Recipe.create(req.body);    
        res.status(201).json(recipe)
    } catch (err) {
        res.status(422).end();
    }
})

//update one
router.put('/:id', async (req, res) => {
    try{
		const recipe = await Recipe.findByIdAndUpdate(req.params.id, req.body);
    	res.status(204).json(recipe);
    } catch(err) {
        res.status(422).end();
    }
})

```

