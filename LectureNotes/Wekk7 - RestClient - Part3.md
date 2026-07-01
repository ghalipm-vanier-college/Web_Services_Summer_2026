# Spring RestClient

## A Simpler Way to Consume RESTful Web Services

Starting with **Spring Framework 6.1**, Spring introduced **RestClient**, a modern HTTP client that makes consuming RESTful Web Services much easier.

Instead of manually creating `HttpRequest` objects, handling headers, and processing responses, **RestClient** hides much of the boilerplate code while still using HTTP underneath.

You can think of it as:

- **Java HttpClient → Low-Level HTTP Client**
- **Spring RestClient → High-Level HTTP Client**

Both send HTTP requests.

The difference is **how much work the programmer has to do.**

---

# Learning Objectives

After completing this lesson, students will be able to:

- Explain what Spring RestClient is.
- Compare RestClient with Java HttpClient.
- Send GET requests using RestClient.
- Send POST requests with JSON data.
- Read Java objects directly from JSON responses.
- Consume REST APIs created using Servlets or Spring Boot.

---

# 1. The Big Picture

Suppose our server exposes this endpoint:

```
GET /students
```

The communication remains exactly the same.

```
             HTTP Request

RestClient ----------------------> Web Server

             HTTP Response

RestClient <---------------------- Web Server
```

The HTTP protocol has **not changed**.

Only the Java API becomes simpler.

---

# 2. Why Spring Created RestClient

Using Java HttpClient requires several steps.

Example:

```java
HttpClient client = HttpClient.newHttpClient();

HttpRequest request =
        HttpRequest.newBuilder()
                .uri(URI.create(url))
                .GET()
                .build();

HttpResponse<String> response =
        client.send(request,
                BodyHandlers.ofString());
```

This is perfectly fine...

...but it becomes repetitive.

Spring RestClient reduces this to:

```java
RestClient client = RestClient.create();

String response = client.get()
        .uri(url)
        .retrieve()
        .body(String.class);
```

Much less code.

---

# 3. Java HttpClient vs Spring RestClient

| Java HttpClient | Spring RestClient |
|-----------------|------------------|
| Part of Java | Part of Spring |
| More verbose | Less code |
| Manual request building | Fluent API |
| Manual response handling | Automatic conversion |
| Great for learning HTTP | Great for Spring applications |

---

# 4. Creating a RestClient

Creating a RestClient is simple.

```java
RestClient client = RestClient.create();
```

or

```java
RestClient client =
        RestClient.builder()
                  .build();
```

---

# 5. Sending a GET Request

Suppose our server has:

```
GET /hello
```

The client becomes

```java
RestClient client = RestClient.create();

String response = client
        .get()
        .uri("http://localhost:8080/myServerApp/hello")
        .retrieve()
        .body(String.class);

System.out.println(response);
```

Output

```
Hello from Servlet!
```

---

# 6. Reading JSON Automatically

Suppose the server returns

```json
{
   "id":1,
   "name":"Alice"
}
```

Create a Java class.

```java
public class Student {

    private int id;
    private String name;

    // getters
    // setters
}
```

Reading JSON becomes

```java
Student student = client
        .get()
        .uri(url)
        .retrieve()
        .body(Student.class);
```

No JSON parsing required.

Spring does it automatically.

---

# 7. Reading a List of Students

Suppose

```
GET /students
```

returns

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

The response can be mapped directly.

```java
Student[] students =
        client.get()
              .uri(url)
              .retrieve()
              .body(Student[].class);

for(Student s : students){

    System.out.println(s.getName());

}
```

Output

```
Alice
Bob
```

---

# 8. Sending POST Requests

Suppose the server creates students.

```
POST /students
```

The client creates an object.

```java
Student student =
        new Student(3,"John");
```

Send it.

```java
client.post()
      .uri(url)
      .body(student)
      .retrieve()
      .toBodilessEntity();
```

Spring automatically converts

```
Student
```

into

```json
{
   "id":3,
   "name":"John"
}
```

---

# 9. HTTP Methods

RestClient supports all common HTTP methods.

| HTTP Method | Purpose |
|--------------|----------|
| GET | Read data |
| POST | Create data |
| PUT | Replace data |
| PATCH | Update part of data |
| DELETE | Delete data |

---

# 10. Fluent API

RestClient uses method chaining.

```java
client
    .get()
    .uri(url)
    .retrieve()
    .body(String.class);
```

Each method returns another object.

```
client
      ↓
get()
      ↓
uri()
      ↓
retrieve()
      ↓
body()
```

This style is called a **Fluent API**.

---

# 11. Request–Response Lifecycle

```
+----------------------+
| Spring RestClient    |
+----------------------+
          │
          │ HTTP Request
          ▼
+----------------------+
| Apache Tomcat        |
+----------------------+
          │
          ▼
+----------------------+
| Servlet / Controller |
+----------------------+
          │
          ▼
Business Logic
          │
          ▼
HTTP Response
          │
          ▼
+----------------------+
| Spring RestClient    |
+----------------------+
```

---

# 12. RestClient vs Java HttpClient

```
Java HttpClient

Create Request
↓

Send Request
↓

Receive Response
↓

Read Body
```

becomes

```
Spring RestClient

GET
↓

Retrieve
↓

Read Object
```

Much cleaner.

---

# 13. Where Does RestClient Fit?

```
REST API

        ▲
        │
 Spring RestClient
        │
Java HttpClient
        │
 HTTP Protocol
```

RestClient simply sits on top of HTTP.

Nothing changes on the server.

---

# 14. Evolution of Spring HTTP Clients

```
RestTemplate
      │
      ▼
WebClient
      │
      ▼
RestClient
```

Spring recommends using **RestClient** for new synchronous applications.

---

# Lab Exercise

## Objective

Use **Spring RestClient** to consume a Servlet application.

---

## Part 1

Create the Servlet application

```
myServerApp
```

Endpoints

```
GET /hello
```

returns

```
Hello from Servlet!
```

```
GET /students
```

returns

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

Deploy the application to Tomcat.

---

## Part 2

Create a Spring project

```
myRestClientApp
```

Add dependency

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
</dependency>
```

---

## Part 3

Create a RestClient.

```java
RestClient client =
        RestClient.create();
```

---

## Part 4

Call

```
GET /hello
```

Display

```
Hello from Servlet!
```

---

## Part 5

Call

```
GET /students
```

Deserialize the response into

```java
Student[]
```

Print every student's name.

Expected output

```
Alice
Bob
```

---

## Bonus Challenge

Create another Servlet endpoint.

```
POST /students
```

The RestClient should create

```java
Student student =
        new Student(5,"Mary");
```

Send it to the server and display the server's confirmation response.

---

# Summary

| Java HttpClient | Spring RestClient |
|-----------------|------------------|
| Built into Java | Part of Spring |
| More code | Less code |
| Manual HTTP handling | Automatic object mapping |
| Manual JSON parsing | Automatic JSON conversion |
| Good for learning HTTP | Good for Spring applications |

---

# Key Takeaways

- **RestClient is a modern Spring HTTP client introduced in Spring Framework 6.1.**
- It uses the same HTTP protocol as Java `HttpClient` but provides a cleaner, more readable API.
- It automatically converts Java objects to JSON and JSON responses back into Java objects.
- RestClient is ideal for consuming RESTful Web Services in Spring applications.
- The server does not know whether requests come from `HttpClient`, `RestClient`, Postman, or a browser—they all communicate using standard HTTP.
