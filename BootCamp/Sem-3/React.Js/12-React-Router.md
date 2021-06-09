# React-Router

*important Links:*

https://reactrouter.com/web/guides/quick-start

https://reactrouter.com/web/api/Link

https://reactrouter.com/web/api/Route

https://reactrouter.com/web/api/Hooks



#### What is react-router

React routes does not reload or ask for specific http request it simply loads the app with new components.

### How To use router

First thing you must do is install the react router package using :
`npm install react-router-dom`

Then you must import the router in the App.js file :
` `

From there you encapsulate the components you want to have a route with a `<Router>` (meant to be `BrowserRouter`)

```jsx
<div>
  <Router>
    <Home />
    <CategorySelection />
    <NewEntry />
  </Router>
</div>
```

You then need to convert the previous components to `<Route>`'s. The problem with the below code is that whenever you load category or new because the path includes the `/` it also renders the Home component.

```jsx
<div>
  <Router>
    <Route path="/" component={Home} />
    <Route path="/category" component={CategorySelection} />
    <Route path="/entry/new" component={NewEntry} />
  </Router>
</div>
```

Because of this it is better to also include the keyword `exact` which we can put if we want the path to be exactly as given.
`<Route exact path="/" component={Home} />`

From here if we want to create a 404 page not found we could do so by not giving a path:
`<Route component={NotFound} />`

But this would also render on any page. This is when we also need to include Switch in the imports. And encapsulate the existing Routes in a `<Switch>`. This is done so it can do one OR whatever the last route is.

```jsx
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom'

<Switch>
  <Route exact path="/" component={Home} />
  <Route path="/category" component={CategorySelection} />
  <Route path="/entry/new" component={NewEntry} />
  <Route component={NotFound} />
</Switch>
```



#### Link

From here we need to create the links that will take us from one URL path to another. We should not be using `<a>` tags in routes but instead we should use `<Link>`. We do this as below.

```jsx
import { BrowserRouter as Router, Route, Switch, Link } from 'react-router-dom'

<Router>
  <Link to="/">HOME</Link>
  <Link to="/category">Category Selection</Link>
  <Link to="/entry/new">New Entry</Link>
  <Switch>
```

You can encapsulate the links as a `<ul>` and `<li>` like you would a nav bar.



#### Adding Data

From here we can start adding data and passing it through to the right fields. In this example we will be adding a state in home that holds some category's

```jsx
const defaultCategories = ["Food", "Coding", "Other"]
const [categories, setCategories] = useState(defaultCategories)
```

You can pass the categories in the component the same way you would normally or we can use a render. The benefit of a render is you can avoid unmount and mounting behaviour if there is no change. From here we would change the component keyword and start using the render prop.

```jsx
<Route 
    path="/category" 
    render={(props) => <CategorySelection {...props} categories={categories} />} 
/>
```

*Note: There is no benefit using render when you are not passing props*

#### Use specific categories...

```jsx
<Link key={`${index}-${item}`} to={`/entry/new/${index}`}>{item}</Link>
```

The above will let you pass the index as a parameter being used in the url

To use the url parameter we then need to first change the router Link and Route to include the `/:id`

```jsx
<li><Link to="/entry/new/:id">New Entry</Link></li>

<Route path="/entry/new/:id" render={(props) => <NewEntry {...props} categories={categories} />} />
```

From there we then have access to the params which should show as an object with the key of id. We can capture this using match which can be destructured in the props section.

```jsx
const NewEntry = ({match, categories}) => {
```

```jsx
import React, { useState, useEffect } from 'react'

const NewEntry = ({match, categories}) => {
  const selectedCategory = match.params ? match.params.id : -1
  const category = categories[selectedCategory] 
  const [errorMsg, setErrorMsg] = useState(null)
  

  useEffect(() => {
    category ? setErrorMsg(null) : setErrorMsg("Category not found please try another link")
  }, [category, categories])

  return(
    <div>
      {errorMsg ? <p>{errorMsg}</p> : <h1>New Entry for {category}</h1>}
    </div>
  )
}

export default NewEntry
```

#### History

If at any point you want to go back to another page you can use history which can be destructured as long as you use {withRouter} or {useHistory}

```jsx
import {withRouter} from "react-router"

const EntryForm = ({addEntryToJournal, category, history}) => {

export default withRouter(EntryForm)
```

We then can use push the new route in the handleSubmit using the below

```jsx
  const handleSubmit = (event) => {
    event.preventDefault()
    if(entry && entry.length > 0){
      addEntryToJournal({category, entry})
      return history.push("/")
    }
  }
```





---

# ALL files for ref

*App.js*

```jsx
import React, {useState} from 'react'
import { BrowserRouter as Router, Route, Switch, Link } from 'react-router-dom'
import Home from "./components/Home"
import CategorySelection from "./components/CategorySelection"
import NewEntry from "./components/NewEntry"
import NotFound from "./components/NotFound"

const App = () => {
  const defaultCategories = ["Food", "Coding", "Other"]
  const [categories, setCategories] = useState(defaultCategories)
  const [entries, setEntries] = useState([])

  const addEntryToJournal = (newEntry) => {
    const updatedEntries = [...entries, newEntry]
    setEntries(updatedEntries)
  }

  return(
    <div>
      <Router>
        <ul>
          <li><Link to="/">HOME</Link></li>
          <li><Link to="/category">Category Selection</Link></li>
          <li><Link to="/entry/new/:id">New Entry</Link></li>
        </ul>

        <Switch>
          <Route exact path="/" render={(props) => (<Home {...props} entries={entries}/>)} />
          <Route path="/category" render={(props) => <CategorySelection {...props} categories={categories} />} />
          <Route path="/entry/new/:id" render={(props) => <NewEntry {...props} categories={categories} addEntryToJournal={addEntryToJournal} />} />
          <Route component={NotFound} />
        </Switch>
      </Router>
    </div>
  )
}

export default App;
```



*Home.jsx*

```jsx
import React from 'react'
import { Link } from 'react-router-dom'


const Home = ({entries}) => {
  return(
    <div>
      <h1>Home</h1>
      <Link to="/category">Choose a category</Link>
      {entries.map(({entry, category},index) => (
        <div key={index}>
          <h4>{category}</h4>
          <p>{entry}</p>
        </div>
      ))}
    </div>
  )
}

export default Home
```



*CategorySelection.jsx*

```jsx
import React from 'react'
import { Link } from 'react-router-dom'


const CategorySelection = ({categories}) => {
  console.log(categories)
  return(
    <div>
      <h1>Category Selection</h1>
      {categories.map((item, index) => (
        <li key={`${index}-${item}`}>
          <Link  to={`/entry/new/${index}`}>{item}</Link>
        </li>
      ))}
    </div>
  )
}

export default CategorySelection
```



*NewEntry.jsx*

```jsx
import React, { useState, useEffect } from 'react'
import EntryForm from './EntryForm'

const NewEntry = ({match, categories, addEntryToJournal}) => {
  const selectedCategory = match.params ? match.params.id : -1
  const category = categories[selectedCategory] 
  const [errorMsg, setErrorMsg] = useState(null)
  

  useEffect(() => {
    category ? setErrorMsg(null) : setErrorMsg("Category not found please try another link")
  }, [category, categories])

  return(
    <div>
      {errorMsg ? <p>{errorMsg}</p> : <h1>New Entry for {category}</h1>}
      {category && <EntryForm addEntryToJournal={addEntryToJournal} category={category}/>}
    </div>
  )
}

export default NewEntry
```



*EntryForm.jsx*

```jsx
import React, {useState} from 'react'
import {withRouter} from "react-router"



const EntryForm = ({addEntryToJournal, category, history}) => {
  const [entry, setEntry] = useState("")

  const onTextChange = (event) => {
    setEntry(event.target.value)
  }

  const handleSubmit = (event) => {
    event.preventDefault()
    if(entry && entry.length > 0){
      addEntryToJournal({category, entry})
      return history.push("/")
    }
  }

  return(
    <div>
      <form onSubmit={handleSubmit} >
        <div>
          <textarea onChange={onTextChange} />
        </div>
        <input type="submit" value="Submit Entry"/>
      </form>
    </div>
  )
}

export default withRouter(EntryForm)
```



*NotFound.jsx*

```jsx
import React from 'react'

const NotFound = () => {
  return(
    <h1>Page not found please use another URL</h1>
  )
}

export default NotFound;
```

