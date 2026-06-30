#  HTTP Client vs Servlet

## Understanding the Two Sides of HTTP Communication

When learning Web Services, students often confuse **HTTP Clients** (such as Java `HttpClient` or Spring `RestClient`) with **Java Servlets**. Although both are involved in HTTP communication, they have **completely different responsibilities**.

A simple way to understand the difference is:

- **HTTP Client → Sends Requests**
- **Servlet → Receives Requests**

They work together to implement the **client-server architecture** that powers modern web applications and RESTful web services.

---

#  Learning Objectives

- Explain the difference between an HTTP Client and a Servlet.
- Describe the request-response lifecycle.
- Identify whether code belongs on the client side or server side.
- Understand how Java applications communicate over HTTP.
- Explain how Spring Boot builds upon the Servlet architecture.

---

# 1. The Big Picture

HTTP communication always involves **two participants**:

1. A **Client** that sends a request.
2. A **Server** that receives the request and returns a response.

```text
          HTTP Request
Client -----------------------> Server

          HTTP Response
Client <----------------------- Server
```

---

# 2. What is an HTTP Client?

An **HTTP Client** is software that **initiates communication** with a web server.

It creates HTTP requests such as:

- GET
- POST
- PUT
- DELETE

and waits for the server's response.

Examples include:

- Java HttpClient
- Spring RestClient
- Spring WebClient
- Postman
- CURL
- Web Browsers

---

## Responsibilities of an HTTP Client

- Build an HTTP request.
- Send the request to a server.
- Wait for the response.
- Read the status code.
- Process the returned data.

---

### Example

```text
Java Application
        │
        ▼
Java HttpClient
        │
        ▼
HTTP Request
```

---

# 3. What is a Servlet?

A **Servlet** is a Java class that **runs on a web server** (such as Apache Tomcat) and processes incoming HTTP requests.

Unlike an HTTP Client, a Servlet does **not** initiate communication.

Instead, it waits for clients to contact it.

---

## Responsibilities of a Servlet

- Receive HTTP requests.
- Process application logic.
- Access databases or other services.
- Generate a response.
- Return the response to the client.

---

### Example

```text
HTTP Request
      │
      ▼
Servlet
      │
Business Logic
      │
      ▼
HTTP Response
```

---

# 4. HTTP Client vs Servlet

| Feature | HTTP Client | Java Servlet |
|----------|-------------|--------------|
| Role | Client-side component | Server-side component |
| Purpose | Sends HTTP requests | Receives and processes HTTP requests |
| Communication | Consumes web services | Produces web services |
| Runs On | Desktop, CLI, Android, another server | Servlet Container (Tomcat) |
| Starts Communication | Yes | No |
| Waits for Requests | No | Yes |

---

# 5. Real-World Analogy

Consider ordering food at a restaurant.

| Restaurant Example | Web Services |
|--------------------|--------------|
| Customer places an order | HTTP Client sends a request |
| Kitchen prepares the meal | Servlet processes the request |
| Waiter delivers the meal | HTTP Response |

```text
Customer
    │
    ▼
Place Order
    │
    ▼
Kitchen
    │
    ▼
Prepare Meal
    │
    ▼
Customer Receives Meal
```

---

# 6. Request–Response Lifecycle

The HTTP Client and the Servlet work together through the HTTP protocol.

```text
+--------------------+
|  Java HttpClient   |
+--------------------+
          │
          │ 1. HTTP Request
          ▼
+--------------------+
| Apache Tomcat      |
+--------------------+
          │
          │ 2. Route Request
          ▼
+--------------------+
| HelloServlet       |
+--------------------+
          │
          │ 3. Execute doGet()
          ▼
+--------------------+
| Generate Response  |
+--------------------+
          │
          │ 4. HTTP Response
          ▼
+--------------------+
| Java HttpClient    |
+--------------------+
```

---

# 7. Step-by-Step Communication

### Step 1

The HTTP Client creates a request.

```text
GET /hello
```

---

### Step 2

The request is sent to the web server.

```text
Apache Tomcat
```

---

### Step 3

Tomcat identifies the correct Servlet using the URL mapping.

Example:

```java
@WebServlet("/hello")
```

---

### Step 4

The Servlet executes the appropriate method.

```java
doGet()
```

or

```java
doPost()
```

---

### Step 5

The Servlet generates a response.

Example:

```text
Hello from the Servlet!
```

---

### Step 6

The HTTP Client receives:

- Status Code
- Response Headers
- Response Body

---

# 8. Server-Side Example (Servlet)

The following Servlet waits for incoming HTTP requests.

```java
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request,
                         HttpServletResponse response)
            throws IOException {

        response.setContentType("text/plain");

        response.getWriter()
                .write("Hello from the Servlet!");
    }
}
```

### What does this Servlet do?

- Waits for a request to `/hello`.
- Executes the `doGet()` method.
- Sends a plain text response back to the client.

---

# 9. Client-Side Example (Java HttpClient)

The following Java program sends a request to the Servlet above.

Since Java 11, HttpClient is part of Java.

```java
HttpClient client =
        HttpClient.newHttpClient();

HttpRequest request =
        HttpRequest.newBuilder()
                .uri(URI.create(
                    "http://localhost:8080/my-app/hello"))
                .GET()
                .build();

HttpResponse<String> response =
        client.send(
                request,
                HttpResponse.BodyHandlers.ofString());

System.out.println(response.body());
```

### Output

```text
Hello from the Servlet!
```

---

# 10. Visualizing the Communication

```text
Java HttpClient
        │
        │ GET /hello
        ▼
Apache Tomcat
        │
        ▼
HelloServlet
        │
        ▼
"Hello from the Servlet!"
        │
        ▼
Java HttpClient
```

---

# 11. Where Does Spring Boot Fit?

In modern enterprise applications, developers rarely write Servlets directly.

Instead, Spring Boot provides a simpler programming model.

```text
Traditional Java EE

Client
   │
Servlet
   │
Business Logic
```

becomes

```text
Spring Boot

Client
   │
@RestController
   │
Business Logic
```

Although developers work with **Controllers**, Spring Boot still uses the **Servlet API internally**.

---

# 12. Evolution of Server-Side Development

```text
Java Servlet
      │
      ▼
Spring MVC
      │
      ▼
Spring Boot
```

The underlying HTTP request-response model remains the same; Spring Boot simply reduces the amount of configuration and boilerplate code.

---

# 13. Evolution of HTTP Clients

```text
CURL
    │
    ▼
Postman
    │
    ▼
Java HttpClient
    │
    ▼
Spring RestClient
```

Each newer tool provides a more convenient way to consume HTTP-based web services.

---

# 📚 Summary

| HTTP Client | Java Servlet |
|--------------|--------------|
| Sends HTTP requests | Receives HTTP requests |
| Consumes REST APIs | Produces REST APIs |
| Runs in Java applications | Runs inside Tomcat |
| Initiates communication | Waits for communication |
| Reads responses | Generates responses |

---

# ✅ Key Takeaways

- HTTP communication always involves a **client** and a **server**.
- An **HTTP Client** initiates communication by sending requests.
- A **Servlet** listens for requests, processes them, and returns responses.
- Java `HttpClient` is commonly used to **consume** web services.

# Project structure: 
servlet-client-demo/
└── src/
    └── main/
        └── java/
            └── com/
                └── example/
                    ├── server/
                    │   └── MyServlet.java   <-- Runs inside Tomcat (Needs Jakarta EE)
                    │
                    └── client/
                        └── MyClientApp.java <-- Runs as a regular Java App (Needs nothing extra)
- Java Servlets are used to **create** web services.
- Spring Boot simplifies server-side development by building on the Servlet API while hiding much of its complexity.
- Understanding both client-side and server-side components is essential for developing modern RESTful web services.
- In production, these are completely separate applications.

# The Chain of Command
In a restaurant workflow:

The HTTP Client is the Customer: They look at the menu (the API documentation) and place an order (the HTTP Request). They never go into the kitchen.

The Servlet is the Waiter/Kitchen: They take the order, verify it, go to the pantry/fridge (the Database) to get the raw ingredients, cook it up into a meal (JSON response), and bring it back to the customer.

What this means for your demo project:
 - Client code, one will only write code to handle network connections, URLs, and JSON parsing.
 - Servlet Code: If you want your demo to return real data, this is where you would open a database connection, run a SELECT query, map the ResultSet to Java objects, and send it back to the client.
