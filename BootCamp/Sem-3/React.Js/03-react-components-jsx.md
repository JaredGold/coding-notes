# React Components

To add an inline style to a text in jsx you have to pass through an object. This object still needs to be interpolated using curly braces. This looks as bellow: (of course this is not clean/DRY)

```jsx
<p style={{ color: "red" }}>{MESSAGE}</p>
```

 If you create a component that requires data to be passed into it through another component you would do so by calling it with an equal sign and then what you are passing. 
`<Comment author="Jared Goldstein" />` then in the Comment component you would retrieve it by adding props in to the function.

```jsx
const Comment = (props) => {
    // code using props.author here
}
```

