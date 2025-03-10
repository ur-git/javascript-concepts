# Selecting, Creating, and Deleting Elements in JavaScript

This lecture serves as a quick reference for selecting, creating, and deleting elements in the DOM, focusing on practical usage rather than relying on MDN documentation.

---

## 1. Selecting Elements

### Special Elements

- **`document.documentElement`**: Selects the entire `<html>` element.
- **`document.head`**: Selects the `<head>` element.
- **`document.body`**: Selects the `<body>` element.

### Modern Methods

- **`document.querySelector(selector)`**: Returns the first element matching the `selector`.
  - Example: `document.querySelector('.header')`
- **`document.querySelectorAll(selector)`**: Returns a static `NodeList` of all elements matching the `selector`.
  - Example: `document.querySelectorAll('.section')`

### Legacy Methods

- **`document.getElementById(id)`**: Selects an element by its `id`.
  - Example: `document.getElementById('section1')`
- **`document.getElementsByTagName(tagName)`**: Returns a live `HTMLCollection` of elements by `tagName`.
  - Example: `document.getElementsByTagName('button')`
- **`document.getElementsByClassName(className)`**: Returns a live `HTMLCollection` of elements by `className`.
  - Example: `document.getElementsByClassName('btn')`

#### Note on Live Collections

- **Live Collections** (e.g., `HTMLCollection`) update automatically when the DOM changes.
- **Static NodeLists** (e.g., `querySelectorAll`) do not update after creation.

---

## 2. Creating and Inserting Elements

### Creating Elements

- **`document.createElement(tagName)`**: Creates a new element in memory.
  - Example:
    ```javascript
    const message = document.createElement("div");
    message.classList.add("cookie-message");
    message.textContent =
      "We use cookies for improved functionality and analytics.";
    ```

### Inserting Elements

- **`element.append(child)`**: Inserts `child` as the last child of `element`.
- **`element.prepend(child)`**: Inserts `child` as the first child of `element`.
- **`element.before(sibling)`**: Inserts `sibling` before `element`.
- **`element.after(sibling)`**: Inserts `sibling` after `element`.

#### Cloning Elements

- Use **`node.cloneNode(true)`** to create a copy of an element, including its children.

### Example:

```javascript
const header = document.querySelector(".header");
header.append(message); // Appends as the last child
header.prepend(message); // Moves the element to the first child position
```

---

## 3. Deleting Elements

### Modern Method

- **`element.remove()`**: Removes an element from the DOM.
  - Example:
    ```javascript
    const button = document.querySelector(".btn--close-cookie");
    button.addEventListener("click", () => {
      message.remove();
    });
    ```

### Legacy Method

- **`parent.removeChild(child)`**: Removes a child element.
  - Example:
    ```javascript
    const parent = message.parentElement;
    parent.removeChild(message);
    ```

---
