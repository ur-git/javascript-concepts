# Notes: Passing Arguments into Functions in JavaScript

### Key Concepts Covered
1. **Primitive Types vs. Reference Types**
2. **How Arguments Are Passed to Functions**
3. **Pass-by-Value vs. Pass-by-Reference**
4. **Practical Implications and Pitfalls**

---

### Primitive Types vs. Reference Types Recap
- **Primitive types** include `number`, `string`, `boolean`, `undefined`, `null`, `symbol`, and `bigint`.
  - These are immutable and stored directly in the variable.
- **Reference types** include objects, arrays, and functions.
  - These are mutable and stored as references (memory addresses) in the variable.

### Example: Passing Arguments into Functions
```javascript
// Primitive value example
let flight = 'LH234';

// Reference type example
const passenger = {
  name: 'Jonas Schmedtmann',
  passport: 1234567890
};

function checkIn(flightNum, passenger) {
  // Modifying the arguments
  flightNum = 'LH999'; // Bad practice: Modifying parameters
  passenger.name = 'Mr. ' + passenger.name;

  // Validating passport
  if (passenger.passport === 1234567890) {
    alert('Check-in successful!');
  } else {
    alert('Wrong passport!');
  }
}

checkIn(flight, passenger);
console.log(flight); // Output: 'LH234'
console.log(passenger); // Output: { name: 'Mr. Jonas Schmedtmann', passport: 1234567890 }
```

#### Analysis of Results
- The `flight` variable (primitive type) remains unchanged outside the function.
  - Primitives are passed **by value**, creating a copy of the value.
- The `passenger` object (reference type) is modified.
  - Reference types are passed as references to the memory location, so changes affect the original object.

---

### Understanding Argument Behavior
1. **Primitive Types**
   - Passed by value.
   - Modifications to the parameter inside the function do not affect the original variable.

   Example:
   ```javascript
   let x = 10;

   function modifyValue(num) {
     num = 20;
   }

   modifyValue(x);
   console.log(x); // Output: 10
   ```

2. **Reference Types**
   - Passed by reference (the reference itself is passed by value).
   - Modifications to the object inside the function affect the original object.

   Example:
   ```javascript
   const obj = { value: 10 };

   function modifyObject(o) {
     o.value = 20;
   }

   modifyObject(obj);
   console.log(obj.value); // Output: 20
   ```

### Pitfalls of Passing Reference Types
When multiple functions modify the same object, unintended consequences can occur.

#### Example:
```javascript
function newPassport(person) {
  person.passport = Math.trunc(Math.random() * 10000000000);
}

newPassport(passenger);
checkIn(flight, passenger); // Output: 'Wrong passport!'
```
**Problem:**
- The `newPassport` function modifies the `passenger` object.
- The `checkIn` function then fails because the `passport` value no longer matches the expected value.

**Key Takeaway:**
- Be cautious when passing and modifying objects in large codebases, especially when working in teams.

---

### Pass-by-Value vs. Pass-by-Reference
- **JavaScript uses pass-by-value for all function arguments.**
  - For primitives, a copy of the value is passed.
  - For objects, a copy of the reference is passed.
- **Important Distinction:**
  - JavaScript does not support true pass-by-reference (like in C++).
  - A reference to an object is passed as a value, allowing the function to access and modify the original object.

---

### Common Misconceptions
- **"JavaScript passes objects by reference."**
  - Incorrect. JavaScript passes a copy of the reference (pass-by-value).
- **"Modifications inside a function always affect the original object."**
  - True for reference types, but primitives remain unaffected.

---

### Summary and Best Practices
1. **Understand the behavior of primitives and reference types.**
2. **Avoid modifying function parameters directly.**
   - Instead, return new values or objects from the function if needed.
3. **Be cautious when passing reference types to functions.**
   - Document and control how objects are shared and manipulated across functions.
4. **Use immutable programming patterns where appropriate.**
   - Libraries like `Immutable.js` can help enforce immutability.

By understanding these concepts and applying best practices, you can avoid common pitfalls and write more predictable, maintainable JavaScript code.

