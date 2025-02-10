Here are the markdown notes for the Object-Oriented Programming (OOP) lecture in JavaScript:

---

# **Object-Oriented Programming (OOP) in JavaScript**

## **Introduction**

- JavaScript follows a unique OOP model based on **prototypes** rather than classical **class-based inheritance**.
- While JavaScript introduced **ES6 classes**, they are just syntactic sugar over the existing **prototype-based inheritance**.

## **Review of Classical OOP**

- In traditional OOP (e.g., Java, C++):
  - **Classes** act as **blueprints** for creating **instances (objects)**.
  - **Instantiation** refers to the process of creating an object from a class.
  - **Inheritance** allows a class to derive properties and methods from another class.

## **JavaScript’s Prototype-Based OOP**

- Every JavaScript object is linked to a **prototype object**.
- This prototype contains **methods and properties** that can be accessed by all objects linked to it.
- This mechanism is called **prototypal inheritance**.

### **Key Terminology**

- **Prototype:** An object from which other objects inherit methods and properties.
- **Prototypal Inheritance:** Objects inherit directly from other objects (prototypes) rather than from a class.
- **Delegation:** Objects delegate behavior (methods) to their prototype rather than copying them.

### **How It Works**

- When a method is called on an object, JavaScript first checks if the method exists on the object itself.
- If not, it looks up the prototype chain to find the method.

### **Example: Prototypes in Action**

```js
const num = [1, 2, 3]; // An array instance
num.map((x) => x * 2); // Uses the map() method

// But where is map() defined?
console.log(num.__proto__ === Array.prototype); // true
```

- The `map()` method is actually defined in `Array.prototype`, and all arrays inherit from this prototype.

## **Three Ways to Implement OOP in JavaScript**

### 1️⃣ **Constructor Functions**

- Used to programmatically create objects and set their prototype.
- The traditional way of implementing OOP in JavaScript.

### 2️⃣ **ES6 Classes**

- Introduced in ES6 as a more intuitive syntax for OOP.
- **Behind the scenes, ES6 classes use prototypes and constructor functions**.

### 3️⃣ **Object.create()**

- The most direct way to create an object linked to a prototype.
- Less commonly used than the other two methods.