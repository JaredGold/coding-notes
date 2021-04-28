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
// create the XHR object
let request = new XMLHttpRequest();
// Open specifies the main paramaters of the request
// open(method, URL, [async, user, password])
// open does not open the connection but it configures the request
request.open('GET', 'json_example.json')
```

* We define a callback function that will execute when the request is completed and assign it to the onload property.

* We could also assign this with `request.addEventListener("load", callback)`

* This callback function will process the data returned in the request, typically making some updates to the DOM using Javascript:

  ```js
  request.onload = function () {
      console.log(JSON.parse(this.response))
  }
  ```

After all of this we need to send the request

```js
request.send();
```

### Example:

```js
document.querySelector(".btn").addEventLinstener("click", getUserData);
function getUserData() {
    console.log("starting request");
    
    let request = new XMLHttpRequest();
    request.open('GET', 'https://randomuser.me/api/', true);
    request.onload = () => {
        if (request.status >= 200 && request.status < 400) {
            console.log(request.responseText);
        } else {
            console.log("Error");
            console.log(request);
        }
    };
    request.onerror = () => {
        console.log("Connection error");
    };
    request.send();
};
```



## Using AJAX with jQuery

- jQuery is a popular JavaScript library (less popular now because of frameworks like React, Vue and Angular)

- jQuery is supported on browsers.

- Can be downloaded or used with jQuery CDN

  ```html
  <head>
      <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js">		</script>
  </head>
  ```

- jQuery provides us a cleaner syntax and a straightforward implementation

- Same as most modern AJAX libraries, jQuery's AJAX is built on top of XHR requests.

- They are just there to abstract away the complexity

#### Example as above:

```js
function getUserData() {
    console.log("starting request");
    $.ajax({
        url: 'https://randomuser.me/api/',
        type: 'GET',
        success: (data) => {
            console.log(data):
        },
        error: (error) => {
            console.log("Error");
            console.log(error)
        }
    });
}
```

## Fetch API

- The fetch API is just another way to do the same thing that we can do with XHR
- It uses Promises instead of callbacks which has made it very popular and can be easier to use
- Fetch is the standard for AJAX in modern browsers.

```js
let pokeFetch = fetch(pokemonUrl)
	.then((response) => response.json())// returns a promise
	.then((data) => {console.log(data)}) // handles the data and runs a function
	.catch((error) => {console.log(`error: ${error}`)// handles the errors
```

