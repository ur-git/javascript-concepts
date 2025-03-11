# JavaScript Sets and Maps

## Sets in JavaScript

A **Set** is a collection of **unique values** with no duplicates.

### **Creating a Set**

```js
const ordersSet = new Set([
  "pasta",
  "pizza",
  "pizza",
  "risotto",
  "pasta",
  "pizza",
]);
console.log(ordersSet); // Set(3) { 'pasta', 'pizza', 'risotto' }
```

- The duplicate values are removed automatically.
- Sets can store **any data type**.

### Properties & Methods

| Method/Property | Description                           | Example                           |
| --------------- | ------------------------------------- | --------------------------------- |
| `size`          | Returns the number of unique elements | `ordersSet.size` → `3`            |
| `has(value)`    | Checks if a value exists in the set   | `ordersSet.has('pizza')` → `true` |
| `add(value)`    | Adds a new element                    | `ordersSet.add('garlic bread')`   |
| `delete(value)` | Removes an element                    | `ordersSet.delete('risotto')`     |
| `clear()`       | Removes all elements                  | `ordersSet.clear()`               |

### Iteration

Sets are **iterable**, so we can loop through them:

```js
for (const order of ordersSet) console.log(order);
```

### **Use Case: Removing Duplicates from an Array**

```js
const staff = ["waiter", "chef", "waiter", "manager", "chef", "waiter"];
const uniqueStaff = [...new Set(staff)];
console.log(uniqueStaff); // ['waiter', 'chef', 'manager']
```

### Count Unique Values

```js
console.log(new Set(staff).size); // 3
console.log(new Set("javascript").size); // 9 (unique letters in string)
```

---

## Maps in JavaScript

A **Map** is a collection of **key-value pairs** where **keys can be of any type** (objects, arrays, etc.).

Unlike objects, where keys are always strings, map keys can be any type (objects, arrays, even other maps).

### Creating a Map

```js
const rest = new Map();
rest.set("name", "Classico Italiano");
rest.set(1, "Firenze, Italy");
rest.set(2, "Lisbon, Portugal");
```

- Returns the updated map, enabling method chaining.

```js
rest
  .set("categories", ["Italian", "Pizzeria", "Vegetarian", "Organic"])
  .set("open", 11)
  .set("close", 23)
  .set(true, "We are open")
  .set(false, "We are closed");
```

### Retrieving Values

```js
console.log(rest.get("name")); // 'Classico Italiano'
console.log(rest.get(true)); // 'We are open'
console.log(rest.get(1)); // 'Firenze, Italy'
```

### Iterating Over a Map

1. **Using `for-of` loop**

   ```js
   for (const [key, value] of question) {
     if (typeof key === "number") console.log(`Answer ${key}: ${value}`);
   }
   ```

   - Destructures each entry into `[key, value]`.
   - Filters to display only **numeric keys** (answer options).

2. **Getting Keys, Values, and Entries**
   ```js
   console.log([...question.keys()]); // All keys
   console.log([...question.values()]); // All values
   console.log([...question.entries()]); // Key-value pairs
   ```

### Object & Map Conversion

1. **Convert Object → Map**

   ```js
   const hoursMap = new Map(Object.entries(openingHours));
   ```

   - `Object.entries(obj)` returns an **array of key-value pairs**, which can be **directly used** to create a `Map`.

2. **Convert Map → Array**
   ```js
   console.log([...question]);
   ```
   - Spreading a map converts it back to an **array of key-value pairs**.

### **Properties & Methods**

| Method/Property   | Description                               | Example                           |
| ----------------- | ----------------------------------------- | --------------------------------- |
| `set(key, value)` | Adds or updates a key-value pair          | `rest.set('owner', 'Luigi')`      |
| `get(key)`        | Retrieves the value associated with a key | `rest.get('name')`                |
| `has(key)`        | Checks if a key exists                    | `rest.has('categories')` → `true` |
| `delete(key)`     | Removes a key-value pair                  | `rest.delete(2)`                  |
| `clear()`         | Removes all key-value pairs               | `rest.clear()`                    |
| `size`            | Returns the number of key-value pairs     | `rest.size`                       |

### **Using Arrays & Objects as Keys**

```js
const arr = [1, 2];
rest.set(arr, "Test");
console.log(rest.get(arr)); // 'Test'
```

- **Keys must reference the same memory location** (`rest.get([1,2])` won't work).

### **Using DOM Elements as Keys**

```js
rest.set(document.querySelector("h1"), "Heading");
```

- Stores DOM elements as keys, useful for UI-related data storage.

---

## **Summary**

| Feature      | Sets                               | Maps                                       |
| ------------ | ---------------------------------- | ------------------------------------------ |
| Data Storage | Unique values                      | Key-value pairs                            |
| Key Type     | Implicit                           | Any type (string, number, boolean, object) |
| Order        | No guarantee                       | Maintains insertion order                  |
| Duplicates   | Not allowed                        | Allowed                                    |
| Fast Lookup  | Yes (O(1))                         | Yes (O(1))                                 |
| Useful For   | Removing duplicates, quick lookups | Storing structured data                    |

Sets are best for **ensuring uniqueness**, while Maps are useful for **efficient key-value storage with flexible key types**.
