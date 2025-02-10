### **Object-Oriented Programming (OOP) - An Overview**

#### **What is Object-Oriented Programming (OOP)?**

OOP is a programming paradigm that organizes code around **objects**. Objects are used to model real-world entities, such as users, to-do list items, or abstract structures like HTML components and data models.

Each object contains:

- **Data (Properties)** – Represents the characteristics of the object.
- **Methods (Behavior)** – Functions that define actions an object can perform.

By grouping data and behavior together, OOP allows for **better organization, easier maintenance, and improved flexibility** in software development.

#### **Why OOP?**

OOP was developed to solve the problem of **spaghetti code**, where functions and variables are scattered across the global scope, making it difficult to manage large codebases. With OOP, we structure code into **self-contained objects**, making it more maintainable and scalable.

### **Key Concepts in OOP**

#### **1. Classes and Instances**

A **class** is like a **blueprint** for creating objects. It defines the properties and behavior that objects (instances) should have.

- The **class** itself is not an object but a model for creating objects.
- Each **instance** of a class is a real, usable object that follows the blueprint.
- Multiple instances can be created from the same class, each with its own unique data.

📌 **Analogy**: A class is like an **architect’s blueprint** for a house. The actual houses built using that blueprint are the **instances** of the class.

#### **2. The Four Pillars of OOP**

1️⃣ **Abstraction**

- Hiding unnecessary details and exposing only what is needed.
- Example: When using a **smartphone**, users interact with a simple interface (buttons, touchscreen), while the internal processes (battery management, CPU operations) remain hidden.
- In programming, functions like `addEventListener()` work without requiring developers to understand their internal implementation.

2️⃣ **Encapsulation**

- Keeping **properties and methods private** within a class to prevent direct access from outside.
- Instead, we provide a **public interface (API)** to interact with the object.
- **Benefits**:
  - Prevents unintended modifications to an object’s state.
  - Makes code easier to maintain and less error-prone.
- Example:

  ```js
  class User {
    #password; // Private property (not accessible from outside)

    constructor(username, password) {
      this.username = username;
      this.#password = password;
    }

    login(inputPassword) {
      return inputPassword === this.#password;
    }
  }

  const user = new User("JohnDoe", "secure123");
  console.log(user.login("secure123")); // ✅ True
  console.log(user.#password); // ❌ Error: Private property
  ```

3️⃣ **Inheritance**

- A **child class** can inherit properties and methods from a **parent class**.
- This avoids code duplication by reusing logic.
- Example:

  ```js
  class User {
    constructor(username, email) {
      this.username = username;
      this.email = email;
    }

    login() {
      console.log(`${this.username} logged in.`);
    }
  }

  class Admin extends User {
    deleteUser(user) {
      console.log(`${user.username} has been deleted.`);
    }
  }

  const admin = new Admin("AdminUser", "admin@example.com");
  admin.login(); // ✅ AdminUser logged in.
  admin.deleteUser({ username: "JohnDoe" }); // ✅ JohnDoe has been deleted.
  ```

4️⃣ **Polymorphism**

- Allows a child class to **override** a method inherited from its parent class.
- Example:

  ```js
  class User {
    login() {
      console.log("User logged in.");
    }
  }

  class Admin extends User {
    login() {
      console.log("Admin logged in with special privileges.");
    }
  }

  const user = new User();
  const admin = new Admin();

  user.login(); // ✅ "User logged in."
  admin.login(); // ✅ "Admin logged in with special privileges."
  ```

### **Summary**

- OOP organizes code into objects, making it more manageable.
- Objects contain **data (properties)** and **behavior (methods)**.
- Classes are **blueprints** used to create objects (instances).
- The **four pillars of OOP** (Abstraction, Encapsulation, Inheritance, Polymorphism) help in designing efficient, reusable, and scalable code.
