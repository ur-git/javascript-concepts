# Understanding `this` Keyword in JavaScript

## 1. `this` in the Global Scope

- When `this` is used **outside any function**, it refers to the **global object**.
  - In browsers, the global object is `window`.

```js
console.log(this); // window
```

## 2. `this` in Regular Function Calls

- In **strict mode**, `this` inside a **regular function** call is `undefined`.
- In **sloppy mode**, `this` points to the **global object (`window`)**.

```js
"use strict";

function calcAge() {
  console.log(this); // undefined in strict mode
}

calcAge();
```

## 3. `this` in Arrow Functions

- **Arrow functions do not get their own `this`.**
- Instead, they inherit `this` from their **parent scope** (lexical `this`).

```js
const calcAgeArrow = () => {
  console.log(this);
};

calcAgeArrow(); // window (since the parent scope is global)
```

## 4. `this` in Methods

- When `this` is used inside a **method**, it refers to the **object that called the method**.

```js
const jonas = {
  birthYear: 1991,
  calcAge: function () {
    console.log(this); // jonas object
    console.log(2024 - this.birthYear);
  },
};

jonas.calcAge(); // 'this' refers to jonas object
```

## 5. Method Borrowing

- A method can be copied from one object to another (method borrowing).
- The `this` keyword always refers to the **object that calls the method**, **not** the object where the method was originally defined.

```js
const matilda = {
  birthYear: 2017,
};

matilda.calcAge = jonas.calcAge; // Borrowing method
matilda.calcAge(); // 'this' refers to matilda, not jonas
```

## 6. `this` in Standalone Function Calls

- If a method is assigned to a standalone function, `this` is **undefined** in strict mode.

```js
const f = jonas.calcAge;
f(); // undefined, because it's now a regular function call
```

## 7. Key Takeaways

1. **Global Scope (`this`)** → `window` (unless in strict mode, where it's `undefined`).
2. **Regular Function (`this`)** → `undefined` in strict mode.
3. **Arrow Function (`this`)** → Inherits from **parent scope**.
4. **Method (`this`)** → Refers to the **object calling the method**.
5. **Method Borrowing** → `this` is **dynamic**, not fixed to where the method was originally defined.
6. **Standalone Function (`this`)** → `undefined` in strict mode.
