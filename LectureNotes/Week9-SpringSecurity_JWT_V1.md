
# Web Services

# Week 9 — JWT Authentication with Spring Boot & Spring Security

**Course:** Web Services  
** Week 9 Session 1**

---

# Learning Outcomes

- Explain why REST APIs require authentication.
- Differentiate between Authentication and Authorization.
- Describe how JWT works in a Spring Boot application.
- Configure Spring Security to use JWT authentication.
- Generate a JWT after a successful login.
- Access secured REST endpoints using a JWT.
- Test secured APIs using Postman.

---

# Session Theory (20–30 Minutes)

---

# 1. Why Do We Need API Security?

So far, our Spring Boot application allows anyone to access:

```http
GET /students
```

Anyone who knows the URL can retrieve student information.

```
Browser / Postman
        │
        ▼
GET /students
        │
        ▼
Student List
```

For real applications, this is not acceptable.

Only authenticated users should access protected resources.

---

# 2. Authentication vs Authorization

Students often confuse these two concepts.

## Authentication

Authentication answers:

> **Who are you?**

Examples:

- Username & Password
- API Key
- JWT Token

Example:

```
Username: admin
Password: admin123
```

Spring Security verifies the credentials.

---

## Authorization

Authorization answers:

> **What are you allowed to do?**

Example

```
Administrator

✔ View Students
✔ Add Students
✔ Delete Students

Student

✔ View Students
✘ Delete Students
```

Remember:

```
Authentication
        ↓
Authorization
```

Authentication always happens first.

---

# 3. Why JWT?

Without JWT, every request would require sending the username and password.

Example:

```
GET /students

Username: admin
Password: admin123
```

Problems

- Password travels repeatedly across the network.
- Less secure.
- Less efficient.

Instead, users log in **once**.

The server generates a JWT.

The client sends only the JWT for future requests.

---

# 4. What is JWT?

JWT stands for

> **JSON Web Token**

A JWT is a secure token generated after a successful login.

Think of it as a temporary digital ID card.

Example

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Students do **not** need to understand every character.

Just remember:

- Server creates it.
- Client stores it.
- Client sends it with every request.

---

# 5. JWT Authentication Workflow

The following diagram summarizes the entire process.

```text
            Login Request

POST /login

Username + Password
          │
          ▼
   Spring Security
validates credentials
          │
          ▼
    JWT Generated
          │
          ▼
 Client Stores Token
          │
          ▼
------------------------------------

GET /students

Authorization:
Bearer <JWT>

------------------------------------
          │
          ▼
 Spring Security
 validates JWT
          │
          ▼
 StudentController
          │
          ▼
 SQL Server
          │
          ▼
 Student List
```

Remember:

- Login happens **only once**.
- Future requests send only the JWT.

---

# 6. Spring Boot JWT Architecture

Our application will contain the following components.

```text
Browser / Postman
        │
        ▼
 POST /login
        │
        ▼
AuthController
        │
        ▼
Spring Security
        │
        ▼
JwtUtil
(generate JWT)
        │
        ▼
JWT Token

==============================

GET /students
Authorization: Bearer <JWT>

==============================

        │
        ▼
JwtFilter
(validates JWT)
        │
        ▼
StudentController
        │
        ▼
StudentRepository
        │
        ▼
SQL Server
```

---

# 7. Components We Will Create

| Class | Purpose |
|---------|---------|
| StudentController | Handles student requests |
| StudentRepository | Reads students from SQL Server |
| AuthController | Handles login |
| JwtUtil | Generates and validates JWT |
| JwtFilter | Checks every incoming JWT |
| SecurityConfig | Configures Spring Security |

---

# 8. Testing with Postman

## Step 1 — Login

Request

```http
POST /login
```

Body

```json
{
    "username":"admin",
    "password":"admin123"
}
```

Response

```json
{
    "token":"eyJhbGc..."
}
```

Copy the token.

---

## Step 2 — Access Protected API

Request

```http
GET /students
```

Headers

```
Authorization

Bearer eyJhbGc...
```

Expected Result

```json
[
    {
        "id":1,
        "name":"Alice"
    },
    {
        "id":2,
        "name":"Bob"
    }
]
```

---

## Step 3 — Without JWT

Request

```http
GET /students
```

(no Authorization header)

Expected

```
401 Unauthorized
```

---

# 9. Common HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

Remember:

**401 Unauthorized**

No valid JWT was provided.

**403 Forbidden**

The user is authenticated but does not have permission.

---

# Summary

After today's lesson, you should understand:

- Why APIs need authentication.
- The difference between Authentication and Authorization.
- Why JWT is widely used in REST APIs.
- How Spring Security uses JWT.
- How Postman sends JWT using the Authorization header.

---

# Laboratory (2 Hours)

## Objective

Secure the existing Spring Boot Student application using JWT Authentication.

Current application already contains:

- Spring Boot
- Spring MVC
- Spring Security
- SQL Server
- Student Entity
- Student Repository
- Student Controller

We will replace Basic Authentication with JWT Authentication.

---

# Step 1 — Add JWT Dependencies

Add the JWT dependency to your `pom.xml`.

Build the project.

Expected Result:

The project compiles successfully.

---

# Step 2 — Create JwtUtil

Create a helper class named

```
JwtUtil
```

It should provide methods to:

- Generate a JWT.
- Validate a JWT.
- Extract the username from a JWT.

Run the application.

Expected Result:

No compilation errors.

---

# Step 3 — Configure the Secret Key

Add a secret key to

```properties
application.properties
```

Example

```properties
jwt.secret=ThisIsMyVeryLongSecretKey12345678901234567890
```

Discuss:

- Why should the secret not be hardcoded?
- How can environment variables be used in production?

---

# Step 4 — Create the Login Endpoint

Create

```http
POST /login
```

Request

```json
{
    "username":"admin",
    "password":"admin123"
}
```

If the credentials are correct:

- Generate a JWT.
- Return the token to the client.

Expected Response

```json
{
    "token":"eyJhbGc..."
}
```

---

# Step 5 — Configure Spring Security

Update the security configuration.

Allow public access to

```text
POST /login
```

Protect

```text
GET /students
```

Only users with a valid JWT should access `/students`.

---

# Step 6 — Create a JWT Filter

Create a filter that:

- Reads the `Authorization` header.
- Checks for the `Bearer` prefix.
- Validates the JWT.
- Allows the request to continue if the token is valid.
- Returns `401 Unauthorized` if the token is missing or invalid.

---

# Step 7 — Test with Postman

## Test 1 — Login

```
POST /login
```

Receive a JWT.

---

## Test 2 — Without JWT

```
GET /students
```

Expected

```
401 Unauthorized
```

---

## Test 3 — With JWT

Add the following header:

```
Authorization

Bearer <JWT Token>
```

Send

```
GET /students
```

Expected Result

Student data is returned from SQL Server.

---

# Deliverables

Demonstrate the following to the instructor:

- Successful login (`POST /login`)
- JWT token generated successfully
- `GET /students` blocked without a JWT
- `GET /students` returns data with a valid JWT
- Student data retrieved from SQL Server through the secured API

---

# Lab Challenge (Optional)

1. Configure the JWT to expire after a short time (for example, 5 minutes).
2. Generate a token.
3. Wait until the token expires.
4. Call `GET /students` again.

Observe the response:

```
401 Unauthorized
```

Discuss why token expiration improves security.

---

# Key Takeaways

- JWT is the most common authentication mechanism for modern REST APIs.
- Users authenticate once and receive a JWT.
- Every future request includes:

```text
Authorization: Bearer <JWT>
```

- Spring Security validates the JWT before allowing access to protected resources.
- Sensitive information such as JWT secret keys should be stored securely (for example, in environment variables for production), not hardcoded in Java source code.


