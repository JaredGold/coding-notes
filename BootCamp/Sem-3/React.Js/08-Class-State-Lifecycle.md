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











To get users geo location

```jsx
window.navigator.geolocation.getCurrentPosition(
  position => console.log(position),
  error => console.log(error)
)
```

