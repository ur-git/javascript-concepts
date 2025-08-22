# Tree Shaking

## **What is Tree Shaking in JavaScript?**

Tree shaking is a bundler optimization technique that removes unused code from the final JavaScript bundle by statically analyzing ES modules (`import`/`export`). It helps reduce bundle size and improve performance

It is used in modern JavaScript bundlers (like Webpack, Rollup, Parcel, ESBuild)

It’s called “tree shaking” because the bundler analyzes the dependency tree of your modules and _shakes off_ any unused branches (exports) — keeping only the parts of the code that are actually used.

---

### **Why do we need Tree Shaking?**

- To reduce **bundle size**
- Improve **performance & load time**
- Avoid shipping unnecessary code to the browser

---

### **How does it work?**

1. Requires **ES6 Module syntax (`import` / `export`)** because they are **static imports** (analyzed at build time).

   ```js
   // utils.js
   export function add(a, b) {
     return a + b;
   }
   export function multiply(a, b) {
     return a * b;
   }

   // index.js
   import { add } from "./utils.js";
   console.log(add(2, 3));
   ```

   👉 Here, `multiply()` is never used → bundler can tree-shake it.

2. Bundler does **static analysis** → removes unused exports.

3. The final bundle will only include `add()`, not `multiply()`.

---

### **When does Tree Shaking fail?**

- If you use **CommonJS (`require`, `module.exports`)** – since they are **dynamic**, bundlers cannot safely remove unused code.
- If code has **side effects** (e.g., modifying global variables). Bundlers keep them unless `"sideEffects": false` is set in `package.json`.

---

### **package.json Tip (often asked in interviews)**

```json
{
  "sideEffects": false
}
```

- Tells bundler: “My modules have no side effects; unused code can be safely removed.”
- If some files do have side effects (like polyfills or CSS imports), you list them explicitly:

```json
{
  "sideEffects": ["./src/polyfill.js", "*.css"]
}
```

---
