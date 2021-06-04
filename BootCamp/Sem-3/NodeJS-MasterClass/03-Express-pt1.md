# Express

Https://express.js.com

Express is a framework used to write API applications. It is very good and very fast which makes it extremely popular. Express gives a lot of help fixing, http, routing, params and modules. The key is this library is used for the middleware.

In this example we will use a RESTful app for a recipe app. It is going to be an API server that serves JSON.

* GET /recipes -> index
* GET /recipes/:id -> sjpw
* Content-Type: application/json
* Status code 404, otherwise

The below is if you were just using regular Node

<u>***RECIPE.js***</u>

```js
const http = require('http');

const port = process.env.PORT || 1337;

const server = http.createServer(function (req, res) {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify({ message: 'Hi!' }));
})

server.listen(port, function () {
  console.log(`Server listening on port ${port}`)
})
```

This is just a base code to write a server that is serving JSON by default.

**<u>db.js</u>**

```js
const recipes = [
  { id: 1, 
   	title: 'Chocolate Cake', 
   	difficulty: 3, 
   	ingedients: ['flour', 'butter', 'eggs', 'coco']
  }, {
    id: 2,
    title: 'Banana Cake',
    difficulty: 3,
    ingredients: ['flour', 'butter', 'eggs', 'bananas']
  }, {
    id: 3,
    title: 'Carrot Cake',
    difficulty: 3,
    ingredients: ['flour', 'butter', 'eggs', 'carrots']
  }
]

exports.recipes = recipes;

// export default recipes (If it is ES6 syntax)
```

This is an array of hashes. There is a scope which would only be available in this file so we export it. The export is not a copy of the array it is just a reference

We then add :

```js
const { recipes } = require('./db.js')
```

Now on request we want to send the JSON to the browser. We do this by changing our server code to somewhat below.

```js
const http = require('http');
const { recipes } = require('./db.js')
const port = process.env.PORT || 1337;

const server = http.createServer(function (req, res) {
  respondIndex(req, res);
})

function respondIndex(req, res) {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify(recipes));
}

server.listen(port, function () {
  console.log(`Server listening on port ${port}`)
})
```

---

#### **<u>TO ALWAYS LOOK FOR CHANGES</u>**

By default you can't have the server always listen for changes so every time a file changes the server would need to be restarted. There is a package to fix that. To install that package run the code below

`$ npx nodemon file.js` the file.js would be the name of the file we are looking for.

---

By default the code we have written will work no matter the request type or url. We want to wrap the requests in an expression to check that the url matches.

```js
const server = http.createServer(function (req, res) {
  if (req.url.match(/\/recipes/) && req.method === 'GET') respondIndex(req,res);
  // the above is regular expression which matches the /recipes
})
```

This will work by default but if there is an error it will not respond with an error or a 404.

```js
const server = http.createServer(function (req, res) {
  if (req.url.match(/\/recipes/) && req.method === 'GET') return respondIndex(req,res);
  respondNotFound(req, res);
})

function respondNotFound(req, res){
//  res.statusCode = 404;
//  res.setHeader('Content-Type', 'text/plain');
  res.writeHead(404, {'Content-Type': 'text/plain'}) // cleaner head
  res.end('Not found');
}
```

This works well for the recipes but it still needs to include the `/recipe/:id`

```js
function respondShow(req,res) {
	const recipe = {}
  res.statusCode = 200;
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify(recipe));
}
```

We then need the route

```js
const server = http.createServer(function (req, res) {
  const match = req.url.match(/\/recipes\/\d+$/);
  // the above matches /recipes/ then any amount of digits with nothing following
  if (match & req.method === 'GET') return respondShow(req,res)
// the bottom has been placed under so that it is called last in the case that it's less integral
  
  if (req.url.match(/\/recipes/) && req.method === 'GET') return respondIndex(req,res);
  respondNotFound(req, res);
})
```

Now this works but if we want the numbers that follow in the ID we need to change our regular expression to look like this : `(/\/recipes\/(\d+$)/)` of course in regular expressions we can name that 'group' as follows : `(/\/recipes\/(?<id>\d+$)/)` - to acces it we use `match.groups.id`

```js
const server = http.createServer(function (req, res) {
  const match = req.url.match(/\/recipes\/(?<id>\d+$)/);
  if (match & req.method === 'GET') return respondShow(req,res, match.groups.id)  
  
  if (req.url.match(/\/recipes/) && req.method === 'GET') return respondIndex(req,res);
  respondNotFound(req, res);
})

function respondShow(req,res,id) {
	const recipe = recipes.find(r => r.id == id)
  if (!recipe) return respondNotFound(req, res)
  res.statusCode = 200;
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify(recipe));
}
```

We should also set a catcher in the server function.

```js
const server = http.createServer(function (req, res) {
  if (req.headers['content-type'] != 'application/json'){
    return respondUnsupportedMediaType(req,res)
  } 
  
  const match = req.url.match(/\/recipes\/(?<id>\d+$)/);
  if (match & req.method === 'GET') return respondShow(req,res, match.groups.id)  
  if (req.url.match(/\/recipes/) && req.method === 'GET') return respondIndex(req,res);
  respondNotFound(req, res);
})
```

```js
function respondUnsupportedMediaType(req,res) {
	res.writeHead(415, {'Content-Type': 'text/plain'}) 
  res.end('Not JSON');
}
```





The final File

```js
const http = require('http');
const querystring = require('querystring');

const { recipes } = require('./db.js');
const port = process.env.PORT || 1337;

const server = http.createServer(function (req, res) {
  if (req.headers['content-type'] !== 'application/json') return respondUnsupportedMediaType(req, res);

  const match = req.url.match(/\/recipes\/(?<id>\d+)$/);
  if (match && req.method === 'GET') return respondShow(req, res, match.groups.id);

  if (req.url.match(/\/recipes/) && req.method === 'GET') return respondIndex(req, res);
  respondNotFound(req, res);
});

// /recipes
function respondIndex(req, res) {
  const qs = req.url.split('?').slice(1).join('');
  let { page = 1, perpage = 10 } = querystring.parse(qs);

  page = Number(page), perpage = Number(perpage);
  const startIdx = (page - 1) * perpage, endIdx = (startIdx + perpage);
  const pagedRecipes = recipes.slice(startIdx, endIdx);

  res.statusCode = 200;
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify(pagedRecipes));
}

// /recipes/:id
function respondShow(req, res, id) {
  const recipe = recipes.find(r => r.id == id);
  if (!recipe) return respondNotFound(req, res);

  res.statusCode = 200;
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify(recipe));
}


function respondNotFound(req, res) {
  res.writeHead(404, { 'Content-Type': 'text/plain' })
  res.end('Not found');
}

function respondUnsupportedMediaType(req, res) {
  res.writeHead(415, { 'Content-Type': 'text/plain' })
  res.end('Not JSON');
}

server.listen(port, function () {
  console.log(`Server listening on port ${port}`);
});

```

