# Function Polyfill

## Fundamentals for Any Polyfill

1. **Check if the method exists first**

   ```js
   if (!Array.prototype.map) {
     // define polyfill
   }
   ```

2. **Work with `this`**

   - If the method is from a prototype (like `map`, `filter`), then inside your polyfill, `this` refers to the array/string/object the method is called on.
   - If it’s a static method (like `Promise.all`, `Object.assign`), you don’t use `this`, but parameters.

3. **Mimic native behavior**

   - Follow the **spec basics**: arguments, return value, and edge cases.
   - Example: `map` takes a callback and an optional `thisArg`.

4. **Use simple loops or core JS methods**

   - Most polyfills boil down to `for` loops or `for..of`.

5. **Handle edge cases**

   - If callback is not a function → throw error.
   - If array is empty → return an empty array.
   - If something is `null` or `undefined` → throw TypeError.

6. **Return the correct type**

   - Array methods usually return a **new array** (e.g. `map`, `filter`).
   - Some modify the original (e.g. `forEach` just iterates, no return).
   - Promise methods return a **new Promise**.

## Polyfills Examples

- Array.prototype.map
- Array.prototype.filter
- Array.prototype.reduce
- Array.prototype.forEach

  ```js
  Array.prototype.myForEach = function (callback) {
    if (typeof callback !== "function") {
      throw new TypeError("callback not a function");
    }

    let arr = this;

    for (let i = 0; i < arr.length; i++) {
      if (i in arr) {
        callback.call(this, arr[i], i);
      }
    }
  };

  let num = [1, 2, 3, 4, 5];

  num.myForEach(function (element, index) {
    console.log(`${element} , ${index}`);
  });
  ```

- Array.prototype.find
- Function.prototype.bind
- Function.prototype.call
- Function.prototype.apply

```

```
