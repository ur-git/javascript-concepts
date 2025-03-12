# **Memoization in JavaScript**

## **Introduction**

**Memoization** is an **optimization technique** that speeds up expensive function calls by caching their results. When the function is called again with the same inputs, the cached result is returned instead of recomputing it.

### **Why Use Memoization?**

- **Improves performance** by reducing redundant computations.
- **Avoids re-executing expensive operations** (e.g., recursion, API calls, mathematical calculations).
- **Optimizes recursive algorithms** like **Fibonacci, Factorial, and Dynamic Programming** problems.

---

## **How Memoization Works**

- **Create a cache (object or Map) to store computed results.**
- **Before computing a result, check if it already exists in the cache.**
- **If cached, return the stored result.**
- **If not cached, compute the result, store it, and return it.**

---

## **Basic Memoization Implementation**

### **Example: Memoizing a Fibonacci Function**

```js
function fibonacci(n, cache = {}) {
  if (n <= 1) return n;
  if (n in cache) return cache[n]; // Check cache
  return (cache[n] = fibonacci(n - 1, cache) + fibonacci(n - 2, cache));
}

console.log(fibonacci(10)); // 55
console.log(fibonacci(50)); // Efficient due to memoization
```

- **Without memoization**, `fibonacci(50)` would take **exponential time** (`O(2ⁿ)`).
- **With memoization**, it runs in **O(n) time complexity**.

---

## **Optimized Memoization with Closures**

A more **modular** and **reusable** approach:

```js
function memoize(fn) {
  const cache = {};
  return function (...args) {
    const key = JSON.stringify(args);
    if (key in cache) return cache[key];
    return (cache[key] = fn(...args));
  };
}

const factorial = memoize(function (n) {
  if (n === 0 || n === 1) return 1;
  return n * factorial(n - 1);
});

console.log(factorial(5)); // 120
console.log(factorial(10)); // 3628800 (computed)
console.log(factorial(5)); // 120 (cached)
```

✔ **Benefits of Closures:**

- **Encapsulates cache** inside `memoize()`.
- **Works with any function**, making it **reusable**.

---

## **Memoization with Map (More Efficient than Object)**

Using `Map()` instead of an object for caching:

```js
function memoize(fn) {
  const cache = new Map();
  return function (...args) {
    const key = args.toString();
    if (cache.has(key)) return cache.get(key);
    const result = fn(...args);
    cache.set(key, result);
    return result;
  };
}

const add = memoize((a, b) => a + b);
console.log(add(3, 5)); // 8 (computed)
console.log(add(3, 5)); // 8 (cached)
```

### **Why Use Map?**

- **Better performance** for large datasets.
- **Preserves insertion order**.
- **Handles complex keys** (arrays, objects).

---

## **Advanced Memoization: Handling Multiple Arguments**

When a function takes multiple arguments, we need a **robust key generation strategy**.

```js
function memoize(fn) {
  const cache = new Map();
  return function (...args) {
    const key = args.map((arg) => JSON.stringify(arg)).join(",");
    if (cache.has(key)) return cache.get(key);
    const result = fn(...args);
    cache.set(key, result);
    return result;
  };
}

const multiply = memoize((a, b) => a * b);
console.log(multiply(3, 4)); // 12 (computed)
console.log(multiply(3, 4)); // 12 (cached)
```

---

## **Least Recently Used (LRU) Cache with Memoization**

Memoization can lead to excessive memory usage. To avoid this, we use **LRU (Least Recently Used) cache**, which **removes the least used items** when the cache reaches a certain size.

### **LRU Cache Implementation**

```js
class LRUCache {
  constructor(limit = 5) {
    this.cache = new Map();
    this.limit = limit;
  }

  get(key) {
    if (!this.cache.has(key)) return null;
    const value = this.cache.get(key);
    this.cache.delete(key); // Remove and re-add to maintain recent use order
    this.cache.set(key, value);
    return value;
  }

  set(key, value) {
    if (this.cache.has(key)) this.cache.delete(key);
    if (this.cache.size >= this.limit)
      this.cache.delete(this.cache.keys().next().value);
    this.cache.set(key, value);
  }
}

// Usage
const lru = new LRUCache(3);
lru.set("a", 1);
lru.set("b", 2);
lru.set("c", 3);
console.log(lru.get("a")); // 1
lru.set("d", 4); // "b" will be removed
console.log(lru.get("b")); // null (evicted)
```

### **How LRU Works?**

- When a **new item is added**, the **oldest unused item** is **removed**.
- When an **existing item is accessed**, it is moved to the most recent position.
- Ensures **memory efficiency** while keeping frequently used items cached.

---

## **Practical Use Cases of Memoization**

1. **Recursive Problems** (Fibonacci, Factorial, Dynamic Programming).
2. **Expensive Calculations** (Prime Number Generation, Matrix Operations).
3. **API Calls & Data Fetching** (Cache previous responses).
4. **DOM & UI Rendering Optimizations** (Avoid unnecessary calculations).
5. **Parsing Large Data Structures** (Efficient processing).

---

## **Comparison: Memoization vs. Caching**

| Feature  | Memoization                      | Caching                                  |
| -------- | -------------------------------- | ---------------------------------------- |
| Scope    | Function-level                   | Application-level                        |
| Storage  | Stores computed values           | Stores data from external sources        |
| Use Case | Optimizing repeated calculations | Storing API responses, database results  |
| Example  | Fibonacci series, Factorial      | Web caching, CDN, database query caching |

---

## **When to Avoid Memoization?**

- **Functions with side effects** (e.g., modifying global state, making API calls).
- **When inputs are always unique** (memoization is useless).
- **When memory usage is a concern** (caching too much data can cause memory overflow).

---

## **Conclusion**

- **Memoization** is a powerful technique to improve performance by caching function results.
- It is most effective for **pure functions** that return **the same output for the same input**.
- **Closures & Maps** make memoization more **efficient** and **modular**.
- **LRU Cache** helps manage memory effectively.
- Used correctly, it **reduces computation time**, especially for **recursive and expensive calculations**.

---
