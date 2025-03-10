# Rest Pattern & Rest Parameters in JavaScript

## **Rest Pattern vs. Spread Operator**
- Both use the `...` (three dots) syntax.
- **Spread Operator (`...`)**: Expands elements into individual values.
- **Rest Pattern (`...`)**: Collects multiple elements into an array or object.
- **Key Difference**:  
  - Spread **unpacks** elements.
  - Rest **packs** elements into a new structure.

---

## **Rest Pattern in Arrays (Destructuring)**
- Used to collect the remaining elements when destructuring an array.
- Appears **on the left-hand side** of the assignment operator.

### **Example:**
```javascript
const numbers = [1, 2, 3, 4, 5];

const [a, b, ...others] = numbers;

console.log(a);       // 1
console.log(b);       // 2
console.log(others);  // [3, 4, 5]
```


### **Key Rules:**
- The rest pattern **must be the last element** in the destructuring assignment.
- There **can only be one rest element** in an array destructuring.

**Invalid Example:**
```javascript
const [x, ...y, z] = numbers; // SyntaxError: Rest element must be last
```

---

## **Rest Pattern in Objects (Destructuring)**
- Works similarly to arrays but collects remaining properties into an object.

### **Example:**
```javascript
const openingHours = {
  thu: { open: 12, close: 22 },
  fri: { open: 11, close: 23 },
  sat: { open: 0, close: 24 }
};

const { sat, ...weekdays } = openingHours;

console.log(sat);       // { open: 0, close: 24 }
console.log(weekdays);  // { thu: { open: 12, close: 22 }, fri: { open: 11, close: 23 } }
```
- `sat` is extracted as its own variable.
- `weekdays` collects the remaining properties (`thu` & `fri`) into a new object.

---

## **Rest Parameters in Functions**
- Used to collect multiple arguments into an array.
- Used in function **parameter lists** to handle **an arbitrary number of arguments**.

### **Example:**
```javascript
function add(...numbers) {
  let sum = 0;
  for (let num of numbers) sum += num;
  console.log(sum);
}

add(2, 3);          // 5
add(5, 3, 7, 2);    // 17
add(1, 2, 3, 4, 5); // 15
```
- `...numbers` collects all passed arguments into an array.

### **Rest Parameters vs. Arguments Object**
- The `arguments` object exists in regular functions but **not** in arrow functions.
- Rest parameters (`...`) work in both function expressions and arrow functions.
  
**Invalid Example in Arrow Functions:**
```javascript
const add = () => {
  console.log(arguments); // ReferenceError: arguments is not defined
};
```

**Use Rest Parameters Instead:**
```javascript
const add = (...numbers) => numbers.reduce((sum, num) => sum + num, 0);

console.log(add(5, 3, 2)); // 10
```

---

## **Combining Rest Parameters & Spread Operator**
- **Rest Parameters** collect values into an array.
- **Spread Operator** expands an array into individual values.

### **Example:**
```javascript
const x = [23, 5, 7];

add(...x); // Equivalent to add(23, 5, 7) => Output: 35
```
- `...x` expands the array into individual arguments.
- Inside `add()`, the **rest parameter** collects them back into an array.

---

## **Rest Parameters in Methods (Real-World Example)**
- **Use case**: Handling variable-length arguments in object methods.

### **Example:**
```javascript
const restaurant = {
  orderPizza: function (mainIngredient, ...otherIngredients) {
    console.log(`Main ingredient: ${mainIngredient}`);
    console.log(`Other ingredients: ${otherIngredients.join(', ')}`);
  }
};

restaurant.orderPizza('Mushrooms', 'Onion', 'Olives', 'Spinach');
// Output:
// Main ingredient: Mushrooms
// Other ingredients: Onion, Olives, Spinach

restaurant.orderPizza('Cheese');
// Output:
// Main ingredient: Cheese
// Other ingredients:
```
- The **first argument** is stored in `mainIngredient`.
- The **rest of the arguments** are collected into an array (`otherIngredients`).

---

## **Key Takeaways**
| Feature | **Spread Operator (`...`)** | **Rest Pattern (`...`)** |
|---------|-----------------------------|---------------------------|
| **Purpose** | Expands elements | Collects elements |
| **Used In** | Arrays, function calls, objects | Destructuring (arrays, objects), function parameters |
| **Placement** | Right-hand side of `=` | Left-hand side of `=` |
| **Example** | `const arr = [...numbers, 10]` | `const [a, b, ...rest] = arr` |
| **Functions** | `myFunc(...arr)` (spreading) | `function myFunc(...args) {}` (rest parameters) |