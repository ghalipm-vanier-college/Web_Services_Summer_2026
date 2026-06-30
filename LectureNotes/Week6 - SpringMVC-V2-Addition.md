# 📘 Spring MVC (Brief Introduction)

## What is Spring MVC?

Spring MVC (Model-View-Controller) is a web framework within the Spring Framework that organizes an application into three main components:

- **Model** – stores application data.
- **View** – displays information to the user.
- **Controller** – receives requests and coordinates the application.

Spring MVC helps separate application logic from presentation, making applications easier to develop and maintain.

---

## MVC Architecture

```text
Browser
    │
    ▼
Controller
    │
    ▼
Model
    │
    ▼
View
    │
    ▼
Browser
```

---

## MVC Components

### Model

Contains application data.

Example:

```java
Student
```

---

### Controller

Handles incoming HTTP requests.

Example:

```java
@GetMapping("/students")
```

---

### View

Displays the data.

Common view technologies include:

- Thymeleaf
- JSP

---

# Spring MVC vs Spring Boot

Students often confuse these two technologies.

| Spring MVC | Spring Boot |
|------------|-------------|
| Web framework | Application framework |
| Implements the MVC pattern | Uses Spring MVC internally |
| Requires more manual configuration | Provides automatic configuration |
| Focuses on Controllers, Models and Views | Simplifies the entire application setup |

> **Important:** Spring Boot is **not a replacement** for Spring MVC. Instead, Spring Boot builds on Spring MVC and makes it much easier to configure and use.

---

# Why Are We Learning Spring MVC?

Although this course focuses on **RESTful Web Services using Spring Boot**, understanding Spring MVC helps explain:

- how HTTP requests are processed,
- how controllers work,
- how data flows through an application.

This knowledge makes it much easier to understand Spring Boot REST APIs in the following weeks.

---

# Session Goal

The objective of this session is **not** to become experts in Spring MVC.

Instead:

- understand the MVC architecture,
- create one simple MVC application,
- recognize how Spring Boot uses the MVC framework internally.

After this introduction, the remainder of the course will focus on **Spring Boot**, **REST APIs**, **SQL Server**, **JPA**, and **building complete web services**.
