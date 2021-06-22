# Async Middleware for Express

Being able to use Async and Await for express is key when we want to add a database system. So we can do this by

```js
const Recipe = require('../db'')

router.get('/', async (req, res) => {	// change async function
    const recipes = await Recipe.all()	// fetches the Recipe db and waits for all of the sync files
    res.json(recipes);
})
```

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

function all() {
    const json = JSON.parse(JSON.stringify(recipes))
    return Promise.resolve(recipes);
}

function find(id) {
    const recipe = recipes.find(r => r.id == id);
    return Promise.resolve(recipe)
}

// exports.recipes = recipes; //=> not async
module.exports = {all, find}

```

