# Memoza

### Description

Like `_.memoize` this one allows to cache functions and
store the results on the filesystem or any other cache which provides
 `.get(key)`, `.set(key, data)` methods.

### Configuration
```javascript
const memoza = require('node-memoza');
const wrapper = memoza({ cache: { path: cachePath } });
```

 1. Remembers cb's arguments
 ```javascript
 const func = (param1, cb) => {
  setTimeout(() => { cb(param1); }, 10000);
 }
 const wrapped = wrapper(func);
 wrapped(1234, (param) => console.log(param)); //will log "1234" in 10 seconds
 // ...once cb called
 wrapped(1234, (param) => console.log(param)); //will log "1234" without delay
 ```

 2. Remembers Promise resolution value

 ```javascript
const func = (param1) => {
  return new Promise((resolve) => {
    setTimeout(() => { resolve(param1); }, 10000);
  });
 }
 const wrapped = wrapper(func);
 wrapped(1234).then((param) => console.log(param)); //will log "1234" in 10 seconds
 wrapped(1234).then((param) => console.log(param)); // ...once promise has been resolved it will log "1234"
 ```
