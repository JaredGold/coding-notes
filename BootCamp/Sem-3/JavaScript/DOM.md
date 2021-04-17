# JS Dom

The DOM is a document modification method. 

DOM is used to modify html documents. 

You have to add the script element in HTML in order to access the JS file.

In order to select an object in HTML in the JS file you write

`document.querySelector("h1")` 

`document.querySelector(".class")`

`document.querySelector("#id")`

There is a lot you can do to the object afterwards.

```js
document.querySelector("h1").innerHTML = 'New Text' // - changes the html to New Text

document.querySelector("h1").style.color = "red"  //changes the font color to red

document.querySelector("h1").style.color = "#00FF00" // changes the font color to green

//------------------------------------------------------------------------------//

document.querySelectorAll("li")	 // to select all of the list items as an array
```

You can also create elements in the dom

```js
let x = document.createElement("p");

x.innerHTML = "Lorem Ipsum"		//changes the p value but the p value is not iactually in the doc

document.body.appendChild(x) 	// adds x to the body
document.body.RemoveChild(ul)	// removes the ul's
```



---

## Practice Dom from Udemy

# Browser use

#### Selecting class in html file

`document.querySelector()` allows you to select some element in the document the script is loaded on.

`document.querySelector('.message')`
`document.querySelector('#message')`

```js
console.log(document.querySelector('.message').textContent);
// this logs the item of class message text content

document.querySelector('.message').textContent = 'change';
// this will change the class message text content to 'change'

document.querySelectorAll('.message');
// this selects all elements with class message
```



## DOM

DOM is **Document Object Model**: Structured representation of HTML documents. This allows javascript to access HTML elements and styles to manipulate them.

You interact with the page through the `document`. Everything under it is similar to a tree object starting with `<html>` then `<head>` or `<body>` and so on.

DOM and `document.querySelector()` is not default in JS it is specifically a web browser language (WEB APIs).

#### Selection

To select we use the `querySelector` and the class but to find the content inside of that we need to use different code.

```js
document.querySelector('.message').textContent;
// this gets the text content
document.querySelector('.guess').value;
// this gets the <input> content

```

To change styles you change the `.style` in the query selector. Note that the amount or the change is always a string.

```js
document.querySelector('body').style.backgroundColor = '#60b347';
// changes background color of the entire body

document.querySelector('.number').style.width = '30rem';
// changes font width of the .number class
```



#### Event Listener

An event listener is a line of code that waits to hear something specific happen on the webpage (a button).

```js
document.querySelector('.check').addEventListener('click', function(){});
// first we select the correct class, then we add an event listener which is listening for when it is 'click'ed. After it is clicked it will run whatever function is passed.
```



#### Class List

To change and update the classes on a selected element you can do so using the `.classList` selector.

```js
const modal = document.querySelector('modal');

btn.addEventListener('click', function(){
    modal.classList.remove('hidden');
})

// removes the class hidden from the line with the .modal class.

const closeModal = function () {
  modal.classList.add('hidden');
  overlay.classList.add('hidden');
};

// function to add classes
```



### Event Listener

Adding an event listener is how we have  previously accessed an event listener on a specific tag although we can do this on the document. 

```js
document.addEventListener('keydown', function(event){
    console.log('hello world')
})

// you could also call event `e` to make it easier
```

An event listener is also an object which allows for you to take some information from it. So in the above `keydown` whenever we press a key you could pass a variable in the function such as event to track what was passed in that event. 



### `class` removal

```js
let title = document.querySelector("h1")

title.classList.add("blue")
title.classList.remove("blue")
title.classList.toggle("blue")
```



---

## More Dom Examples

```js
let form = document.getElementById("page-form")
console.log(form)

let allParagraphs = document.getElementsByTagName("p")
console.log(allParagraphs)

let odds = document.getElementsByClassName("odd")
console.log(odds)
```

```js
// Here we are creating a new list element
let newLi = document.createElement("li")
newLi.textContent = "new li"
document.querySelector("ul").appendChild(newLi)
```

```js
let li1 = document.querySelectorAll("li")
let li2 = document.getElementsByTagName("li")

console.log(li1)
console.log(li2)

// Here we are creating a new list element, we'll go over this in more detail.
let newLi = document.createElement("li")
newLi.textContent = "new li"
document.querySelector("ul").appendChild(newLi)

console.log(li1)	// shows 4 elements
console.log(li2)	// shows all 5 elements << updates regularly
```



#### Remove attributes

```js
let ul = document.querySelector("ul")
let li1 = ul.children[0]
ul.removeChild(li1)

let li2 = document.querySelector("li")
li2.parentNode.removeChild(li2)

```



#### Modify Attributes

```js
let formButton = document.querySelector("input[type=submit]")

console.log(formButton.value)

formButton.value = "Don't click me!"

//We can assign multiple attributes at once using Object.assign()

Object.assign(formButton, {
    id: "form-button",
    value: "ok you can click"
})
```



### `window.getComputedStyle`

This method on the window object gets the currently applied style for the specified node, no matter how that style was applied. The currently computed style values based on the applied CSS and any DOM manipulations in JavaScript is returned.

```js
title = document.querySelector(".title")
window.getComputedStyle(title).getPropertyValue("color") //==> "rgb(255,0,0)"

title.classList.add("blue")
window.getComputedStyle(title).getPropertyValue("color") //==> "rgb(0,0,255)"

title.style.color = "purple"
window.getComputedStyle(title).getPropertyValue("color") //==> "rgb(128,0,128)"

title.style.color = ""
window.getComputedStyle(title).getPropertyValue("color") //==> "rgb(0,0,255)"

title.classList.remove("blue")
window.getComputedStyle(title).getPropertyValue("color") //==> "rgb(255,0,0)"
```





---

### Ed Challenges

##### Querying the Dom

```js
function findAllAnchors() {
	let allAnchors = document.querySelectorAll("a");
	return allAnchors;
}

function findFirstH3() {
	let firstH3 = document.querySelector("h3");
	return firstH3;
}

function findAllTextBlocks() {
	// There is a class called 'text-block'
	let textBlocks = document.getElementsByClassName("text-block");
	return textBlocks;
}

function findAllNestedParagraphs() {
	// There is a div with the id "zen-requirements"
	// return all the paragraph elements inside that div
	let zenRequirementParagraphs = document.getElementById("zen-requirements").querySelectorAll("p");
	return zenRequirementParagraphs;
}

function findTheFooter() {
	let footer = document.querySelector("footer");
	return footer;
}
```

