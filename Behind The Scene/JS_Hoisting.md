# Understanding Hoisting in JavaScript

## Execution Context Recap

Every execution context in JavaScript contains three essential parts:

- **Variable Environment**
- **Scope Chain**
- **`this` Keyword**

We've previously explored the scope chain. Now, let's dive into the **Variable Environment** and how variables are created in JavaScript.

## What is Hoisting?

Hoisting is a mechanism in JavaScript where some types of variables can be accessed before they are declared. Many mistakenly believe that hoisting moves variables to the top of their scope, but in reality:

- The JavaScript engine **scans** for variable declarations before executing the code.
- During the **creation phase** of the execution context, properties for each variable are stored in the **variable environment object**.

However, hoisting works differently depending on the type of variable or function declaration.

## Hoisting Behavior by Type

### 1. Function Declarations

✅ **Hoisted with full definition**

- Stored in the variable environment **before execution**.
- Can be used **before** they are declared in the code.
- **Block-scoped** in **strict mode** (otherwise function-scoped).

```js
sayHello(); // ✅ Works fine
function sayHello() {
  console.log("Hello!");
}
```

### 2. `var` Variables

✅ **Hoisted but initialized as `undefined`**

- When accessed before declaration, returns `undefined`.
- A common source of bugs.
- Not recommended in modern JavaScript.

```js
console.log(name); // ❌ undefined (not an error)
var name = "John";
```

### 3. `let` and `const` Variables

🚫 **Hoisted but uninitialized (Temporal Dead Zone)**

- Accessing them before declaration results in a **ReferenceError**.
- **Block-scoped**.
- Recommended over `var`.

```js
console.log(age); // ❌ ReferenceError
let age = 30;
```

## Function Expressions and Arrow Functions

Hoisting behavior depends on how they are declared:

| Declaration Type    | `var`                 | `let`/`const`        |
| ------------------- | --------------------- | -------------------- |
| Function Expression | `undefined` (hoisted) | ReferenceError (TDZ) |
| Arrow Function      | `undefined` (hoisted) | ReferenceError (TDZ) |

```js
console.log(sum(2, 3)); // ❌ TypeError: sum is not a function
var sum = function (a, b) {
  return a + b;
};
```

## Temporal Dead Zone (TDZ)

The **Temporal Dead Zone (TDZ)** is the region of a variable’s scope where it is **not accessible** before its declaration.

```js
if (true) {
  console.log(job); // ❌ ReferenceError: Cannot access 'job' before initialization
  const job = "Developer";
}
```

### Key Differences:

- **Variables in the TDZ exist but are uninitialized.**
- Trying to access them results in a **ReferenceError**.
- If a variable does not exist at all, the error states it is "not defined".

## Why Does TDZ Exist?

1. **Prevents silent bugs** – `var`'s `undefined` behavior is confusing.
2. **Ensures `const` variables behave correctly** – They **must** be assigned when declared.

## Why Does Hoisting Exist?

- **Function hoisting** allows for more flexible code structure and mutual recursion.
- **`var` hoisting** was an unintended side effect.
- Modern JavaScript solves issues by using `let` and `const`.

## Best Practices

✅ **Use `let` and `const` instead of `var`.**
✅ **Declare variables at the top of their scope.**
✅ **Use function expressions for better control over execution order.**

---

With this understanding, let's now explore practical examples of hoisting in action!
