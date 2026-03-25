# 1. What is Web Storage?

> **Web Storage** is a browser API that allows you to store data **key-value pairs on the client side**.

### Types:

- **`localStorage`** → persists even after browser close
- **`sessionStorage`** → persists only for the session (tab lifetime)

---

# 2. What is a Cookie?

> A **cookie** is a small piece of data stored in the browser and **automatically sent to the server with every HTTP request**.

---

## Why Do We Need Cookies?

- Authentication (session IDs)
- Tracking user behavior (analytics)
- Personalization (preferences)

---

## How to Delete a Cookie?

### Method 1: Set Expiry in Past

```js
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
```

### Method 2: Using Max-Age

```js
document.cookie = "username=; max-age=0";
```

---

# 3. Differences: Cookie vs LocalStorage vs SessionStorage vs IndexedDB

## 🔥 Complete Comparison Table

| Feature         | Cookies                    | localStorage          | sessionStorage         | IndexedDB                          |
| --------------- | -------------------------- | --------------------- | ---------------------- | ---------------------------------- |
| Storage Size    | ~4 KB                      | ~5–10 MB              | ~5–10 MB               | Large (hundreds MB+)               |
| Data Type       | String only                | String only           | String only            | Structured (objects, blobs, files) |
| Expiry          | Set manually               | Never (until cleared) | On tab close           | Persistent                         |
| Sent to Server  | ✅ Yes (every request)     | ❌ No                 | ❌ No                  | ❌ No                              |
| Performance     | ❌ Slow (network overhead) | ✅ Fast               | ✅ Fast                | ⚠️ Slower (async DB)               |
| Accessibility   | Server + Client            | Client only           | Client only            | Client only                        |
| API Type        | Synchronous                | Synchronous           | Synchronous            | Asynchronous                       |
| Storage Scope   | Domain + path              | Same origin           | Same origin + tab      | Same origin                        |
| Security        | Vulnerable (XSS/CSRF)      | Vulnerable (XSS)      | Vulnerable (XSS)       | More secure (less exposed)         |
| Use Case        | Auth, tracking             | Persistent UI data    | Temporary session data | Complex apps, offline storage      |
| Data Structure  | Flat string                | Flat string           | Flat string            | Key-value DB with indexes          |
| Transactions    | ❌ No                      | ❌ No                 | ❌ No                  | ✅ Yes                             |
| Indexing/Search | ❌ No                      | ❌ No                 | ❌ No                  | ✅ Yes                             |
| Auto Expiry     | ✅ Yes                     | ❌ No                 | ✅ Yes (tab close)     | ❌ No                              |

---

# Why Use Cookies Over Client-Side Storage

> Cookies are used over client-side storage when data needs to be automatically sent to the server, shared with backend systems, or secured using flags like HttpOnly and SameSite, making them ideal for authentication and sensitive data.

## 1. Automatic Server Communication

- Cookies are **automatically sent with every HTTP request**
- `localStorage` / `sessionStorage` are **not sent to the server**

## 2. Better Security Controls

Cookies support important flags, these features are **NOT available** in localStorage/sessionStorage

- **HttpOnly** → Not accessible via JavaScript (protects from XSS)
- **Secure** → Sent only over HTTPS
- **SameSite** → Protects against CSRF

---

## 3. Server-Side Rendering (SSR) Compatibility

- Cookies are available on:

  - Browser ✅
  - Server (Node.js / SSR) ✅

- `localStorage` / `sessionStorage`:

  - Browser ✅
  - Server ❌ (not accessible)

---

## 4. Standard for Authentication

- Industry standard:

  - Session-based auth → Cookies
  - Secure token storage → HttpOnly cookies

---

# When NOT to Use Cookies?

## Avoid Cookies For:

- Large data (limit ~4KB)
- UI state (theme, filters)
- Client-only caching

---

# When to Use Client-Side Storage Instead?

| Use Case              | Best Choice    |
| --------------------- | -------------- |
| Theme (dark/light)    | localStorage   |
| Form data (temporary) | sessionStorage |
| Large offline data    | IndexedDB      |
| Auth (secure)         | Cookies        |

---

# Interview Insight

### Why NOT store JWT in localStorage?

- Vulnerable to **XSS attacks**
- JavaScript can access it

### Why Cookies are safer?

- `HttpOnly` prevents JS access
- `SameSite` prevents CSRF

---
