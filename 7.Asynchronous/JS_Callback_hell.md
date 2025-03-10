# Callback Hell

So basically, callback hell is when we have a lot of nested callbacks in order to execute asynchronous tasks in sequence.And in fact, this happens for all asynchronous tasks, which are handled by callbacks.

Example of **callback hell**:

```javascript
setTimeout(() => {
  console.log("1 second passed");
  setTimeout(() => {
    console.log("2 seconds passed");
    setTimeout(() => {
      console.log("3 seconds passed");
    }, 1000);
  }, 1000);
}, 1000);
```

This **nested structure** makes code **hard to read, maintain, and debug**.
