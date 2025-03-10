# Understanding Hoisting in JavaScript

Hoisting is a mechanism in JavaScript where some types of variables can be accessed before they are declared. Many mistakenly believe that hoisting moves variables to the top of their scope, but in reality:

- The JavaScript engine **scans** for variable declarations before executing the code.
- During the **creation phase** of the execution context, properties for each variable are stored in the **variable environment object**.

However, hoisting works differently depending on the type of variable or function declaration.

## Hoisting Behavior by Type

### 1. Function Declarations

- **Hoisted with full definition**
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

- **Hoisted but initialized as `undefined`**
- When accessed before declaration, returns `undefined`.
- A common source of bugs.
- Not recommended in modern JavaScript.

```js
console.log(name); // ❌ undefined (not an error)
var name = "John";
```

### 3. `let` and `const` Variables

- **Hoisted but uninitialized (Temporal Dead Zone)**
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

## Why Does TDZ Exist?

- **Prevents silent bugs** – `var`'s `undefined` behavior is confusing.
- **Ensures `const` variables behave correctly** – They **must** be assigned when declared.
