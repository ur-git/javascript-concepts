# JS Common Problems Set

## **String Manipulation**

1. **Reverse a string without using built-in methods**

   - Implement a function that takes a string as input and returns the reversed version of the string without using JavaScript’s built-in `.reverse()` method.

2. **Check if a given string is a palindrome**

   - Write a function that determines whether a given string reads the same forward and backward (ignoring case and spaces).

3. **Find the longest word in a given sentence**

   - Given a sentence as a string, write a function to return the longest word in the sentence. If multiple words have the same length, return the first one encountered.

4. **Count the occurrences of each character in a string**

   - Implement a function that takes a string as input and returns an object where the keys are characters, and the values are the number of times each character appears in the string.

5. **Check if a string contains balanced parentheses**

   - Given a string containing only parentheses (`()`, `{}`, `[]`), write a function to determine if the brackets are properly balanced.

6. **Find the first non-repeating character in a string**

   - Implement a function that returns the first character in a string that does not repeat. If all characters repeat, return `null`.

7. **Reverse the order of words in a sentence without using built-in methods**

   - Given a string containing multiple words, write a function to reverse the order of the words without using the `.reverse()` method.

8. **Generate all permutations of a given string**
   - Write a function that returns an array containing all possible permutations of a given string.

---

## **Array Manipulation**

9. **Find the largest number in an array**

   - Implement a function that takes an array of numbers as input and returns the largest number.

10. **Find the smallest missing number in an array of numbers from 1 to N**

    - Given an array containing unique numbers from `1` to `N`, but missing one number, write a function to find the missing number.

11. **Find the maximum count of consecutive 1s in a binary array**

    - Write a function that takes an array of `0s` and `1s` and returns the maximum number of consecutive `1s`.

12. **Find the Kth largest element in an array**

    - Given an unsorted array and an integer `K`, implement a function to find the `K`th largest element without sorting the entire array.

13. **Sort an array without using the built-in `.sort()` method**

    - Implement a sorting algorithm (such as Bubble Sort or Quick Sort) to sort an array of numbers in ascending order.

14. **Sort an array of numbers in ascending order**

    - Write a function that sorts an array of numbers from smallest to largest.

15. **Sort an array of numbers in descending order**

    - Write a function that sorts an array of numbers from largest to smallest.

16. **Remove duplicate elements from an array**

    - Given an array with duplicate values, write a function that returns a new array with only unique values.

17. **Flatten a nested array into a single-dimensional array**

    - Implement a function that takes a deeply nested array and returns a flattened array without using built-in methods like `.flat()`.

18. **Merge two sorted arrays into a single sorted array**

    - Given two sorted arrays, write a function to merge them into one sorted array without using built-in sorting methods.

19. **Find the intersection of two arrays**

    - Write a function that returns an array containing only the common elements present in both given arrays.

20. **Rotate an array by K steps**

    - Implement a function that rotates an array to the right by `K` steps, where `K` is a non-negative integer.

21. **Return only the even numbers from an array**
    - Write a function that filters out and returns only even numbers from a given array.

---

## **Object Manipulation**

22. **Deep clone an object**

    - Implement a function that creates a deep copy of a given object, ensuring that nested objects and arrays are also cloned.

23. **Convert a string input into an object**

    - Given a string representing an object (e.g., `"name:John, age:30"`), write a function to convert it into a JavaScript object.

24. **Find unique objects in an array of objects**
    - Given an array of objects, write a function that returns only unique objects based on specific properties.

---

## **Mathematical Computation**

25. **Find the factorial of a given number**

    - Implement a function that returns the factorial of a given number using both iterative and recursive approaches.

26. **Check if a given number is prime**

    - Write a function that determines whether a given number is a prime number.

27. **Return the Fibonacci sequence up to a given number of terms**

    - Implement a function that generates and returns the Fibonacci sequence up to `N` terms.

28. **Find the maximum profit from stock prices**
    - Given an array where each element represents the stock price on a particular day, write a function to determine the maximum possible profit by buying and selling once.

---

## **Anagram & Frequency Matching**

29. **Group anagrams from an array of strings**

    - Given an array of words, write a function to group words that are anagrams of each other.

30. **Check if two strings are anagrams**

    - Implement a function that checks if two given strings are anagrams (i.e., they contain the same letters in a different order).

31. **Check if every value in `arr1` has its corresponding squared value in `arr2` with the same frequency**
    - Given two arrays, write a function that returns `true` if every number in `arr1` has its squared value present in `arr2` with the same frequency.

---

## **Asynchronous Programming & Performance Optimization**

32. **Implement a custom Promise**

    - Write a basic implementation of JavaScript’s `Promise` class with `resolve` and `reject` functionality.

33. **Write a polyfill for `Promise.all()`**

    - Implement the `Promise.all()` function from scratch, which takes an array of promises and resolves when all of them resolve.

34. **Implement an event emitter (`on`, `off`, `emit`)**

    - Build an event emitter that allows adding event listeners (`on`), removing them (`off`), and triggering them (`emit`).

35. **Implement memoization in JavaScript**

    - Write a function that optimizes performance by storing the results of expensive function calls and returning the cached result when the same inputs occur again.

36. **Implement a debounce function**

    - Implement a debounce function that ensures a function executes only after a specified delay since the last invocation.

37. **Implement a throttle function**

    - Implement a throttle function that ensures a function executes at most once every specified time interval.

38. **Implement an LRU (Least Recently Used) cache**
    - Design and implement an LRU cache with `get` and `set` methods that maintains the most recently used elements.

---
