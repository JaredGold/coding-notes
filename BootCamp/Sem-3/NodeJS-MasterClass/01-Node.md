# NodeJs

Node JS is a fairly new library for JavaScript used to work on the serverside. Javascript was initially created to run in browsers for websites only but was expanded in 2009 to work on servers. This allows for a much cleaner experience as a JavaScript developer.

NodeJS uses the event queue similar to the way our browsers work. Which allows us to do a tonne of requests in the shortest ammount of time.

Due to this we have the ability to use npm which allows us to use a lot of packages.

Node tends to be used to host API's or command line tools. With that you can also create cross platform desktop apps using **Electron** or mobile apps using **React Native**.

Docs can be found at https://nodejs.org/en/ or https://nodejs.org/docs/guides/ or https://nodejs.dev
https://nodejs.org/api/



#### Installing Node

To install node you can download and install node on the website (although this is not reccomended.) The best way to do this is to download a version manager so you can install multiple versions of node if required. We use NVM (node version manager.)

Follow the steps on https://github.com/nvm-sh/nvm (I would suggest Long-term support version)

To access node inside of the terminal you can simply write `node`



#### Write a webserver

When first writing a web server we need to use a http request so first we require the package http. You do this as below. (This example is using require although you can use the ES6 syntax of import and export). For more on HTTP read the docs (https://nodejs.org/api/http.html)

```js
const http = require('http'); // a package to allow you to use 
```

After using http we want to then create a port. It's important when writing this to allow for the port to be hardcoded OR the environments port. The environments port would be if you are hosting the app the server you've hosted it on's port that they have available.

```js
const port = process.env.PORT || 1337;
```

You could then ask about what process is. Process is a global object similar to `console`.
https://nodejs.org/api/globals.html#globals_process

We then need to actually create the server which we do by (you guessed it) another `const` this time passing in server code. This code takes a callback function that needs a `request`(req) and a `response` (res).

```js
const server = http.createServer((req, res) => {
  
})
```

From there we then need to pass some more code to tell it what is going on with the server. We do this as below and explained line by line.

```js
const server = http.createServer((req, res) => {
  res.statusCode = 200; // default success status code
  res.setHeader('Content-Type', 'text/plain'); // what you will receive this can be HTML
  res.end('Hi!'); // after the response end (IMPORTANT) passing the Hi is just a fun thing you can do.
})
```

Even though this server was created we still need to actively be listening for specific requests ('/' and/or 'get'). To do this we have a line under listening on the port.

```js
server.listen(port, function() {
  console.log(`Server listening on port ${port}`)
})
```

If you want to return JSON instead of plain text you would do this by changing what is in the createServer section in the header.

```js
const server = http.createServer((req, res) => {
  res.statusCode = 200; 
  res.setHeader('Content-Type', 'application/json'); // changed for JSON
  res.end(JSON.stringify({ message: 'Hi!' })); // the response needs to be JSON
})
```



