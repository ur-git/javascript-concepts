# **Creating and Consuming Promises in JavaScript**

## **Understanding Promises**

A **Promise** is a special JavaScript object that represents a future value. It can be in one of three states:

- **Pending** → Initial state
- **Fulfilled** → Resolved with a value
- **Rejected** → Rejected with an error

Promises help manage **asynchronous operations** effectively, avoiding **callback hell**.

---

## **Creating a Promise**

We can create a Promise using the `new Promise` constructor, which takes an **executor function** as an argument.

### **Example: Simulating a Lottery with Promises**

```js
const lotteryPromise = new Promise((resolve, reject) => {
  console.log("Lottery draw is happening... 🔮");

  setTimeout(() => {
    if (Math.random() >= 0.5) {
      resolve("🎉 You won the lottery!");
    } else {
      reject(new Error("💩 You lost your money."));
    }
  }, 2000);
});

// Consuming the promise
lotteryPromise
  .then((res) => console.log(res)) // Handles success
  .catch((err) => console.error(err)); // Handles failure
```

### **Explanation**

1. The **executor function** runs immediately when the promise is created.
2. It receives two arguments:
   - `resolve(value)`: Marks the promise as **fulfilled**.
   - `reject(error)`: Marks the promise as **rejected**.
3. The outcome is decided using `Math.random()`, simulating a **50% win/loss probability**.
4. A `setTimeout` function delays the resolution or rejection by **2 seconds** to mimic async behavior.
5. The promise is consumed using:
   - `.then()` → Handles success
   - `.catch()` → Handles errors

---

## **Promisifying Callback-Based Functions**

**Promisification** refers to converting **callback-based asynchronous functions** into **promise-based functions**.

### **Example: Promisifying `setTimeout`**

```js
const wait = (seconds) => {
  return new Promise((resolve) => {
    setTimeout(resolve, seconds * 1000);
  });
};

// Using the wait function
wait(2)
  .then(() => {
    console.log("I waited for 2 seconds");
    return wait(1);
  })
  .then(() => {
    console.log("I waited for 1 second");
  });
```

### **Explanation**

1. The `wait(seconds)` function **returns a Promise**.
2. The executor function calls `setTimeout`, delaying resolution.
3. The `resolve()` function is executed **after the timeout**.
4. Since there’s no failure case, **`reject` is not needed**.
5. The function is consumed by chaining `.then()` calls.

---

## **Avoiding Callback Hell with Promise Chaining**

- Instead of **nested callbacks**, use **promise chaining**
- **Advantages of Chaining**
  - Cleaner syntax
  - Easier to read & maintain
  - No callback hell

```js
wait(1)
  .then(() => {
    console.log("1 second passed");
    return wait(1);
  })
  .then(() => {
    console.log("2 seconds passed");
    return wait(1);
  })
  .then(() => {
    console.log("3 seconds passed");
    return wait(1);
  })
  .then(() => console.log("4 seconds passed"));
```

---

## **Creating Immediately Resolved & Rejected Promises**

JavaScript provides **static methods** on the `Promise` object to create resolved or rejected promises instantly.

### **Example: `Promise.resolve()` & `Promise.reject()`**

```js
Promise.resolve("Resolved immediately").then(console.log);

Promise.reject(new Error("Rejected immediately")).catch(console.error);
```

---

## **Summary**

| Concept               | Description                             |
| --------------------- | --------------------------------------- |
| **Promise**           | Object representing a future value      |
| **resolve(value)**    | Marks the promise as fulfilled          |
| **reject(error)**     | Marks the promise as rejected           |
| **.then(callback)**   | Handles a fulfilled promise             |
| **.catch(callback)**  | Handles a rejected promise              |
| **Promisification**   | Converts callbacks into promises        |
| **Promise.resolve()** | Creates an immediately resolved promise |
| **Promise.reject()**  | Creates an immediately rejected promise |

---

## **Key Takeaways**

- Promises help handle **asynchronous operations** efficiently.
- The **executor function** runs immediately and decides the promise’s outcome.
- Use **`resolve()`** to fulfill and **`reject()`** to reject a promise.
- **Promise chaining** improves readability over nested callbacks.
- **Promisification** converts callback-based async functions into promises.
- `Promise.resolve()` and `Promise.reject()` create instantly settled promises.
