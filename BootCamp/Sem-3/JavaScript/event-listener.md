# Event Listener

https://developer.mozilla.org/en-US/docs/Web/Events - _All the diff events_

An Event listener is the script telling you to wait for a specific even to happen on a specific object in the DOM.

```js
const el = document.querySelector('.btn')
el.addEventListener('click', () => {
    el.style.color = "green"
})
```

You can remove an event listener as below

```js
const el = document.querySelector('.btn')
let count = 0
el.addEventListener('click', function(e){
    if (count >=3) {
        // at 3 clicks the event listener will be removed and no longer used
        el.removeEventListener('click');
    } else {
        count++;
        alert(`Times clicked: ${count}`)
    }
})
```

---

### `event.preventDefault()`

Sometimes a default event can occur when pressing specific buttons on a website. For example a form will have a bunch of defaults. We can circumvent the default and remove it as below.

```js
const el = document.querySelector('#signup-form')

el.addEventListener('submit', function(event){
    event.preventDefault()
})
```



---

### `event.target`

This allows us to place a handler on a large amount of objects but specifically look for the specific one that has been pressed.

```html
<input id="username" type="text">
```

```js
const userName = document.querySelector('#username')

userName.addEventListener('input', function(event) {
    console.log(event.target.value)
})
```

The event object passes multiple different objects. Below will show you exactly what is passed in. This is only showing what the `'click'` event is passing. There are different things passed by different events, e.g. `'keypress'`.

```js
let myButton = document.querySelector("input[type=submit]")

// Must include event in the callback function parameter list to use it
myButton.addEventListener("click", function(event) {
    event.preventDefault()
    console.log(event)
})
```

You can also access the target node that the event was fired on.

```js
let myButton = document.querySelector("input[type=submit]")

// Must pass event through the callback function
myButton.addEventListener("click", function(event) {
    event.preventDefault()
    console.log(event.target)
})
```

You can also then view the target attributes and values as below.

```js
let myButton = document.querySelector("input[type=submit]")

// Must pass event through the callback function
myButton.addEventListener("click", function(event) {
    event.preventDefault()
    event.target.value = "You clicked!"
})

// event.target.style.backgroundColor = "blue"
```

