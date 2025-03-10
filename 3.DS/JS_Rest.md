# The Spread Operator (`...`)

The **spread operator** (`...`) is used to expand elements of an **iterable** (like arrays, strings, maps, and sets) into individual values. It is commonly used for **array expansion, function arguments, copying, and merging data structures**.

---

## **Expanding Arrays**

The spread operator **unpacks** array elements, making it easy to include existing arrays within new ones.

```js
const arr = [7, 8, 9];

// Bad way (manual copying)
const badNewArr = [1, 2, arr[0], arr[1], arr[2]];

//  Good way (spread operator)
const goodNewArr = [1, 2, ...arr];
console.log(goodNewArr); // [1, 2, 7, 8, 9]
```

---

## **Using Spread Operator in Function Calls**

The spread operator allows passing array elements as separate function arguments.

```js
const numbers = [23, 5, 7];

console.log(Math.max(...numbers)); //  23 (Expanded array elements)
```

### **Function Example**

```js
const orderPasta = (ing1, ing2, ing3) => {
  console.log(
    `Here is your delicious pasta with ${ing1}, ${ing2}, and ${ing3}.`
  );
};

// Prompt user for ingredients
const ingredients = [
  prompt("Ingredient 1?"),
  prompt("Ingredient 2?"),
  prompt("Ingredient 3?"),
];

//  Using spread to pass arguments
orderPasta(...ingredients);
```

---

## **Copying Arrays (Shallow Copy)**

The spread operator can create **shallow copies** of arrays.

```js
const mainMenu = ["Pizza", "Pasta", "Risotto"];

//  Copying an array
const mainMenuCopy = [...mainMenu];
```

---

## **Merging Arrays**

Easily combine multiple arrays using the spread operator.

```js
const starters = ["Bruschetta", "Garlic Bread", "Salad"];
const mainMenu = ["Pizza", "Pasta", "Risotto"];

//  Merge arrays
const menu = [...starters, ...mainMenu];

console.log(menu);
// ["Bruschetta", "Garlic Bread", "Salad", "Pizza", "Pasta", "Risotto"]
```

---

## **Using Spread with Strings**

Strings are also **iterables**, so they can be spread into arrays.

```js
const name = "Jonas";
const letters = [...name, " ", "S."];

console.log(letters);
// ["J", "o", "n", "a", "s", " ", "S."]
```

---

## **Spread Operator with Objects (ES2018+)**

Although objects are **not iterables**, the spread operator works with them for **copying and merging**.

### **Copying an Object**

```js
const restaurant = {
  name: "Classico Italiano",
  location: "Via Angelo Tavanti 23, Italy",
  categories: ["Italian", "Pizzeria", "Vegetarian", "Organic"],
};

//  Shallow copy
const restaurantCopy = { ...restaurant };
restaurantCopy.name = "Ristorante Roma";

console.log(restaurant.name); // "Classico Italiano" (Original Unchanged)
console.log(restaurantCopy.name); // "Ristorante Roma" (New Copy)
```

### **Merging Objects**

```js
const newRestaurant = {
  ...restaurant,
  founder: "Giuseppe",
  foundedIn: 1998,
};

console.log(newRestaurant);
/*
{
  name: "Classico Italiano",
  location: "Via Angelo Tavanti 23, Italy",
  categories: ["Italian", "Pizzeria", "Vegetarian", "Organic"],
  founder: "Giuseppe",
  foundedIn: 1998
}
*/
```

---

## **Key Differences: Spread Operator vs Destructuring**

| Feature            | Spread Operator (`...`)                            | Destructuring (`[]` or `{}`)                    |
| ------------------ | -------------------------------------------------- | ----------------------------------------------- |
| Purpose            | Expands an iterable into individual elements       | Extracts values from an iterable into variables |
| Creates variables? | No                                                 | Yes                                             |
| Usage              | Creating new arrays, function calls, object copies | Assigning values to variables                   |

### **Example**

```js
const arr = [1, 2, 3];

const newArr = [...arr]; //  Spread (Creates new array)
const [a, b, c] = arr; //  Destructuring (Creates variables)
```

---

## **Summary**

- **The spread operator (`...`) makes working with arrays and objects much easier.**
- **It expands elements for function calls, creates shallow copies, merges arrays/objects, and works with iterables.**
- **It does NOT create new variables like destructuring.**
- **Objects (non-iterables) support spread since ES2018.**
