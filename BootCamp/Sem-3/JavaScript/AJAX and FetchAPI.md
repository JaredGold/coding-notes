# AJAX and Fetch API

* A web API is a way to access data on the web.
* We send a request to a URL (with AJAX) and the server sends us the required data (usually JSON) back.

#### What is AJAX

- AJAX stands for Asynchronous Javascript And XML
- Allows reloading only specific elements of the page instead of the entire page
- Applied to create fast, dynamic, and modern websites
- Not dependent on what browser it's running on
- Can send and receive information in various formats like JSON, XML, HTML and text files.

#### How it works

1. An event occurs in a web page (the page is loaded, a button is clicked...)
2. An XMLHttpRequest object is created by JavaScript
3. The XMLHttpRequest object sends a request to a web server
4. The server processes the request
5. The server sends a response back to the web page
6. The response is read by JavaScript
7. Proper action (like DOM element update) is performed by JavaScript

#### XMLHttpRequest Object (XHR)

Before the fetch() API was introduced, the only built-in way of doing AJAX in a browser was XHR.

```js
```

