# Async Middleware for Express

Being able to use Async and Await for express is key when we want to add a database system. So we can do this by

```js
const Recipe = require('../db'')

router.get('/', (req, res) => {
    const recipes = Recipe.all()	// the fetch to the db
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
    return Promise.resolve(recipes);
}

// exports.recipes = recipes; //=> not async

```

