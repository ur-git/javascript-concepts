# Closure Examples

### Example 1: Nested Functions

```js
function a() {
  var grandpa = "grandpa";
  return function () {
    var father = "father";
    return function () {
      var son = "son";
      return `${grandpa} > ${father} > ${son}`;
    };
  };
}
console.log(a()()()); // grandpa > father > son
```

- **Explanation**: Even after `function a` is invoked and removed from the call stack, its variables remain accessible to the nested functions due to closures.

---

### Example 2: Lexical Scope

```js
let x = 1;

const parentFunction = () => {
  let myValue = 2;
  console.log(x); // 1
  console.log(myValue); // 2

  const childFunction = () => {
    console.log((x += 5)); // 6
    console.log((myValue += 1)); // 3
  };
  childFunction();
};

parentFunction();
```

- **Explanation**: The child function has access to variables in the parent function's scope, showcasing lexical scoping.

---

### Example 3: Closure with Return

```js
const parentFunction = () => {
  let myValue = 2;

  const childFunction = () => {
    console.log((myValue += 1)); // 3, 4, 5 on subsequent calls
  };
  return childFunction;
};

const result = parentFunction();
result();
result();
```

- **Explanation**: The child function retains access to `myValue` in the parent scope, even after the parent function is executed.

---

### Example 4: IIFE and Closures

```js
const privateCounter = (() => {
  let count = 0;
  console.log(`Initial value: ${count}`);
  return () => {
    count += 1;
    console.log(count);
  };
})();

privateCounter();
privateCounter();
```

- **Explanation**: An IIFE (Immediately Invoked Function Expression) creates a private scope. The inner function retains access to `count` through closure.

---

### Example 5: Credits System with IIFE

```js
const credits = ((num) => {
  let credits = num;
  console.log(`Initial credits value: ${credits}`);
  return () => {
    credits -= 1;
    if (credits > 0) {
      console.log(`Playing game, ${credits} credits remaining`);
    } else {
      console.log("Not enough credits");
    }
  };
})(3);

credits();
credits();
credits();
```

- **Explanation**: The `credits` function retains the private `credits` variable and modifies it upon each invocation.

---

### Example 6: setTimeout and Closure

```js
function callFunc() {
  const callMe = "Hi!";
  setTimeout(function () {
    console.log(callMe); // Logs 'Hi!' after 4 seconds
  }, 4000);
}

callFunc();
```

- **Explanation**: The inner function retains access to `callMe` even after `callFunc` execution is complete.

---

### Example 7: Memory Efficiency with Closures

#### Without Closures

```js
function heavyDuty(index) {
  const bigArray = new Array(7000).fill("emoji");
  console.log("Created");
  return bigArray[index];
}

console.log(heavyDuty(688));
console.log(heavyDuty(688));
console.log(heavyDuty(688));
```

- **Output**: Creates a new array each time.

#### With Closures

```js
function heavyDuty2() {
  const bigArray = new Array(7000).fill("emoji");
  console.log("Created");
  return function (index) {
    return bigArray[index];
  };
}

const getHeavyDuty = heavyDuty2();
console.log(getHeavyDuty(688));
console.log(getHeavyDuty(688));
```

- **Explanation**: The array is created only once and reused, showcasing memory efficiency.

---

### Example 8: Data Encapsulation

```js
function Counter() {
  let count = 0;

  return {
    increment: function () {
      count += 1;
    },
    decrement: function () {
      count -= 1;
    },
    getCount: function () {
      return count;
    },
  };
}

const myCounter = Counter();
myCounter.increment();
myCounter.increment();
console.log(myCounter.getCount()); // 2

myCounter.decrement();
console.log(myCounter.getCount()); // 1
```

- **Explanation**: The `count` variable is private and can only be accessed through the returned methods.

---

### Example 9: Loops and Closures

#### Using `var`

```js
const array1 = [1, 2, 3, 4];
for (var i = 0; i < array1.length; i++) {
  (function (index) {
    setTimeout(function () {
      console.log("I'm at index " + array1[index]);
    }, 1000);
  })(i);
}
```

- **Output**: Logs "I'm at index 1", "I'm at index 2", etc.

#### Using `let`

```js
const array2 = [1, 2, 3, 4];
for (let i = 0; i < array2.length; i++) {
  setTimeout(function () {
    console.log("I'm at index " + array2[i]);
  }, 1000);
}
```

- **Output**: Same as above, but simpler syntax due to `let`.

---

## Advantages of Closures

### 1. Memory Efficiency

Closures can prevent recreating large objects or data structures, as shown in the `heavyDuty` example.

### 2. Data Encapsulation

Closures enable private variables, restricting direct access to sensitive data, as shown in the `Counter` example.
