# Class Components, States and Lifecycle

In these examples we use class components but as of 2019 you can use react hooks to do the same in functional programming. Functional programming is the preferred method. - links given in state.

#### Component

A component is the smallest unit in the web page which can always be configured, reused and nested. A component is called as seen previously as `<App />` a component returns html elements that are placed into a main div. 

When designing a component the it is very important for it to be reusable, configurable and nested

Example code - https://github.com/JaredGold/React-State-Class-Lifecycle-Starter?organization=JaredGold&organization=JaredGold

#### State

https://reactjs.org/docs/hooks-state.html

Each time a state value is updated, the page reacts and re-renders the areas in the DOM that requires change. A state is a saved variable that can be changed and updated live. This is how react get's it's reactionary name.

A state is very useful with asynchronous functions as it can update the state when the function is finally complete. 

You can see below in class how states can be created using classes.

#### Class

A class can be used with states (Although we use functions instead). A class holds a constructor function which is similar to a initialization function which runs on the class being created, as well as a render function which will render and constantly be watched in the virtual DOM. A class looks as below:

```jsx
class App extends Component { // class name is a Component
	constructor(props){
		super(props)
		this.state = {latitude:null}  // state being created (This can be multiple lines)
	
		window.navigator.geolocation.getCurrentPosition(
			position => this.setState({latitude: position.coords.latitude}),
			error => console.log(error)
		)
	}

	render(){
		const {latitude} = this.state  // before getting the latitude this will be null
		return(
			<div>
				<h1>{latitude}</h1>
				<Clock date={new Date()} />
			</div>
		)
	}
}
```

#### LifeCycle Methods

The lifecycle method can be explained similarly to our lives. We do something the moment we are born, then we do something the moment we are teenagers and the moment we are adults and finally the moment we die. Lifecycle methods are methods that run at specific points in the apps lifetime.

https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

Constructor, render, componentDidMount, componentDidUpdate, componentWillUnmount

1. `componentDidMount` : runs after the first render
   - API calls
2. `componentDidUpdate` : this runs after subsequent renders, not the first render, provided prevState is different to the newState value
   - If there is any repetitive tasks this would be best place (like setInterval)
3. `componentWillUnmount` : runs towards the end of the component lifecycle
   - Clear any background task running for this component ( like clearInterval )







---

## Example:

```jsx
import React, {Component} from "react"
import Clock from "./Clock"

class App extends Component {
	constructor(props){
		super(props)
		this.state = {latitude:null, errorMessage: "", date: new Date()}
	}

	componentDidMount(){
		window.navigator.geolocation.getCurrentPosition(
			position => this.setState({latitude: position.coords.latitude}),
			error => this.setState({errorMessage: error.message})
		)
	}

	componentWillUnmount(){
		clearInterval(this.timerID)
	}

	tick(){
		this.setState({date: new Date()})
	}

	componentDidUpdate(prevState){
		if(prevState.date !== this.state.date){
			this.timerID = setInterval(() => this.tick(), 1000)
		}
	}

	isItWarm(){
		const {latitude} = this.state
		const month = new Date().getMonth()

		if(((month > 4 && month <=9 ) || latitude > 0) || ((month <= 4 || month > 9) && latitude < 0) || latitude === 0){
			return true
		}
		return false
	}

	getClockIcon(){
		if(this.isItWarm()){
			return "summer.png"
		}
		return "winter.png"
	}

	render(){
		const {latitude, errorMessage, date} = this.state
		return(
			<div>
				<h1>{latitude}</h1>
				{errorMessage || 
					<Clock 
						date={date} 
						icon={latitude ? this.getClockIcon() : null}
					/>}
			</div>
		)
	}
}

export default App

```







#### Increment a given amount

```jsx
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```







To get users geo location

```jsx
window.navigator.geolocation.getCurrentPosition(
  position => console.log(position),
  error => console.log(error)
)
```





