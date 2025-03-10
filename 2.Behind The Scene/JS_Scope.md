# **Scoping & Scope Chain in JavaScript**

## **Introduction**

- Scoping controls how variables are organized and accessed by the JavaScript engine.
- It determines **where variables live** and **where they can be accessed**.
- JavaScript uses **lexical scoping**, meaning scope is determined by **where functions and blocks are written** in the code.

## **What is Scope?**

- **Scope** is the space/environment in which a variable is declared.
- For functions, scope is equivalent to their **variable environment**.
- In JavaScript, there are **three types of scope**:
  1. **Global Scope**
  2. **Function Scope**
  3. **Block Scope**

## **Scope of a Variable**

- The **scope of a variable** refers to the entire region of the code where the variable can be accessed.

## **Types of Scope**

### **1. Global Scope**

- Variables declared outside of **any function or block**.
- Accessible **everywhere** in the program.

### **2. Function Scope (Local Scope)**

- Each function creates a **new scope**.
- Variables declared inside a function **can only be accessed within that function**.
- This is also known as **local scope**.

### **3. Block Scope (Introduced in ES6)**

- Blocks `{}` also create a **new scope**, but only for variables declared with `let` and `const`.
- **Variables declared with `var` are NOT block scoped**, they are function scoped.
- **Example:**
  ```javascript
  {
    let a = 10;
    const b = 20;
  }
  console.log(a, b); // ReferenceError: a is not defined
  ```
- Functions are **also block scoped in strict mode**.

## **The Scope Chain**

- Every scope has **access to all variables from its outer (parent) scopes**.
- The **scope chain** is used when a variable is not found in the current scope:
  - The JavaScript engine looks **up the scope chain** until it finds the variable.
  - If the variable isn't found, a **ReferenceError** occurs.

### **Example of Scope Chain**

```javascript
const myName = "Jonas";

function first() {
  const age = 30;

  function second() {
    const job = "teacher";
    console.log(`${myName} is a ${age}-year-old ${job}`);
  }

  second();
}
first();
```

**Explanation:**

- `myName` is in the **global scope**, so it is accessible inside `first()` and `second()`.
- `age` is in `first()`'s scope but can be accessed inside `second()` due to **scope chain**.
- `job` is inside `second()`, so it **cannot** be accessed by `first()`.

## **Lexical Scoping**

- Lexical scoping means:
  - The **placement** of functions and blocks in the code **determines** how variables are accessed.
  - **Functions can access variables from their parent scopes**.
  - **Functions cannot access variables from child scopes**.

### **Scope Chain Rules**

- **One scope can only look "up" the scope chain, not "down"**.
- **Sibling scopes do not have access to each other's variables**.

## **Scope Chain vs Call Stack**

- **Scope chain** is determined by **where functions are written** in the code (lexical scoping).
- **Call stack** is determined by **the order in which functions are called**.
- The **scope chain has nothing to do with the order of function calls**.

### **Example: Call Stack vs Scope Chain**

```javascript
function first() {
  const b = "Hello";
  second();
}

function second() {
  const c = "World";
  third();
}

function third() {
  console.log(b, c); // ReferenceError: b is not defined
}

first();
```

**Explanation:**

- Even though `third()` was called from `second()`, it **cannot access** `b` and `c` because they are not in its **scope chain**.
- **Function calls do not change the scope chain**.

## **Key Takeaways**

1. **Scoping determines where variables are accessible**.
2. **Three types of scope:**
   - **Global Scope** (accessible everywhere).
   - **Function Scope** (local to a function).
   - **Block Scope** (only applies to `let` and `const`).
3. **Lexical scoping** means:
   - A function has access to **all variables from its parent scope**.
   - **Inner scopes cannot be accessed from outer scopes**.
4. **Scope chain**:
   - If a variable is not found in the current scope, **JavaScript looks up the scope chain**.
   - **It does not look down or sideways**.
5. **Scope chain is different from the call stack**.
   - **Scope chain is based on where functions are defined**.
   - **Call stack is based on the order of function calls**.
