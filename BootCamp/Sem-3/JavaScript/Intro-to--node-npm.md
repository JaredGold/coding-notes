# NodeJS

JS runs in terminal and the browser.

#### NodeJS terms

- npm (or yarn) is the node package manager
- package.json is the main configuration file
- package-lock.json keeps a record of all package versions
- node_modules directory stores the code for each package



## Create node project

- `npm init` creates the file giving options to create the node project

- to skip the options use `npm init -y` to use default config

- you can then open it up `code .`

- change the order of where scripts run using the package.json and adding 
  `start: node index.js` to run the index.js file

- `npm i lorem-ipsum` allows you to install the lorem ipsum package

- `npm i` is telling you to install the js package.

- to use the loremIpsum you have to call it in the script you want

  ```js
  const loremIpsum = require('lorem-ipsum').loremIpsum;
  const sentence = loremIpsum();
  console.log(sentence)
  ```

  

