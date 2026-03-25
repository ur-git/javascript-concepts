# Difference Between `window` and `document`

## 1. `window`

> `window` is the **global object** in the browser.

### Key Points:

- Represents the **entire browser window**
- Top-level object (everything is inside it)
- Contains:

  - `document`
  - `localStorage`
  - `setTimeout`
  - `console`
  - `location`, `history`, etc.

## 2. `document`

> `document` represents the **HTML page (DOM)** loaded in the browser.

### Key Points:

- Part of `window`
- Used to **manipulate HTML elements**
- Entry point to the DOM

# Visual Hierarchy

```text
window (global)
  ├── document (DOM)
  │     ├── html
  │          ├── body
  │               ├── elements
```

---

# What is BOM (Browser Object Model)?

> The **Browser Object Model (BOM)** represents the **browser environment** and provides APIs to interact with things **outside the HTML page (DOM)**.

---

# Key Idea

- **DOM** → Represents the **web page (HTML structure)**
- **BOM** → Represents the **browser itself**

---

# BOM Structure

At the top is the **`window` object**, which is the global object in the browser.

```text
window
 ├── document (DOM)
 ├── location
 ├── history
 ├── navigator
 ├── screen
 ├── localStorage / sessionStorage
 ├── setTimeout / setInterval
```

---

# Common BOM Objects

## 1. `window`

- Global object
- Controls browser window

```js
window.alert("Hello");
window.innerWidth;
```

---

## 2. `location`

- Information about URL

```js
location.href; // full URL
location.reload(); // reload page
location.assign("https://example.com");
```

---

## 3. `history`

- Browser navigation

```js
history.back();
history.forward();
```

---

## 4. `navigator`

- Browser information

```js
navigator.userAgent;
navigator.language;
```

---

## 5. `screen`

- User screen info

```js
screen.width;
screen.height;
```

---

## 6. Storage APIs

```js
localStorage.setItem("key", "value");
sessionStorage.getItem("key");
```

---

## 7. Timers

```js
setTimeout(() => {}, 1000);
setInterval(() => {}, 1000);
```

---
