# **ES6 Classes in JavaScript**

- ES6 introduced **classes** as **syntactic sugar** over JavaScript’s **prototypal inheritance**.
- Unlike classes in Java or C++, JavaScript classes **do not create copies** of objects; instead, they use **prototypes** behind the scenes.

```js
// Class Declaration
class PersonCl {
  constructor(firstName, birthYear) {
    this.firstName = firstName;
    this.birthYear = birthYear;
  }
}

// Class Expression (Alternative)
const PersonClExpr = class {
  constructor(firstName, birthYear) {
    this.firstName = firstName;
    this.birthYear = birthYear;
  }
};
```

- Both **class declarations** and **class expressions** exist, similar to functions.

---

## The `constructor` Method

- Every class **must** have a `constructor` method.
- This method runs automatically when a new instance is created.

```js
class PersonCl {
  constructor(firstName, birthYear) {
    this.firstName = firstName;
    this.birthYear = birthYear;
  }
}

const jessica = new PersonCl("Jessica", 1996);
console.log(jessica);
// PersonCl { firstName: "Jessica", birthYear: 1996 }
```

### **Behind the Scenes (How `new` Works)**

1. A new empty object `{}` is created.
2. `this` is set to the new object.
3. The `constructor` function runs and assigns properties.
4. The new object is **linked** to the class prototype.

```js
console.log(jessica.__proto__ === PersonCl.prototype); // true
```

---

## Adding Methods to the Prototype

- Unlike the `constructor`, class methods are automatically added to the prototype, **not directly to the object**.

```js
class PersonCl {
  constructor(firstName, birthYear) {
    this.firstName = firstName;
    this.birthYear = birthYear;
  }

  // Instance Method (added to the prototype)
  calcAge() {
    return new Date().getFullYear() - this.birthYear;
  }
}

const jessica = new PersonCl("Jessica", 1996);
console.log(jessica.calcAge()); // Works via prototype
```

### **Proof: Methods Exist on the Prototype**

```js
console.log(jessica.__proto__); // { calcAge: f }
console.log(jessica.hasOwnProperty("calcAge")); // false (because it's on the prototype)
```

---

## Manually Adding Methods to the Prototype

- You can still manually attach methods to the prototype:

```js
PersonCl.prototype.greet = function () {
  console.log(`Hey ${this.firstName}!`);
};

jessica.greet(); // Hey Jessica!
```

This shows that ES6 classes are **just a cleaner syntax** for prototype-based inheritance.

---

## Key Differences Between Classes and Constructor Functions

| Feature             | Constructor Function          | ES6 Class                            |
| ------------------- | ----------------------------- | ------------------------------------ |
| Syntax              | Function-based                | `class` keyword                      |
| Method Definition   | Manually added to `prototype` | Automatically added to `prototype`   |
| Hoisting            | (functions are hoisted)       | (classes are NOT hoisted)            |
| `this` Behavior     | Must use `new` or it fails    | Must use `new`, strict mode enforced |
| First-Class Citizen | Can be passed around          | Can be passed around                 |

---

## Important Rules About Classes

### **Classes Are NOT Hoisted**

- Unlike function declarations, class declarations **do not get hoisted**.

```js
console.log(new PersonCl("John", 2000)); // ❌ ReferenceError
class PersonCl {
  constructor(firstName, birthYear) {
    this.firstName = firstName;
    this.birthYear = birthYear;
  }
}
```

### **Classes Are First-Class Citizens**

- Just like functions, classes can be:
  - Passed as arguments
  - Returned from functions
  - Stored in variables

### **Classes Are Always in Strict Mode**

- Even if `"use strict"` is not declared, **class body code runs in strict mode**.
