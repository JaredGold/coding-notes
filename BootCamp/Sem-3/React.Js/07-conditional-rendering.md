# Conditional Rendering

A conditional rendering is using a control structure (if statements etc.) to render specific things if certain conditions are true or false.

With conditional rendering in react there are multiple more falsey values, but the main ones are false, null and ""

Below is a conditional rendering basics. If the loading is true then it will show loading. When loading is false it will return a different statement. This is the basics on how we make conditional rendering.

```jsx
const Main = () => {
    const name ="Jared"
    const loading = true
    
    if(loading) {
        return <main><h1>Loading...</h1></main>
    } else {
        return <main><h1>My name is {name}</h1></main>
    }
}
```

The best way to really see this is if you are using an API and you are waiting for the fetch request to finish. This tends to be used in State's.

Similarly as above below is a cleaner ternary version.

```jsx
const Main = () => {
    const name ="Jared"
    const loading = true
  
  	return loading ? null : (
    	<main>
            <h1>My name is {name}</h1>
        </main>
    )
}
```

#### Short Circuit

Alternate from the above we can do short circuit logic. A short circuit logic is only going to return if both elements are true. In the below example in order for the main elements to be in view loading has to be true.

```jsx
const Main = () => {
    const name ="Jared"
    const loading = true
    
    return loading && (
    	<main>
        	<h1>Hi my name is {name}</h1>
        </main>
    )
}
```

Alternatively if you wanted to do as the first example and return text inside of the main we can do so as below.

```jsx
const Main = () => {
    const name ="Jared"
    const loading = true
    
    return (
    	<main>
        	{loading ? (
            	<h1>Loading...</h1>
            ) : (
            	<h1>Hello my name is {name}</h1>
            )}
        </main>
    )
}
```



## Looping Through Array

To loop through an array you need to use a map function as it returns something, where a for loop does not. Below is an example of how you could do this with a list objects.

```jsx
const Main = () => {
    return(
    	<div>
        	<h1>Star Wars Char's</h1>
            {characters.map((character) => {
                return (
                	<div className="character">
                    	<h3>Name: {character.name}</h3>
                    </div>
                )
            })}
        </div>
    )
}
```

In react it is important that while you map through elements you pass in a key element. This key is a unique number that each object holds. It is normally best to do this as a number attached to the object in the actual array, although you can also do this with the index value as seen below.

```jsx
{characters.map((character, index) => {
  return (
    <div className="character" key={index}>
      <h3>Name: {character.name}</h3>
    </div>
  )
}
```

#### Conditional rendering in array loop

To do conditional rendering you may have an object that does not hold an element. You can say in the loop a conditional expression: (Note use an alt tag as well)

```jsx
{characters.map((character, index) => {
  return (
    <div className="character" key={index}>
      <h3>Name: {character.name}</h3>
      {character.pic ? (
        <img src={character.pic}>
      ) : (
        <h4>No Image Found</h4>}
      )
    </div>
  )
}
```

Note you can use any conditional expression as we saw above.