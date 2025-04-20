# CORS (Cross-Origin Resource Sharing) – Interview Notes

CORS stands for **Cross-Origin Resource Sharing**. It is a **security mechanism implemented by web browsers** that restricts how resources on a web page can be requested from another **origin** (domain, protocol, or port) than the one the page originated from.

- It is **not a JavaScript or frontend concept**, but rather **a browser-enforced security feature**.
- CORS is enforced because of the **Same-Origin Policy (SOP)**, which prevents potentially malicious cross-site requests.

## Origin Definition

An **origin** is defined as the combination of:

- Protocol (http or https)
- Domain (e.g., `example.com`)
- Port (e.g., `:3000`)

Two URLs with any difference in the above are considered **cross-origin**.

**Example**:  
Frontend → `https://frontend.com`  
Backend API → `https://api.backend.com`  
→ This is a cross-origin request.

---

## **Why Does CORS Exist?**

CORS exists due to the **Same-Origin Policy**, which:

- Prevents a malicious site from reading sensitive data from another site via the user's browser.
- Blocks **cross-origin reads**, but **not the request itself**.
- The **browser initiates the request**, but **blocks access to the response** unless explicitly allowed by the server.

### Security Purpose

This protects users from:

- Cross-site scripting (XSS)
- Cross-site request forgery (CSRF)
- Unauthorized API access with session tokens or cookies

---

## **CORS Error Behavior**

A common browser error looks like:

```
Access to fetch at 'https://api.backend.com' from origin 'https://frontend.com'
has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present.
```

This occurs **not because the request is blocked**, but because the **response is rejected** due to missing or incorrect headers.

---

## **How to Fix CORS Issues**

### Step 1: Configure Server-Side CORS Headers

The server must respond with proper HTTP headers like:

```http
Access-Control-Allow-Origin: https://frontend.com
```

Or to allow any origin (less secure):

```http
Access-Control-Allow-Origin: *
```

Other headers often required:

```http
Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Allow-Credentials: true  # If using cookies
```

> 💡 Allowing `*` for `Access-Control-Allow-Origin` cannot be used when `credentials` are set to `true`.

---

### Step 2: Handle Preflight Requests (OPTIONS)

For non-simple requests (e.g., custom headers, `PUT`, `DELETE`, etc.), the browser sends a **preflight OPTIONS request** first to check CORS policy.

**Server must respond with:**

```http
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://frontend.com
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Max-Age: 86400
```

---

### Step 3: Use a Proxy for Development

If the backend cannot be updated immediately:

- Use a **proxy** to tunnel API requests through the same origin as the frontend.
- Angular/React CLIs support this via proxy configuration:

**Angular Example (`proxy.conf.json`):**

```json
{
  "/api": {
    "target": "http://localhost:3000",
    "secure": false,
    "changeOrigin": true
  }
}
```

In `angular.json`:

```json
"serve": {
  "options": {
    "proxyConfig": "src/proxy.conf.json"
  }
}
```

---
