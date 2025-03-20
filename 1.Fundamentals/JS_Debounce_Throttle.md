Both throttling and debouncing help optimize performance by controlling how often a function is executed, but they serve different purposes.

# Debounce

A **debounce function** ensures that a function **executes only after a specified delay has passed since the last event trigger**.

This is useful for optimizing performance in events like scrolling, resizing, and keypresses.

---

## **Debounce Polyfill (Without `setTimeout` Overwrite)**

```js
function debounce(fn, delay) {
  let timer; // Stores the timeout reference

  return function (...args) {
    let context = this;

    // Clear the previous timer if a new call is made within 'delay'
    if (timer) clearTimeout(timer);

    // Set a new timer to execute the function after the delay
    timer = setTimeout(function () {
      fn.apply(context, args);
    }, delay);
  };
}
```

---

## **Step-by-Step Explanation**

### **1. Maintain a Timer Variable**

```js
let timer;
```

- This stores the reference to the `setTimeout` so that we can cancel it when needed.

---

### **2. Return a Function That Handles Calls**

```js
return function (...args) {
```

- The **debounced function** returns another function that captures any **arguments** passed to it.

---

### **3. Clear the Previous Timer If a New Call Is Made**

```js
if (timer) clearTimeout(timer);
```

- If the function is called **again before the delay completes**, the **previous timer is canceled**.

---

### **4. Set a New Timer**

```js
timer = setTimeout(function () {
  fn.apply(context, args);
}, delay);
```

- After `delay` milliseconds, **`fn` executes** with the original `this` context and arguments.

---

## Integrating Debounce with a Search Box

To integrate the debounce function with a search box:

1. **HTML Structure:**

   ```html
   <input type="text" onkeyup="processChange()" />
   ```

2. **JavaScript Integration:**

   ```javascript
   function debounce(func, timeout = 300) {
     let timer;
     return (...args) => {
       clearTimeout(timer);
       timer = setTimeout(() => {
         func.apply(this, args);
       }, timeout);
     };
   }

   // Function to handle the search query
   function handleSearch(event) {
     const query = event.target.value;
     console.log("Searching for:", query);
     // Implement your search logic here
   }

   // Attach the debounced function to the input event
   const processChange = debounce(() => handleSearch());
   ```

**Explanation:**

- `handleSearch` is the function that processes the search query. It retrieves the current value of the search box and performs the desired search operation.
- `searchBox` references the input element.
- `debounce(handleSearch, 300)` creates a debounced version of `handleSearch` with a 300ms delay, ensuring that `handleSearch` is invoked only after the user has stopped typing for 300ms.

---

# Throttling

Throttling ensures that a function **executes at most once in a specified time interval, even if it is triggered multiple times**.

## Integrating Throttle with a Scroll Event

```js
function throttle(func, limit) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      func.apply(this, args);
    }
  };
}

function onScroll() {
  console.log("Scroll event triggered at", new Date().toLocaleTimeString());
}

window.addEventListener("scroll", throttle(onScroll, 200)); // Executes at most every 200ms
```

---

## **Key Differences**

| Feature             | Throttling                                                    | Debouncing                                          |
| ------------------- | ------------------------------------------------------------- | --------------------------------------------------- |
| **Definition**      | Limits execution to **once per interval**                     | Delays execution **until inactivity**               |
| **Use Case**        | **Events happening frequently** (e.g., scrolling, mouse move) | **User-triggered actions** (e.g., typing, resizing) |
| **Execution Style** | **Ensures periodic execution** (e.g., every 500ms)            | **Waits for inactivity before execution**           |

---
