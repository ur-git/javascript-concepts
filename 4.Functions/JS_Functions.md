# JavaScript: First-Class Functions and Higher-Order Functions

## First-Class Functions

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
    console.log("Hello!");
  };

  // Function stored as an object method
  const obj = {
    sayHi: function () {
      console.log("Hi!");
    },
  };
  ```

- **Passing Functions as Arguments**:

  ```javascript
  // addEventListener is a higher-order function
  document.querySelector("button").addEventListener("click", greet);
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

---

## Higher-Order Functions

A **higher-order function** is a function that:

1. Receives another function as an argument, or
2. Returns a new function.

### Examples

1. **Receiving a Function as an Argument**:

   ```javascript
   // addEventListener is a higher-order function
   document.querySelector("button").addEventListener("click", greet);
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

   const greetJohn = greetCreator("John");
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

# More About Higher-Order Functions in JavaScript

## Creating a Higher-Order Function

To understand how higher-order functions work, let’s create one step by step.

### Step 1: Writing Generic Functions

First, we define two basic string transformation functions:

```javascript
// Function to remove all spaces and convert to lowercase
const oneWord = function (str) {
  return str.replace(/\s/g, "").toLowerCase();
};

// Function to capitalize the first word of a string
const upperFirstWord = function (str) {
  const [first, ...others] = str.split(" ");
  return [first.toUpperCase(), ...others].join(" ");
};
```

These functions operate independently, performing specific transformations:

- `oneWord`: Removes spaces and converts the string to lowercase.
- `upperFirstWord`: Capitalizes only the first word of the string.

---

### Step 2: Defining the Higher-Order Function

Now, we create the higher-order function `transformer`, which:

- Accepts a string.
- Accepts a function as its second argument (a callback function).

```javascript
const transformer = function (str, fn) {
  console.log(`Original string: ${str}`);
  console.log(`Transformed string: ${fn(str)}`);
  console.log(`Transformed by: ${fn.name}`);
};
```

#### Explanation:

1. `str`: The string to transform.
2. `fn`: The callback function to apply.
3. Outputs the original string, transformed string, and the name of the transformation function (using the `name` property of the function).

---

### Step 3: Using the Higher-Order Function

```javascript
transformer("JavaScript is the best!", upperFirstWord);
// Output:
// Original string: JavaScript is the best!
// Transformed string: JAVASCRIPT is the best!
// Transformed by: upperFirstWord

transformer("JavaScript is the best!", oneWord);
// Output:
// Original string: JavaScript is the best!
// Transformed string: javascriptisthebest!
// Transformed by: oneWord
```

- The `transformer` function applies the passed callback to the string and logs relevant information.
- Callback functions (`upperFirstWord`, `oneWord`) handle the transformation logic.

---

## Example: Built-In Higher-Order Functions

### Event Listeners as Higher-Order Functions

Event listeners in JavaScript use the concept of higher-order functions. For example:

```javascript
const highFive = () => console.log("👋");

document.body.addEventListener("click", highFive);
```

#### Explanation:

- `addEventListener` is a higher-order function that takes an event type (e.g., `click`) and a callback function (`highFive`).
- The callback executes when the event occurs.

### Array Methods Using Callbacks

The `forEach` method demonstrates the same principle:

```javascript
["Jonas", "Martha", "Adam"].forEach(highFive);
// Output:
// 👋
// 👋
// 👋
```

- The `forEach` method is a higher-order function that takes a callback function (`highFive`) and executes it for each array element.

---

## Why Use Higher-Order Functions?

### Benefits:

1. **Code Reusability**: Break down functionality into reusable, modular pieces.
2. **Abstraction**: Hide low-level implementation details and work at a higher conceptual level.

For example:

- The `transformer` function abstracts away string transformation details, delegating the implementation to the callback functions (`oneWord` or `upperFirstWord`).
- This makes `transformer` a reusable function that focuses only on applying a transformation, without being concerned about how the transformation happens.

---
