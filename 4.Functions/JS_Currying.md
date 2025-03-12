# Currying Function in JavaScript

A **currying function** is a function that **takes multiple arguments one at a time instead of all at once**. It transforms a function with multiple parameters into a sequence of **nested functions**, each taking a **single** argument.

## syntax of a Curried Function

```js
const add = (a) => (b) => a + b;
console.log(add(2)(3)); // Output: 5
```

**Instead of `add(2, 3)`, we call it as `add(2)(3)`.**

---

## Why Use Currying

| Feature                    | Benefit                                                     |
| -------------------------- | ----------------------------------------------------------- |
| **Code Reusability**       | Easily create specialized functions by fixing one argument. |
| **Avoid Repetition**       | Helps eliminate duplicate code patterns.                    |
| **Functional Programming** | Works well with `.map()`, `.reduce()`, and `.filter()`.     |
| **Composability**          | Makes function composition easier.                          |

---

# Currying in Real-World Scenarios

## Filtering Data with Currying

```js
const filterBy = (property) => (value) => (array) =>
  array.filter((item) => item[property] === value);

const filterByCategory = filterBy("category");
const electronics = filterByCategory("Electronics");

const products = [
  { name: "Laptop", category: "Electronics" },
  { name: "Shirt", category: "Clothing" },
  { name: "Phone", category: "Electronics" },
];

console.log(electronics(products));
// Output: [{ name: "Laptop", category: "Electronics" }, { name: "Phone", category: "Electronics" }]
```

**Reusable filtering function without rewriting code!**

---

## Currying with `.map()`

```js
const multiply = (x) => (y) => x * y;
const double = multiply(2);
const numbers = [1, 2, 3, 4];
console.log(numbers.map(double)); // Output: [2, 4, 6, 8]
```

**We fixed `x = 2` and reused it to double each number!**

---

## Curried API Call

Instead of writing separate API calls for different endpoints, we can use **currying** to create a reusable function.

#### Traditional API Call (Without Currying)

```js
async function fetchData(url, endpoint) {
  const response = await fetch(`${url}/${endpoint}`);
  return response.json();
}

fetchData("https://jsonplaceholder.typicode.com", "users").then((data) =>
  console.log(data)
);
```

🚨 **Issue**: We always need to pass `url` and `endpoint` manually.

#### Curried API Call

```js
const fetchDataCurried = (url) => async (endpoint) => {
  const response = await fetch(`${url}/${endpoint}`);
  return response.json();
};

// Create a reusable API function
const fetchFromPlaceholder = fetchDataCurried(
  "https://jsonplaceholder.typicode.com"
);

fetchFromPlaceholder("users").then((data) => console.log(data));
fetchFromPlaceholder("posts").then((data) => console.log(data));
```

✅ **Now, we only need to pass the `endpoint` while keeping `url` fixed.**

---

## Async Currying with setTimeout

Currying is useful when we need **delayed execution** in async tasks.

```js
const delay = (ms) => (message) =>
  new Promise((resolve) => setTimeout(() => resolve(message), ms));

const delay3s = delay(3000); // Creates a 3-second delay function

delay3s("Hello after 3 seconds").then(console.log);
```

✅ **Keeps the delay time fixed, allowing easy reuse**

---

## Currying with Event Listeners

- Basic Event Listener (Without Currying)

  ```js
  document.getElementById("btn").addEventListener("click", function (event) {
    console.log("Button Clicked!", event.target);
  });
  ```

  🚨 **Issue**: If we need multiple event listeners with different configurations, we must write multiple functions.

- Curried Event Listener

  ```js
  const handleEvent = (eventType) => (message) => (event) => {
    console.log(`${message} - Event Type: ${eventType}`, event.target);
  };

  // Create specific event handlers
  const clickHandler = handleEvent("click")("Button clicked!");
  const mouseOverHandler = handleEvent("mouseover")("Mouse hovered!");

  // Attach event listeners
  document.getElementById("btn").addEventListener("click", clickHandler);
  document
    .getElementById("btn")
    .addEventListener("mouseover", mouseOverHandler);
  ```

  ✅ **Advantages:**

  - **Reusability:** We can create multiple event handlers by fixing `eventType` and `message`.
  - **Flexibility:** The function remains modular, making it easier to maintain.

- Example: Currying for Multiple Elements

  Currying helps when attaching **the same event listener** to multiple elements.

  ```js
  const addEventListenerCurried = (eventType) => (selector) => (callback) => {
    document.querySelectorAll(selector).forEach((element) => {
      element.addEventListener(eventType, callback);
    });
  };

  // Create reusable event listeners
  const handleClick = (event) =>
    console.log(`Clicked: ${event.target.textContent}`);
  const handleHover = (event) =>
    console.log(`Hovered over: ${event.target.textContent}`);

  // Attach event listeners to multiple elements
  addEventListenerCurried("click")(".btn")(handleClick);
  addEventListenerCurried("mouseover")(".btn")(handleHover);
  ```

  ✅ **Now, all `.btn` elements will have click & hover listeners without repeating code!**

---
