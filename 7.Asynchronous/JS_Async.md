# Understanding Asynchronous JavaScript

# Async/Await in JavaScript

## **Introduction**

- Introduced in **ES2017**, `async/await` provides a better way to consume promises.
- It makes asynchronous code **look synchronous** while running **in the background**.
- `async` functions **always return a promise**.

---

## **Creating an Async Function**

- To define an **async function**, add `async` before the function declaration.
- The function **executes asynchronously**, meaning:
  - It **does not block** the main thread.
  - It **returns a promise** that resolves when execution completes.

```js
async function whereAmI(country) {
  const res = await fetch(`https://restcountries.com/v3.1/name/${country}`);
  console.log(res);
}
```

## **The `await` Keyword**

- Used to **pause execution** of an `async` function **until a promise is resolved**.
- Can only be used inside `async` functions.
- **Behind the scenes:**
  - `fetch()` returns a **promise**.
  - `await fetch()` **pauses execution** until resolved.
  - The **resolved value** is stored in `res`.
  - `res.json()` also returns a **promise**, requiring another `await`.

```js
async function whereAmI(country) {
  const res = await fetch(`https://restcountries.com/v3.1/name/${country}`);
  const data = await res.json();
  console.log(data[0]);
}
```

---

## **Async Functions Are Non-Blocking**

- Even though `await` **pauses execution**, the rest of the script **continues running**.
- The `async` function runs in the **background**, **not blocking** the main thread.

```js
console.log("FIRST");
whereAmI("Portugal");
console.log("SECOND");
```

**Output:**

```
FIRST
SECOND
{ country data }  // Appears after the fetch completes
```

---

## **Async/Await vs Promises**

- **Traditional Promise-based Approach:**

```js
getPosition()
  .then((pos) =>
    fetch(
      `https://geocode.xyz/${pos.coords.latitude},${pos.coords.longitude}?geoit=json`
    )
  )
  .then((res) => res.json())
  .then((dataGeo) =>
    fetch(`https://restcountries.com/v3.1/name/${dataGeo.country}`)
  )
  .then((res) => res.json())
  .then((data) => console.log(data));
```

- **With Async/Await:**

```js
async function whereAmI() {
  const pos = await getPosition();
  const resGeo = await fetch(
    `https://geocode.xyz/${pos.coords.latitude},${pos.coords.longitude}?geoit=json`
  );
  const dataGeo = await resGeo.json();

  const res = await fetch(
    `https://restcountries.com/v3.1/name/${dataGeo.country}`
  );
  const data = await res.json();

  console.log(data);
}
```

---

## **Handling Errors with Try/Catch**

- `await` does **not** have `.catch()`, so use `try...catch` for error handling.
- Prevents **unhandled promise rejections**.
- Catches **network failures** and **invalid responses**.

```js
async function whereAmI() {
  try {
    const pos = await getPosition();
    const resGeo = await fetch(
      `https://geocode.xyz/${pos.coords.latitude},${pos.coords.longitude}?geoit=json`
    );

    if (!resGeo.ok) throw new Error("Problem getting location data");

    const dataGeo = await resGeo.json();
    const res = await fetch(
      `https://restcountries.com/v3.1/name/${dataGeo.country}`
    );

    if (!res.ok) throw new Error("Country not found");

    const data = await res.json();
    console.log(data);
  } catch (err) {
    console.error(`💥 ${err.message}`);
  }
}
```

---

## **Summary**

| Feature           | Async/Await              | Promises (`.then()`) |
| ----------------- | ------------------------ | -------------------- |
| Readability       | **Easier to read/write** | More callbacks       |
| Error Handling    | `try...catch`            | `.catch()` needed    |
| Parallel Requests | `Promise.all()`          | `Promise.all()`      |
| Blocking Behavior | Non-blocking             | Non-blocking         |

### **Key Takeaways**

- `async/await` **simplifies promise consumption** by making code look synchronous.
- The **`await` keyword** pauses execution **inside an `async` function`**, but does not block the main thread.
- Always wrap `await` calls in **`try...catch`** for **error handling**.
