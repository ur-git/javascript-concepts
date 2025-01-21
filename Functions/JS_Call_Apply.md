# Understanding and Controlling the `this` Keyword in JavaScript

## Overview

In this guide, we will revisit the `this` keyword and learn how to **manually set its value** using the `call`, `apply`, and `bind` methods. This enables us to control how functions behave in different contexts, particularly when reusing methods across multiple objects.

---

## Setting the Stage: Example Scenario

Imagine you're managing an airline booking system for the Lufthansa Group, which includes multiple airlines such as **Lufthansa**, **Eurowings**, and **Swiss Airlines**.

### Creating the Lufthansa Object

Here's how we define an object for Lufthansa with its booking system:

```javascript
const lufthansa = {
  airline: "Lufthansa",
  iataCode: "LH",
  bookings: [],
  book(flightNumber, passengerName) {
    console.log(
      `${passengerName} booked a seat on ${this.airline} flight ${this.iataCode}${flightNumber}`
    );
    this.bookings.push({ flight: `${this.iataCode}${flightNumber}`, passengerName });
  },
};

// Example usage
lufthansa.book(239, "Jonas Schmedtmann");
lufthansa.book(635, "Mike Smith");
console.log(lufthansa.bookings);
```

Output:
```plaintext
Jonas Schmedtmann booked a seat on Lufthansa flight LH239
Mike Smith booked a seat on Lufthansa flight LH635
[
  { flight: 'LH239', passengerName: 'Jonas Schmedtmann' },
  { flight: 'LH635', passengerName: 'Mike Smith' }
]
```

---

## Extending the Booking System to New Airlines

Instead of duplicating the `book` method across objects, we'll **reuse it** for other airlines. To achieve this, we need to control the `this` keyword dynamically.

### Creating the Eurowings Object

```javascript
const eurowings = {
  airline: "Eurowings",
  iataCode: "EW",
  bookings: [],
};

// Attempt to reuse the book method
const book = lufthansa.book;
book(23, "Sarah Williams"); // Error: Cannot read property 'airline' of undefined
```

This error occurs because the `this` keyword in the `book` function points to `undefined` when called as a regular function. To fix this, we use **manual control** of `this`.

---

## Method 1: Using the `call` Method

The `call` method allows us to manually set the `this` keyword.

### Syntax
```javascript
functionName.call(thisArg, arg1, arg2, ...);
```

### Example
```javascript
book.call(eurowings, 23, "Sarah Williams");
console.log(eurowings.bookings);

book.call(lufthansa, 239, "Mary Cooper");
console.log(lufthansa.bookings);
```

Output:
```plaintext
Sarah Williams booked a seat on Eurowings flight EW23
Mary Cooper booked a seat on Lufthansa flight LH239
```

---

## Method 2: Using the `apply` Method

The `apply` method works similarly to `call` but accepts an **array** of arguments instead of a list.

### Syntax
```javascript
functionName.apply(thisArg, [arg1, arg2, ...]);
```

### Example
```javascript
const flightData = [583, "George Cooper"];
book.apply(eurowings, flightData);
console.log(eurowings.bookings);
```

Output:
```plaintext
George Cooper booked a seat on Eurowings flight EW583
```

### Modern Alternative: Spread Operator with `call`

Instead of using `apply`, you can use the spread operator with `call`:

```javascript
book.call(eurowings, ...flightData);
```

This is now the preferred approach in modern JavaScript.

---

## Summary

- The `call` and `apply` methods allow us to **manually control the `this` keyword**.
- Use `call` for passing arguments as a list and `apply` for passing arguments as an array.
- The **spread operator** with `call` is a modern and concise alternative to `apply`.
