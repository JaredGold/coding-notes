# React Context (global sate)

https://www.youtube.com/watch?v=rFnfvhtrNbQ

#### Why Context?

* It gives us a way to make values accessible by any component without having to pass them as props.
* It is intended to be used for values that are considered 'global' for a tree of React components
* An alternative to using something complicated like Redux to suit simpler use cases.

#### Common applications

Some common uses of React Context are:

* UI theme (light mode/dark mode)
* User authentication (the currently authenticated user)
* User preferences (language, currency, etc)

#### Context vs Props

Using props, the theme value has to be explicitly passed to each component that needs it. This is convenient if you want to control which components need that prop. This is inconvenient if it is a variable that multiple components need everywhere.

Using context, the theme value is provided at the top of the component tree, and can be accessed by any descendent component. Just like with props, context consumers can only access the value, not change it.

#### React Context

We define the **provider** of a value at the top of the component tree that uses it, and then **consumers** of that value will be re-rendered when the value is updated by the provider.

```jsx
const myContext = React.createContext();

<MyContext.Provider value={*/some value */}?
    // components using context value here
</MyContext.Provider>
```

#### useContext hook

Components using a context value access the value with the `useContext` hook

```jsx
const MyContext = React.createContext()

useContext(MyContext)
```

Every update to the context value will result in a re-render of the component using it.

---

# Global State

#### What is global state?

Global state refers to application state that is available to components throughout a component tree without passing props

We learned about using React Context to provide individual global state values (like theme, logged in user and user preferences)

Used with a reducer, Context can be used to provide Redux-like global state.

#### Why do we want it?

Global state addresses the problems caused by **prop drilling**

**Prop drilling** refers to using props to access and update application state values from multiple components at different levels in the component tree, including components that don't use the props.

In even moderately complex applications, this can create a lot of confusing and inefficient code. 

#### Why not use it all of the time?

Global state can quickly become confusing and hard to maintain as an application grows

* Becomes difficult to find where state values are initialized, used and modified

If state is only used by a component and it's direct descendants, local state is almost always the right choice - because it is simple and  (BLOCKED BY A CAMERA...).

#### Implementing global state with Context

By using a Context Provider that provides both he store and dispatch function returned by `useReducer`, we can provide a way to access and change application state to all children of the Provider



#### Example:

A good way to set the global state is to `useReducer`. 

This can be provided in another file and then imported in our App.js to be used in our reducer

```jsx
import {createContext, useContext} from 'react'

export const StateContext = createContext()

// useContext(StateContext) // used to access the global state (Below is a hook)

export const useGlobalState = () => useContext(StateContext)
```



Any child inside of the `StateContext.Provider` will be able to access the values inside of `value`

```jsx
<StateContext.Provider value={{store, dispatch}}>
	<Heading>Colour Tester</Heading>
	<MessageField message={message} setMessage={setMessage}/>
	<MessageCard message={message} textColour={textColour} cardColour={cardColour}/>
	<ColourChoicePanel textColour={textColour} cardColour={cardColour} setTextColour={setTextColour} setCardColour={setCardColour}/>
</StateContext.Provider>
```

