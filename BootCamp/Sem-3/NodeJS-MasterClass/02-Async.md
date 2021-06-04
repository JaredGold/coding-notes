# NodeJs Async

JS was built deliberately to allow multiple things happening in the background. It was only single threaded but it is non blocking, which means while something is happening it can put it off to the operating system and then when the operation is complete it will insert itself back into the queue. This is using promises.

So to do this to node js we would have to start with the below.

```js
const fs = require('fs'); // file system

const filename = 'callbacks-01.js';

fs.readFile(filename, (err, fileData) => {	// takes an error and the fileData
  if(err) console.error(err);
  console.log(`${filename}` : ${fileData.length})
})		// comes second

fs.readdir('/', (err, files) => {
  if (err) console.error(err)
  console.log(files);
})		// comes first
```

To fix the above code we want to make these promises or async await.

```js
const fs = require('fs').promises;

fs.readdir('./') // because this is a promise it returns a promise
	.then(fileList => {
  	return Promise.all( // waits for all Promises to be complete
    	fileList.map(file => fs.readFile(file).then(data=> [file, data.length]))
    )
})
	.then(results => {
  	results.forEach({file, length} => console.log(`${file} : ${length}`));
		console.log('done!');
})
```

Incase there is an error that will throw the program it is still important to have a catch.

```js
const fs = require('fs').promises;

fs.readdir('./') // because this is a promise it returns a promise
	.then(fileList => {
  	return Promise.all( // waits for all Promises to be complete
    	fileList.map(file => fs.readFile(file)
                   .then(data=> [file, data.length])
                   .catch(err => [file, 0]))	// good to catch an error
    )
})
	.then(results => {
  	results.forEach({file, length} => console.log(`${file} : ${length}`));
		console.log('done!');
})
```

While this is good it would be much better to write this as an asynh function!



---

```js
const fs = require('fs').promises;
printLengths('./')

// async function printLengths(dir)  // another accepted way to write this

const printLengths = async (dir) => {
  const fileList = await fs.readdir(dir)		// await a resolved response
  const results = await Promise.all(
    //fileList.map(file => fs.readFile(file)
			//.then(data=> [file, data.length])
			//.catch(err => [file, 0]))
    fileList.map(async file => {
      try{
      	let data = await fs.readFile(file);
      	return [file, data.length];
      } catch (err) {
        return [file, 0];
      }

    })
  )
  results.forEach(([file, length]) => console.log(`${file}: ${length}`));
  console.log('done!');
}
```

