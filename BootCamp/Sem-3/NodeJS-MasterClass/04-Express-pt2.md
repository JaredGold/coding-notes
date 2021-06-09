# Express

http://expressjs.com/en/api.html

https://expressjs.com/en/guide/writing-middleware.html

https://expressjs.com/en/guide/using-middleware.html

Below is the same as part 1 but using express

In this example we will use a RESTful app for a recipe app. It is going to be an API server that serves JSON.

* GET /recipes -> index
* GET /recipes/:id -> sjpw
* Content-Type: application/json
* Status code 404, otherwise

First of all we need to use `npm init`

Then `npm install express` and `npm install --save-dev nodemon`

The begining is very similar to base node although we can get to the '/recipes' much easier using express

*index.js*

```js
const express = require('express')
const {recipes} = require('./db') // deconnstructed

const port = process.env.PORT || 1337
const app = express();

app.get('/recipes', (req,res) => {
  res.json(recipes);
  res.send('ok');
});

app.get('/recipes/:id', (req, res) => {
  const recipe = recipes.find(r => r.id == req.params.id)
  res.json(recipe)
})

app.listen(port, () => console.log('Recipes listening on port ' + port));
```

---

#### Force nodemon for server

in the package.json file add in scripts, `"dev" : "nodemon index.js",` and `"start" : "node index.js",` Then `$ npm run dev` will use nodemon.

---

#### Middleware

Middleware is the part in the request that is best changed with Express. This part is the below part.

```js
... (req,res) => {
  res.json(recipes);
  res.send('ok');
});
```

`express.json` is some built in middleware. We can do this as below. This automatically prases the data given as a json file.

```js
app.use(express.json)

....
// add
app.post('/recipes', (req, res) => {
  const recipe = req.body;
  recipe.id = recipes.length + 1
  recipes.push(recipe)
  res.status(201).json(recipe)
})
// edit
app.put('/recipes/:id', (req, res) => {
    const recipe = recipes.find(r => r.id == req.params.id);
    Object.assign(recipe, req.body);
    res.status(204).json(recipe);
}
    
```

This works as is but it is good to make routes, which is a middleware. Routes is going to be similar to rails routes where we can put all of our previous routes in it's own folder and file.

`mkdir routes` `touch routes/recipes.js` << in here will be all of the routes and only the routes

To include this we first need to require it and then use it. `use` is like all requests in one

```js
const express = require('express')
const recipesRouter = require('./routes/recipes')

const port = process.env.PORT || 1337
app.use('/recipes', recipeRouter); // for any request using /recipes use recipeRouter
const app = express();
```

We still need to tell the recipes file to use a couple files and tweak some things.
First we need to require express (self explanatory). Then we need to add router instead of app. Router is like a mini express app. It does mostly the same thing. Then we need to change every instance of `app` to `router`. Finally we need to export the routes out. And finally we have to remove the `/recipes` context as it would actually be `/recipes/recipes` as /recipes takes us to the recipes router. In this example as well we need to also get the recipes file.

```js
const express = require('express');
const router = express.Router();
const {recipes} = require('../db')

// see all
router.get('/', (req,res) => {
  res.json(recipes);
});

// show
router.get('/:id', (req, res) => {
  const recipe = recipes.find(r => r.id == req.params.id)
  res.json(recipe)
})

// add
router.post('/', (req, res) => {
  const recipe = req.body;
  recipe.id = recipes.length + 1
  recipes.push(recipe)
  res.status(201).json(recipe)
})
// edit
router.put('/:id', (req, res) => {
    const recipe = recipes.find(r => r.id == req.params.id);
    Object.assign(recipe, req.body);
    res.status(204).json(recipe);
})
    
module.exports = router;
```

We have the ability to string multiple requests with multiple middleware. We do this using the `next` keyword. This looks as below and is described as below. This is very useful for logging.

```js
router.get('/', (req, res, next) => {	// middleware with next
    console.log('Request received');
    next()		// call to next runs next middleware
  },
  (req, res) => { // and second middleware
    res.json(recipes);
});
```

 We can use this for security purposes and including regular HTTP Authorizations. This can be found in the `http` MDN for headers. 

```js
router.get('/', (req, res, next) => {	// middleware with next
    if (req.headers['authorization'] === 'Bearer 666'){ // look for auth
        next();	// if auth next
    } else {
        res.status(401).end(); // else break
    }
  },
  (req, res) => { // and second middleware
    res.json(recipes);
});
```

This if statement can become a function. After this you could use this function for almost all requests.

```js
const authorize = (req, res, next) => {
    if (req.headers['authorization'] === 'Bearer 666'){ // look for auth
        next();	// if auth next
    } else {
        res.status(401).end(); // else break
    }
}

router.get('/', authorize, (req, res) => {
    res.json(recipes);
});
```

Alternitavely you can put the auth at the top of the file to work down. By using `router.use()` it will add the given middleware for everything under that.

```js
router.use(authorize);
```

