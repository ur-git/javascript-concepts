# JavaScript Code Execution

## How is JavaScript Code Executed?

JavaScript code is executed within the **JavaScript engine** using a **call stack**. The execution begins after compilation, creating a **global execution context** for the **top-level code**.

---

## Execution Context

### What is an Execution Context?

An **execution context** is an abstract concept that represents an environment where JavaScript code runs. It consists of:

- **Variable environment** (stores variables and function declarations)
- **Scope chain** (keeps track of variables outside the function)
- **`this` keyword** (refers to the current execution context)

### Types of Execution Contexts:

1. **Global Execution Context**

   - Created by default.
   - Executes top-level code (code outside functions).
   - Only one global execution context exists per program.

2. **Function Execution Context**

   - Created each time a function is called.
   - Contains its own variable environment, scope chain, and `this` keyword.

3. **Arrow Function Special Case**
   - Does **not** have its own `this` or `arguments` object.
   - Inherits these from the closest regular function.

---

## The Call Stack

### What is the Call Stack?

The **call stack** is a data structure that manages execution contexts in JavaScript. It keeps track of function calls and determines which function is currently executing.

### How It Works:

1. The **global execution context** is created and pushed onto the stack.
2. When a function is called, a **new execution context** is created and pushed onto the stack.
3. When a function finishes execution, its execution context is **popped off** the stack.
4. Execution resumes in the previous execution context.

### Example:

```javascript
function first() {
  let a = 1;
  let b = second();
  return a + b;
}

function second() {
  let c = 2;
  return c;
}

let x = first();
```

#### Call Stack Execution:

1. **Global Execution Context** is created and pushed onto the stack.
2. `first()` is called → **New Execution Context** is created and pushed.
3. `second()` is called inside `first()` → **New Execution Context** is created and pushed.
4. `second()` finishes → Its execution context is popped off.
5. `first()` resumes, completes, and is popped off.
6. The **global execution context** remains until the program finishes.

### Importance of the Call Stack:

- Ensures the correct **order of execution**.
- Keeps track of function calls.
- JavaScript is **single-threaded**, meaning it can only execute one task at a time.

---

## Summary

- **Execution contexts** are environments where JavaScript code runs.
- **The global execution context** is always present.
- **Functions get their own execution context** when called.
- **The call stack** manages execution contexts in a **last-in, first-out (LIFO)** manner.
- **Arrow functions** do not have their own `this` or `arguments`.
- JavaScript execution halts until all functions are finished.