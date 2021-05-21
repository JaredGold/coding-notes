# React Forms

Forms in react will work differently to each of our previous language knowledges.
*This example does not use hooks*

To create a form with jsx we use the same syntax as html `<form action="">` but unlike in html we do not need the action `<form>`

Inside of the form we need a label for an input, an input and a submit (minimum).

Inside of label we will get a `htmlFor` which is the label for element. `<label htmlFor="email">Email</label>`

We then use an input adding the type, name and id.

```jsx
import React from 'react' 

class App extends React.Component {
    render() {        
        return(
        	<div>
            	<h2>Login</h2>
                <form>
                	<label htmlFor="email">Email</label>
                    <input type="text" name="email" id="email" />
                    <label htmlFor="password">Password</label>
                    <input type="password" name="password" id="password"/>
                    <input type="submit" value="Submit" id="submit" />
                </form>
            </div>
        )
    }
}
```



Now with the above code we need to use javascript to actually have validation and have it actually do something.

We now want to tell the form to do something when a specific event is fired. That event is known as `onSubmit`.

The `onSubmit` takes a function and is placed in the `<form>`

Specifically in a class component to to call the function passed on submit you need to pass `this.function` `<form onSubmit={this.onFormSubmit}>`

To pass the specific input values into the function on the function we add an event to the function brackets. In the event object we use `event.target` which will show us the form values. (we can use this for a lot of things).

Because in the form we have the children of the form being the inputs we are able to take the values in the input.

We do this by using the `event.target.children` which returns an array. We then select the correct index that we are looking for and `.value` to show the value

The below is what we have been doing which is an 'uncontrolled component' (not the best solution)



```jsx
const users = [
    {
        email:"test@mail.com",
        password: "password"
    },
    {
        email:"reelmael@meail.com",
        password: "dontlook123"
    }
]

constructor(props){
    super(props)
    this.state = {
        errorMessage: "",
        successMessage: ""
    }
}

onFormSubmit = (event) => {
    event.preventDefault();
    this.setState({
        errorMessage: "",
        successMessage: ""
    })
    const formElements = event.target.children
    const emailInput = formElements[1]
    const passwordInput = formElements[3]
    const emailValue = emailInput.value
    const passwordValue = passwordInput.value
    const foundUser = users.find((user) => user.email === emailValue)
    if (foundUser){
        // check pwd
        if (passwordValue === foundUser.password){
            this.setState({
                successMessage: "User sucesfully authenticated!"
            })
        } else {
            this.setState({
            errorMessage: "Wrong credentials entered!"
        })
        }
    } else {
        // set some state saying user hasn't been found
        this.setState({
            errorMessage: "Wrong credentials entered!"
        })
    }
}

render(){
...
<div>
    {this.state.errorMessage && <p>{this.state.errorMessage}</p> }
    {this.state.successMessage && <p>{this.state.successMessage}</p> }
  <h2>Login</h2>
  <form onSubmit={this.onFormSubmit}>
    <label htmlFor="email">Email</label>
    <input type="text" name="email" id="email" />
    <label htmlFor="password">Password</label>
    <input type="password" name="password" id="password"/>
    <input type="submit" value="Submit" id="submit" />
  </form>
</div>
}
```



We want to create a 'controlled component' where we use states and events to add dynamically to the state.

A controlled component would be in our form instead of grabbing the info through getting the form elements it would actually be grabbing it from a state which is being updated using the input field

We do this by adding a value to a state that is handled  by the input. `<input ... value={this.state.password}>` of course by default this will lock us out of updating and that is where `onChange` comes into play.

The on change takes a function which can look like below. As long as the state name and the id name is the same then the value will update. This will work for both the password and the email.

```jsx
onInputChange = (event) => {
    this.setState({
        [event.target.id]: event.target.value
    })
}
```

Because we have the state we no longer need all of the `const` in the form submit.

We can also destructure the states as const's in the onFormSubmit.

```jsx
const users = [
    {
        email:"test@mail.com",
        password: "password"
    },
    {
        email:"reelmael@meail.com",
        password: "dontlook123"
    }
]

constructor(props){
    super(props)
    this.state = {
        errorMessage: "",
        successMessage: "",
        email: "",
        password: ""
    }
}

onFormSubmit = (event) => {
    event.preventDefault();
	const {email, password} = this.state
    
    this.setState({
        errorMessage: "",
        successMessage: ""
    }
                  
    const foundUser = users.find((user) => user.email === email)
    
    if (foundUser){
        if (foundUser.password === password){
            this.setState({
                successMessage: "User sucesfully authenticated!"
            })
        } else {
            this.setState({
            errorMessage: "Wrong credentials entered!"
        })
        }
    } else {
        // set some state saying user hasn't been found
        this.setState({
            errorMessage: "Wrong credentials entered!"
        })
    }
}

onInputChange = (event) => {
    this.setState({
        [event.target.id]: event.target.value
    })
}

render(){
...
const { errorMessage, successMessage, email, password } = this.state

return(
<div>
    {errorMessage && <p>{errorMessage}</p> }
    {successMessage && <p>{successMessage}</p> }
  <h2>Login</h2>
  <form onSubmit={this.onFormSubmit}>
    <label htmlFor="email">Email</label>
    <input 
        type="text" 
        name="email" 
        id="email" 
        value={email}
        onChange={this.onInputChange}
     />
    <label htmlFor="password">Password</label>
    <input 
        type="password" 
        name="password" 
        id="password" 
        value={password}
        onChange={this.onInputChange}
      />
    <input type="submit" value="Submit" id="submit" />
  </form>
</div>
})
```

