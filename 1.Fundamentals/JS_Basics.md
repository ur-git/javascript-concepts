# JS Basics

## What is Javascript?

JavaScript is a high-level, interpreted, dynamically typed programming language used primarily for web development. It allows developers to create interactive and dynamic web pages.

JavaScript is **primarily an interpreted language**, meaning it executes code **line by line** at runtime without requiring a separate compilation step. However, modern JavaScript engines (like **V8, SpiderMonkey, and Chakra**) use **Just-In-Time (JIT) Compilation** to optimize performance.

**How JavaScript Works in Modern Browsers:**

1. **Parsing:** The JavaScript engine reads the code.
2. **Compilation (JIT):** Converts the code into **bytecode** for faster execution.
3. **Execution:** The browser executes the bytecode.

**So, JavaScript is BOTH interpreted and JIT-compiled!**

JavaScript is a **multi-paradigm language**, meaning it supports different programming styles, including:

| Paradigm                              | Description                                  | Example                                |
| ------------------------------------- | -------------------------------------------- | -------------------------------------- |
| **Imperative**                        | Step-by-step execution                       | `for` loops, `if` statements           |
| **Functional**                        | Uses pure functions & avoids changing state  | `.map()`, `.reduce()`, arrow functions |
| **Object-Oriented (Prototype-Based)** | Objects inherit from prototypes, not classes | `Object.create()`, `this` keyword      |
| **Event-Driven**                      | Executes code in response to events          | `addEventListener()`                   |

---

## What are primitive data types?

Primitive data types are **immutable**, fundamental data types that store simple values. They are stored **by value** (not by reference) and do not have methods or properties (though JavaScript temporarily wraps them in objects when needed).

### List of Primitive Data Types

| Data Type        | Example             | Description                                                |
| ---------------- | ------------------- | ---------------------------------------------------------- |
| **String**       | `"Hello"`           | Represents text, enclosed in quotes (`""`, `''`, or \`\`)  |
| **Number**       | `42`, `3.14`        | Represents both integers and floating-point numbers        |
| **BigInt**       | `9007199254740991n` | For large numbers beyond `Number.MAX_SAFE_INTEGER`         |
| **Boolean**      | `true`, `false`     | Represents logical values                                  |
| **Undefined**    | `undefined`         | A variable that has been declared but not assigned a value |
| **Null**         | `null`              | Represents an intentional absence of value                 |
| **Symbol (ES6)** | `Symbol('id')`      | Unique and immutable values used as object keys            |

---

## What are the different ways to access object properties?

In JavaScript, there are **two main ways** to access object properties:

- Dot Notation (`.`)
- Bracket Notation (`[]`)

There are also some advanced methods like **`Object.keys()`, `Object.values()`, and `Object.entries()`** for iterating over object properties.

| Method                      | Usage                               | Pros                                        | Cons                                                      |
| --------------------------- | ----------------------------------- | ------------------------------------------- | --------------------------------------------------------- |
| **Dot Notation (`.`)**      | `obj.property`                      | Simple, readable                            | Cannot handle special characters, spaces, or dynamic keys |
| **Bracket Notation (`[]`)** | `obj["property"] `                  | Works with dynamic keys, special characters | Less readable                                             |
| **`Object.keys(obj)`**      | Returns an array of property names  | Best for iteration                          | Only gives keys                                           |
| **`Object.values(obj)`**    | Returns an array of property values | Easy to get values                          | No key reference                                          |
| **`Object.entries(obj)`**   | Returns an array of key-value pairs | Great for iteration                         | Slightly complex                                          |
| **`for...in` Loop**         | Iterates over all properties        | Dynamic property access                     | Includes inherited properties                             |
| **`hasOwnProperty()`**      | Checks if a property exists         | Avoids prototype chain issues               | Must be called explicitly                                 |

---

## What is the difference between a parameter and an argument?

| Feature          | Parameter                                               | Argument                                          |
| ---------------- | ------------------------------------------------------- | ------------------------------------------------- |
| Definition       | Placeholder in function definition                      | Actual value passed to the function               |
| Where it is used | In function declaration                                 | When calling the function                         |
| Example          | `function greet(name) {}` (here, `name` is a parameter) | `greet("Alice")` (here, `"Alice"` is an argument) |

---

## What is the difference between internal and external JavaScript?

The difference between **internal** and **external** JavaScript lies in **where** the script is written and how it is included in an HTML file.

### Internal JavaScript

Internal JavaScript is written inside the `<script>` tag within the HTML file itself.

#### Example

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Internal JS Example</title>
    <script>
      function greet() {
        alert("Hello from Internal JavaScript!");
      }
    </script>
  </head>
  <body>
    <button onclick="greet()">Click Me</button>
  </body>
</html>
```

### External JavaScript

External JavaScript is written in a separate `.js` file and linked to the HTML file using the `<script>` tag with the `src` attribute.

#### **Example:**

**HTML file (`index.html`):**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>External JS Example</title>
    <script src="script.js"></script>
  </head>
  <body>
    <button onclick="greet()">Click Me</button>
  </body>
</html>
```

---

## Is JavaScript faster than server-side scripts?

It depends on the context. JavaScript (running in the browser) is generally **faster** than server-side scripts (like Python, PHP, or Node.js) for tasks that involve UI interactions, DOM manipulation, or animations because it executes directly in the user's browser without needing to communicate with a server.

However, **server-side scripts can be faster** when handling complex computations, database queries, or processing large amounts of data, since they run on powerful server hardware without being limited by a user’s device.

### **Comparison:**

| Factor          | JavaScript (Client-Side)      | Server-Side Scripts          |
| --------------- | ----------------------------- | ---------------------------- |
| Execution Speed | Faster for UI & small tasks   | Faster for heavy processing  |
| Resource Usage  | Uses user's CPU & memory      | Uses server's CPU & memory   |
| Latency         | No network delay              | Network delay for requests   |
| Security        | Less secure (code is exposed) | More secure (code is hidden) |
| Scalability     | Limited by user’s device      | Can scale with server power  |
