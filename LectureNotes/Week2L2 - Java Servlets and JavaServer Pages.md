# Lecture Notes: Java Servlets vs. JavaServer Pages (JSP)

## Module: Server-Side Java Technologies & Web Architecture

Objective: Understand the architectural roles, structural differences, and execution cycles of Servlets and JSPs in dynamic web applications.

---

## 1. Introduction: The Dynamic Web Layer

Java Servlets and JavaServer Pages (JSP) are foundational server-side technologies used to build dynamic, data-driven web applications. While they share the underlying goal of generating dynamic content, they approach the task from opposite perspectives: one is code-centric, while the other is markup-centric.

The essential difference between these two technologies lies in their **primary role** and **structure** within an application's architecture.

```
[ Client Browser ]  --->  [ Controller: Servlet ]  --->  [ Model: Java Class/DB ]
                                  |
                                  v
                          [ View: JSP Page ]      --->  [ HTML Response to Client ]

```

---

## 2. Quick Comparison Matrix
<img width="570" height="417" alt="image" src="https://github.com/user-attachments/assets/4036dbdc-4f4f-44ad-ae12-dc763b0fae0d" />


---

## 3. Java Servlets: The Controller Component

### What They Are

Servlets are specialized Java classes that run inside a web container or servlet engine (such as Apache Tomcat) to intercept client requests and dynamically build responses.

### Core Architectural Features

* 
**Request Processing:** A servlet acts as a gatekeeper. It parses an incoming HTTP request, coordinates with backend business models or databases (via JDBC), and writes a stream back to the client—typically as HTML or raw JSON.


* **Lifecycle Hooks:** They rely on core lifecycle methods to process target actions:
* 
`doGet()`: Automatically invoked to handle data retrieval requests.


* 
`doPost()`: Invoked to manage data updates, form submissions, and structural payloads.




* 
**Routing Setup:** Modern environments utilize metadata annotations like `@WebServlet("/path")` to direct URL mappings natively. Legacy systems register these endpoints within a `web.xml` deployment descriptor file.



---

## 4. JavaServer Pages (JSP): The View Component

### What They Are

JSP is an abstraction layer built on top of servlet technology. It allows frontend developers to write standard HTML markup while inserting dynamic server-side hooks where variable data needs to appear.

### The Lifecycle Traversal

When a client requests a `.jsp` file for the first time, the web container executes a multi-step translation cycle:

1. 
**Translation:** The container parses the file and compiles the markup/tags into a standard `.java` servlet source file.


2. 
**Compilation:** The temporary servlet source code is compiled into a bytecode `.class` file.


3. 
**Execution:** The compiled servlet runs normally to output pure HTML back to the browser user.



### Key Scripting Features

To ensure code files remain clean and maintainable, modern JSPs use specific toolsets instead of raw Java scriptlets:

* 
**Expression Language (EL):** Syntactic shorthand (e.g., `${user.name}`) that extracts properties from backend objects without direct script blocks.


* 
**Implicit Objects:** Built-in system abstractions accessible instantly without initialization (such as `request`, `response`, and `session`).


* 
**JSTL (JSP Standard Tag Library):** Pre-defined tags (like `<c:forEach>` or `<c:if>`) that handle loops and structural logic, keeping Java code entirely out of presentation screens.



---

## 5. Architectural Context & Current Relevance

### The Model-View-Controller (MVC) Pattern

In professional production systems, these components are rarely used in isolation. Instead, they work together as part of the **MVC architecture**:

* **The Controller (Servlet):** Processes the request, extracts input parameters, runs validation, and updates data models.
* **The View (JSP):** Receives formatted data from the servlet and renders the final user interface.

### Enterprise Landscape

While contemporary software patterns favor decoupled API environments (like Spring Boot backends serving React or Vue single-page frontends), Servlets and JSPs remain deeply integrated into the architecture of existing web systems. Understanding these concepts is vital when maintaining, securing, and migrating enterprise software applications.

---

Technically, JSP (Jakarta Server Pages) is **not deprecated**, but it is **obsolete for new projects**. It has been superseded by modern front-end frameworks (like **React or Vue**) and server-side rendering engines (like **Thymeleaf**).

## Why JSP is Fading
### Legacy Tech: 
There have been no major updates to the JSP specification in years. It is widely considered technical debt in new application stacks.

No Direct Previews: Designers cannot open a JSP file locally in a browser; it must be compiled on a server first.

Spaghetti Code: Mixing HTML and Java logic easily leads to bloated, unmaintainable codebases.

## Where It’s Still Alive

Despite its age, JSP is still heavily maintained in older enterprise, banking, and university systems. If you are maintaining a legacy Java EE or Spring application, you will still encounter it.

## Modern Alternatives

If you are building a modern Java web application, you should utilize these industry-standard alternatives:

For Server-Side Rendering (SSR): Use Thymeleaf for seamless integration with Spring Boot.

For Single-Page Applications (SPA): Expose data via REST APIs using Spring Boot and consume it with modern frontend frameworks like React or Vue.

# Lecture Notes: The Modern Role & Evolution of Java Servlets

## Module: Server-Side Java Infrastructure and Evolving Web Frameworks

### Objective: Evaluate the contemporary relevance of the Java Servlet API, analyze how modern frameworks build upon its architecture, and distinguish between traditional and non-blocking web models.

---

## The Reality of Servlets Today

There is a common misconception that Java Servlets are a deprecated or obsolete technology. In modern software engineering, **Java Servlets are not deprecated; they remain the core foundation of almost all Java web development.**

While engineers rarely write raw, manual Servlets for modern greenfield projects, they are technically highly relevant because dominant industry frameworks like **Spring Boot**, **Jakarta EE**, and **Quarkus** run directly on top of them. Understanding the Servlet architecture is equivalent to understanding how the engine of your framework operates.

---

### The Architectural State of Servlets

To master high-level tools, developers must understand the lower-level abstractions that power them. The modern footprint of Servlets spans across four critical areas:

```
                  ┌──────────────────────────────────────┐
                  │      Modern Spring Boot App          │
                  └──────────────────┬───────────────────┘
                                     │ Abstracts away
                                     v
                  ┌──────────────────────────────────────┐
                  │    Spring MVC (DispatcherServlet)    │
                  └──────────────────┬───────────────────┘
                                     │ Runs on top of
                                     v
                  ┌──────────────────────────────────────┐
                  │    Core Servlet API Architecture     │
                  └──────────────────────────────────────┘

```

### A. The Foundation of Frameworks

Major frameworks do not replace Servlets; they formalize them into central design patterns. For instance, **Spring MVC uses a single, centralized servlet called the `DispatcherServlet**` to act as a Front Controller. This servlet intercepts every incoming HTTP request and routes it to your high-level `@RestController` or `@Controller` beans.

### B. Active Maintenance & Evolution

The technology continues to evolve under the **Jakarta EE specification** (formerly Java EE). It is actively maintained, with new features and optimizations being introduced to keep pace with modern cloud-native environments.

### C. Low-Level Precision & Performance

Raw Servlets remain the preferred choice for specialized architectural tasks that demand precise control over the raw HTTP protocol. Examples include:

* Building ultra-lightweight microservices where importing a heavy framework introduces unnecessary overhead.
* Implementing optimized, chunked file-streaming endpoints.
* Managing custom, low-level binary data uploads.

### D. Legacy Dominance

Millions of mission-critical enterprise systems—particularly in banking, insurance, healthcare, and government infrastructure—still run directly on classic Servlet and JSP stacks. Maintaining, securing, and migrating these heavy-transaction codebases represents a massive share of enterprise development roles.

---

## 3. Modern Alternatives & Structural Shifts

While the Servlet API continues to power the backend, the methods engineers use to interact with it have fundamentally changed.

#### Shift 1: Configuration Abstraction (Spring Boot over Raw Servlets)

Instead of manually extending the `HttpServlet` class, overriding lifecycle hooks (`doGet`, `doPost`), and registering web mappings in boilerplate XML configuration files, developers use Spring Boot or Jakarta EE annotations. The framework takes care of generating and compiling the underlying Servlet boilerplate on the fly.

#### Shift 2: Threading Paradigms (Thread-per-Request vs. Reactive Programming)

* **The Traditional Servlet Model:** Relies on a **one-thread-per-request** architecture. If a database query takes 2 seconds to execute, that specific request thread is completely blocked and idle during that time.
* **The Modern Reactive Model:** Newer ecosystems like **Spring WebFlux** or asynchronous runtimes like **Netty** offer non-blocking alternatives. They bypass the traditional Servlet model entirely, using an event-driven loop to process massive concurrency with a very small, fixed footprint of CPU threads.

#### Shift 3: Interface Separation (JSP vs. Modern Frontends)

While Servlets remain highly relevant as the backend API engine, their traditional UI companion, **JavaServer Pages (JSP), is largely considered obsolete for new interfaces.** It has been replaced by two dominant approaches:

1. **Server-Side Templating Engines:** **Thymeleaf** has become the industry standard for Spring MVC applications requiring server-rendered views due to its clean HTML integration and lack of brittle scriptlet code.
2. **Decoupled Single-Page Applications (SPAs):** Modern architecture heavily favors using Java strictly to build secure, robust **REST APIs** (returning raw JSON payloads) while using JavaScript/TypeScript frameworks like **React, Angular, or Vue** to handle the user interface in the client's browser.

---

## 4. Architectural Comparison Matrix

| Metric / Dimension | Traditional Raw Servlet | Modern Framework (Spring Boot) | Reactive Model (WebFlux/Netty) |
| --- | --- | --- | --- |
| **Development Style** | Imperative, low-level boilerplate | Declarative, configuration-driven | Functional, event-driven streams |
| **Concurrency Model** | One Thread per Request | One Thread per Request | **Non-blocking Event Loop** |
| **UI Paradigm** | Tied tightly to JSP pages | Tied to Thymeleaf or JSON APIs | Exclusively decoupled JSON/Event APIs |
| **Primary Use Case** | Legacy support or custom streaming | Standard enterprise web apps | High-concurrency, streaming data |

---

## 5. Review & Discussion Questions:

1. **If a Spring Boot application uses standard `@RestController` annotations and never explicitly references the `javax.servlet` or `jakarta.servlet` packages, can we say it is a "Servlet-free" application? Explain why or why not.**
* *Answer:* No, it is not Servlet-free. Under the hood, Spring Boot configures an embedded web container (typically Apache Tomcat). When the application launches, Spring registers its core `DispatcherServlet`. Your high-level controller methods are simply target endpoints invoked *by* that underlying Servlet when it maps and parses incoming HTTP traffic.


2. **Under what specific system performance scenario would an architect choose a reactive backend framework (like Spring WebFlux) over a traditional Servlet-based framework (like Spring MVC)?**
* *Answer:* An architect should lean towards a reactive framework when the system must handle a high volume of concurrent, long-running connections that are bound by I/O constraints (e.g., streaming real-time data, chat applications, or orchestrating calls to many slow microservices). Reactive programming allows the server to free up threads while waiting for network responses, avoiding thread starvation that degrades performance in traditional Servlet environments.
* 

## 6. Review & Discussion Questions for Students

1. **If a JSP page is ultimately turned into a Servlet by the web container, why do we bother writing distinct JSPs in modern software engineering?**
* *Answer:* Writing user interfaces inside a Servlet requires wrapping every HTML tag in Java print statements (e.g., `out.println("<html>")`), which is incredibly tedious and prone to formatting errors. JSPs reverse this relationship, allowing designers to write clean HTML while injecting data points through simple expression languages. This enforces a clean separation of concerns.


2. **What occurs during the very first client request to a JSP page compared to subsequent requests to that exact same page?**
* *Answer:* The initial request incurs a slight performance hit because the container must actively translate and compile the `.jsp` file into a Java servlet class. On all subsequent requests, the server skips translation and executes the compiled bytecode directly, matching the execution speed of a traditional servlet.

# [Apache Tomcat Installation Guide](https://github.com/ghalipm-vanier-college/Web_Services_Summer_2026/blob/main/LectureNotes/Apache%20Tomcat%20Installation%20Guide.md)

