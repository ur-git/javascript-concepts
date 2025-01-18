# JavaScript: First-Class Functions and Higher-Order Functions

## First-Class Functions

### Definition
JavaScript has **first-class functions**, meaning that functions are treated as **first-class citizens**. This is a fundamental property of the language.

### Key Characteristics
1. **Functions are values**:
   - Functions can be treated like any other value (e.g., numbers, strings).
   - Functions can be stored in variables or object properties.

2. **Functions as objects**:
   - Functions are a special type of object in JavaScript.
   - Since objects are values, functions are values too.

### Practical Examples
- **Storing Functions**:
  ```javascript
  // Function expression stored in a variable
  const greet = function () {
    console.log('Hello!');
  };

  // Function stored as an object method
  const obj = {
    sayHi: function () {
      console.log('Hi!');
    }
  };
  ```

- **Passing Functions as Arguments**:
  ```javascript
  // addEventListener is a higher-order function
  document.querySelector('button').addEventListener('click', greet);
  ```
  Here, the `greet` function is passed as a value (callback) to `addEventListener`.

- **Returning Functions from Functions**:
  ```javascript
  function createMultiplier(multiplier) {
    return function (value) {
      return value * multiplier;
    };
  }

  const double = createMultiplier(2);
  console.log(double(5)); // 10
  ```

### Function Methods
Since functions are objects, they can have methods, just like arrays or other objects. One such method is `bind`, which we will explore further later.

---

## Higher-Order Functions

### Definition
A **higher-order function** is a function that:
1. Receives another function as an argument, or
2. Returns a new function.

### Examples
1. **Receiving a Function as an Argument**:
   ```javascript
   // addEventListener is a higher-order function
   document.querySelector('button').addEventListener('click', greet);
   ```
   - `addEventListener` receives the `greet` function as a callback.
   - A callback function is executed later by the higher-order function.

2. **Returning a Function**:
   ```javascript
   function greetCreator(name) {
     return function () {
       console.log(`Hello, ${name}!`);
     };
   }

   const greetJohn = greetCreator('John');
   greetJohn(); // Hello, John!
   ```

### Importance
Higher-order functions are made possible because JavaScript supports first-class functions. They are widely used in functional programming and are powerful tools for abstraction.

---

## First-Class Functions vs. Higher-Order Functions

- **First-Class Functions**:
  - A **feature** of the JavaScript language.
  - Means functions are treated as values.
  - Does not refer to any specific function in practice.

- **Higher-Order Functions**:
  - Actual functions in practice.
  - Either receive or return other functions.

**Key Distinction**: First-class functions are a **concept**, while higher-order functions are a **practical application** of that concept.

---

## Summary
- JavaScript's first-class functions enable powerful programming paradigms, such as higher-order functions.
- Higher-order functions allow us to:
  - Pass functions as arguments.
  - Return functions from functions.
- Understanding the distinction between first-class and higher-order functions is essential for mastering JavaScript.

In the next lecture, we will explore creating our own higher-order functions in more detail.

