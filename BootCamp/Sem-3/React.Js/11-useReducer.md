# `useReducer` / State Reducer

* `useReducer` is another hook used for state management
* Allows more flexibility than the `useState` hook
* Pattern mimics Redux (global state package)
* Significantly more complicated than `useState`, but powerful

#### Why use a reducer?

* Complex state management logic
  * When just 'set' to replace the entire value is not sufficient
* Cleaner state management interface
  * Define 'actions' that can be performed on the state to change it.
* Global state implementation
  * Provides a way to abstract state management for sharing globally with React Context

#### `useReducer` hook

* Takes two arguments - a **reducer function** and an initial state (and an optional third argument for an init function to initialize state)
* The reducer is a Redux-style reducer function of the form `(state, action) => newState`
* The useReducer hook returns an array with the current state (like useState) and a `dispatch` function for calling the reducer function (like Redux)

#### Call to useReducer

```jsx
const [store, dispatch] = useReducer(reducer, initialState)
```

It is a common practice to **store** as the name of the current state object, and **dispatch** as the function used to change the state in Redux

#### What is the reducer function?

It is a function that is used to change application state

It follows a particular pattern

It can be called with the `dispatch` function returned by `useReducer`

#### How the reducer function works

* The reducer function takes the current `state`, and an `action` to perform on the state (including the updated data for the action)
* It returns a new copy of the state, with the changes dictated by the `action`
* If the `action` is unrecognized or invalid, it will just return the current state

#### example:

```jsx
function reducer(state, action){
    // action type field decides what happens
    switch (action.type) {
            //Do something here based on the different types of actions
        case 'setProjects' : {
            return {
                ...state,
                projects: action.data
            }
        }
        default:
            // if this reducer doesn't recognise or care about this
            // specific action, return the existing state unchanged
            return state
    }
}
```

#### Line by line

##### Function

`function reducer(state, action) {`

The `state` parameter is the current state of the object

The `action` parameter is an object with two properties:

​	`type` - A string label for the action to perform on state

​	`Data` - The updated data that will be applied to the current state

##### action.type

`switch (action.type) {`

The `action.type` is a string that identifies what action we want to perform on the state

If the `action.type` is not recognized, the current state is returned in the default statement.

```jsx
default:
	return state
```

##### action.data

```jsx
case 'setProjects' : {
    return {
        ...state,
        projects: action.data
    }
}
```

Updated state data is passed through `action.data`, and is used in the action clause to update the state appropriately.

#### Defining state

It is a common practice to use a state **object** with **properties** for each piece of state with `useReducer` 

```jsx
const initialState = {
    projects: []
}
```

Rather than separate the state objects for each piece of state with `useState`

```jsx
const initialState = []
const [projects, setProjects] = useState(initialState)
```

#### Accessing state

```jsx
const [store, dispatch] = useReducer(reducer, initialState)
const {projects} = store
```

Since state is implemented as an object with properties for each piece of state, it needs to be accessed a little differently

Some people to use destructuring to define separate variables for each piece of state

#### Modifying state

We call `dispatch` (the function returned by useReducer) with an action to make changes to state.

The reducer function will be called by `dispatch` with the current `state` and `action`

The reducer function will update the current state based on the `action`

```jsx
dispatch({
    type: 'setProjects',
    data: projects
  data: {
  id: 1,
  modifier: 0.5
}
})
```



## Example

```jsx
export default function reducer(state, action){
    switch(action.type) {
        case 'setProjects' : {
            return {
                ...state,
                projects: action.data
            }
        }
    }
}
```



