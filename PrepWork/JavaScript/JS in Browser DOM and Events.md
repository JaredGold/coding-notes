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

