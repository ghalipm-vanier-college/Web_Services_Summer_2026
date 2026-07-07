# Web Services

# Week 8 — API Security and Secure Configuration in Spring Boot

**Course:** Web Services  
**Duration:** 3 Hours

- Theory: 20–30 Minutes
- Hands-on Lab: 2 Hours

---

# Learning Objectives

- Explain why API security is important.
- Identify common API security threats.
- Distinguish between authentication and authorization.
- Explain the purpose of HTTPS.
- Understand API Keys, JWT, and OAuth2.
- Store configuration values using `.properties` files.
- Understand why secrets should be stored in environment variables.
- Create and use environment variables.
- Protect a Spring Boot endpoint using a simple API Key mechanism.
- Test secured APIs using Postman.

---

# 1. Why Do APIs Need Security?

Most modern applications expose functionality through APIs.

Examples:

```http
GET /employees

GET /accounts

POST /payments
```

Without security, anyone could access or modify sensitive data.

---

## Real-World Example

Imagine an online banking system.

If anyone could access:

```http
GET /accounts
```

they could view customer account information.

Or worse:

```http
POST /transfer
```

could transfer money without authorization.

---

## Goal of API Security

API Security protects against:

- Unauthorized access
- Data theft
- Data modification
- Identity impersonation
- Malicious attacks

---

# 2. Common API Security Threats

| Threat | Description |
|----------|-------------|
| Unauthorized Access | Accessing protected resources |
| SQL Injection | Injecting malicious SQL commands |
| Cross-Site Scripting (XSS) | Injecting malicious scripts |
| Brute Force Attack | Repeated login attempts |
| Data Exposure | Returning sensitive information |
| Broken Authentication | Weak login systems |

---

# 3. Authentication vs Authorization

Students frequently confuse these two concepts.

---

## Authentication

Authentication answers:

> **Who are you?**

Examples:

- Username and Password
- API Key
- JWT Token
- OAuth Login

---

### Example

```text
Username: alice
Password: password123
```

The server verifies the identity of the user.

---

## Authorization

Authorization answers:

> **What are you allowed to do?**

Example:

```text
Administrator

✔ View Employees
✔ Add Employees
✔ Delete Employees

Employee

✔ View Employees
✘ Delete Employees
```

---

# Authentication vs Authorization Summary

| Authentication | Authorization |
|---------------|---------------|
| Verifies identity | Verifies permissions |
| Who are you? | What can you do? |
| Happens first | Happens after authentication |

---

# 4. HTTPS

HTTP transmits information as plain text.

Example:

```text
username=admin
password=1234
```

Anyone monitoring the network could read this information.

---

## HTTPS

HTTPS encrypts communication.

```text
Client
   │
Encrypted Data
   │
Server
```

---

## Best Practice

Always use HTTPS for:

- Production systems
- Login forms
- REST APIs
- Financial transactions

---

# 5. API Keys

## What is an API Key?

An API Key is a unique identifier assigned to an application.

Example:

```http
GET /employees

X-API-Key: abc123xyz
```

The server checks the key before processing the request.

---

## Who Creates API Keys?

Usually:

- The API Provider
- The System Administrator
- The Cloud Platform

Examples:

- Google Maps API
- OpenWeather API
- Stripe API

When an application registers, the provider generates a unique API key.

---

## When Should API Keys Be Used?

API Keys are useful for:

- Identifying applications
- Limiting API usage
- Monitoring requests

They are **not ideal for user authentication**.

---

# 6. JSON Web Tokens (JWT)

JWT stands for:

> **JSON Web Token**

JWT is the most common authentication mechanism used by modern REST APIs.

---

## JWT Workflow

```text
User Login
      │
      ▼
Server Validates Credentials
      │
      ▼
JWT Created
      │
      ▼
JWT Returned to Client
      │
      ▼
Client Stores JWT
      │
      ▼
Future Requests Include JWT
```

---

## Example

```http
Authorization: Bearer eyJhbGciOiJIUzI1Ni...
```

---

## Who Creates JWT Tokens?

The server creates the JWT after successful login.

Examples:

- Spring Security
- Identity Server
- Authentication Service

---

## When Should JWT Be Used?

JWT is ideal for:

- User authentication
- Mobile applications
- REST APIs
- Single Page Applications

---

# 7. OAuth 2.0

## What is OAuth?

OAuth allows users to log in using another trusted provider.

Examples:

```text
Login with Google

Login with Microsoft

Login with GitHub
```

---

## OAuth Workflow

```text
User
   │
   ▼
Google Login
   │
   ▼
Google Verifies User
   │
   ▼
Google Returns Token
   │
   ▼
Application Grants Access
```

---

## Who Creates OAuth Tokens?

The OAuth Provider creates the token.

Examples:

- Google
- Microsoft
- GitHub
- Facebook

---

## When Should OAuth Be Used?

Use OAuth when:

- Allowing social logins
- Delegating authentication
- Avoiding password storage

---

# JWT vs OAuth

| JWT | OAuth |
|-------|--------|
| Token format | Authorization framework |
| Usually created by your application | Usually provided by external providers |
| Used for authentication | Used for delegated authorization |
| Common in REST APIs | Common in enterprise applications |

---

# 8. Storing Configuration Securely

Applications require configuration values such as:

```text
Database URL
Database Password
API Keys
JWT Secrets
```

These values should not be hardcoded in Java code.

---

# Bad Example

```java
String password = "admin123";
```

Problems:

- Visible in source code
- Easy to leak
- Difficult to change

---

# Better Approach

Use:

- application.properties
- Environment Variables

---

# 9. application.properties

Example:

```properties
app.name=EmployeeService

server.port=8080

spring.datasource.url=jdbc:sqlserver://localhost:1433
```

---

## Appropriate Uses

Store:

- Application settings
- Feature flags
- Default values
- Port numbers

---

## Avoid Storing

Avoid storing:

```properties
database.password=admin123

api.key=secret123
```

especially in projects committed to Git repositories.

---

# 10. Environment Variables

Environment Variables are stored outside the application.

Example:

```text
DB_PASSWORD=admin123

API_KEY=abc123xyz
```

---

## Advantages

- Not stored in source code
- Not committed to Git
- Different values per environment
- More secure

---

# Creating Environment Variables (Windows)

### Temporary

```cmd
set API_KEY=abc123
```

---

### Permanent

```text
Windows Settings
    ↓
System
    ↓
Advanced System Settings
    ↓
Environment Variables
```

Add:

```text
Variable Name:
API_KEY

Variable Value:
abc123xyz
```

---

# Properties vs Environment Variables

| Feature | application.properties | Environment Variables |
|----------|----------------------|-----------------------|
| Scope | Application-specific | Operating System level |
| Security | Lower | Higher |
| Best Use | Configuration | Secrets |
| Git Safe | Only if no secrets | Yes |
| Priority | Lower | Higher |

---

# 11. Security-Related HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## Important Difference

### 401 Unauthorized

User has not authenticated.

Example:

```text
No API Key
No JWT
```

---

### 403 Forbidden

User is authenticated but lacks permission.

Example:

```text
Employee attempting to delete records
```

---

# 12. Security Best Practices

Always:

- Use HTTPS
- Validate user input
- Use PreparedStatement
- Store secrets outside source code
- Use API Keys or JWTs
- Return only necessary data
- Avoid detailed error messages

---

# 💻 Laboratory (2 Hours)

# Lab Goal

Create a simple Spring Boot API protected by an API Key.

- Environment Variables
- API Keys
- HTTP Security Concepts
- Postman Testing

---

# Part 1 — Create Spring Boot Project

Create:

```text
EmployeeSecurityDemo
```

Dependencies:

```text
Spring Web
```

---

# Part 2 — Create Controller

Create:

```java
@RestController
@RequestMapping("/employees")
public class EmployeeController {
}
```

---

# Part 3 — Add Simple Endpoint

```java
@GetMapping
public String getEmployees() {
    return "Employee Data";
}
```

Test:

```http
GET /employees
```

Expected:

```text
Employee Data
```

---

# Part 4 — Add API Key Check

Require:

```http
X-API-Key
```

Example:

```java
@GetMapping
public ResponseEntity<String> getEmployees(
        @RequestHeader(value="X-API-Key",
        required=false) String apiKey) {

    if(apiKey == null ||
       !apiKey.equals("secret123")) {

        return ResponseEntity
                .status(401)
                .body("Unauthorized");
    }

    return ResponseEntity.ok("Employee Data");
}
```

---

# Part 5 — Test with Postman

### Request Without Header

Expected:

```text
401 Unauthorized
```

---

### Request With Header

```text
X-API-Key: secret123
```

Expected:

```text
200 OK
```

---

# Part 6 — Move API Key to application.properties

```properties
security.api-key=secret123
```

Inject:

```java
@Value("${security.api-key}")
private String apiKey;
```

---

# Part 7 — Move API Key to Environment Variable

Create:

```text
API_KEY=secret123
```

Use:

```properties
security.api-key=${API_KEY}
```

Run the application again.

Verify functionality still works.

---

# Deliverables

✔ Spring Boot application running

✔ Endpoint returns 401 without API key

✔ Endpoint returns 200 with API key

✔ API key stored in properties file

✔ API key loaded from environment variable

✔ Postman screenshots

---

# 🎓 Summary

Concepts learned:

- Why API security is important
- Authentication vs Authorization
- HTTPS fundamentals
- API Keys
- JWT Authentication
- OAuth Authentication
- Secure configuration management
- application.properties
- Environment Variables
- Security best practices in Spring Boot

These concepts provide the foundation for implementing secure REST APIs and understanding modern authentication mechanisms used in enterprise applications.

# Extra 
# Weather API Integration Guide

This document outlines the end-to-end workflow required to obtain a free API access key/token from a public weather data provider and consume its endpoints successfully using code implementations.

---

## Phase 1: Acquiring a Free API Token

To authenticate requests and prevent service abuse, modern web APIs require an explicit alphanumeric key string appended to every query. 

1. **Register an Account**: Visit the [OpenWeatherMap API Portal](https://openweathermap.org/api) and sign up for a free developer account profile.
2. **Verify Registration**: Confirm your account via the activation link sent to your registration email inbox.
3. **Access the Console Dashboard**: Log into the platform and find the **API Keys** management tab on your user control security panel.
4. **Generate Key**: Select **Create/Generate Key**, assign an identification tag or project alias to it (e.g., `web-services-demo`), and save it.
5. **Copy the String Value**: Keep this generated token confidential. Do not commit raw security strings publicly to Git repositories.

> ⚠️ **Important Activation Delay:** Newly provisioned API keys from OpenWeatherMap typically require anywhere from
> **30 minutes to 2 hours** to fully propagate across global caching networks. If your code receives an HTTP `401 Unauthorized`
> error immediately after creation, allow some time for token activation to complete.

---

## Phase 2: Analyzing the REST API Request URL Structure

The structure of a standard HTTP GET request sent to a geographical weather endpoint looks like this:

```text
[https://api.openweathermap.org/data/2.5/weather?q=](https://api.openweathermap.org/data/2.5/weather?q=){city_name}&appid={api_key}&units=metric
```
