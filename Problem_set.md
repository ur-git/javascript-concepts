# Basic

1. **Reverse a String**
   Input: `"hello"` → Output: `"olleh"`

2. **Check Palindrome**
   Input: `"madam"` → Output: `true`
   Input: `"hello"` → Output: `false`

3. **FizzBuzz (1–15)**
   Output: `1, 2, fizz, 4, buzz, fizz, 7, 8, fizz, buzz, 11, fizz, 13, 14, fizzbuzz`

4. **Factorial of a Number**
   Input: `5` → Output: `120`

5. **Largest Number in an Array**
   Input: `[2, 8, 1, 10, 6]` → Output: `10`

6. **Count Occurrences of Characters in String**
   Input: `"banana"` → Output: `{ b: 1, a: 3, n: 2 }`

7. **Sort Array Ascending**
   Input: `[5, 1, 4, 2]` → Output: `[1, 2, 4, 5]`

8. **Sort Array Descending**
   Input: `[5, 1, 4, 2]` → Output: `[5, 4, 2, 1]`

9. **Remove Duplicates from Array**
   Input: `[1, 2, 2, 3, 4, 4]` → Output: `[1, 2, 3, 4]`

10. **Max Consecutive 1’s**
    Input: `[1, 1, 0, 1, 1, 1]` → Output: `3`

11. **Filter Even Numbers**
    Input: `[1, 2, 3, 4, 5, 6]` → Output: `[2, 4, 6]`

12. **Longest Word in a Sentence**
    Input: `"I am learning JavaScript"` → Output: `"JavaScript"`

13. **Reverse Words in a Sentence**
    Input: `"I love coding"` → Output: `"coding love I"`

14. **Check Prime Number**
    Input: `7` → Output: `true`
    Input: `10` → Output: `false`

---

# Intermediate

15. **Longest Substring Without Repeating Characters**
    Input: `"abcabcbb"` → Output: `3` (`"abc"`)

16. **Flatten Nested Array**
    Input: `[1, [2, [3, 4]], 5]` → Output: `[1, 2, 3, 4, 5]`

17. **Unique Objects in Array**
    Input: `[{name:"sai"},{name:"sai"},{name:"Nang"}]`
    Output: `[{name:"sai"},{name:"Nang"}]`

18. **Merge Two Sorted Arrays**
    Input: `[0, 3, 4, 31]` and `[4, 6, 30]` → Output: `[0, 3, 4, 4, 6, 30, 31]`

19. **Intersection of Two Arrays**
    Input: `[1,2,3,4]` and `[3,4,5,6]` → Output: `[3,4]`

20. **Rotate Array by K steps**
    Input: `[1,2,3,4,5,6,7], k=3` → Output: `[5,6,7,1,2,3,4]`

21. **Balanced Parentheses Check**
    Input: `"(()())"` → Output: `true`
    Input: `"(()"` → Output: `false`

22. **Group Anagrams**
    Input: `["eat","tea","tan","ate","nat","bat"]`
    Output: `[["eat","tea","ate"], ["tan","nat"], ["bat"]]`

23. **Check Squared Array Relationship**
    Input: `[1,2,3]` and `[1,4,9]` → Output: `true`
    Input: `[1,2,3]` and `[1,9]` → Output: `false`

24. **Largest Element in Nested Array**
    Input: `[[3,4,58], [709,8,9,[10,11]], [111,2]]` → Output: `709`

25. **Fibonacci Sequence up to N terms**
    Input: `5` → Output: `[0,1,1,2,3]`

26. **Convert String Path to Nested Object**
    Input: `("a.b.c", "value")` → Output: `{a:{b:{c:"value"}}}`

27. **3rd Least Occurred Number**
    Input: `[4,4,2,2,3,3,3,1,1,1,1]` → Output: `2`

---

# Advanced JavaScript

28. **Deep Clone an Object**
    Input: `{a:1, b:{c:2}}` → Output: Deeply cloned copy

29. **Check Anagrams**
    Input: `"listen"`, `"silent"` → Output: `true`

30. **First Non-Repeating Character**
    Input: `"swiss"` → Output: `"w"`

31. **Smallest Missing Number (1 to N)**
    Input: `[1,2,3,5]` → Output: `4`

32. **Generate All Permutations of a String**
    Input: `"abc"` → Output: `["abc","acb","bac","bca","cab","cba"]`

33. **Kth Largest Element**
    Input: `[3,2,1,5,6,4], k=2` → Output: `5`

34. **Max Profit from Stock Prices**
    Input: `[7,1,5,3,6,4]` → Output: `5`

35. **Serialize & Deserialize Binary Tree**
    Example:
    Input: `Tree(1, left=2, right=3)` → `"1,2,#,#,3,#,#"`

36. **Given an array, return an array where the each value is the product of the next two items**
    Input: `[3, 4, 5]` → Output `[20, 15, 12]`

37. **Debounce Function**
    Example: Prevents firing API calls on every keystroke.

38. **Throttle Function**
    Example: Ensures a function runs at most once every X ms.

39. **Custom Promise Implementation**
    Example:

```js
let p = new MyPromise((res, rej) => res(10));
p.then((val) => console.log(val)); // 10
```

40. **Event Emitter**
    Example:

```js
emitter.on("event", () => console.log("hi"));
emitter.emit("event"); // hi
```

41. **Polyfill for `Array.map()`**
    Input: `[1,2,3].myMap(x => x*2)` → Output: `[2,4,6]`

42. **Polyfill for `Promise.all()`**
    Input: `[Promise.resolve(1), Promise.resolve(2)]`
    Output: `[1,2]`

---
