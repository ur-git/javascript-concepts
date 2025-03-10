# JavaScript Closures

Closures are one of the most fascinating and sometimes misunderstood features of JavaScript. Understanding closures requires a solid grasp of concepts like **execution context**, **call stack**, and **scope chain**, as closures bring all of these concepts together in a powerful way.

Closures in JavaScript are created due to two primary concepts:

- **Functions**
- **Lexical Scope**

### Key Definitions

- **Formal Definition:** A closure is the closed-over variable environment of the execution context in which a function was created, even after that execution context is gone.
- **Simpler Definition:** A closure allows a function to remember and access variables from its parent scope, even after the parent function has finished execution.

### Key Characteristics of Closures

- Closures **happen automatically** in JavaScript; they are not something you manually create.
- They are **internal properties** of functions and cannot be explicitly accessed.
- Variables in a closure are preserved in memory and cannot be garbage collected as long as the closure exists.

---

## How Closures Work

### Example Walkthrough

```javascript
function secureBooking() {
  let passengerCount = 0;

  return function () {
    passengerCount++;
    console.log(`${passengerCount} passengers`);
  };
}

const booker = secureBooking();
booker(); // 1 passengers
booker(); // 2 passengers
booker(); // 3 passengers
```

### Step-by-Step Breakdown

1. **Creating the Closure:**

   - When `secureBooking` is called, it creates the `passengerCount` variable and returns an inner function.
   - The inner function is stored in the `booker` variable.

2. **Memory Management:**

   - Once `secureBooking` finishes execution, its execution context is removed from the call stack.
   - However, the variable environment (containing `passengerCount`) is preserved in memory because the returned inner function still references it.

3. **Using the Closure:**
   - Every time `booker` is called, it increments `passengerCount` and logs it.
   - The closure allows `booker` to access `passengerCount`, even though `secureBooking`'s execution context is gone.

### Why Does This Happen?

- JavaScript functions always retain access to the **variable environment** of the context in which they were created.
- This connection is what we call a closure.

---

## Behind the Scenes

### Call Stack and Scope Chain

- When `secureBooking` executes, a new execution context is created and pushed onto the call stack.
- Its local variables (like `passengerCount`) are stored in its **variable environment**.
- After `secureBooking` returns, its execution context is popped off the stack, but the variable environment remains in memory due to the closure.

### Memory and Garbage Collection

- Normally, variables are garbage collected once they are no longer reachable.
- In the case of closures, the variable environment remains in memory because the returned function keeps referencing it.

---

## Practical Applications of Closures

1. **Data Encapsulation:**

   - Closures allow variables to be private and inaccessible from the outside.

   ```javascript
   function createCounter() {
     let count = 0;

     return function () {
       count++;
       console.log(count);
     };
   }

   const counter = createCounter();
   counter(); // 1
   counter(); // 2
   ```

2. **Event Listeners:**

   - Closures are often used in event handlers to retain state.

3. **Function Factories:**

   - Create functions dynamically with pre-set behavior.

   ```javascript
   function multiplier(factor) {
     return function (number) {
       return number * factor;
     };
   }

   const double = multiplier(2);
   console.log(double(5)); // 10
   ```

4. **Memoization:**

   - Store computed results for faster access.

   ```javascript
   function memoize(fn) {
     const cache = {};

     return function (arg) {
       if (cache[arg]) return cache[arg];
       const result = fn(arg);
       cache[arg] = result;
       return result;
     };
   }

   const square = memoize((x) => x * x);
   console.log(square(4)); // 16
   console.log(square(4)); // 16 (from cache)
   ```

---

## Observing Closures

### Using `console.dir`

To inspect the closure associated with a function, use `console.dir()`:

```javascript
console.dir(booker);
```

- Look for the `[[Scopes]]` property in the console output.
- This shows the variable environment that the function has access to via the closure.

---

## Important Notes

1. **Closures are Everywhere:**

   - Even if you don’t realize it, closures are at work in many common JavaScript patterns.

2. **Performance Considerations:**

   - Be mindful of closures in performance-critical code as they can lead to higher memory usage.

---

## Summary

- A closure allows a function to "remember" the variables of its parent scope, even after the parent function has finished executing.
- Closures are created automatically in JavaScript; you don’t need to do anything special to create them.
- They are used for data encapsulation, event handling, dynamic function creation, and more.
