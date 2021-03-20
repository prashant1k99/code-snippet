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
for (const el of Object.keys(obj)) {
  // Logic here, eg. if(obj[el] === 'test')
}
```

**Method 2**
```js
Object.keys(obj).forEach((el) => {
  // if (obj[el] === 'test') {
  //   return logic
  // }
})
```
***

### Polyfill:
```js
// From https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys
if (!Object.keys) {
  Object.keys = (function() {
    'use strict';
    const hasOwnProperty = Object.prototype.hasOwnProperty,
        hasDontEnumBug = !({ toString: null }).propertyIsEnumerable('toString'),
        dontEnums = [
          'toString',
          'toLocaleString',
          'valueOf',
          'hasOwnProperty',
          'isPrototypeOf',
          'propertyIsEnumerable',
          'constructor'
        ],
        dontEnumsLength = dontEnums.length;

    return function(obj) {
      if (typeof obj !== 'function' && (typeof obj !== 'object' || obj === null)) {
        throw new TypeError('Object.keys called on non-object');
      }

      const result = [], prop, i;

      for (prop in obj) {
        if (hasOwnProperty.call(obj, prop)) {
          result.push(prop);
        }
      }

      if (hasDontEnumBug) {
        for (i = 0; i < dontEnumsLength; i++) {
          if (hasOwnProperty.call(obj, dontEnums[i])) {
            result.push(dontEnums[i]);
          }
        }
      }
      return result;
    };
  }());
}
```
