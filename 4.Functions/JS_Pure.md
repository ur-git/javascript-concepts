# Pure Function in JavaScript

A **pure function** is a function that:

1. **Always returns the same output** for the same input.
2. **Has no side effects** (does not modify external state).

Pure functions are a key concept in **functional programming** because they make code predictable, testable, and easy to debug.

---

## Example of a Pure Function

```js
const add = (a, b) => a + b;
console.log(add(2, 3)); // Output: 5
console.log(add(2, 3)); // Output: 5 (Always the same result)
```

**This function is pure** because:

- It **always returns the same output** for the same input.
- It does **not modify any external variable or state**.

---

## Characteristics of a Pure Function

| Feature                             | Description                                              | Example                                               |
| ----------------------------------- | -------------------------------------------------------- | ----------------------------------------------------- |
| **Same Output for Same Input**      | No randomness, always predictable.                       | `multiply(2, 3) // Always returns 6`                  |
| **No Side Effects**                 | Does not modify global variables, DOM, or external data. | Does **not** update `document.title` or `console.log` |
| **No Dependency on External State** | Only depends on its parameters.                          | Does **not** use `Math.random()` or `Date.now()`      |

---

## Example of an Impure Function

```js
let count = 0;
const increment = () => (count += 1); // Impure function
console.log(increment()); // Output: 1
console.log(increment()); // Output: 2 (Different result for same call)
```

**This function is impure** because:

- It **modifies an external variable (`count`)**.
- The output **changes every time it's called**.

---

## Example of a Pure Function

```js
const increment = (num) => num + 1;
console.log(increment(5)); // Output: 6
console.log(increment(5)); // Output: 6 (Always the same result)
```

**Pure because**

- **No external state is modified**.
- **Same input always gives the same output**.

---

## Common Impure vs. Pure Functions

| **Impure Function**                  | **Pure Function**                      |
| ------------------------------------ | -------------------------------------- |
| Modifies global variables            | Uses only local variables              |
| Calls `console.log()`, `alert()`     | Returns values instead of logging them |
| Modifies DOM (`document.body.style`) | Does not interact with the DOM         |
| Uses `Math.random()` or `Date.now()` | Only depends on input arguments        |

---

## Real-World Example: Filtering Data

- Impure Function (Modifies External Array)

  ```js
  let numbers = [1, 2, 3, 4];

  const removeOdds = () => {
    numbers = numbers.filter((n) => n % 2 === 0); // Modifies the original array
  };
  removeOdds();
  console.log(numbers); // Output: [2, 4] (Original array is changed)
  ```

  **This function is impure** because it **modifies `numbers`**.

- Pure Function (Returns a New Array)

  ```js
  const removeOddsPure = (arr) => arr.filter((n) => n % 2 === 0);
  const numbers = [1, 2, 3, 4];
  console.log(removeOddsPure(numbers)); // Output: [2, 4]
  console.log(numbers); // Output: [1, 2, 3, 4] (Original array is unchanged)
  ```

  **Pure because:**

  - **It does not modify the original array**.
  - **It only depends on its input and returns a new array**.

---

## Why Use Pure Functions?

✅ **Predictability** – Always returns the same output for the same input.  
✅ **Easier to Test & Debug** – No need to track external changes.  
✅ **Better Performance** – Enables optimizations like **memoization** & **parallel execution**.  
✅ **Reusability** – Can be reused across different projects without side effects.
