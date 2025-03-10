# JavaScript Memory Management: Primitives, Objects, and References

## Introduction

Memory management in JavaScript refers to how the JavaScript engine allocates and deallocates memory for variables, ensuring efficient application performance. Unlike lower-level languages like C or C++, where memory management is manual, JavaScript handles it automatically, reducing risks like memory leaks.

## Memory Lifecycle

Each value in JavaScript goes through a **memory lifecycle**:

1. **Allocation**: The engine reserves memory when a value is created.
2. **Usage**: Memory is utilized when the value is accessed (read, updated, etc.).
3. **Deallocation**: When the value is no longer needed, its memory is freed.

## Memory Allocation in JavaScript

Memory allocation in JavaScript depends on the type of value:

- **Primitive values** (numbers, strings, Booleans, undefined, null, symbols, BigInts) are stored **in the call stack**.
- **Objects** (including arrays, functions, and objects) are stored **in the heap**.
- **Object references** are stored **in the call stack**.

## The JavaScript Engine: Call Stack & Heap

The JavaScript engine consists of two primary memory areas:

- **Call Stack**: Where execution contexts are managed, and primitive values are stored.
- **Heap**: Where objects are stored, allowing dynamic memory allocation.

### Primitive Values and the Call Stack

When a primitive value is assigned to a variable, its actual value is stored in the call stack. Each variable gets its own copy, meaning changes to one variable do not affect another.

```js
let age = 30;
let newAge = age;
newAge++;
console.log(age); // 30 (unchanged)
console.log(newAge); // 31
```

Each variable has an independent copy of the value.

### Objects and the Heap

Objects are stored in the heap, and variables in the call stack hold references (memory addresses) to these objects.

```js
const location = { city: "Paris" };
const newLocation = location;
newLocation.city = "Lisbon";
console.log(location.city); // "Lisbon"
```

Since `newLocation` and `location` reference the **same** object, modifying one affects the other.

## Object References and Mutability

- **Objects are reference types**: Assigning an object to another variable copies the reference, not the object itself.
- **Mutations affect all references**: Changing an object through one variable reflects in all variables pointing to the same object.

## Functions as Objects

Functions in JavaScript are also objects and are stored in the heap. The variable pointing to a function stores a reference, not the function itself.

```js
function calcAge(year) {
  return 2024 - year;
}
const newFunc = calcAge;
console.log(newFunc(2000)); // 24
```

Both `calcAge` and `newFunc` reference the same function in the heap.

## Key Takeaways

- **Primitive values are stored in the call stack and copied when assigned.**
- **Objects are stored in the heap, and variables hold references to them.**
- **Copying an object only copies its reference, not the object itself.**
- **Changes to an object affect all references pointing to it.**

## Shallow Copy vs Deep Copy

### Shallow Copy (Using Spread Operator)

```javascript
const jessica1 = {
  firstName: "Jessica",
  lastName: "Williams",
  age: 27,
  family: ["Alice", "Bob"],
};

const jessicaCopy = { ...jessica1 };
jessicaCopy.lastName = "Davis";
jessicaCopy.family.push("Mary", "John");

console.log("Original:", jessica1);
console.log("Copy:", jessicaCopy);
```

**Unexpected Output:**

```plaintext
Original: { firstName: "Jessica", lastName: "Williams", age: 27, family: ["Alice", "Bob", "Mary", "John"] }
Copy: { firstName: "Jessica", lastName: "Davis", age: 27, family: ["Alice", "Bob", "Mary", "John"] }
```

#### Issue:

- The **spread operator creates a shallow copy**, meaning only the first level of properties is copied.
- The `family` array (a nested object) is **still referenced**, so changes affect both objects.

### Deep Copy (Using `structuredClone`)

```javascript
const jessicaClone = structuredClone(jessica1);
jessicaClone.family.push("Mary", "John");

console.log("Original:", jessica1);
console.log("Clone:", jessicaClone);
```

**Correct Output:**

```plaintext
Original: { firstName: "Jessica", lastName: "Williams", age: 27, family: ["Alice", "Bob"] }
Clone: { firstName: "Jessica", lastName: "Williams", age: 27, family: ["Alice", "Bob", "Mary", "John"] }
```

#### Explanation:

- `structuredClone()` creates a **deep copy**, including all nested objects.
- Modifying the cloned object does not affect the original object.

## Key Takeaways

1. **Objects are stored in the heap**, and variables hold references to them.
2. **Assigning an object to a new variable does not create a new object**; it copies the reference.
3. **Functions modify objects passed to them by reference**.
4. **Spread operator (`...`) creates a shallow copy**, copying only the first level of properties.
5. **`structuredClone()` creates a deep copy**, ensuring nested objects are also copied separately.

**Remember:** If you need a deep copy in JavaScript, always use `structuredClone()` or similar deep cloning methods to avoid unexpected mutations!

## Memory Management and Garbage Collection

### Memory Lifecycle in JavaScript

1. **Allocation:** Memory is allocated when a variable is declared.
2. **Usage:** The allocated memory is used for computations and operations.
3. **Release:** Memory is automatically released when it is no longer needed.

### Stack Memory Management

- Primitives are stored in the **call stack**.
- When an execution context is removed from the stack, its variables are also removed.
- Global variables stay in memory as long as the program runs.

### Heap Memory and Garbage Collection

- Objects are stored in the **heap**.
- The JavaScript engine automatically manages heap memory using **garbage collection**.
- The most common algorithm used is **mark-and-sweep**:
  1. **Mark Phase:** The engine marks all objects that are reachable from the **root** (global execution context, function execution contexts, event listeners, etc.).
  2. **Sweep Phase:** Unmarked (unreachable) objects are removed, freeing up memory.

### Preventing Memory Leaks

- **Unnecessary global variables:** Avoid storing large objects globally, as they are never garbage collected.
- **Dangling event listeners:** Remove event listeners when they are no longer needed.
- **Timers and intervals:** Clear `setTimeout` and `setInterval` when they are no longer required.

## Key Takeaways

1. **Objects are stored in the heap**, and variables hold references to them.
2. **Assigning an object to a new variable does not create a new object**; it copies the reference.
3. **Functions modify objects passed to them by reference**.
4. **Spread operator (`...`) creates a shallow copy**, copying only the first level of properties.
5. **`structuredClone()` creates a deep copy**, ensuring nested objects are also copied separately.
6. **Garbage collection automatically removes unreachable objects to free memory.**
7. **Prevent memory leaks by managing global variables, event listeners, and timers properly.**

**Remember:** If you need a deep copy in JavaScript, always use `structuredClone()` or similar deep cloning methods to avoid unexpected mutations!
