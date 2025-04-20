# JWT – JSON Web Token

## What is JWT?

- JWT is a **form of token-based authentication**.
- Based on an **open standard (RFC 7519)**.
- Used for **authorization** and **secure data exchange**.
- Self-contained: holds all required information within the token itself.

---

## How JWT Works

1. Client sends credentials (`username`, `password`) to the server.
2. Server **validates credentials**.
3. Server **generates a JWT** using a **secret key**.
4. Token is returned to the client.
5. Client includes JWT in **request headers** to access secure endpoints.
6. Server **verifies token** using the same secret before responding.

 ![](../../../Images/jwt.png)

---

## Structure of a JWT

A JWT is a single string with three parts, separated by dots:

```
xxxxx.yyyyy.zzzzz
|     |     |
|     |     └── Signature
|     └─────── Payload
└──────────── Header
```

### 1. Header

- Metadata about the token.
- Contains:
  ```json
  {
    "typ": "JWT",
    "alg": "HS256"
  }
  ```
  - `typ`: Token type (always `JWT`)
  - `alg`: Algorithm used to sign the token (e.g., HS256)

### 2. Payload (Claims)

- Contains the **data** (claims) about the user and token.
- Encoded using `base64`.
- Example:
  ```json
  {
    "userId": "XF11-1123",
    "email": "john@doe.com",
    "exp": "1592427933",
    "iat": "1590696000"
  }
  ```

#### Types of Claims:

- **Registered Claims** (standardized fields):

  - `iss`: Issuer
  - `sub`: Subject
  - `aud`: Audience
  - `exp`: Expiration time
  - `nbf`: Not before
  - `iat`: Issued at
  - `jti`: JWT ID (unique token ID)

- **Public Claims**: Custom claims that can be used publicly (e.g., `email`, `userId`).
- **Private Claims**: Custom data understood only by the token consumer and producer.

### 3. Signature

- Ensures the **integrity** of the token.
- Created using a secret key:

  ```
  HMACSHA256(
    base64UrlEncode(header) + "." + base64UrlEncode(payload),
    secret
  )
  ```

- Server uses the same secret key to **verify** the token.

---

## Key Characteristics of JWT

- **URL-safe** string format.
- Can be sent in **headers**, **body**, or **URLs**.
- **Self-contained**: all data needed for validation is inside the token.
- **Publicly readable**, but **signed** (not encrypted).
