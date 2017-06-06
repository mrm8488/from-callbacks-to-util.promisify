# From callbacks to util.promisify
We can see the evolution from callbacks to promises. New Node.js 8 feature **'util.promisify()'** alllow us to convert I/O functions that return callbacks into I/O functions that return promises.
We could promisify I/O functions before Node 8 with third party modules such as [bluebird](https://www.npmjs.com/package/bluebird) or [Q](https://www.npmjs.com/package/q).

```js
/* AUTHOR: mrm8488@gmail.com */
const fs = require('fs');

/* BEFORE util.promisify() */

fs.writeFile('/tmp/test.js',"console.log('Hello world');", error => {

	if(error) return console.log(error);

	return console.log('file created successfully!')
});



/* BEFORE util.promisify() handcrafted promise */

const writeFilePromise = (file, data) => {

	return new Promise((resolve,reject) => {

		fs.writeFile(file ,data, error => {

			if(error) reject(error);

			resolve('file created successfully with handcrafted Promise!')
		});
	});
}

writeFilePromise('/tmp/test2.js', "console.log('Hello world with handcrafted promise!');")

.then(result => console.log(result))

.catch(error => console.log(error));



/* WITH util.promisify() (Node.js 8) */

const util = require('util');

const writeFile = util.promisify(fs.writeFile);

writeFile('/tmp/test3.js',"console.log('Hello world with promisify!');")

.then(() => console.log('file created successfully with promisify!'))

.catch(error => console.log(error));
```

## Thanks!
![](https://media.giphy.com/media/jUwpNzg9IcyrK/giphy.gif)
