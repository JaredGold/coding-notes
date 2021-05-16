# Unit Testing w/ Jest

Jest is a testing framework used in js.
Jest will look for any file with the word test in it and then run that file

#### Steps to create and use Jest

1. `npm init -y` create project
2. create the start entry point in `"scripts"` `"start": "node index.js"`
3. create index.js file
4. create a directory called src and a directory called test to future proof.
5. In src create a file called `inches-to-cm.js`
6. create the function (bellow)
7. in the test directory create a file called `inches-to-cm.test.js`
8. create the tests as you can see below
9. install jest `npm i jest`
10. in the package.json file change `"test":` to `"test": "jest",`
11. run test `npm run test`



#### `inches-to-cm.js`

```js
function inchesToCm(inches){
    const cm = inches * 2.54
    return cm
}

module.exports = {
    inchesToCm
}
```

#### `inches-to-cm.test.js`

```js
const {inchesToCm} = require('../src/inches-to-cm')

describe('inchesToCm', () => {
    it('converts from inches to cm', () =>{
        expect(inchesToCm(1)).toBe(2.54)
        expect(inchesToCm(2)).toBe(5.08)
        expect(inchesToCm(4)).toBe(10.16)
    })
})
```





## How to send require a function from another file

#### `index.js`

```js
const { hello } = require('./src/hello')
hello()
```

#### `hello.js`

```js
function hello(){
    console.log('hello world!!!!')
}

module.exports = {
    hello
}
```

