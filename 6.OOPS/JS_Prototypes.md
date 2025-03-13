# Prototypes & Prototypal Inheritance in JavaScript

**Prototype** and **prototypal inheritance** are core concepts in JavaScript that enable **object-oriented programming (OOP)** without traditional class-based inheritance. Instead of copying properties and methods, JavaScript **delegates** them through the prototype chain.

---

## **Prototype in JavaScript**

### **What is a Prototype?**

A **prototype** is an object from which other objects inherit properties and methods. Every JavaScript function (including constructor functions) has a special property called `prototype`.

### **How Prototypes Work?**

1. Every function in JavaScript has a property called `prototype`.
2. When an object is created using a constructor function, it **inherits** properties and methods defined on the constructor’s `prototype` property.
3. Objects have an internal property `[[Prototype]]` (accessible as `__proto__`), which points to their prototype.

---

## **Creating Prototypal Inheritance with Constructor Functions**

```js
// Constructor Function
function Person(firstName, birthYear) {
  this.firstName = firstName;
  this.birthYear = birthYear;
}

// Adding a method to the prototype
Person.prototype.calcAge = function () {
  return new Date().getFullYear() - this.birthYear;
};

// Creating objects using the constructor
const jonas = new Person("Jonas", 1991);
const matilda = new Person("Matilda", 2017);

console.log(jonas.calcAge()); // Accesses the prototype method
console.log(matilda.calcAge());
```

### **How It Works?**

- `Person.prototype` is an object that contains shared methods.
- `jonas` and `matilda` **do not have the `calcAge` method directly on them** but can access it through **prototypal inheritance**.
- `jonas.__proto__ === Person.prototype // true`

---

## **Understanding `__proto__` and `prototype`**

### **`__proto__` vs `prototype`**

| Property    | Purpose                                                                 |
| ----------- | ----------------------------------------------------------------------- |
| `prototype` | Exists on **functions** (constructor functions), used for inheritance.  |
| `__proto__` | Exists on **objects**, points to their prototype (used for delegation). |

`Person.prototype` is **not** the prototype of `Person`. Instead, it is the prototype of objects created by `Person`.

---

## **Adding Properties to the Prototype**

Prototypes can contain **not only methods but also properties**:

```js
Person.prototype.species = "Homo Sapiens";

console.log(jonas.species); // 'Homo Sapiens'
console.log(matilda.species); // 'Homo Sapiens'
```

**Species is not a direct property** of `jonas` or `matilda` but is inherited from the prototype.

### **Checking for Own Properties**

```js
console.log(jonas.hasOwnProperty("firstName")); // true (own property)
console.log(jonas.hasOwnProperty("species")); // false (inherited property)
```

`hasOwnProperty()` checks if a property exists **directly** on an object (not inherited).

---

## **Prototype Chain**

JavaScript objects are linked through a **prototype chain**:

1. If a property/method is not found on an object, JavaScript looks up the chain.
2. It follows `__proto__` → `constructor.prototype` → `Object.prototype`.

### **Visualizing the Chain**

```js
console.log(jonas.__proto__); // Person.prototype
console.log(jonas.__proto__.__proto__); // Object.prototype
console.log(jonas.__proto__.__proto__.__proto__); // null
```

**All objects ultimately inherit from `Object.prototype`**.

---

## **Checking Prototypes**

### **Using `isPrototypeOf()`**

```js
console.log(Person.prototype.isPrototypeOf(jonas)); // true
console.log(Person.prototype.isPrototypeOf(matilda)); // true
```

Confirms that `Person.prototype` is the prototype of `jonas`.

---

## **Prototypal Inheritance with `Object.create()`**

Another way to implement prototypal inheritance is using `Object.create()`:

```js
const personProto = {
  calcAge() {
    return new Date().getFullYear() - this.birthYear;
  },
};

// Creating a new object with `personProto` as its prototype
const sarah = Object.create(personProto);
sarah.birthYear = 1990;

console.log(sarah.calcAge()); // Works due to inheritance
console.log(sarah.__proto__ === personProto); // true
```

**`Object.create()` creates objects with a given prototype** instead of using constructor functions.

---

## **Why Use Prototypes?**

- Saves memory (methods are not duplicated).
- Enables object inheritance without class-based OOP.
- Forms the basis for modern JavaScript classes.
