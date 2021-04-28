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

---

### DOM Objects

[Handling Events :: Eloquent JavaScript](https://eloquentjavascript.net/15_event.html)

In the event handler you can use `window` to access the entire browser window. For example the below will log "You knocked?" when the browser window is clicked.

```js
window.addEventListener("click", () => {
  console.log("You knocked?");
});
```

#### One Time button

```js
let button = document.querySelector("button");
function once() {
  console.log("Done.");
  button.removeEventListener("click", once);
}
button.addEventListener("click", once);
```

The above can only be pressed once as after it is clicked the event listener for click is removed.

#### Event Propagation

Event Propagation is that when a child element and a parent element have a click event it will first run the object clicked but then it will continue to go outward. For example a button inside of a `<p>` tag will press the button first then run the p tag code, then the body code, then the html code. This could mean a bunch of click events get pressed although unneeded. The below is a way to stop this.

###### `stopPropagation()`

```html
<p>A paragraph with a <button>button</button>.</p>
<script>
  let para = document.querySelector("p");
  let button = document.querySelector("button");
  para.addEventListener("mousedown", () => {
    console.log("Handler for paragraph.");
  });
  button.addEventListener("mousedown", event => {
    console.log("Handler for button.");
    if (event.button == 2) event.stopPropagation();
  });
</script>
```

#### One class for multiple buttons

```html
<button>A</button>
<button>B</button>
<button>C</button>
<script>
  document.body.addEventListener("click", event => {
    if (event.target.nodeName == "BUTTON") {
      console.log("Clicked", event.target.textContent);
    }
  });
</script>
```



#### Keypress

```html
<p>This page turns violet when you hold the V key.</p>
<script>
  window.addEventListener("keydown", event => {
    if (event.key == "v") {
      document.body.style.background = "violet";
    }
  });
  window.addEventListener("keyup", event => {
    if (event.key == "v") {
      document.body.style.background = "";
    }
  });
</script>
```

