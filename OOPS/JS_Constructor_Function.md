# Object-Oriented Programming with Constructor Functions in JavaScript

## Introduction

In this lecture, we explore **Object-Oriented Programming (OOP)** using **constructor functions** in JavaScript. Constructor functions allow us to **programmatically create objects**, a major step beyond simple object literals.

---

## Constructor Functions in JavaScript

A **constructor function** is a **regular function** used to create objects. The key distinction is that **it is called with the `new` keyword**.

### Example: Creating a Constructor Function

```js
const Person = function (firstName, birthYear) {
  this.firstName = firstName;
  this.birthYear = birthYear;
};
```

### Calling a Constructor Function

```js
const jonas = new Person("Jonas", 1991);
console.log(jonas);
```

### **What Happens When We Call a Constructor Function?**

Calling a constructor function with the `new` keyword follows these **four steps**:

1. **A new empty object is created**  
   → `{}`

2. **The function is called, and `this` is set to the new object**  
   → `this = {}`

3. **The new object is linked to the constructor’s prototype**  
   → `this.__proto__ = Person.prototype`

4. **The function automatically returns the newly created object**  
   → `return this`

Example:

```js
const matilda = new Person("Matilda", 2017);
const jack = new Person("Jack", 1985);
console.log(matilda, jack);
```

---

## **Constructor Function Naming Conventions**

- Constructor functions **start with a capital letter** (e.g., `Person`).
- Only **function expressions** and **function declarations** can be used as constructors.
  - ❌ **Arrow functions do not work** because they lack their own `this`.

---

## **Checking if an Object is an Instance of a Constructor**

JavaScript provides the **`instanceof`** operator to check if an object was created using a specific constructor:

```js
console.log(jonas instanceof Person); // true
console.log(matilda instanceof Person); // true
console.log({} instanceof Person); // false
```

---

## **Instance Properties and Methods**

Properties like `firstName` and `birthYear` are called **instance properties** because they are specific to each instance of `Person`.

### **Adding Methods to a Constructor Function (⚠️ Bad Practice)**

You can add methods inside a constructor, but this is inefficient:

```js
const Person = function (firstName, birthYear) {
  this.firstName = firstName;
  this.birthYear = birthYear;

  // ❌ Bad practice - creates a new function for every instance
  this.calcAge = function () {
    console.log(2037 - this.birthYear);
  };
};
```

❌ **Problem:** If we create 1,000 objects, this approach creates **1,000 copies of the `calcAge` method**, negatively impacting performance.

---

## **Best Practice: Using Prototypes for Methods**

Instead of adding methods directly in the constructor, use the **prototype chain** (covered in the next lecture):

```js
Person.prototype.calcAge = function () {
  console.log(2037 - this.birthYear);
};
```

Now all instances **share** the same method, avoiding duplicate function creations.

```js
jonas.calcAge(); // 46
matilda.calcAge(); // 20
```

---

## **Summary**

✔️ **Constructor functions** allow us to programmatically create objects.  
✔️ Always use the `new` keyword with constructors.  
✔️ The **four steps of `new`**:

1.  Create an empty object `{}`
2.  Set `this` to the new object
3.  Link the object to a prototype
4.  Return the object  
    ✔️ Use `instanceof` to check if an object was created from a constructor.  
    ✔️ **Avoid defining methods inside constructors**—use **prototypes** instead for efficiency.
