# React Intro

React is a javascript framework to build frontends. As opposed rails us a framework for front end and back end use with Ruby.

React has great performance and does not have to refresh to update itself. For example updating if something is public or private can be done without a refresh unlike rails.

React uses components which allow you to reuse chunks of code where needed. This is alternate to pages which is less reusable.

It is flexible as it uses javascript as it's base language.

It is also asynchronous

Tool chain allows you to install js libraries (Like lodash) (from yarn or npm)

Lets you create Native apps (mobile apps!)

---

###### *Part 2*

There are 2 libraries you need to work with react.

```
react === react components
reactDOM === renders content to the browser
```

tool to get up and running quickly with react

```
npx create-react-aoo <your-app-name>
```

npx downloads and executes an executable from npm

folder structure

```
src === where our code goes
node_modules === where our libraries go
packages.json === lists our dependencies and scripts
```

setting up a `.env.development` and `.gitignore`, setting up a port, preventing the browser from always opening when running development server

#### `.env.development`

```
PORT=8080
BROWSER=none
```

Then put this in the `.gitignore` file

---

###### *Part 3*

To start the app you use `yarn start`

jsx is the syntax used to write to the screen on react. It looks like bellow.

```jsx
ReactDOM.render(
	<h1>Hello World!</h1>,
    document.getElementById('root')
);

//jsx
<h1>Hello World!</h1>
//react
React.createElement("h1", "Hello World!")
```

The file first loads index.js and then runs whatever is inside. In our case it runs the app (app)

```react
import React from "react";
import ReactDOM from "react-dom";
import App from "./App.jsx";

ReactDOM.render(
  <App />,
  document.getElementById("root")
);
```

Then it renders whatever is inside of App

```jsx
import React from 'react'

function App() {
  return (
    <h1>Hello World</h1>
  );
}

export default App;
```

---

###### *Part 4*

component nesting is when you add multiple components to the project.

There used to be class components but now it is all done through functional components.

```jsx
const App = () => {
  return (
    <h1>Hello World</h1>
  );
}
```

if you want to create 2 other components running inside of app you create a directory in `src` called components. You never move index.js but everything else can be in components

Functions created in jsx need an upcase to the first character i.e. `const Nav` not `const nav`

To write code inside of a jsx you do so with curly brackets. 

```jsx
import React from 'react'
import Nav from './nav'
import Main from './Main'

// functional component
const App = () => {
  return (
    <div>
      <Nav />
      <Main />
    </div>
  );
}

export default App;

```

```js
import React from 'react'

const Main = () => {
  const name = "Jared"
  return (
    <main>
      <h1>Hello World! My name is {name + " Goldstein" }</h1>
      <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Nesciunt, sit sequi? Doloribus perspiciatis tempore assumenda consectetur aut natus porro esse!</p>
    </main>
  )
} 

export default Main
```

```jsx
import React from 'react'

const Nav = () => {
  return (
    <nav>
      <a href="/">Home</a>
      <a href="/">About Me</a>
      <a href="/">Projects</a>
      <a href="/">Contact</a>
    </nav>
  )
}

export default Nav;
```

