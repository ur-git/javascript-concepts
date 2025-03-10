# **Asynchronous JavaScript: Behind the Scenes**

## **JavaScript Runtime Overview**

A **JavaScript runtime** is a container that includes everything necessary to execute JavaScript code.

### **Key Components:**

1. **JavaScript Engine (Single-threaded)**

   - Executes synchronous JavaScript code.
   - Consists of:
     - **Call Stack** → Executes function calls.
     - **Heap** → Stores objects and data.

2. **Web APIs (Provided by Browser, Not JavaScript Itself)**

   - Enables asynchronous operations like:
     - **DOM Manipulation**
     - **Timers (`setTimeout`)**
     - **AJAX (`fetch`)**
     - **Geolocation API**

3. **Callback Queue (Task Queue)**

   - Stores **callbacks** from web APIs (e.g., `setTimeout`, DOM events).
   - Follows **FIFO (First In, First Out)** order.

4. **Microtasks Queue (Higher Priority Queue)**

   - Stores **callbacks from Promises (`.then()`, `.catch()`)**.
   - Microtasks always execute **before** callbacks from the Callback Queue.

5. **Event Loop (Orchestrator)**
   - Continuously checks if the **Call Stack is empty**.
   - If **empty**, it moves the first **callback/microtask** into the Call Stack.

---

## **How Asynchronous JavaScript Works**

### **Synchronous vs Asynchronous Execution**

- **Synchronous Execution** → JavaScript executes **line by line** in a **single thread**.
- **Asynchronous Execution** → Some tasks (like `fetch`) run **in the background** using the **Web APIs**.

### **Example Code**

```js
console.log("Start");

// Asynchronous Timer
setTimeout(() => console.log("Timer done"), 2000);

// Asynchronous Fetch Request
fetch("https://jsonplaceholder.typicode.com/todos/1")
  .then((res) => res.json())
  .then((data) => console.log("Fetch done:", data));

console.log("End");
```

### **Execution Flow**

1. `console.log("Start")` → Runs **synchronously** in the Call Stack.
2. `setTimeout()` → Moves **to Web APIs** (does not block execution).
3. `fetch()` → Moves **to Web APIs** (performs AJAX request in the background).
4. `console.log("End")` → Runs **synchronously**.
5. **After 2 seconds**, `setTimeout()` callback moves **to Callback Queue**.
6. When the `fetch()` request resolves, its `.then()` callback moves **to Microtasks Queue**.
7. **Event Loop Execution Order:**
   - Microtasks (`fetch.then()`) run **before** callbacks (`setTimeout()`).

### **Expected Output**

```
Start
End
Fetch done: { data... }   // Microtask runs first
Timer done                 // Callback runs after
```

---

## **The Event Loop: How It Works**

The **event loop** controls the execution order of asynchronous tasks.

1. **Checks Call Stack**

   - If **not empty** → Continue executing code.
   - If **empty** → Move the next callback/microtask into the Call Stack.

2. **Microtasks Queue Priority**
   - **Before processing the Callback Queue**, the event loop **empties the Microtasks Queue**.
   - **If a microtask adds another microtask**, it executes **before any callback**.

### **Example: Microtasks Queue Priority**

```js
console.log("Start");

setTimeout(() => console.log("Timer done"), 0);

Promise.resolve("Promise resolved").then(console.log);

console.log("End");
```

### **Execution Flow**

1. `console.log("Start")` → Runs in the Call Stack.
2. `setTimeout()` → Moves **to Web APIs**.
3. `Promise.resolve()` → **Microtask added** to Microtasks Queue.
4. `console.log("End")` → Runs in the Call Stack.
5. **Event Loop Execution Order:**
   - First, Microtasks Queue (`Promise.then()`).
   - Then, Callback Queue (`setTimeout()`).

### **Expected Output**

```
Start
End
Promise resolved  // Microtask runs before
Timer done        // Callback runs after
```

---

## **Why Does `setTimeout(0)` Not Run Immediately?**

A `setTimeout()` with `0ms` delay does **not** execute immediately because:

- It is placed in the **Web APIs environment**.
- It moves **to the Callback Queue**.
- The **Event Loop only picks it up when the Call Stack is empty**.
- **Microtasks execute first**, delaying it further.

### **Example**

```js
setTimeout(() => console.log("Timer done"), 0);
Promise.resolve().then(() => console.log("Promise done"));
console.log("End");
```

### **Expected Output**

```
End
Promise done   // Microtask executes before
Timer done     // Callback executes after
```

---

## **Callback Queue vs Microtasks Queue**

| **Feature**         | **Callback Queue**                              | **Microtasks Queue**                                    |
| ------------------- | ----------------------------------------------- | ------------------------------------------------------- |
| **Handles**         | `setTimeout`, DOM Events                        | `Promise.then()`, `MutationObserver`                    |
| **Execution Order** | **After** Microtasks                            | **Before** Callbacks                                    |
| **Blocking Risk**   | Lower Priority                                  | Can Starve Callbacks                                    |
| **Example**         | `setTimeout(() => console.log("Timer"), 1000);` | `Promise.resolve().then(() => console.log("Promise"));` |

---

## **Starvation of Callback Queue**

If **Microtasks keep adding more Microtasks**, they can **prevent Callbacks from running**.

### **Example: Microtasks Starving the Callback Queue**

```js
setTimeout(() => console.log("Timer done"), 0);

Promise.resolve().then(function repeat() {
  console.log("Microtask");
  Promise.resolve().then(repeat);
});
```

### **Expected Output (Infinite Microtask Execution)**

```
Microtask
Microtask
Microtask
... (Timer never executes)
```

### **Why?**

- `Promise.then()` keeps adding itself to the **Microtasks Queue**.
- The **Event Loop prioritizes Microtasks** over Callbacks.
- `setTimeout()` never gets a chance to execute.

---

## **Key Takeaways**

- **JavaScript is single-threaded** but **handles asynchronous tasks using Web APIs, Callback Queue, and Microtasks Queue**.  
- **Web APIs handle timers, fetch, DOM events asynchronously**, so they don't block the Call Stack.  
- **The Callback Queue stores event listeners and `setTimeout()` callbacks**, which run after microtasks.  
- **The Microtasks Queue stores Promises and has priority over the Callback Queue**.  
- **The Event Loop moves tasks from queues into the Call Stack when it's empty**.  
- **`setTimeout(0)` does not execute immediately because Microtasks run first**.  
- **If Microtasks keep adding more microtasks, the Callback Queue can be starved**, preventing normal execution.
