# **Destructuring in JavaScript**

- Destructuring is an **ES6 feature** that allows unpacking values from **arrays** or **objects** into separate variables.
- Helps break complex data structures into simpler, more manageable variables.
- **Use case**: Extract elements from an array in an elegant way without manual indexing.

---

## **Basic Array Destructuring**

### **Without Destructuring**

```js
const arr = [2, 3, 4];

const a = arr[0];
const b = arr[1];
const c = arr[2];

console.log(a, b, c); // Output: 2 3 4
```

### **With Destructuring**

- **Square brackets `[]`** are used to indicate array destructuring.
- `x`, `y`, and `z` correspond to the first, second, and third elements of `arr`.

```js
const [x, y, z] = arr;
console.log(x, y, z); // Output: 2 3 4
```

## **Skipping Elements**

- You can skip elements by leaving a **gap (`,`)** in the destructuring pattern.
- **Second element ("Pizzeria") is skipped**.

```js
const categories = ["Italian", "Pizzeria", "Vegetarian", "Organic"];

const [first, , third] = categories;
console.log(first, third); // Output: Italian Vegetarian
```

## **Swapping Variables Using Destructuring**

- **No temporary variable needed**, making the code cleaner.

### **Without Destructuring**

```js
let main = "Italian";
let secondary = "Vegetarian";

// Using a temporary variable
let temp = main;
main = secondary;
secondary = temp;

console.log(main, secondary); // Output: Vegetarian Italian
```

### **With Destructuring**

```js
let main = "Italian";
let secondary = "Vegetarian";

[main, secondary] = [secondary, main];

console.log(main, secondary); // Output: Vegetarian Italian
```

## **Destructuring Function Returns**

- Functions can return arrays, which can be **immediately destructured**.
- **Benefit**: Retrieves multiple values from a function **without** accessing array indices manually.

```js
const restaurant = {
  starterMenu: ["Bruschetta", "Garlic Bread", "Salad"],
  mainMenu: ["Pizza", "Pasta", "Risotto"],

  order: function (starterIndex, mainIndex) {
    return [this.starterMenu[starterIndex], this.mainMenu[mainIndex]];
  },
};

// Function call with destructuring
const [starter, mainCourse] = restaurant.order(2, 0);
console.log(starter, mainCourse); // Output: Salad Pizza
```

## **Nested Array Destructuring**

- Arrays can contain **nested arrays** that require multi-level destructuring.
- **Skipping elements is still possible**.
- **Multi-level destructuring** works by nesting square brackets `[]` inside destructuring patterns.

```js
const nested = [2, 4, [5, 6]];

// Extracting values with a single level of destructuring
const [i, , j] = nested;
console.log(i, j); // Output: 2 [5, 6]

// Extracting all values
const [p, , [q, r]] = nested;
console.log(p, q, r); // Output: 2 5 6
```

## **Default Values in Destructuring**

- Useful when **array length is unknown** (e.g., API response).
- `r` is **undefined** in the array, so it **falls back to the default value (`1`)**.

```js
const arr = [8, 9];

// Destructuring with default values
const [p = 1, q = 1, r = 1] = arr;

console.log(p, q, r); // Output: 8 9 1
```

---

## **Summary**

| Concept                       | Example                                    |
| ----------------------------- | ------------------------------------------ |
| Basic Destructuring           | `[a, b, c] = [1, 2, 3]`                    |
| Skipping Elements             | `[first, , third] = ['A', 'B', 'C']`       |
| Swapping Variables            | `[x, y] = [y, x]`                          |
| Function Return Destructuring | `[starter, main] = restaurant.order(1, 2)` |
| Nested Destructuring          | `[a, , [b, c]] = [1, 2, [3, 4]]`           |
| Default Values                | `[x = 10, y = 20] = [5]`                   |

# Object Destructuring in JavaScript

To destructure objects, we use **curly braces `{}`**, specifying the property names we want to extract.
- The variable names must match the property names in the object.
- Order does not matter, unlike array destructuring.

```js
const restaurant = {
  name: "Italian Bistro",
  categories: ["Italian", "Vegetarian", "Organic"],
  openingHours: {
    fri: { open: 11, close: 23 },
    sat: { open: 12, close: 24 },
  },
};

// Object Destructuring
const { name, categories, openingHours } = restaurant;
console.log(name, categories, openingHours);
```
## Renaming Variables
We can rename variables while destructuring using the `:` syntax.

```js
const { name: restaurantName, openingHours: hours, categories: tags } = restaurant;
console.log(restaurantName, hours, tags);
```
- `name` → `restaurantName`
- `openingHours` → `hours`
- `categories` → `tags`

## Default Values
If a property doesn't exist, destructuring will return `undefined`. We can set default values using `=`.

```js
const { menu = [], starterMenu: starters = [] } = restaurant;
console.log(menu, starters);
```
- `menu` doesn’t exist, so it defaults to an empty array `[]`.
- `starterMenu` exists, so it retains its actual value.

## Mutating Variables While Destructuring
To **mutate existing variables**, wrap the destructuring statement in parentheses `()`.

```js
let a = 10;
let b = 20;

const obj = { a: 23, b: 7, c: 14 };

// Wrap in parentheses to avoid syntax errors
({ a, b } = obj);
console.log(a, b); // 23, 7
```
- Without `()`, JavaScript interprets `{}` as a **code block**, causing an error.

## Nested Object Destructuring
For **nested objects**, we can destructure multiple levels.

```js
const { fri: { open, close } } = openingHours;
console.log(open, close); // 11, 23
```
- Extracts `open` and `close` from `openingHours.fri`.

We can also rename these variables:

```js
const { fri: { open: o, close: c } } = openingHours;
console.log(o, c); // 11, 23
```

## Practical Use Case: Function Parameters
When dealing with functions that have multiple parameters, we can **pass an object** and immediately destructure it inside the function.

```js
const restaurant = {
  orderDelivery({ starterIndex = 1, mainIndex = 0, time = '20:00', address }) {
    console.log(`Order received: ${this.starterMenu[starterIndex]} and ${this.mainMenu[mainIndex]} will be delivered to ${address} at ${time}`);
  }
};

// Calling the function
restaurant.orderDelivery({
  time: '23:30',
  address: 'Via del Sole, 21',
  mainIndex: 2,
  starterIndex: 2
});
```
### Advantages:
- **No need to remember argument order**.
- **More readable and flexible**.
- **Can set default values** (e.g., `starterIndex = 1`, `mainIndex = 0`).

Another example with missing values:

```js
restaurant.orderDelivery({
  address: 'Via del Sole, 21',
  starterIndex: 2
});
```
- `time` defaults to **'20:00'**.
- `mainIndex` defaults to **0** (first item in `mainMenu`).