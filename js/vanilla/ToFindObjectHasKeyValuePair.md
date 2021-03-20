# To Find whether the Object has Key Value Pair

In Javascript, Object has some additional prototype methods like key, which returns the boolean for the key.

### `hasOwnProperty`

```js
const obj = {
  t1: 'test1',
  t2: 'test2'
}

console.log(obj.hasOwnProperty('t1'))
// OUTPUT: true

console.log(obj.hasOwnProperty('t3'))
// OUTPUT: false
```

***

### Polyfill

```js
;(function(hasOwnProp) { // IIFE with guarding semicolon
  function hasOwnProperty(name) {
    if (this == null) { throw new TypeError("Cannot convert undefined or null to object!") }
    var O = Object(this), key = String(name);
    var _proto = O.__proto__ || O.constructor.prototype || {}; // Object.prototype
    return key in O && ( !(key in _proto) || O[key] !== _proto[key] );
  }
  if (!hasOwnProp) {
    try {
      Object.defineProperty( Object.prototype, 'hasOwnProperty', {
        enumerable: false, configurable: true, writable: true,
        value: hasOwnProperty
      });
    } catch (e) { // Object.defineProperty isn't supported
      Object.prototype['hasOwnProperty'] = hasOwnProperty;
    }
  }
})(Object.prototype.hasOwnProperty);
```
