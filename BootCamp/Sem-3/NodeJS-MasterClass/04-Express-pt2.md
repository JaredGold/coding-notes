# Express

http://expressjs.com/en/api.html

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
const

const port = process.env.PORT || 1337
const app = express();

app.get('/recipes', (req,res) => {
  res.send('ok');
});

app.listen(port, () => console.log('Recipes listening on port ' + port));
```

---

#### Force nodemon for server

in the package.json file add in scripts, `"dev" : "nodemon index.js",` and `"start" : "node index.js",` Then `$ npm run dev` will use nodemon.

---

