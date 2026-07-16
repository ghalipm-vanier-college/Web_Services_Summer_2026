````markdown
# OAuth2 with Spring Boot & Spring Security
## Understanding OAuth2, JWT, and Spring Security

---

# Learning Objectives

After completing this lesson, you will be able to:

- Explain what OAuth2 is.
- Explain what JWT is.
- Understand the relationship between Spring Security, OAuth2, and JWT.
- Know when to use JWT.
- Know when to use OAuth2.
- Understand how OAuth2 works in Spring Boot.
- Understand when JWT is used together with OAuth2.
- Understand the authentication flow in modern web applications.

---

# Before We Begin

Many students confuse these terms:

- Spring Security
- JWT
- OAuth2

They are **not the same thing**.

Think of them as different pieces of one security system.

---

# The Big Picture

```
                    Spring Security
                  (Security Framework)
                          │
          ┌───────────────┴───────────────┐
          │                               │
     Username/Password               OAuth2 Login
          │                               │
          │                               │
      Session or JWT               JWT / Access Token
```

Spring Security is the framework.

JWT and OAuth2 are authentication mechanisms that Spring Security can use.

---

# What is Spring Security?

Spring Security is a framework that protects your application.

It answers questions like

- Who are you?
- Can you access this page?
- Are you allowed to perform this action?

Spring Security handles

- Authentication
- Authorization
- Password encryption
- Login
- Logout
- Session management
- JWT authentication
- OAuth2 login

---

# Authentication vs Authorization

Authentication answers

```
Who are you?
```

Example

```
Username

admin

Password

1234
```

If correct

↓

Authenticated

---

Authorization answers

```
What are you allowed to do?
```

Example

```
Admin

Can delete students
```

```
Student

Cannot delete students
```

---

# What is JWT?

JWT stands for

```
JSON Web Token
```

A JWT is simply a **token**.

It is **not** a login system.

It is **not** a security framework.

It is only a way of carrying information.

Example

```
eyJhbGc...

eyJzdWIi...

abcXYZ...
```

---

# JWT Contains Information

Example payload

```json
{
   "sub":"alice",
   "role":"ADMIN",
   "exp":1710000000
}
```

The token contains

- username
- role
- expiration

The server signs it using a secret key.

---

# JWT Authentication

```
Client

Login

↓

Spring Security

↓

Username/password verified

↓

JWT created

↓

Client stores JWT

↓

Every request

Authorization:
Bearer JWT

↓

Spring validates JWT

↓

Controller executes
```

JWT is ideal for

- REST APIs
- Mobile applications
- React
- Angular
- Vue
- Flutter
- Microservices

---

# What is OAuth2?

OAuth2 is **not** a token.

OAuth2 is **not** encryption.

OAuth2 is **an authorization framework**.

Its purpose is

> Allow one application to access another application's resources **without sharing the user's password**.

---

# Everyday Example

Imagine you want to use Canva.

Instead of creating a new account,

you click

```
Continue with Google
```

Google asks

```
Do you allow Canva
to know your name
and email?
```

You click

```
Allow
```

Google returns an access token.

Canva never knows your Google password.

That is OAuth2.

---

# OAuth2 Authentication Flow

```
Browser

↓

Click

Login with Google

↓

Google Login Page

↓

User enters Google password

↓

Google verifies user

↓

Google returns Access Token

↓

Spring Boot

↓

Spring Security

↓

User authenticated
```

Notice

Your application never receives the user's password.

Google authenticates the user.

---

# OAuth2 Roles

There are four important roles.

---

## Resource Owner

Usually the user.

```
Alice
```

---

## Client

The application requesting access.

```
Your Spring Boot application
```

---

## Authorization Server

The server that authenticates users.

Examples

- Google
- GitHub
- Facebook
- Microsoft
- Okta

---

## Resource Server

The server containing protected data.

Example

```
Google Drive

Google Calendar

GitHub API
```

---

# OAuth2 Example

```
Your App

↓

Login with GitHub

↓

GitHub Login Page

↓

GitHub authenticates user

↓

GitHub returns Access Token

↓

Your App can call

GitHub API
```

---

# OAuth2 Does NOT Mean JWT

Many beginners think

```
OAuth2

=

JWT
```

This is incorrect.

OAuth2 does **not** require JWT.

OAuth2 may use

- opaque tokens
- JWT tokens
- other token formats

JWT is only one possible token format.

---

# Relationship Between OAuth2 and JWT

Think of it like mailing a package.

OAuth2 is

```
The delivery service
```

JWT is

```
The package
```

OAuth2 defines **how** authentication and authorization happen.

JWT defines **how information is stored inside a token**.

---

# Analogy

Suppose you order a package.

```
FedEx

UPS

DHL
```

These companies deliver packages.

The package itself may be

```
Small box

Large box

Envelope
```

OAuth2 is like

```
FedEx
```

JWT is like

```
The package
```

Different concepts.

---

# Can OAuth2 Use JWT?

Yes.

Very often.

Modern systems commonly use

```
OAuth2

+

JWT Access Token
```

Example

```
Google

↓

JWT Access Token

↓

Spring Boot
```

---

# Spring Security with OAuth2

Spring Security already supports OAuth2.

Example dependency

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>
```

Example configuration

```properties
spring.security.oauth2.client.registration.google.client-id=YOUR_CLIENT_ID

spring.security.oauth2.client.registration.google.client-secret=YOUR_CLIENT_SECRET
```

These values are obtained by registering your application with Google in the Google Cloud Console.

---

# OAuth2 Login Flow

```
Browser

↓

Login with Google

↓

Spring Security

↓

Redirect

↓

Google Login

↓

Google verifies user

↓

Returns Authorization Code

↓

Spring Security exchanges code

↓

Receives Access Token

↓

User authenticated
```

Notice

Spring Security performs most of the work.

---

# JWT Login Flow

```
Browser

↓

POST /login

↓

Spring Security

↓

Database

↓

Username

↓

Password

↓

Generate JWT

↓

Return JWT

↓

Browser stores JWT

↓

Authorization:
Bearer JWT
```

---

# OAuth2 Login Flow

```
Browser

↓

Login with Google

↓

Google Login Page

↓

Google authenticates

↓

Returns Access Token

↓

Spring Security

↓

User logged in
```

---

# Comparing JWT and OAuth2

| Feature | JWT | OAuth2 |
|----------|------|---------|
| What is it? | Token format | Authorization framework |
| Purpose | Carry user information securely | Allow delegated access to resources |
| Authentication | No (by itself) | Yes, through an authorization flow |
| Authorization | No (contains claims that can help) | Yes |
| Can be used alone? | Yes (with Spring Security) | Yes |
| Used with Spring Security? | Yes | Yes |
| Can they work together? | Yes | Yes |

---

# Which One Does What?

```
Spring Security

↓

Protects application

↓

Uses JWT

or

Uses OAuth2

or

Uses Sessions

or

Uses Basic Authentication
```

Spring Security is the framework.

JWT is one authentication mechanism.

OAuth2 is another authentication/authorization mechanism.

---

# When Should I Use JWT?

Use JWT when

- You built the login page yourself.
- Users have accounts in your database.
- You are building REST APIs.
- You have mobile apps.
- You have React or Angular front ends.
- You want stateless authentication.

Example

```
Spring Boot

↓

SQL Server

↓

Users Table

↓

Generate JWT

↓

React
```

---

# When Should I Use OAuth2?

Use OAuth2 when

- Users already have Google accounts.
- Users already have Microsoft accounts.
- Users already have GitHub accounts.
- You do not want to manage passwords.
- You want "Login with Google."

Example

```
Login with Google

Login with GitHub

Login with Microsoft

Login with Facebook
```

---

# Can I Use Both?

Absolutely.

This is common in enterprise applications.

```
User

↓

Login with Google

↓

OAuth2

↓

Google returns JWT Access Token

↓

Spring Security

↓

Authenticated User
```

---

# Which One Should You Teach First?

Recommended order

1. Spring Security
2. Username/Password Authentication
3. Roles and Authorities
4. JWT Authentication
5. OAuth2 Login
6. OAuth2 Resource Server
7. OAuth2 Authorization Server (advanced)

It is easier to understand OAuth2 much better after already understanding authentication and JWT.

---

# Summary

| Technology | Responsibility |
|------------|----------------|
| Spring Security | Security framework for Spring applications |
| JWT | Token that carries authenticated user information (claims) |
| OAuth2 | Authorization framework for delegated access and third-party login |
| SQL Server | Stores users, passwords, and roles (when using local authentication) |
| Google/GitHub | External Identity Providers for OAuth2 login |

---

# Key Takeaways

- **Spring Security** is the security framework that protects your application.
- **JWT** is a compact token format used to carry user information securely between the client and server.
- **OAuth2** is an authorization framework that allows users to grant applications access without sharing their passwords.
- JWT and OAuth2 are **not competitors**; they solve different problems and are often used together.
- Use **JWT** for applications that manage their own users and expose REST APIs.
- Use **OAuth2** when users authenticate through external providers such as Google, GitHub, Microsoft, or Facebook.
- In many modern applications, **Spring Security + OAuth2 + JWT** work together to provide secure, scalable authentication and authorization.
````
