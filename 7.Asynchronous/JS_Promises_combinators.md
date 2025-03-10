# JavaScript Promise Combinators: `race`, `allSettled`, and `any`

- JavaScript provides **Promise combinators** to handle multiple asynchronous operations.
- These include:
  - `Promise.race()`
  - `Promise.allSettled()`
  - `Promise.any()`
- Each combinator takes an **array of Promises** and returns a new Promise.

---

## **`Promise.race()`**

- Returns **the first settled promise**, whether **fulfilled or rejected**.
- The "winning" promise **determines the outcome** of `Promise.race()`.
- Commonly used for **fetch timeouts**.

### **Example: Racing Multiple API Calls**

```js
const getJSON = (url) => fetch(url).then((res) => res.json());

(async function () {
  const response = await Promise.race([
    getJSON(`https://restcountries.com/v3.1/name/italy`),
    getJSON(`https://restcountries.com/v3.1/name/egypt`),
    getJSON(`https://restcountries.com/v3.1/name/mexico`),
  ]);
  console.log(response);
})();
```

- The first API response **resolves the race**, ignoring the others.

### **Example: Using for Timeout**

- Helps **prevent long-running requests** by enforcing a time limit.
- If the API response takes longer than **1 second**, the timeout **rejects** first.

```js
const timeout = (sec) =>
  new Promise((_, reject) =>
    setTimeout(() => reject(new Error("Request took too long!")), sec * 1000)
  );

Promise.race([
  getJSON(`https://restcountries.com/v3.1/name/tanzania`),
  timeout(1),
])
  .then((res) => console.log(res))
  .catch((err) => console.error(err.message));
```

---

## **`Promise.allSettled()`**

- Returns **an array of all settled promises**, regardless of **fulfillment or rejection**.
- **Never short-circuits**; it waits for all promises to settle.
- Useful when **all results matter**, even if some fail.

### **Example: Handling Multiple API Calls**

```js
Promise.allSettled([
  Promise.resolve("Success"),
  Promise.reject("ERROR"),
  Promise.resolve("Another success"),
]).then((results) => console.log(results));
```

**Output:**

```js
[
  { status: "fulfilled", value: "Success" },
  { status: "rejected", reason: "ERROR" },
  { status: "fulfilled", value: "Another success" },
];
```

**Comparison with `Promise.all()`:**

```js
Promise.all([
  Promise.resolve("Success"),
  Promise.reject("ERROR"),
  Promise.resolve("Another success"),
])
  .then((results) => console.log(results))
  .catch((err) => console.error(err));
```

**Output:**

```js
"ERROR"; // Short-circuits on first rejection
```

- `Promise.all()` **fails completely** if any promise rejects.
- `Promise.allSettled()` **returns all results**.

---

## **`Promise.any()`**

- Returns **the first fulfilled promise**, ignoring rejections.
- If **all promises reject**, it returns an **AggregateError**.

### **Example: Ignoring Rejected Promises**

```js
Promise.any([
  Promise.reject("ERROR"),
  Promise.resolve("First Success"),
  Promise.resolve("Another Success"),
])
  .then((res) => console.log(res)) // "First Success"
  .catch((err) => console.error(err));
```

### **Example: Handling All Rejections**

```js
Promise.any([Promise.reject("ERROR 1"), Promise.reject("ERROR 2")])
  .then((res) => console.log(res))
  .catch((err) => console.error(err));
```

**Output:**

```js
AggregateError: All promises were rejected
```

---

## **Summary: Promise Combinators Comparison**

| Combinator             | Returns First?                        | Handles Errors?                           | Short-Circuits? |
| ---------------------- | ------------------------------------- | ----------------------------------------- | --------------- |
| `Promise.race()`       | First settled (fulfilled or rejected) | Yes (if first promise rejects)            | Yes             |
| `Promise.allSettled()` | All settled promises                  | Yes (returns all results)                 | No              |
| `Promise.any()`        | First fulfilled promise               | No (ignores rejections unless all reject) | No              |
| `Promise.all()`        | All fulfilled promises                | No (fails if any rejects)                 | Yes             |

### **Key Takeaways**

- **Use `Promise.race()`** for **timeouts** or choosing the fastest response.
- **Use `Promise.allSettled()`** when you need **all results**, regardless of failure.
- **Use `Promise.any()`** when you want **at least one success** and **can ignore failures**.
