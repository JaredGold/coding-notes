# React Hooks

*State and lifeCycle*

Hooks are the correct way to use state changes as they are functional and not class.

A state is used for dynamic data that changes on render.

Because react works from a top down perspective it is important to decide where the state is most appropriate to be created and then passed from there. If you have 2 components that need a list you would create the state in the parent component that best holds those components.

#### What are hooks?

* Intended to enable functional components to be as feature rich as class components
  * Provide a way to use state and override lifecycle methods
  * Enable definition of custom hooks that can be reused
  * Makes it easier to define modular code
* A hook is a **function**

##### Rules of Hooks

* Hooks can only be used in functional components (or in custom hooks)
* Hooks must be used at <u>the top level of the function</u>
  * They cannot be called in loops, conditionals, or nested functions

### State Hook

#### The `useState` hook

* Called with the default state value for a piece of state
* Returns an array with 2 items
  * The state variable
  * The set function
* Best practice is to use a sperate state hook for each state item

The first important thing to do is to import the `useState` function from react.
`import React, {useState} from 'react`'

From there to define the state we create is as below.
`const [projects, setProjects] = useState([{title: "item", description:"thing"}])`

This would create an array of objects as a state. This can be used for a boolean as below.
`const [isUsed, setIsUsed] = useState(true)`

If you want to pass the function of adding a new project into another component you do this by below.

```jsx
const [projects, setProjects] = useState(initialProjects)

function addProjects(project) {
    setProjects([project, ...projects]) // spread the array and then add an array in the front
}

return(
	<>
    	<NewProjectForm addProject={addProject} />
    </>
)
```

If you want to **create a form** that adds to a state you would do so as below

```jsx
import React,{useState} from 'react'

export default NewProjectForm = () => {
    const {addProject} = props
    const initialFormState = {
        name: "",
        description: ""
    }
    const [formData, setFormData] = useState(initialFormState)
    
    changeHandler = (event) => {
        setFormData({
            ...formData, // take what is already in form data
            [event.target.name] : event.target.value
        })
    }
    
    submitHandler = (event) {
        event.preventDefault()
        addProject(formData)
		setFormData({
            name: "",
            description: ""
        })
    }
    
    return(
    	<form onSubmit={submitHandler}>
            <div>
        		<label>Name:</label>
            	<input 
                    type="text" 
                    name="name"
                    value={formData.name}
                    onChange={changeHandler}
                />
            </div>
			<div>
            	<label>Description:</label>
            	<input 
                    type="text" 
                    name="description"
                    value={formData.description}
                    onChange={changeHandler}
                />            
            </div>
            <input 
                type="submit" 
                value="submit"
            />
        </form>
    )
}
```

### LifeCycle / Effect Hook

A JSON Generator https://www.pluralsight.com/guides/fetch-data-from-a-json-file-in-a-react-app

JSON file's that are going to be imported need to be in the public directory

#### Effect Hook

* The effect hook provides access to override the Lifecyle methods:
  * `componentDidMount`
  * `componentDidUpdate`
  * `componentWillUnmount`
* Executed once on `componentDidMount`
* Executed optionally on `componentDidUpdate`
  * By default, executes on every render
* Executes another optional function on `componentWillUnmount`



#### useEffect hook

* Called with a callback function, and optional array of trigger values
* By default callback function executed on every single component render!
* Limit execution using the optional array of trigger values
  * Empty array means it only executes once on `componentDidMount`
* Callback function optionally returns another callback function to be executed on `componentWillUnmount`
  * If needed for cleanup (timers, close fetch's)

To get the effect hook we need to import it the same way we do as useState `import React. {useEffect} from 'react'`

```jsx
const App = () {
    useEffect(() => {
        console.log("Component is mounted")
    }, []) // empty array runs on comp mount
    
    useEffect(() => {
        console.log("Component is mounted")
    }) // no array runs on comp update
    
    useEffect(() => {
        console.log("Component is mounted")
    }, [projects]) // will update only when projects is updated
    
    useEffect(() => {
        console.log("Component is mounted")
        return () => {
            console.log("Component is unmounting")
        }
    }, [])  // will trigger the return when unmounted (needs to be a callback function)
    
    return(
    	<h1>Recent Projects</h1>
    )
} 
```

It is **<u>IMPORTANT</u>** to always star writing the use effect before passing any argument as below!

```jsx
useEffect(() => {}, [])		// do not put anything in the curly brackets before the 
```



```jsx
// This one here is similar to componentDidMount
// useEffect is taking 2 arguments (an exmpty array)
  useEffect(() => {
    document.title = `You've clicked ${timesClicked} times`
  }, [])

// This is similar to componentDidMount + componentDidUpdate
// useEffect is taking 1 argument
  useEffect(() => {
    document.title = `You've clicked ${timesClicked} times`
  })

// This is similar to shouldComponentUpdate
// useEffect is taking 2 arguments (an array of variables we want to check the changes)
  useEffect(() => {
    document.title = `You've clicked ${timesClicked} times`
  }, [timesClicked])

// This is similar to shouldComponentUpdate + componentWillUnmount
// useEffect is taking 1 arguments, the return states if it will unmount do this.
  useEffect(() => {
    document.title = `You've clicked ${timesClicked} times`
    
    // equivalent to componentWillUnmount
    return () => document.title = "goodbye"
  })
```

