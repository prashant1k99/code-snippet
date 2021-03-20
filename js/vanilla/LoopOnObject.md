# Loop On Objects

In Javascript, Object has some additional prototype methods like key, which returns the array of keys. So looping can be easily done on that.

### Example:
```js
const obj = {
  t1: 'test',
  t2: 'test2'
}

console.log(Object.keys(obj))
// OUTPUT: [ 't1', 't2' ]
```
So, now we can easily run for loop on that:
```js
for (const k of Object.keys(obj)) {
  // Logic here, eg. if(obj[k] === 'test')
}
```
